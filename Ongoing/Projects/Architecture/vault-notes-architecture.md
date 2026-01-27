# VAULT NOTES APP — PRODUCTION ARCHITECTURE
## System Design for 1 Million Users & 100 Million Documents

---

## EXECUTIVE SUMMARY
A distributed, microservices-based notes system with:
- **CRDT-based conflict-free sync** (Automerge + Yjs) for offline-first collaboration
- **Edge-deployed API servers** with regional failover
- **Columnar storage** (Apache Parquet + TimescaleDB) for analytics and text search
- **Document versioning** via time-series DB (TimescaleDB Hypertables)
- **Real-time sync** using WebSocket + gRPC streaming
- **Content-addressable storage** (IPFS-like hashing) for deduplication
- **99.99% uptime SLA** with sub-100ms p99 latency

---

## PART 1: SYSTEM ARCHITECTURE OVERVIEW

### 1.1 High-Level Design
```
┌─────────────────────────────────────────────────────────────────┐
│                    EDGE LAYER (CDN + Regional)                  │
│   Cloudflare Workers / Fastly / AWS CloudFront                  │
│   - Auth token validation                                        │
│   - Request routing                                              │
│   - Static asset delivery                                        │
└────────────┬────────────────────────────────────────────────────┘
             │
┌────────────▼────────────────────────────────────────────────────┐
│              API GATEWAY LAYER (Multi-Region)                    │
│   Kong / AWS API Gateway + gRPC proxy                            │
│   - Rate limiting, quota management                              │
│   - Request logging & observability                              │
│   - Route to microservices                                       │
└────────────┬────────────────────────────────────────────────────┘
             │
      ┌──────┴─────────┬──────────────┬──────────────┐
      │                │              │              │
┌─────▼───┐     ┌──────▼──┐   ┌──────▼──┐   ┌──────▼──┐
│  Auth   │     │  Vault  │   │  Sync   │   │ Search  │
│ Service │     │ Service │   │Service  │   │Service  │
└────┬────┘     └────┬────┘   └────┬────┘   └────┬────┘
     │               │             │            │
     └───────────────┴─────────────┴────────────┘
              (Service Mesh: Istio)
             
     ┌────────────────────────────────────┐
     │      DATA LAYER (Multi-Region)     │
     │                                    │
     ├─ PostgreSQL + TimescaleDB         │  (Metadata, versions)
     ├─ Redis (Cluster mode)             │  (Cache, sessions)
     ├─ MinIO / S3                       │  (Binary blobs)
     ├─ Elasticsearch                    │  (Full-text search)
     ├─ EventBus (Kafka/Pulsar)          │  (Event streaming)
     └────────────────────────────────────┘
```

---

## PART 2: CORE MICROSERVICES

### 2.1 AUTH SERVICE (Identity & Access Control)

**Responsibility:** OAuth2 + JWT token management, device binding, permission delegation

**API:**
```protobuf
service AuthService {
  rpc SignUp(SignUpRequest) returns (AuthToken);
  rpc SignIn(SignInRequest) returns (AuthToken);
  rpc RefreshToken(RefreshTokenRequest) returns (AuthToken);
  rpc ValidateToken(ValidateTokenRequest) returns (ValidateTokenResponse);
  rpc RevokeToken(RevokeTokenRequest) returns (Empty);
  rpc BindDevice(BindDeviceRequest) returns (DeviceBinding);
}
```

**Database Schema (PostgreSQL):**
```sql
CREATE TABLE users (
  id UUID PRIMARY KEY,
  email VARCHAR(255) UNIQUE NOT NULL,
  password_hash VARCHAR(255),
  created_at TIMESTAMP NOT NULL,
  email_verified BOOLEAN DEFAULT FALSE,
  account_status ENUM('active', 'suspended', 'deleted'),
  mfa_enabled BOOLEAN DEFAULT FALSE,
  INDEX (email)
);

CREATE TABLE devices (
  id UUID PRIMARY KEY,
  user_id UUID NOT NULL REFERENCES users(id),
  device_name VARCHAR(255),
  device_type ENUM('web', 'ios', 'android', 'windows', 'macos'),
  device_id_hash VARCHAR(255),
  last_seen_at TIMESTAMP,
  push_token VARCHAR(1024),
  created_at TIMESTAMP NOT NULL,
  UNIQUE(user_id, device_id_hash),
  INDEX (user_id, last_seen_at)
);

CREATE TABLE oauth_tokens (
  id UUID PRIMARY KEY,
  user_id UUID NOT NULL REFERENCES users(id),
  refresh_token_hash VARCHAR(255) UNIQUE,
  device_id UUID REFERENCES devices(id),
  expires_at TIMESTAMP NOT NULL,
  scope VARCHAR(1024),
  revoked BOOLEAN DEFAULT FALSE,
  INDEX (user_id, expires_at),
  INDEX (refresh_token_hash)
);
```

