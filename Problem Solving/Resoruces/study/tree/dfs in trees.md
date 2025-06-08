# Depth First Search (DFS) in N-ary Trees - Complete Notes

Of course! Here are detailed notes on Depth First Search (DFS) in N-ary trees, with a focus on the classic problem of finding the depth and height of every node.

---

## **Part 1: Core Concepts and Theory**

### 1.1 What is an N-ary Tree?

An N-ary tree is a tree data structure where each node can have at most 'N' children. A binary tree is a specific type of N-ary tree where N=2. In a general N-ary tree, a node can have any number of children, and we don't have the concept of a "left" or "right" child, but rather a list of children.

**Representation:** While you can create a `Node` class with a `vector<Node*>` for its children, a very common and efficient way to represent N-ary trees (and graphs in general) in competitive programming and algorithms is using an **Adjacency List**.

- An adjacency list is an array of vectors. For a tree with `V` vertices, we'd have `vector<int> adj[V+1]`.
- `adj[u]` stores a list of all nodes directly connected to node `u`. Since it's a tree, these are its parent and its children.

### 1.2 What is Depth First Search (DFS)?

DFS is an algorithm for traversing or searching a tree or graph. The algorithm starts at a chosen root node and explores as far as possible along each branch before backtracking.

**The Core Idea:**

1. Start at a node `u`.
2. Mark `u` as visited.
3. Perform some action on `u`.
4. For each unvisited neighbor `v` of `u`, recursively call DFS on `v`.
5. After all neighbors have been fully explored, backtrack.

This "go deep first" strategy is what gives it its name. The recursive nature of DFS makes it particularly elegant for tree problems.

### 1.3 Theory: Depth vs. Height

This is the most crucial part. People often confuse these two terms, but they are distinct concepts.

**A. Depth of a Node**

- **Definition:** The **depth** of a node `u` is the length of the path from the **root** of the tree to `u`. The length of a path is the number of edges in it.
- **Key Properties:**
    - The depth of the root node is always **0**.
    - If node `v` is a child of node `u`, then `depth(v) = depth(u) + 1`.
- **How to Calculate:** Depth is a "top-down" property. As we descend the tree from the root, we can easily calculate the depth of each node we visit. This fits perfectly with the natural flow of a DFS traversal. We can simply pass the current depth down as a parameter in our recursive function.

**B. Height of a Node**

- **Definition:** The **height** of a node `u` is the length of the longest path from `u` to any **leaf node** in its own subtree.
- **Key Properties:**
    - The height of a leaf node is always **0**.
    - For any non-leaf node `u`, its height is `1 + max(height of its children)`.
    - The height of the entire tree is simply the height of its root node.
- **How to Calculate:** Height is a "bottom-up" property. To calculate the height of a node `u`, we first need to know the heights of all its children. This means we can only compute the height of `u` _after_ the DFS calls for all its children have completed and returned. This is a classic **post-order** action in a traversal.

---

## **Part 2: The Combined Algorithm**

We can cleverly calculate both depth and height for all nodes in a **single DFS pass**. The key is to understand when each value can be computed.

- **Depth:** Calculated on the way **down** (pre-order action). When we first arrive at a node, we can immediately set its depth.
- **Height:** Calculated on the way **back up** (post-order action). After we have visited all of a node's children and calculated their heights, we can then calculate the parent's height.

Let's design our DFS function: `dfs(currentNode, parentNode, currentDepth)`

1. **Enter the function for `currentNode`:**
    
    - This is a **pre-order** position (before recursive calls).
    - Set `depth[currentNode] = currentDepth`.
    - Initialize `height[currentNode] = 0`. We assume it's a leaf until proven otherwise.
2. **Loop through the neighbors of `currentNode`:**
    
    - For each neighbor `v`:
        - If `v` is the `parentNode`, skip it to avoid going back up the tree immediately.
        - Make the recursive call: `dfs(v, currentNode, currentDepth + 1)`.
3. **After the recursive call `dfs(v, ...)` returns:**
    
    - This is a **post-order** position (after a recursive call has fully finished).
    - We now know the final computed `height[v]`.
    - Update the parent's height: `height[currentNode] = max(height[currentNode], 1 + height[v])`. This formula correctly finds the longest path among all children's subtrees.
4. **Exit the function for `currentNode`:** The `depth` and `height` for this node are now finalized.
    

---

## **Part 3: Example Walkthrough**

Let's trace the algorithm on this tree. Let's assume **Node 1 is the root**.

**Tree Structure:**

- 1 is connected to 2, 3
- 2 is connected to 4, 5
- 3 is connected to 6

```
        1
       / \
      2   3
     / \   \
    4   5   6
```

**DFS Trace (`dfs(u, p, d)`):**

