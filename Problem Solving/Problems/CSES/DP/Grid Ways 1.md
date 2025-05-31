#dp #cses
```cpp
#include <bits/stdc++.h>
using namespace std;
int n;
int mod = 1e9 + 7;
void solveRec(int row, int col, vector<vector<char>>& grid) {
    if (row == n - 1 && col == n - 1) {
        ans++;
        return;
    }

    // go down
    if (row + 1 < n && grid[row + 1][col] != '*') {
        solve(row + 1, col, grid);
    }
    // go right
    if (col + 1 < n && grid[row][col + 1] != '*') {
        solve(row, col + 1, grid);
    }
}


int solve(int row, int col, vector<vector<char>>& grid, vector<vector<int>>& dp) {
    if (row == n - 1 && col == n - 1) {
        return 1;
    }

    int ways = 0;

    if (dp[row][col] != -1) return dp[row][col];
    // go down
    if (row + 1 < n && grid[row + 1][col] != '*') {
        ways = (ways + solve(row + 1, col, grid, dp)) % mod;
    }
    // go right
    if (col + 1 < n && grid[row][col + 1] != '*') {
        ways = (ways + solve(row, col + 1, grid, dp)) % mod;
    }

    return dp[row][col] = ways % mod;
}

int main() {
    cin >> n;

    vector<vector<char>> grid(n, vector<char>(n));
    vector<vector<int>> dp(n, vector<int>(n, -1));

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cin >> grid[i][j];
        }
    }

    if (grid[0][0] == '*' || grid[n - 1][n - 1] == '*') {
        cout << 0;
        return 0;
    }

    cout << solve(0, 0, grid, dp);
    return 0;
}

```

To **convert a recursive solution to memoization (top-down dynamic programming)** in C++, you follow a few structured steps. Let’s walk through them using your code as the base.

---

### ✅ Step-by-step Conversion from Recursive to Memoization

#### 🔁 **Step 1: Identify the Parameters of Recursion**

In your recursive function:

```cpp
void solveRec(int row, int col, vector<vector<char>>& grid)
```

the parameters that change are:

- `row` and `col`: current cell
    
- `grid`: the input matrix (remains constant)
    
- `ans`: a global counter (which you haven’t defined yet, but assuming it's used to count the paths)
    

So the **changing parameters** that define the recursive state are `row` and `col`.

---

#### 🧠 **Step 2: Add a Memoization Table**

Use a 2D DP table to memoize the number of ways from each cell:

```cpp
vector<vector<int>> dp(n, vector<int>(n, -1));
```

We use `-1` to indicate uncomputed states.

---

#### 🔁 **Step 3: Modify the Recursive Function to Return a Value**

Instead of using a global `ans++`, return the number of ways from each state:

```cpp
int solve(int row, int col, vector<vector<char>>& grid, vector<vector<int>>& dp)
```

---

#### 🧱 **Step 4: Add Base Case and Memoization Check**

Add these:

- **Base Case:** if you're at the destination cell, return 1.
    
- **Memo Check:** if value already computed for this state, return it.
    

```cpp
if (row == n - 1 && col == n - 1) return 1;
if (dp[row][col] != -1) return dp[row][col];
```

---

#### 🧭 **Step 5: Recurse and Store Result in `dp` Table**

Recurse to bottom and right cells (if valid), sum the ways, and store the result in `dp[row][col]`.

---

### 🔍 Final Dry Explanation of Code

- You start from `(0, 0)` and try to reach `(n-1, n-1)` only by moving **right** or **down**, and you can't go through cells with `*`.
    
- At each cell `(i, j)`, the total number of ways to reach the goal is:
    
    - ways from `(i+1, j)` **if** it's not a wall and within bounds
        
    - ways from `(i, j+1)` **if** it's not a wall and within bounds
        
- You cache the result using `dp[i][j]` to avoid recomputation.
    

---

### 🧠 Difference Summary:

|Aspect|Recursive (`solveRec`)|Memoization (`solve`)|
|---|---|---|
|Returns|void, uses global `ans`|Returns `int` (number of paths)|
|Repeats state|Yes|No, due to `dp[row][col]`|
|Time Complexity|Exponential (TLE for large `n`)|O(n²), since each cell is computed once|

---

Would you like me to show the full **iterative DP** (tabulation) version next for further optimization?