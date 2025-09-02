# DFS Tree Traversal with Subtree Computations - Complete Guide

## Overview

This algorithm demonstrates **Depth-First Search (DFS)** on a tree to compute subtree properties. It calculates two key metrics for each node:

1. **Subtree Sum**: Sum of all node values in the subtree rooted at each node
2. **Even Count**: Count of even-numbered nodes in each subtree

## Theoretical Concepts

### 1. Tree Representation

- **Adjacency List**: The tree is stored using `vector<int> g[N]` where `g[i]` contains all neighbors of node `i`
- **Undirected Tree**: Each edge is stored bidirectionally, but we use parent tracking to avoid cycles
- **Root**: Node 1 is chosen as the root (arbitrary choice)

### 2. DFS Traversal Pattern

The algorithm follows the classic DFS pattern with three key phases:

```
1. ENTER vertex (pre-processing)
2. RECURSE on children
3. EXIT vertex (post-processing)
```

### 3. Subtree Computation Strategy

**Bottom-up approach**:

- Process children first (recursive calls)
- Then aggregate results from children to parent
- This ensures when we process a node, all its subtree information is ready

## Algorithm Breakdown

### Input Format

```
n                    // Number of nodes
x1 y1               // Edge 1
x2 y2               // Edge 2
...
xn-1 yn-1           // Edge n-1 (tree has n-1 edges)
```

### Key Data Structures

- `g[N]`: Adjacency list representation of the tree
- `subtree_sum[N]`: Stores sum of all nodes in subtree rooted at each node
- `even_cnt[N]`: Stores count of even nodes in subtree rooted at each node

### DFS Function Analysis

```cpp
void dfs(int vertex, int parent) {
    // PHASE 1: Process current vertex (ENTER)
    if (vertex % 2 == 0) {
        even_cnt[vertex]++;        // Count this vertex if even
    }
    subtree_sum[vertex] += vertex; // Add this vertex to its subtree sum
    
    // PHASE 2: Process all children (RECURSE)
    for (int child : g[vertex]) {
        if (child == parent) continue;  // Skip parent to avoid cycles
        
        dfs(child, vertex);            // Recursive call
        
        // PHASE 3: Aggregate child results (POST-PROCESS)
        subtree_sum[vertex] += subtree_sum[child];
        even_cnt[vertex] += even_cnt[child];
    }
}
```

## Visual Example

Let's trace through a sample tree:

```
Tree Structure:
        1
       / \
      2   3
     /   / \
    4   5   6
```

### Step-by-Step Execution:

**Input:**

```
6
1 2
1 3
2 4
3 5
3 6
```

**DFS Traversal Order:** 1 → 2 → 4 → 3 → 5 → 6

### Detailed Trace:

1. **dfs(1, 0)**:
    
    - even_cnt[1] = 0 (1 is odd)
    - subtree_sum[1] = 1
    - Process children: 2, 3
2. **dfs(2, 1)**:
    
    - even_cnt[2] = 1 (2 is even)
    - subtree_sum[2] = 2
    - Process child: 4
3. **dfs(4, 2)**:
    
    - even_cnt[4] = 1 (4 is even)
    - subtree_sum[4] = 4
    - No children, return
4. **Back to dfs(2, 1)**:
    
    - Aggregate from child 4:
    - subtree_sum[2] += subtree_sum[4] = 2 + 4 = 6
    - even_cnt[2] += even_cnt[4] = 1 + 1 = 2
5. **dfs(3, 1)**:
    
    - even_cnt[3] = 0 (3 is odd)
    - subtree_sum[3] = 3
    - Process children: 5, 6
6. **dfs(5, 3)** and **dfs(6, 3)**:
    
    - Similar processing...
7. **Back to dfs(3, 1)**:
    
    - Aggregate from children 5 and 6
8. **Back to dfs(1, 0)**:
    
    - Aggregate from children 2 and 3

### Final Results:

```
Node | Subtree Sum | Even Count | Subtree Nodes
-----|-------------|------------|---------------
  1  |     21      |     3      | {1,2,3,4,5,6}
  2  |      6      |     2      | {2,4}
  3  |     14      |     1      | {3,5,6}
  4  |      4      |     1      | {4}
  5  |      5      |     0      | {5}
  6  |      6      |     1      | {6}
```

## Time and Space Complexity

### Time Complexity: O(n)

- Each node is visited exactly once
- Each edge is traversed exactly twice (once in each direction)
- Total operations: O(n + 2*(n-1)) = O(n)

### Space Complexity: O(n)

- Adjacency list: O(n) for storing edges
- Arrays: O(n) for subtree_sum and even_cnt
- Recursion stack: O(h) where h is height of tree
- In worst case (skewed tree): O(n)

## Key Algorithmic Insights

### 1. Parent Tracking

```cpp
if (child == parent) continue;
```

This prevents infinite recursion by avoiding traversal back to parent.

### 2. Bottom-Up Aggregation

```cpp
dfs(child, vertex);                    // Process child first
subtree_sum[vertex] += subtree_sum[child];  // Then aggregate
```

This ensures complete subtree information before aggregation.

### 3. Subtree Property

For any node v:

- `subtree_sum[v]` = sum of all nodes in subtree rooted at v
- `even_cnt[v]` = count of even nodes in subtree rooted at v

## Applications

This pattern is fundamental for:

1. **Tree DP**: Dynamic programming on trees
2. **Subtree Queries**: Answering queries about subtree properties
3. **Heavy-Light Decomposition**: Advanced tree algorithms
4. **Centroid Decomposition**: Tree decomposition techniques
5. **LCA Preprocessing**: Lowest Common Ancestor algorithms

## Common Variations

### 1. Multiple Properties

```cpp
int subtree_max[N], subtree_min[N], leaf_count[N];
```

### 2. Conditional Aggregation

```cpp
if (some_condition) {
    subtree_sum[vertex] += subtree_sum[child];
}
```

### 3. Path Queries

Store path information during DFS for path-related queries.

## Practice Problems

1. **Subtree Size**: Count nodes in each subtree
2. **Subtree Maximum**: Find maximum value in each subtree
3. **Distance Queries**: Compute distances from root to all nodes
4. **Tree Rerooting**: Compute answers for all possible roots

This algorithm demonstrates the power of DFS for tree computations and forms the foundation for many advanced tree algorithms.