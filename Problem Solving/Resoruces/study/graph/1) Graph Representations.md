# Graph Representations: Adjacency Matrix vs Adjacency List

## Overview

Graphs can be represented in computer memory using two primary data structures: adjacency matrices and adjacency lists. Each representation has distinct advantages and trade-offs that make them suitable for different scenarios.

## Adjacency Matrix

### Definition

An adjacency matrix is a 2D array where `matrix[i][j]` represents the relationship between vertex `i` and vertex `j`. For unweighted graphs, the value is typically 1 (edge exists) or 0 (no edge). For weighted graphs, the value represents the weight of the edge.

### Characteristics

**Space Complexity:** O(n²)

- Requires n² space regardless of the actual number of edges
- Memory usage grows quadratically with the number of vertices

**Practical Limitations:**

- Cannot efficiently handle graphs with more than ~10⁴ vertices due to memory constraints
- For n = 10⁴, requires 100 million entries (approximately 400MB for integers)

**Time Complexities:**

- **Edge lookup:** O(1) - Direct array access to check if edge exists
- **Add edge:** O(1) - Simple assignment operation
- **Remove edge:** O(1) - Set value to 0 or null
- **Get all neighbors:** O(n) - Must scan entire row

### Advantages

- **Constant-time edge queries:** Checking if an edge exists between two vertices is O(1)
- **Easy weight storage:** Natural support for weighted graphs by storing weights directly
- **Simple implementation:** Straightforward to code and understand
- **Efficient for dense graphs:** When the graph has many edges relative to vertices

### Disadvantages

- **High space overhead:** Uses O(n²) space even for sparse graphs
- **Scalability issues:** Impractical for large graphs (n > 10⁴)
- **Inefficient neighbor iteration:** Finding all neighbors requires O(n) time
## C++ Implementation

### Adjacency Matrix Implementation

```cpp
#include <iostream>
#include <vector>
using namespace std;

class AdjacencyMatrix {
private:
    vector<vector<int>> matrix;
    int vertices;
    
public:
    // Constructor
    AdjacencyMatrix(int v) {
        vertices = v;
        matrix.assign(v, vector<int>(v, 0));
    }
    
    // Add edge (for unweighted graph)
    void addEdge(int src, int dest) {
        matrix[src][dest] = 1;
        matrix[dest][src] = 1; // For undirected graph
    }
    
    // Add weighted edge
    void addWeightedEdge(int src, int dest, int weight) {
        matrix[src][dest] = weight;
        matrix[dest][src] = weight; // For undirected graph
    }
    
    // Remove edge
    void removeEdge(int src, int dest) {
        matrix[src][dest] = 0;
        matrix[dest][src] = 0;
    }
    
    // Check if edge exists - O(1)
    bool hasEdge(int src, int dest) {
        return matrix[src][dest] != 0;
    }
    
    // Get weight of edge
    int getWeight(int src, int dest) {
        return matrix[src][dest];
    }
    
    // Print all neighbors of a vertex - O(V)
    void printNeighbors(int vertex) {
        cout << "Neighbors of " << vertex << ": ";
        for (int i = 0; i < vertices; i++) {
            if (matrix[vertex][i] != 0) {
                cout << i << "(" << matrix[vertex][i] << ") ";
            }
        }
        cout << endl;
    }
    
    // Print the entire matrix
    void printMatrix() {
        for (int i = 0; i < vertices; i++) {
            for (int j = 0; j < vertices; j++) {
                cout << matrix[i][j] << " ";
            }
            cout << endl;
        }
    }
};
```


## Adjacency List

### Definition

An adjacency list represents a graph as an array of lists. Each vertex has a list containing all vertices adjacent to it. For weighted graphs, each list entry can store both the destination vertex and the edge weight.

### Characteristics

**Space Complexity:** O(V + E)

- V is the number of vertices, E is the number of edges
- Much more space-efficient for sparse graphs

**Time Complexities:**

- **Edge lookup:** O(degree of vertex) - Must search through the list
- **Add edge:** O(1) - Add to the beginning of the list
- **Remove edge:** O(degree of vertex) - Search and remove from list
- **Get all neighbors:** O(degree of vertex) - Direct list access

### Advantages

- **Space efficient:** Only stores existing edges, ideal for sparse graphs
- **Scalable:** Can handle graphs with millions of vertices
- **Fast neighbor iteration:** Direct access to all neighbors of a vertex
- **Dynamic:** Easy to add/remove vertices and edges