---

### 2.2 VAULT SERVICE (File Tree & Metadata)

**Responsibility:** Vault structure, folder hierarchy, note metadata, move/rename operations, trash/recovery

**API:**
```protobuf
service VaultService {
  rpc CreateVault(CreateVaultRequest) returns (Vault);
  rpc GetVault(GetVaultRequest) returns (Vault);
  rpc CreateFolder(CreateFolderRequest) returns (Folder);
  rpc RenameFolder(RenameFolderRequest) returns (Folder);
  rpc MoveFolder(MoveFolderRequest) returns (Folder);
  rpc DeleteFolder(DeleteFolderRequest) returns (Empty);
  
  rpc CreateNote(CreateNoteRequest) returns (Note);
  rpc GetNote(GetNoteRequest) returns (Note);
  rpc RenameNote(RenameNoteRequest) returns (Note);
  rpc MoveNote(MoveNoteRequest) returns (Note);
  rpc DeleteNote(DeleteNoteRequest) returns (Empty);
  rpc RestoreFromTrash(RestoreRequest) returns (Note);
  
  rpc ListNotes(ListNotesRequest) returns (ListNotesResponse);
  rpc ListFolders(ListFoldersRequest) returns (ListFoldersResponse);
  rpc GetVaultTree(GetVaultTreeRequest) returns (VaultTree);
}
```

**Database Schema (PostgreSQL + TimescaleDB):**
```sql
CREATE TABLE vaults (
  id UUID PRIMARY KEY,
  user_id UUID NOT NULL REFERENCES users(id),
  name VARCHAR(255) NOT NULL,
  created_at TIMESTAMP NOT NULL,
  updated_at TIMESTAMP NOT NULL,
  is_default BOOLEAN DEFAULT FALSE,
  deleted_at TIMESTAMP,
  UNIQUE(user_id, name),
  INDEX (user_id, deleted_at)
);

CREATE TABLE folders (
  id UUID PRIMARY KEY,
  vault_id UUID NOT NULL REFERENCES vaults(id),
  parent_id UUID REFERENCES folders(id),
  name VARCHAR(255) NOT NULL,
  path VARCHAR(1024) NOT NULL,
  created_at TIMESTAMP NOT NULL,
  updated_at TIMESTAMP NOT NULL,
  deleted_at TIMESTAMP,
  UNIQUE(vault_id, parent_id, name),
  INDEX (vault_id, deleted_at),
  INDEX (parent_id)
);

-- CRDT version tracking using TimescaleDB hypertable
CREATE TABLE note_versions (
  id BIGSERIAL,
  note_id UUID NOT NULL,
  user_id UUID NOT NULL,
  content_hash VARCHAR(64) NOT NULL,
  version_vector JSONB NOT NULL,  -- CRDT version vector {device_id: timestamp}
  operations JSONB NOT NULL,       -- Automerge/Yjs operations
  created_at TIMESTAMP NOT NULL,
  device_id UUID NOT NULL,
  PRIMARY KEY (note_id, created_at, device_id)
) PARTITION BY RANGE (created_at);

SELECT create_hypertable('note_versions', 'created_at', if_not_exists => TRUE);

CREATE TABLE notes (
  id UUID PRIMARY KEY,
  vault_id UUID NOT NULL REFERENCES vaults(id),
  folder_id UUID REFERENCES folders(id),
  title VARCHAR(255) NOT NULL,
  path VARCHAR(1024) NOT NULL,
  created_at TIMESTAMP NOT NULL,
  updated_at TIMESTAMP NOT NULL,
  last_sync_version_vector JSONB,
  deleted_at TIMESTAMP,
  size_bytes INTEGER,
  word_count INTEGER,
  UNIQUE(vault_id, folder_id, title),
  INDEX (vault_id, deleted_at),
  INDEX (folder_id),
  INDEX (updated_at DESC)
);

-- Attachment metadata
CREATE TABLE attachments (
  id UUID PRIMARY KEY,
  note_id UUID NOT NULL REFERENCES notes(id),
  filename VARCHAR(1024) NOT NULL,
  mime_type VARCHAR(255),
  size_bytes INTEGER NOT NULL,
  s3_key VARCHAR(1024) NOT NULL,
  content_hash VARCHAR(64) NOT NULL,
  created_at TIMESTAMP NOT NULL,
  UNIQUE(note_id, filename),
  INDEX (note_id),
  INDEX (content_hash)
);

-- Trash / soft delete tracking
CREATE TABLE trash (
  id UUID PRIMARY KEY,
  vault_id UUID NOT NULL REFERENCES vaults(id),
  item_type ENUM('note', 'folder'),
  item_id UUID NOT NULL,
  original_path VARCHAR(1024),
  deleted_by UUID REFERENCES users(id),
  deleted_at TIMESTAMP NOT NULL,
  expires_at TIMESTAMP,
  metadata JSONB,
  INDEX (vault_id, deleted_at DESC),
  INDEX (expires_at)
);
```

