```cpp

class Solution {
   public:
    int m, n;
    int dfs(int i, int j, vector<vector<int>>& grid,
            vector<vector<bool>>& vis) {
        //making sure the directions are valid
        //and doesnt go out of boundaries
        if (i < 0 || j < 0 || i >= m || j >= n)
            return 0;
        if (vis[i][j])
            return 0;
        //checking if the value is 0, if yes we will skip it
        if (grid[i][j] == 0)
            return 0;

        vis[i][j] = true;
		//including the cell itself as well 
		//that is why area is 1
        int area = 1;

		//keep adding the area to the area
		//recursively
        area += dfs(i + 1, j, grid, vis);
        area += dfs(i - 1, j, grid, vis);
        area += dfs(i, j - 1, grid, vis);
        area += dfs(i, j + 1, grid, vis);

        return area;
    }
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        m = grid.size();
        n = grid[0].size();

        vector<vector<bool>> vis(m, vector<bool>(n, false));

        int maxArea = 0;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (!vis[i][j] && grid[i][j] == 1) {
                    maxArea = max(maxArea, dfs(i, j, grid, vis));
                }
            }
        }
        return maxArea;
    }
};
```

# Max Area of Island - Code Notes

## Problem Overview

This solution finds the maximum area of an island in a 2D binary grid, where `1` represents land and `0` represents water. An island is a group of connected `1`s (horizontally or vertically adjacent).

## Algorithm: Depth-First Search (DFS)

### Key Components

#### Class Variables

- `m`: Number of rows in the grid
- `n`: Number of columns in the grid

#### Main Function: `maxAreaOfIsland()`

**Purpose**: Iterate through the entire grid and find the maximum island area

**Process**:

1. Initialize grid dimensions (`m` and `n`)
2. Create a visited matrix to track explored cells
3. Iterate through each cell in the grid
4. For unvisited land cells (`grid[i][j] == 1`), start DFS to calculate island area
5. Keep track of the maximum area found

#### Helper Function: `dfs()`

**Purpose**: Calculate the area of an island starting from a given cell

**Parameters**:

- `i, j`: Current cell coordinates
- `grid`: The input grid
- `vis`: Visited matrix to avoid revisiting cells

**Base Cases** (Return 0):

- Out of bounds: `i < 0 || j < 0 || i >= m || j >= n`
- Already visited: `vis[i][j] == true`
- Water cell: `grid[i][j] == 0`

**Recursive Process**:

1. Mark current cell as visited
2. Initialize area count as 1 (current cell)
3. Recursively explore all 4 directions (up, down, left, right)
4. Sum up areas from all connected land cells
5. Return total area

## Time & Space Complexity

**Time Complexity**: O(m × n)

- Each cell is visited at most once due to the visited matrix
- In worst case, we visit every cell in the grid

**Space Complexity**: O(m × n)

- Visited matrix: O(m × n)
- Recursion stack: O(m × n) in worst case (when entire grid is one large island)

## Key Algorithm Features

### Visited Matrix Pattern

- Prevents infinite loops and redundant calculations
- Ensures each cell is processed exactly once
- Boolean matrix parallel to the input grid

### 4-Directional Exploration

- Explores horizontally and vertically adjacent cells
- Does not consider diagonal connections
- Uses coordinate offsets: `(+1,0)`, `(-1,0)`, `(0,-1)`, `(0,+1)`

### Boundary Checking

- Explicit bounds checking prevents array out-of-bounds errors
- Handles edge cases naturally

## Example Walkthrough

For grid:

```
[1,1,0]
[0,1,0]
[0,0,1]
```

1. Start at (0,0): DFS explores (0,0)→(0,1)→(1,1), returns area 3
2. Skip water cells and visited cells
3. Start at (2,2): DFS returns area 1
4. Maximum area = max(3,1) = 3

## Alternative Approaches

- **BFS**: Use queue instead of recursion, same time/space complexity
- **Union-Find**: Good for dynamic connectivity problems
- **Iterative DFS**: Use explicit stack to avoid recursion depth issues