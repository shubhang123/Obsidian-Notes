# FastAPI Crash Course – In-Depth Guide

This crash course covers everything from installation through advanced features of FastAPI. You’ll learn how to build, validate, secure, test, and deploy production-ready APIs.

---

## 1. Introduction

- **What is FastAPI?**  
    FastAPI is a modern, high-performance Python web framework for building APIs using standard Python type hints. It’s built on **Starlette** (web parts) and **Pydantic** (data validation), offering automatic docs, high concurrency (via ASGI/uvicorn), and developer-friendly features.
    
- **Why FastAPI?**
    
    - **Type safety & validation** with Pydantic
        
    - **Automatic OpenAPI & Swagger** docs
        
    - **Fast**: comparable to Node.js and Go
        
    - **Asynchronous** support out-of-the-box
        
    - **Dependency injection** for clean, testable code
        

---

## 2. Setup & Installation

1. **Create a virtualenv** (recommended):
    
    ```bash
    python3 -m venv venv
    source venv/bin/activate
    ```
    
2. **Install FastAPI + ASGI server**:
    
    ```bash
    pip install fastapi uvicorn[standard]
    ```
    
3. **Project Structure** (suggested):
    
    ```
    myapi/
    ├── app/
    │   ├── main.py
    │   ├── routers/
    │   │   └── items.py
    │   ├── models.py
    │   ├── schemas.py
    │   └── dependencies.py
    ├── tests/
    │   └── test_items.py
    ├── requirements.txt
    └── README.md
    ```
    

---

## 3. Your First App

**`app/main.py`**

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def read_root():
    return {"message": "Hello, FastAPI!"}
```

- **Run**:
    
    ```bash
    uvicorn app.main:app --reload
    ```
    
- **Interactive Docs**:
    
    - Swagger UI: `http://127.0.0.1:8000/docs`
        
    - ReDoc: `http://127.0.0.1:8000/redoc`
        

---

## 4. Routing & Path Parameters

```python
@app.get("/items/{item_id}")
async def read_item(item_id: int):
    return {"item_id": item_id}
```

- **Path param** declared with `{}`.
    
- **Type conversion** via function signature (`int`).
    
- **Validation**: invalid types → 422 error.
    

---

## 5. Query Parameters

```python
@app.get("/search")
async def search(q: str = None, limit: int = 10):
    return {"q": q, "limit": limit}
```

- **Default values** in signature → optional.
    
- **Type hints** enforce conversion & validation.
    

---

## 6. Request Bodies & Pydantic Models

**`schemas.py`**

```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    price: float
    tags: list[str] = []
```

**`main.py`**

```python
from fastapi import FastAPI
from .schemas import Item

app = FastAPI()

@app.post("/items/")
async def create_item(item: Item):
    return item
```

- **Automatic parsing** of JSON to `Item`.
    
- **Validation**: missing/invalid fields → descriptive error.
    
- **OpenAPI schema** generated from Pydantic models.
    

---

## 7. Response Models & Serialization

```python
from .schemas import Item, ItemOut

@app.get("/items/{id}", response_model=ItemOut)
async def get_item(id: int):
    item = fetch_from_db(id)   # raw dict or ORM model
    return item                # automatically converted to ItemOut
```

- **`response_model`** filters & serializes output.
    
- Protects against leaking internal fields.
    

---

## 8. Dependency Injection

**`dependencies.py`**

```python
from fastapi import Depends, HTTPException

def get_db():
    db = connect_to_db()
    try:
        yield db
    finally:
        db.close()
```

**`main.py`**

```python
@app.get("/users/")
async def list_users(db=Depends(get_db)):
    return db.query_users()
```

- **`Depends()`** injects dependencies cleanly.
    
- Supports **generator** functions for startup/teardown.
    

---

## 9. Security & Authentication

### 9.1 OAuth2 with Password (Bearer)

```python
from fastapi.security import OAuth2PasswordBearer

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")

@app.post("/token")
async def login(form_data: OAuth2PasswordRequestForm = Depends()):
    # verify user, return {"access_token": token, "token_type": "bearer"}

@app.get("/users/me")
async def read_users_me(token: str = Depends(oauth2_scheme)):
    user = verify_token(token)
    return user
```