**Key behaviors:**
- Path constraints: `path` column stores full hierarchy path (e.g., `/Projects/Q1/Design.md`)
- Rename/move: atomic path + metadata update in single transaction
- Soft delete: set `deleted_at`, move to `trash` table
- Trash auto-cleanup: 30-day expiration (configurable)

---

### 2.3 SYNC SERVICE (Conflict-free replication + offline support)

**Responsibility:** CRDT-based sync, conflict detection/resolution, delta transmission, offline queue

**Technology Stack:**
- **CRDT Library:** Automerge (for JSON/Markdown operations) + custom binary encoding for ink layer
- **Sync Protocol:** gRPC streaming for real-time, fallback to HTTP polling for web
- **Version Control:** Lamport timestamp + device ID for deterministic ordering

**API:**
```protobuf
service SyncService {
  rpc GetChanges(GetChangesRequest) returns (stream ChangeMessage);
  rpc SendChanges(stream ChangeMessage) returns (SendChangesResponse);
  rpc GetSnapshot(GetSnapshotRequest) returns (DocumentSnapshot);
  rpc GetHistory(GetHistoryRequest) returns (stream VersionRecord);
  rpc ResolveConflict(ResolveConflictRequest) returns (DocumentSnapshot);
}

message ChangeMessage {
  string note_id = 1;
  bytes crdt_operations = 2;       // Automerge encoded ops
  repeated InkStroke ink_strokes = 3;
  google.protobuf.Timestamp client_ts = 4;
  string device_id = 5;
  string version_vector_json = 6;  // {device_id: lamport_ts}
}

message InkStroke {
  repeated Point points = 1;
  string color = 2;
  float size = 3;
  string tool = 4;  // pen, highlighter, eraser
  bytes pressure_curve = 5;  // Compressed array of 0.0-1.0 values
  int64 created_at_ms = 6;
}

message DocumentSnapshot {
  string note_id = 1;
  bytes markdown_content = 2;  // Full Markdown blob
  string version_vector_json = 3;
  repeated InkLayer ink_layers = 4;
  google.protobuf.Timestamp snapshot_ts = 5;
}
```

**Conflict Resolution Strategy (CRDT):**
- **Markdown text:** Use Automerge's RGA (Replicated Growable Array) algorithm
  - Concurrent inserts at same position use (lamport_ts, device_id) to break ties deterministically
  - Deletions are tombstoned, not actually removed from CRDT ops
  - Merge = replay all ops in canonical order, automatically converge
- **Ink strokes:** Last-write-wins per stroke ID (lamport_ts + device_id)
  - Strokes are immutable once created; erasing creates erase operations
  - No human intervention needed
- **Metadata (title, path):** Last-write-wins (updated_at timestamp)

