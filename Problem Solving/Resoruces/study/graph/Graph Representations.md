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

// Global graph representation
int vertices;
vector<vector<pair<int, int>>> adjList; // Each pair is {neighbor, weight}

// Add unweighted edge (default weight = 1)
void addEdge(int src, int dest) {
    adjList[src].push_back({dest, 1});
    adjList[dest].push_back({src, 1}); // Undirected
}

// Add weighted edge
void addWeightedEdge(int src, int dest, int weight) {
    adjList[src].push_back({dest, weight});
    adjList[dest].push_back({src, weight}); // Undirected
}

// Remove edge (slower than list, but works)
void removeEdge(int src, int dest) {
    // Remove from src's list
    for (int i = 0; i < adjList[src].size(); ++i) {
        if (adjList[src][i].first == dest) {
            adjList[src].erase(adjList[src].begin() + i);
            break; // Exit after removing one occurrence
        }
    }

    // Remove from dest's list (for undirected graph)
    for (int i = 0; i < adjList[dest].size(); ++i) {
        if (adjList[dest][i].first == src) {
            adjList[dest].erase(adjList[dest].begin() + i);
            break;
        }
    }
}


// Check if edge exists
bool hasEdge(int src, int dest) {
    for (const auto& p : adjList[src]) {
        if (p.first == dest) return true;
    }
    return false;
}

// Get weight of edge
int getWeight(int src, int dest) {
    for (const auto& p : adjList[src]) {
        if (p.first == dest) return p.second;
    }
    return -1; // Not found
}

// Print neighbors
void printNeighbors(int vertex) {
    cout << "Neighbors of " << vertex << ": ";
    for (const auto& p : adjList[vertex]) {
        cout << p.first << "(" << p.second << ") ";
    }
    cout << endl;
}

// Print the entire adjacency list
void printList() {
    for (int i = 0; i < vertices; i++) {
        cout << i << ": ";
        for (const auto& p : adjList[i]) {
            cout << p.first << "(" << p.second << ") ";
        }
        cout << endl;
    }
}

```


## Example Comparison

For a graph with 1000 vertices:

- **Adjacency Matrix:** Always uses 1,000,000 entries
- **Adjacency List:** Uses only 2 × (number of edges) entries

If the graph has only 5,000 edges, the adjacency list uses 200 times less memory than the adjacency matrix.