### Disadvantages

- **Slower edge queries:** Checking edge existence requires list traversal
- **More complex weight handling:** Requires additional data structures for weights

## When to Use Which?

### Use Adjacency Matrix When:

- Graph is dense (many edges relative to vertices)
- Frequent edge existence queries
- Graph size is small to moderate (n ≤ 10⁴)
- Working with weighted graphs where quick weight access is needed
- Algorithm requires O(1) edge lookups

### Use Adjacency List When:

- Graph is sparse (few edges relative to vertices)
- Large number of vertices (n > 10⁴)
- Frequent traversal operations (DFS, BFS)
- Memory is a constraint
- Dynamic graph operations (frequent additions/deletions)


### Adjacency List Implementation

```cpp
#include <iostream>
#include <vector>
using namespace std;

const int N = 1e5 + 10; // max number of vertices
vector<int> graph[N];   // graph[u] holds neighbors of node u
int n, m;               // n = number of vertices, m = number of edges

// Add edge (undirected)
void addEdge(int u, int v) {
    graph[u].push_back(v);
    graph[v].push_back(u);
}

// Print neighbors of a node
void printNeighbors(int u) {
    cout << "Neighbors of " << u << ": ";
    for (int v : graph[u]) {
        cout << v << " ";
    }
    cout << endl;
}

// Print full adjacency list
void printGraph() {
    for (int i = 0; i < n; ++i) {
        cout << i << ": ";
        for (int v : graph[i]) {
            cout << v << " ";
        }
        cout << endl;
    }
}

// Check if edge exists between u and v
bool hasEdge(int u, int v) {
    for (int x : graph[u]) {
        if (x == v) return true;
    }
    return false;
}

// Remove edge (undirected)
void removeEdge(int u, int v) {
    // remove v from u's list
    for (int i = 0; i < graph[u].size(); ++i) {
        if (graph[u][i] == v) {
            graph[u].erase(graph[u].begin() + i);
            break;
        }
    }

    // remove u from v's list
    for (int i = 0; i < graph[v].size(); ++i) {
        if (graph[v][i] == u) {
            graph[v].erase(graph[v].begin() + i);
            break;
        }
    }
}


```


## Example Comparison

For a graph with 1000 vertices:

- **Adjacency Matrix:** Always uses 1,000,000 entries
- **Adjacency List:** Uses only 2 × (number of edges) entries

If the graph has only 5,000 edges, the adjacency list uses 200 times less memory than the adjacency matrix.

## 🧠 What is `vector<int> g[N]`?

It is an **array of vectors**, where:

- `N` is a constant (e.g., `1e5 + 10`)
    
- Each `g[i]` is a `vector<int>` that stores the **neighbors** of vertex `i`.
    

This is a way to represent an **adjacency list** for an **unweighted graph**.

---

## 🔍 Visual Example

### Suppose we have this **undirected graph**:

```
     0
    / \
   1   2
        \
         3
```

### Edges:

```
(0, 1)
(0, 2)
(2, 3)
```

### Code to Build It:

```cpp
addEdge(0, 1);
addEdge(0, 2);
addEdge(2, 3);
```

### Then `g[]` will look like:

```
g[0] = [1, 2]      // 0 is connected to 1 and 2
g[1] = [0]         // 1 is connected to 0
g[2] = [0, 3]      // 2 is connected to 0 and 3
g[3] = [2]         // 3 is connected to 2
g[4] = []          // unused vertex
g[5] = []          // unused vertex
...
```

---

## 🔧 Visualization as a Table

|Index `i` (Node)|`g[i]` (Neighbors)|
|---|---|
|`0`|`1, 2`|
|`1`|`0`|
|`2`|`0, 3`|
|`3`|`2`|
|`4`|(empty)|
|...|(empty)|

---

## 🖼 Visual Graph ↔ Adjacency List

### Graph:

```
0 —— 1
|
2 —— 3
```

### Adjacency List via `g[N]`:

```cpp
g[0]: 1 2
g[1]: 0
g[2]: 0 3
g[3]: 2
```

---

## 📌 Important Notes

- The order in `g[i]` depends on the order of `addEdge()`.
    
- It's ideal for DFS, BFS, and other graph algorithms.
    
- Memory-efficient for sparse graphs (i.e., when number of edges is much less than `n²`).
    

---

Would you like a **visual image-style diagram** or perhaps a **console-based simulation of adding and printing edges**? I can provide both.