**Database Schema (PostgreSQL + TimescaleDB):**
```sql
-- Document snapshots (point-in-time backup for fast access)
CREATE TABLE note_snapshots (
  id UUID PRIMARY KEY,
  note_id UUID NOT NULL,
  vault_id UUID NOT NULL,
  markdown_content BYTEA NOT NULL,
  ink_data BYTEA,
  version_vector JSONB NOT NULL,
  created_at TIMESTAMP NOT NULL,
  source ENUM('auto', 'manual', 'merge'),
  INDEX (note_id, created_at DESC),
  INDEX (vault_id, created_at DESC)
) PARTITION BY RANGE (created_at);

SELECT create_hypertable('note_snapshots', 'created_at', if_not_exists => TRUE);

-- Sync checkpoints (client → server last acknowledged version)
CREATE TABLE sync_checkpoints (
  id UUID PRIMARY KEY,
  note_id UUID NOT NULL,
  device_id UUID NOT NULL,
  user_id UUID NOT NULL,
  version_vector JSONB NOT NULL,
  last_synced_at TIMESTAMP NOT NULL,
  UNIQUE(note_id, device_id),
  INDEX (user_id, last_synced_at DESC),
  INDEX (note_id)
);

-- Ink strokes (separate table for fast query + indexing)
CREATE TABLE ink_strokes (
  id UUID PRIMARY KEY,
  note_id UUID NOT NULL,
  vault_id UUID NOT NULL,
  created_at TIMESTAMP NOT NULL,
  device_id UUID NOT NULL,
  lamport_ts BIGINT NOT NULL,
  color VARCHAR(7),
  size FLOAT NOT NULL,
  tool ENUM('pen', 'highlighter', 'eraser', 'select'),
  points_data BYTEA NOT NULL,  -- Protobuf-encoded [(x, y, pressure), ...]
  is_deleted BOOLEAN DEFAULT FALSE,
  deleted_at TIMESTAMP,
  INDEX (note_id, created_at DESC),
  INDEX (vault_id, created_at DESC),
  UNIQUE(note_id, id)
) PARTITION BY RANGE (created_at);

SELECT create_hypertable('ink_strokes', 'created_at', if_not_exists => TRUE);

-- Conflict log (audit trail for debugging)
CREATE TABLE sync_conflicts (
  id UUID PRIMARY KEY,
  note_id UUID NOT NULL,
  device_a_id UUID,
  device_b_id UUID,
  conflicted_at TIMESTAMP NOT NULL,
  device_a_version JSONB,
  device_b_version JSONB,
  resolved_version JSONB,
  resolution_strategy ENUM('crdt_merge', 'keepa', 'keepb', 'manual'),
  resolved_at TIMESTAMP,
  resolved_by_user UUID REFERENCES users(id),
  INDEX (note_id, conflicted_at DESC),
  INDEX (resolved_at)
);
```

---

### 2.4 SEARCH SERVICE (Full-text + filtering)

**Responsibility:** Indexing, full-text search, filtering by folder/tag/date

**Tech Stack:**
- **Indexing Engine:** Elasticsearch 8.x (with vector embeddings for semantic search later)
- **Sync:** Kafka topics push document changes → Elasticsearch indexer
- **Query:** Filter by folder, tag, date range; highlight matches

**API:**
```protobuf
service SearchService {
  rpc Search(SearchRequest) returns (SearchResponse);
  rpc GetFacets(GetFacetsRequest) returns (FacetsResponse);
  rpc IndexDocument(IndexDocumentRequest) returns (Empty);
  rpc DeleteDocumentIndex(DeleteDocumentIndexRequest) returns (Empty);
}

message SearchRequest {
  string query = 1;
  string vault_id = 2;
  repeated string folder_ids = 3;
  repeated string tags = 4;
  google.protobuf.Timestamp from_date = 5;
  google.protobuf.Timestamp to_date = 6;
  int32 limit = 7;
  int32 offset = 8;
  string sort_by = 9;  // relevance, updated_at, created_at
}
```