- **Auto-generated `/docs` auth UI**.
    
- **Token extraction** handled by FastAPI.
    

### 9.2 API Key in Header/Query

```python
from fastapi import Security, APIKeyHeader

api_key_header = APIKeyHeader(name="X-API-Key")

@app.get("/secure")
async def secure_route(api_key: str = Security(api_key_header)):
    if api_key != "expected":
        raise HTTPException(403)
    return {"hello": "secure"}
```

---

## 10. Middleware & Events

### 10.1 Middleware

```python
from starlette.middleware.base import BaseHTTPMiddleware

class LogMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request, call_next):
        print(f"Request: {request.url}")
        response = await call_next(request)
        print(f"Response status: {response.status_code}")
        return response

app.add_middleware(LogMiddleware)
```

### 10.2 Startup & Shutdown Events

```python
@app.on_event("startup")
async def startup():
    # connect to services

@app.on_event("shutdown")
async def shutdown():
    # cleanup
```

---

## 11. Background Tasks

```python
from fastapi import BackgroundTasks

def write_log(message: str):
    with open("log.txt", "a") as f:
        f.write(message + "\n")

@app.post("/notify")
async def notify(background_tasks: BackgroundTasks):
    background_tasks.add_task(write_log, "User notified")
    return {"status": "queued"}
```

---

## 12. WebSockets

```python
from fastapi import WebSocket

@app.websocket("/ws")
async def websocket_endpoint(ws: WebSocket):
    await ws.accept()
    while True:
        data = await ws.receive_text()
        await ws.send_text(f"Echo: {data}")
```

---

## 13. File Uploads

```python
from fastapi import File, UploadFile

@app.post("/upload")
async def upload(file: UploadFile = File(...)):
    contents = await file.read()
    return {"filename": file.filename, "size": len(contents)}
```

---

## 14. CORS

```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_methods=["*"],
    allow_headers=["*"],
)
```

---

## 15. Pagination & Filtering

- Use **query params** for `skip`, `limit`.
    
- Leverage **Pydantic** for complex filters:
    
    ```python
    class ItemFilter(BaseModel):
        min_price: float = 0.0
        max_price: float = 100.0
    
    @app.get("/items/")
    async def list_items(filter: ItemFilter = Depends()):
        return query_db(filter.min_price, filter.max_price)
    ```
    

---

## 16. Testing

**`tests/test_main.py`**

```python
from fastapi.testclient import TestClient
from app.main import app

client = TestClient(app)

def test_read_root():
    res = client.get("/")
    assert res.status_code == 200
    assert res.json() == {"message": "Hello, FastAPI!"}
```

- Use **`TestClient`** from Starlette.
    
- Combine with **pytest** fixtures for dependencies.
    

---

## 17. Documentation & OpenAPI

- FastAPI auto-generates:
    
    - **OpenAPI schema** at `/openapi.json`
        
    - **Swagger UI** at `/docs`
        
    - **ReDoc** at `/redoc`
        

Customize metadata in `FastAPI(...)` constructor (`title`, `version`, `description`, `tags`).

---

## 18. Deployment

- **Uvicorn** or **Hypercorn** as ASGI servers.
    
- **Docker**:
    
    ```dockerfile
    FROM python:3.11
    WORKDIR /app
    COPY . .
    RUN pip install -r requirements.txt
    CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "80"]
    ```
    
- **Cloud Platforms**: AWS ECS/Fargate, Google Cloud Run, Azure Container Instances.
    
- **Serverless**: AWS Lambda + API Gateway via Mangum adapter.
    

---

## 19. Best Practices

1. **Pin dependencies** in `requirements.txt`.
    
2. **Use response models** to avoid leaking internals.
    
3. **Leverage type hints** everywhere for clarity.
    
4. **Structure code** with routers, models, schemas, and dependencies modules.
    
5. **Limit CORS** origins in production.
    
6. **Monitor** with middleware and structured logging.
    
7. **Write tests** for all routes, dependencies, and edge cases.
    

---

### 🚀 You’re Ready!

With this guide, you now understand FastAPI from basics to advanced usage. Go build fast, reliable, and type-safe APIs!