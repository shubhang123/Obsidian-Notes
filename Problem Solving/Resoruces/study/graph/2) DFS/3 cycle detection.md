#dfs
# Cycle Detection in Undirected Graph - Algorithm Analysis

## Overview

This algorithm detects whether a cycle exists in an undirected graph using Depth-First Search (DFS) traversal. The key insight is that in an undirected graph, a cycle exists if we encounter a visited vertex that is NOT the parent of the current vertex.
```cpp
#include <bits/stdc++.h>
using namespace std;

const int N = 1e5 + 10;  // Maximum number of vertices (100,010)

vector<int> g[N];  // Adjacency list representation of the graph
bool vis[N];       // Visited array to track which vertices have been explored

/*
 * DFS function to detect cycles in an undirected graph
 * 
 * Key Insight: In an undirected graph, a cycle exists if we encounter 
 * a visited vertex that is NOT the parent of the current vertex.
 * 
 * Parameters:
 * - vertex: current vertex being explored
 * - parent: the vertex from which we came to the current vertex
 * 
 * Returns: true if a cycle is detected, false otherwise
 */
bool dfs(int vertex, int parent) {
    vis[vertex] = true;  // Mark current vertex as visited
    bool doesLoopExist = false;
    
    // Explore all adjacent vertices (neighbors)
    for (int child : g[vertex]) {
        // Case 1: Skip the parent vertex (avoid false cycle detection)
        // In undirected graphs, parent is always in adjacency list
        if (vis[child] && child == parent) {
            continue; // This is just the edge we came from
        }
        
        // Case 2: Found a visited vertex that's NOT the parent
        // This indicates a back edge, which means a cycle exists
        if (vis[child] && child != parent) {
            doesLoopExist = true;
            continue; // Continue to check other neighbors
        }
        
        // Case 3: Unvisited vertex - recursively explore
        // If any subtree contains a cycle, propagate it upward
        if (!vis[child]) {
            doesLoopExist |= dfs(child, vertex);
        }
    }
    
    return doesLoopExist;
}

int main() {
    int v, e;  // v = number of vertices, e = number of edges
    cin >> v >> e;
    
    // Build the adjacency list representation
    // Since it's an undirected graph, add edge in both directions
    for (int i = 0; i < e; i++) {
        int v1, v2;
        cin >> v1 >> v2;
        g[v1].push_back(v2);  // Add edge v1 -> v2
        g[v2].push_back(v1);  // Add edge v2 -> v1 (undirected)
    }
    
    bool doesLoopExist = false;
    
    // Check all connected components
    // The graph might be disconnected, so we need to start DFS 
    // from every unvisited vertex
    for (int i = 1; i <= v; i++) {
        if (!vis[i]) {
            // Start DFS from vertex i with parent as 0 (no parent)
            doesLoopExist |= dfs(i, 0);
        }
    }
    
    // Output result: 1 if cycle exists, 0 otherwise
    cout << doesLoopExist << endl;
    
    return 0;
}
```
## Time and Space Complexity

### Time Complexity: O(V + E)

- **Vertex visits**: Each vertex is visited exactly once → O(V)
- **Edge traversals**: Each edge is traversed twice (once from each endpoint in undirected graph) → O(E)
- **Total**: O(V + E)

### Space Complexity: O(V + E)

- **Adjacency list storage**: O(V + E)
- **Visited array**: O(V)
- **Recursion stack**: O(V) in worst case (for a linear graph)
- **Total**: O(V + E)

## Core Algorithm Logic

### Cycle Detection Strategy

1. **DFS Traversal**: Use recursive DFS to explore the graph
2. **Parent Tracking**: Keep track of the parent vertex to avoid false positives
3. **Back Edge Detection**: If we encounter a visited vertex that's not our parent, we've found a back edge indicating a cycle

### Three Cases in DFS Loop

1. **Parent Edge**: `vis[child] && child == parent`
    - Skip this edge (it's the edge we came from)
    - Prevents false cycle detection
2. **Back Edge**: `vis[child] && child != parent`
    - Found a cycle! This is a back edge to an ancestor
    - Set `doesLoopExist = true`
3. **Tree Edge**: `!vis[child]`
    - Unvisited vertex, continue DFS recursively
    - Propagate cycle detection result upward

## Detailed Example

Consider this graph:

```
    1
   / \
  2---3
```

**Execution trace:**

1. Start DFS from vertex 1 (parent = 0)
2. Visit vertex 2 (parent = 1)
3. From vertex 2, visit vertex 3 (parent = 2)
4. From vertex 3, encounter vertex 1:
    - Vertex 1 is visited ✓
    - Vertex 1 is not parent (parent = 2) ✓
    - **Cycle detected!** Path: 1 → 2 → 3 → 1

## Edge Cases Handled

### Disconnected Graph

- **Problem**: Graph might have multiple connected components
- **Solution**: Check all unvisited vertices in main loop
- **Code**: `for (int i = 1; i <= v; i++) if (!vis[i]) dfs(i, 0);`

### Self Loops

- **Scenario**: Edge from vertex to itself (v1 == v2)
- **Detection**: Would be caught as `child != parent`
- **Note**: Input format typically doesn't include self loops

### Multiple Cycles

- **Behavior**: Algorithm detects if ANY cycle exists
- **Early termination**: Could be optimized to return immediately when first cycle is found
- **Current approach**: Continues checking all components

## Algorithm Variations

### Alternative Approaches

1. **Union-Find (Disjoint Set Union)**
    - Check if adding an edge creates a cycle
    - Time: O(E × α(V)) where α is inverse Ackermann function
2. **BFS-based Detection**
    - Similar logic but using queue instead of recursion
    - Same time complexity but different space usage pattern

### Optimization Opportunities

1. **Early Return**: Return immediately when first cycle is found
2. **Iterative DFS**: Use stack to avoid recursion overhead
3. **Cycle Counting**: Modify to count number of cycles instead of just detection

## Common Pitfalls

### Why Parent Tracking is Crucial

Without parent tracking, every edge would be detected as a cycle:

```cpp
// WRONG - without parent check
if (vis[child]) {
    return true; // This would always trigger on the parent!
}
```

### Index Considerations

- Vertices are 1-indexed in this implementation
- Arrays are 0-indexed but we use indices 1 to V
- Parent is initialized as 0 (non-existent vertex)

## Testing Strategy

### Test Cases to Consider

1. **Simple cycle**: Triangle (3 vertices, 3 edges)
2. **No cycle**: Tree (V vertices, V-1 edges)
3. **Disconnected with cycle**: Multiple components, one has cycle
4. **Single vertex**: Edge case with V=1
5. **Large cycle**: Performance testing with many vertices in cycle

### Expected Outputs

- **Cycle exists**: Output = 1
- **No cycle**: Output = 0
- **Tree structure**: Always outputs 0
- **Complete graph**: Always outputs 1 (many cycles)