**Elasticsearch Mapping:**
```json
{
  "mappings": {
    "properties": {
      "note_id": { "type": "keyword" },
      "vault_id": { "type": "keyword" },
      "folder_id": { "type": "keyword" },
      "title": {
        "type": "text",
        "analyzer": "standard",
        "fields": { "keyword": { "type": "keyword" } }
      },
      "content": {
        "type": "text",
        "analyzer": "standard"
      },
      "tags": { "type": "keyword" },
      "created_at": { "type": "date" },
      "updated_at": { "type": "date" },
      "word_count": { "type": "integer" }
    }
  }
}
```

---

### 2.5 INK LAYER SERVICE (Drawing metadata + storage)

**Responsibility:** Stroke storage, layer management, export (flattened view)

**API:**
```protobuf
service InkService {
  rpc CreateInkStroke(CreateInkStrokeRequest) returns (InkStroke);
  rpc DeleteInkStroke(DeleteInkStrokeRequest) returns (Empty);
  rpc GetInkLayers(GetInkLayersRequest) returns (InkLayersResponse);
  rpc ExportFlattened(ExportFlattenedRequest) returns (stream bytes);
}
```

**Ink Stroke Format (in `ink_strokes` table):**
```protobuf
message InkPoint {
  float x = 1;
  float y = 2;
  float pressure = 3;  // 0.0 - 1.0, normalized across all devices
  uint64 timestamp_ms = 4;  // Relative to stroke start
}

message InkStroke {
  string id = 1;
  string note_id = 2;
  string device_id = 3;
  repeated InkPoint points = 4;
  string color = 5;  // Hex: #RRGGBB
  float size = 6;    // In logical pixels
  string tool = 7;   // "pen", "highlighter", "eraser", "select"
  bool is_erased = 8;
  int64 lamport_ts = 9;
}
```

**Pressure Normalization (across platforms):**
- **iOS (Apple Pencil):** `pointerEvent.pressure` ranges 0–1 natively
- **Android (S Pen):** `pointerEvent.pressure` ranges 0–1 natively
- **Web (fallback):** Mouse active = 0.5, inactive = 0
- **Storage:** Always 0–1 float; clients interpret for brush rendering

---

## PART 3: DATA LAYER ARCHITECTURE

### 3.1 PostgreSQL + TimescaleDB (Primary Store)

**Why PostgreSQL + TimescaleDB?**
- ACID guarantees for vault metadata
- Time-series optimizations for versioning (hypertables)
- Full-text search (native `tsvector`)
- Row-Level Security (RLS) for multi-tenant isolation
- Can handle 1M concurrent users with proper indexing

**Replication Setup:**
```
┌──────────────────────────┐
│  Primary (us-east-1)     │
│  PostgreSQL + TimescaleDB│
└────────────┬─────────────┘
             │ Synchronous WAL
             │ replication
    ┌────────┴────────┐
    │                 │
┌───▼────────┐  ┌────▼──────┐
│ Replica 1  │  │ Replica 2  │
│(eu-west-1)│  │(ap-south-1)│
└────────────┘  └────────────┘
```

**Connection pooling:**
- Use PgBouncer in transaction mode (max 100k connections)
- Per-region connection pool replica (read) and primary (write)
- Failover via Patroni (automatic primary election)

---

### 3.2 Redis Cluster (Cache + Sessions)

**Purpose:** Sub-millisecond caching for vault trees, user sessions, rate limit buckets

**Architecture:**
```
┌─────────────────────────────┐
│  Redis Cluster (6 nodes)    │
│  Sharded by user_id         │
│  2x replication             │
│  RDB + AOF persistence      │
└─────────────────────────────┘
```

**Key patterns:**
```
cache:vault:{vault_id}:tree → JSON (TTL: 5 min)
session:{device_id}:{token_hash} → {user_id, scopes} (TTL: 7 days)
ratelimit:{user_id}:{endpoint} → counter (TTL: 1 min, sliding window)
sync_queue:{device_id} → [unsent_changes] (persist offline edits)
```

---

### 3.3 S3 / MinIO (Binary Object Storage)

**Purpose:** Attachments, ink blob backup, export bundles

**Design:**
```
s3://vault-notes/
├── attachments/
│   └── {vault_id}/{note_id}/{attachment_id}/
│       └── {filename}
├── ink-exports/
│   └── {vault_id}/{note_id}/
│       └── {timestamp}.pbf  (Protobuf-encoded ink)
└── user-exports/
    └── {user_id}/{export_id}.zip
```

