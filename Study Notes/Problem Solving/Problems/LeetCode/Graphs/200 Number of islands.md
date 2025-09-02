Certainly! Here's a clean, well-structured explanation (as **code comments or notes**) of your **DFS-based solution to the “Number of Islands” problem**:
#dfs #graph
---

## 🔍 **Problem Summary:**

Given a `2D` grid of `'1'`s (land) and `'0'`s (water), count the number of **connected landmasses (islands)**. An island is formed by connecting adjacent `'1'`s **horizontally or vertically**.

```cpp
class Solution {
   public:
    int cnt = 0;
    int m, n;
    int vis[301][301];

    void dfs(int i, int j, vector<vector<char>>& grid) {
        // base condition so we dont go out of bounds
        if (i < 0 || j < 0 || i >= m || j >= n)
            return;

        // only run if it is a 1 as we need to find the connected components

        if (vis[i][j] || grid[i][j] == '0')
            return;

        vis[i][j] = 1;

        if (i - 1 >= 0) {
            dfs(i - 1, j, grid);
        }  // up
        if (j - 1 >= 0) {
            dfs(i, j - 1, grid);
        }  // left
        if (i + 1 < m) {
            dfs(i + 1, j, grid);
        }  // down
        if (j + 1 < n) {
            dfs(i, j + 1, grid);
        }  // right
    }

    int numIslands(vector<vector<char>>& grid) {
        memset(vis, 0, sizeof(vis));
        m = grid.size();
        n = grid[0].size();

        // finding connected components
        // or islands
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                // if already visited then skip
                if (!vis[i][j] && grid[i][j] == '1') {
                    dfs(i, j, grid);
                    // dfs will only be called again
                    // if it is not connected to any islands
                    // because if it was then it would have been
                    // visited by our dfs
                    cnt++;
                }
            }
        }

        return cnt;
    }
};
```
---

## ✅ **Approach: Depth-First Search (DFS)**

### 🔹 **Global Variables**

```cpp
int cnt = 0;                      // Total number of islands found
int m, n;                         // Grid dimensions (rows, cols)
int vis[301][301];               // Visited matrix to track explored cells
```

---

### 🔹 **DFS Function: `dfs(i, j, grid)`**

This function recursively explores all **4-connected** directions from the current land cell.

#### 📌 Base conditions:

```cpp
if (i < 0 || j < 0 || i >= m || j >= n)
    return;  // Out of bounds

if (vis[i][j] || grid[i][j] == '0')
    return;  // Already visited or water
```

#### ✅ Mark the cell as visited:

```cpp
vis[i][j] = 1;
```

#### 🔁 Recur in all 4 directions:

```cpp
if (i - 1 >= 0) dfs(i - 1, j, grid); // Up
if (j - 1 >= 0) dfs(i, j - 1, grid); // Left
if (i + 1 < m)  dfs(i + 1, j, grid); // Down
if (j + 1 < n)  dfs(i, j + 1, grid); // Right
```

This ensures **all connected `'1'`s** of the current island are marked as visited.

---

### 🔹 **Main Function: `numIslands(grid)`**

1. **Initialize**:
    

```cpp
memset(vis, 0, sizeof(vis));     // Clear the visited matrix
m = grid.size();                 // Rows
n = grid[0].size();              // Columns
```

2. **Loop over every cell in the grid**:
    

```cpp
for (int i = 0; i < m; i++) {
    for (int j = 0; j < n; j++) {
        if (!vis[i][j] && grid[i][j] == '1') {
            dfs(i, j, grid);     // Explore the entire island
            cnt++;               // Increment island count
        }
    }
}
```

- If a `'1'` is **unvisited**, it marks the start of a **new island**.
    
- `dfs()` visits all cells in that island.
    
- So `cnt++` is called only once per distinct island.
    

---

## 🔚 **Return the total number of islands**:

```cpp
return cnt;
```

---

## 🧠 Time and Space Complexity

- **Time Complexity**: `O(m * n)`  
    Every cell is visited at most once.
    
- **Space Complexity**: `O(m * n)`  
    Due to recursion stack + visited matrix.
    

---

### ✅ Summary:

This code effectively performs a **flood fill DFS** to explore each island fully and count only distinct island groups. It avoids revisiting by marking visited cells, ensuring each island is counted once.

Let me know if you’d like this explained in interview-style bullet points or want a BFS version too.