1. `dfs(1, 0, 0)`:
    - `depth[1] = 0`.
    - `height[1] = 0`.
    - Recurse on child 2: `dfs(2, 1, 1)`
        - `depth[2] = 1`.
        - `height[2] = 0`.
        - Recurse on child 4: `dfs(4, 2, 2)`
            - `depth[4] = 2`.
            - `height[4] = 0`. (It's a leaf, has no children to recurse on).
            - **Returns.**
        - Back in `dfs(2)`: We just came back from child 4. Update height of 2:
            - `height[2] = max(height[2], 1 + height[4]) = max(0, 1 + 0) = 1`.
        - Recurse on child 5: `dfs(5, 2, 2)`
            - `depth[5] = 2`.
            - `height[5] = 0`. (It's a leaf).
            - **Returns.**
        - Back in `dfs(2)`: We just came back from child 5. Update height of 2:
            - `height[2] = max(height[2], 1 + height[5]) = max(1, 1 + 0) = 1`.
        - `dfs(2)` has no more children. **Returns.**
    - Back in `dfs(1)`: We just came back from child 2. Update height of 1:
        - `height[1] = max(height[1], 1 + height[2]) = max(0, 1 + 1) = 2`.
    - Recurse on child 3: `dfs(3, 1, 1)`
        - `depth[3] = 1`.
        - `height[3] = 0`.
        - Recurse on child 6: `dfs(6, 3, 2)`
            - `depth[6] = 2`.
            - `height[6] = 0`. (It's a leaf).
            - **Returns.**
        - Back in `dfs(3)`: We just came back from child 6. Update height of 3:
            - `height[3] = max(height[3], 1 + height[6]) = max(0, 1 + 0) = 1`.
        - `dfs(3)` has no more children. **Returns.**
    - Back in `dfs(1)`: We just came back from child 3. Update height of 1:
        - `height[1] = max(height[1], 1 + height[3]) = max(2, 1 + 1) = 2`.
    - `dfs(1)` has no more children. **Finished.**

**Final Arrays:**

|Node|Depth|Height|
|---|---|---|
|1|0|2|
|2|1|1|
|3|1|1|
|4|2|0|
|5|2|0|
|6|2|0|

---

## **Part 4: C++ Implementation**

Here is the complete, commented C++ code that implements this single-pass DFS algorithm.

```cpp
#include <iostream>
#include <vector>
#include <algorithm> // For std::max

// Using a constant for max number of nodes is good practice.
const int MAX_NODES = 100005;

// Adjacency list to represent the N-ary tree.
// adj[i] will store a list of nodes connected to node i.
std::vector<int> adj[MAX_NODES];

// Arrays to store the final computed depth and height for each node.
int depth[MAX_NODES];
int height[MAX_NODES];

/**
 * @brief Performs a single DFS pass to calculate depth and height of all nodes.
 * 
 * @param u The current node being visited.
 * @param p The parent of the current node (to avoid going backward).
 * @param d The depth of the current node 'u'.
 */
void dfs(int u, int p, int d) {
    // ---- PRE-ORDER ACTION ----
    // This part of the code executes when we first visit a node,
    // before visiting its children.
    
    // 1. Set the depth of the current node.
    // The depth is passed down from the parent.
    depth[u] = d;
    
    // 2. Initialize the height of the current node to 0.
    // By default, every node is a leaf (height 0) until we find children.
    height[u] = 0;
    
    // ---- RECURSION ----
    // Explore all neighbors of the current node.
    for (int v : adj[u]) {
        // We check if the neighbor 'v' is the parent 'p'.
        // If it is, we skip it to prevent an infinite loop (e.g., 1->2->1).
        if (v == p) {
            continue;
        }
        
        // Recurse on the child 'v'. Its parent is 'u', and its depth is 'd+1'.
        dfs(v, u, d + 1);
        
        // ---- POST-ORDER ACTION ----
        // This part of the code executes *after* the recursive call for a child 'v'
        // has completely finished. This means we have already computed the
        // correct height for the entire subtree of 'v'.
        
        // 3. Update the height of the parent 'u' based on its children's heights.
        // The height of 'u' is 1 + the maximum height among all its children.
        height[u] = std::max(height[u], 1 + height[v]);
    }
}

int main() {
    // Fast I/O
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    int n;
    std::cout << "Enter the number of nodes in the tree: ";
    std::cin >> n;

    // A tree with 'n' nodes has exactly 'n-1' edges.
    std::cout << "Enter the " << n - 1 << " edges (u v) of the tree:\n";
    for (int i = 0; i < n - 1; ++i) {
        int u, v;
        std::cin >> u >> v;
        // Add the edge to the adjacency list for both nodes.
        adj[u].push_back(v);
        adj[v].push_back(u);
    }
    
    // We need to pick a root for the tree. Node 1 is a common choice.
    // The call to DFS:
    // - Start at node 1.
    // - Its parent is a dummy node 0 (since root has no parent).
    // - Its depth is 0.
    int root_node = 1;
    dfs(root_node, 0, 0);

    // Print the results
    std::cout << "\n--- Results ---\n";
    std::cout << "Node\tDepth\tHeight\n";
    std::cout << "---------------------\n";
    for (int i = 1; i <= n; ++i) {
        std::cout << i << "\t" << depth[i] << "\t" << height[i] << "\n";
    }

    return 0;
}
```

### How to Compile and Run:

1. Save the code as a `.cpp` file (e.g., `tree_depth_height.cpp`).
2. Compile it using a C++ compiler like g++: `g++ tree_depth_height.cpp -o tree_solver`
3. Run the executable: `./tree_solver`

**Sample Input/Output (for the example tree):**

```
Enter the number of nodes in the tree: 6
Enter the 5 edges (u v) of the tree:
1 2
1 3
2 4
2 5
3 6

--- Results ---
Node    Depth   Height
---------------------
1       0       2
2       1       1
3       1       1
4       2       0
5       2       0
6       2       0
```