**Multipart upload for >5MB files**, with integrity checks (MD5/SHA256).

---

### 3.4 Elasticsearch (Full-Text Search Index)

**Sharding strategy:**
```
Index: notes-{vault_id}
├── 5 shards (auto-expand with growth)
├── 2 replicas (1 hot, 1 warm tier)
└── ILM policy (rollover after 30 days)
```

**Index refresh:** Kafka consumer polls document updates, bulk index every 5 seconds (trade-off: search staleness vs throughput)

---

### 3.5 Message Bus (Kafka / Apache Pulsar)

**Topics:**
```
notes.created → triggers search indexing
notes.updated → triggers search update
notes.deleted → triggers search deletion
sync.completed → audit trail, analytics
attachments.uploaded → thumbnail generation, virus scan
```

**Partitioning:** By `vault_id` (ensures ordering per vault, enables scaling)

---

## PART 4: CLIENT-SIDE ARCHITECTURE

### 4.1 Web Client (React + Solid.js)

**State Management (Automerge + IndexedDB):**

```typescript
interface VaultState {
  tree: VaultTree;  // Folder structure
  notes: Map<string, NoteDocument>;
}

interface NoteDocument {
  id: string;
  markdown: Automerge.Doc<MarkdownSchema>;  // CRDT text
  ink: InkLayer[];
  metadata: NoteMetadata;
  syncStatus: 'synced' | 'syncing' | 'pending' | 'conflict';
  lastSyncVector: VersionVector;
}

// IndexedDB schema
idb.open('vault-notes', 1, (db) => {
  db.createObjectStore('notes', { keyPath: 'id' })
     .createIndex('vault_id', 'vault_id');
  db.createObjectStore('notes_metadata', { keyPath: 'id' });
  db.createObjectStore('ink_strokes', { keyPath: 'id' })
     .createIndex('note_id', 'note_id')
     .createIndex('created_at', 'created_at');
  db.createObjectStore('sync_queue', { keyPath: 'id' });
});
```

**Sync Engine:**
```typescript
class OfflineFirstSyncEngine {
  async syncNote(noteId: string) {
    // 1. Check if online
    if (!navigator.onLine) {
      // Queue locally
      await this.queueChange(noteId);
      return;
    }

    // 2. Get local version vector
    const local = await this.getVersionVector(noteId);

    // 3. Fetch remote changes since last sync
    const stream = await this.syncService.getChanges({
      noteId,
      sinceVersionVector: local,
    });

    // 4. Merge incoming CRDT operations
    for await (const change of stream) {
      const remoteOps = Automerge.makeChanges(
        change.crdt_operations
      );
      this.markdown = Automerge.merge(
        this.markdown,
        remoteOps
      );
      this.updateVersionVector(change.version_vector);
    }

    // 5. Send local changes
    const localOps = this.collectLocalOps();
    await this.syncService.sendChanges({
      noteId,
      operations: localOps,
    });

    // 6. Mark synced
    this.setSyncStatus(noteId, 'synced');
  }
}
```

---

### 4.2 Web Editor (Real-time + Offline)

**Text editor:** CodeMirror 6 with Markdown syntax highlighting + Automerge plugin

**Ink drawing:** Canvas.js with layers, pressure-aware brush rendering

```typescript
class DrawingCanvas {
  async onPointerMove(event: PointerEvent) {
    // Detect device type
    const isPen = event.pointerType === 'pen';
    const pressure = event.pressure || (isPen ? 0.5 : 0);  // Normalize

    const point: InkPoint = {
      x: event.pageX - this.offsetX,
      y: event.pageY - this.offsetY,
      pressure: Math.max(0, Math.min(1, pressure)),  // Clamp 0–1
      timestamp_ms: Date.now() - this.strokeStartTime,
    };

    if (this.isDrawing) {
      this.currentStroke.points.push(point);
      this.renderStroke(this.currentStroke);
    }
  }

  renderStroke(stroke: InkStroke) {
    const ctx = this.canvas.getContext('2d');
    for (let i = 1; i < stroke.points.length; i++) {
      const prev = stroke.points[i - 1];
      const curr = stroke.points[i];

      // Brush thickness varies with pressure
      const thickness = stroke.size * (0.3 + curr.pressure * 0.7);

      ctx.strokeStyle = stroke.color;
      ctx.lineWidth = thickness;
      ctx.lineCap = 'round';
      ctx.lineJoin = 'round';

      ctx.beginPath();
      ctx.moveTo(prev.x, prev.y);
      ctx.lineTo(curr.x, curr.y);
      ctx.stroke();
    }
  }
}
```

---

## PART 5: DEPLOYMENT & OPERATIONS

### 5.1 Infrastructure (Kubernetes + Terraform)

**Cluster topology:**
```
┌──────────────────────────────────────────────┐
│  EKS / GKE / AKS (pick one: AWS / GCP / Azure)
│
│  Namespaces:
│  ├─ default (system)
│  ├─ vault-notes-api (microservices)
│  ├─ vault-notes-data (databases)
│  └─ vault-notes-monitoring
│
│  Node pools:
│  ├─ general-purpose (API servers)
│  ├─ memory-optimized (Redis, cache)
│  ├─ compute-optimized (search indexing)
│  └─ spot instances (batch jobs, cost-efficient)
└──────────────────────────────────────────────┘
```

**Service mesh:** Istio for traffic management, rate limiting, retries, circuit breakers

**Autoscaling:**
```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: api-server-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: vault-api-server
  minReplicas: 10
  maxReplicas: 500
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageUtilization: 80
  behavior:
    scaleUp:
      stabilizationWindowSeconds: 30
      policies:
      - type: Percent
        value: 50
        periodSeconds: 30
```

---

### 5.2 Observability

**Metrics (Prometheus + Grafana):**
```
API latency (p50, p95, p99) by endpoint
Database connection pool utilization
Sync success/failure rate
Cache hit ratio (Redis)
Search indexing lag (Elasticsearch)
```

**Tracing (Jaeger):**
- Trace every request end-to-end (SDK auto-instrumentation)
- Sample 1% of requests in production (adaptive sampling for errors)

**Logging (ELK stack / Datadog):**
```json
{
  "timestamp": "2026-01-27T19:00:00Z",
  "level": "INFO",
  "service": "sync-service",
  "user_id": "abc123",
  "note_id": "def456",
  "event": "sync_completed",
  "sync_duration_ms": 145,
  "version_vector": "{device_1: 100, device_2: 98}",
  "conflict_resolved": false
}
```

---

### 5.3 Security & Compliance

**Encryption:**
- **In transit:** TLS 1.3 (all APIs)
- **At rest:** AES-256 (S3, RDS encryption)
- **Optional E2E:** Client-side AES-256 for data + key derivation from passphrase (later feature)

**Auth & RBAC:**
- JWT + refresh tokens (48-hour expiry)
- Device binding (device fingerprint for account recovery)
- Row-Level Security (PostgreSQL) for vault isolation

**Audit:**
- All mutations logged to immutable event stream (Kafka)
- Compliance with GDPR (right-to-be-forgotten → soft delete → async cleanup)

---

### 5.4 Disaster Recovery

**RPO (Recovery Point Objective):** 1 minute (Kafka retention)  
**RTO (Recovery Time Objective):** <5 minutes (failover + DNS propagation)

**Backup strategy:**
```
Daily snapshots → S3 + cross-region replication
PostgreSQL WAL archiving → S3
Redis RDB dumps → S3
```

**Failover automation:**
- Patroni auto-promotes replica if primary fails
- Kubernetes restarts failed pods automatically
- Load balancer removes unhealthy nodes

---

## PART 6: PERFORMANCE TARGETS & SLAs

| Metric | Target | How |
|---|---|---|
| API p99 latency | <100ms | Regional deployment, connection pooling |
| Sync latency | <500ms | gRPC streaming, Kafka for batching |
| Search latency | <1s | Elasticsearch sharding, caching |
| Availability | 99.99% | Multi-AZ, auto-failover |
| Data consistency | Strong (ACID) | PostgreSQL transactions |
| Sync conflict rate | <0.1% | CRDT auto-merge |

---

## PART 7: COST OPTIMIZATION

**Estimated monthly for 1M users, 100M documents:**

| Component | Usage | Cost (AWS) |
|---|---|---|
| EKS + EC2 | 200 nodes (mixed) | $15,000 |
| RDS PostgreSQL | 3x r6i.2xlarge (primary + 2 replicas) | $8,000 |
| ElastiCache Redis | 6-node cluster | $3,000 |
| Elasticsearch | 20 nodes, warm tier | $4,500 |
| S3 (storage + transfer) | 50TB attachments | $2,000 |
| Kafka / MSK | 9 brokers | $2,500 |
| Data Transfer (NAT, CloudFront) | 5PB/month | $400 |
| **Total** | | **~$35,400/month** |

**Cost per user:** ~$0.035/month (scales sub-linearly with growth)

**Optimizations:**
- Spot instances (70% discount) for batch jobs
- Intelligent Tiering (S3) for infrequent attachments
- Reserved Instances (RDS, Elasticsearch) with 3-year commitment

---

## PART 8: DEPLOYMENT PHASES

### Phase 1 (Weeks 1–8): Foundation
- [ ] Auth service + PostgreSQL schema
- [ ] Vault service + folder tree
- [ ] Basic Markdown editor (web)
- [ ] IndexedDB + offline queue

### Phase 2 (Weeks 9–16): Sync & Conflict
- [ ] Automerge integration
- [ ] Sync service + gRPC streaming
- [ ] Conflict resolution UI
- [ ] Device binding

### Phase 3 (Weeks 17–24): Search & Ink
- [ ] Elasticsearch indexing
- [ ] Search UI
- [ ] Ink drawing + pressure normalization
- [ ] Ink persistence

### Phase 4 (Weeks 25–32): Production Ops
- [ ] Kubernetes deployment
- [ ] Monitoring + alerting
- [ ] Load testing + optimization
- [ ] Disaster recovery testing

### Phase 5 (Weeks 33–40): Mobile
- [ ] React Native wrapper
- [ ] Capacitor integration (iOS/Android)
- [ ] Apple Pencil + S Pen support
- [ ] App Store submission

---

## PART 9: TECH STACK SUMMARY

| Layer | Technology | Reason |
|---|---|---|
| **Client (Web)** | React + Solid.js + Automerge | Fast reactivity, CRDT native |
| **API Gateway** | Kong + gRPC proxy | Rate limiting, protocol flexibility |
| **Auth** | OAuth2 + JWT | Standard, delegatable |
| **Vault** | Golang microservice | High throughput, low latency |
| **Sync** | Golang + gRPC + Automerge | Streaming, conflict-free |
| **Search** | Python + Elasticsearch | Rich query DSL |
| **Database** | PostgreSQL + TimescaleDB | ACID, time-series, full-text |
| **Cache** | Redis Cluster | Sub-ms latency, distributed |
| **Storage** | S3 / MinIO | Cheap, durable, scalable |
| **Message Bus** | Kafka | Distributed, replayed, fault-tolerant |
| **Container Orchestration** | Kubernetes (EKS/GKE/AKS) | Multi-cloud, auto-scaling |
| **Observability** | Prometheus + Jaeger + ELK | Complete visibility |

---

## PART 10: RISKS & MITIGATION

| Risk | Impact | Mitigation |
|---|---|---|
| CRDT merge explosion | Sync becomes slow at 100M docs | Partition by date, archive old docs |
| Elasticsearch indexing lag | Users see stale search results | Increase consumer parallelism, async UI |
| Database hot partition | One vault dominates I/O | Shard by vault_id at PostgreSQL level |
| gRPC connection leaks | Memory leak, denied service | Implement deadline, connection pooling limits |
| Concurrent edits → merge conflicts (rare) | User confusion | Conflict UI shows both versions, merge tool |

---

## CONCLUSION

This architecture scales to **1M users** and **100M documents** while maintaining:
- **Sub-100ms API latency** (p99)
- **Conflict-free sync** via CRDT
- **99.99% uptime** with multi-region failover
- **Cost-effective** (~$0.035 per user per month)
- **Developer-friendly** (standard tech, clear ownership per service)

**Next step:** Detailed implementation plan + team allocation.

---

**Generated:** January 27, 2026  
**Architecture Version:** v1.0 (Production-ready for 1M users)
