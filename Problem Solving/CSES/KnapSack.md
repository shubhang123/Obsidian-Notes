Here’s your code again with **inline comments and theory explanations** for each section. The problem it's solving is the classic **0/1 Knapsack** using both **brute force** and **memoization (top-down DP)**.

---

```cpp
#include <bits/stdc++.h>
using namespace std;

// Constants
const int N = 1005;

// Input arrays:
// wt[i] = weight of the i-th item
// val[i] = value of the i-th item
int wt[N], val[N];

// Memoization table: dp[i][w] = max value we can get using first i items with capacity w
int dp[1001][100001];

// --------------------------
// Brute Force Recursive Approach (no memoization)
// --------------------------
// Try all combinations of including or excluding each item
int bruteForce(int index, int weightLeft) {
    if (index < 0 || weightLeft < 0)
        return 0;

    // Option 1: skip the current item
    int skip = bruteForce(index - 1, weightLeft);

    // Option 2: take the current item if it fits
    int take = 0;
    if (weightLeft >= wt[index])
        take = bruteForce(index - 1, weightLeft - wt[index]) + val[index];

    // Return the better of the two
    return max(take, skip);
}

// --------------------------
// Recursive with Memoization (Top-Down DP)
// --------------------------
// We store results in dp[][] to avoid recomputation
int rec(int index, int weightLeft) {
    if (index < 0 || weightLeft < 0)
        return 0;

    // If already computed, return it
    if(dp[index][weightLeft] != -1) return dp[index][weightLeft];

    // Option 1: skip this item
    int skip = rec(index - 1, weightLeft);

    // Option 2: take this item (if it fits)
    int take = 0;
    if (weightLeft >= wt[index])
        take = rec(index - 1, weightLeft - wt[index]) + val[index];

    // Store and return the maximum
    return dp[index][weightLeft] = max(take, skip);
}

int main() {
    int n, capacity;
    cin >> n >> capacity;

    // Read item weights
    for (int i = 0; i < n; i++) cin >> wt[i];

    // Read item values
    for (int i = 0; i < n; i++) cin >> val[i];

    // Initialize memoization table to -1 (uncomputed)
    memset(dp, -1, sizeof(dp));

    // Compute result using memoized recursion
    int ans = rec(n - 1, capacity); 

    cout << ans << '\n';
    return 0;
}
```

---

## 🧠 THEORY: 0/1 Knapsack Problem

### ✅ Problem Statement:

You are given:

- `n` items
    
- Each item has a **weight** `wt[i]` and a **value** `val[i]`
    
- A **maximum weight capacity** of the knapsack
    

**Goal**: Maximize the total value of selected items such that total weight ≤ capacity.

Each item can either be:

- Taken **once**
    
- Or **not at all** (that’s why it’s called **0/1** knapsack)
    

---

### ✅ Recurrence Relation:

Let `dp[i][w]` be the max value we can get using items `0..i` with weight limit `w`.

```cpp
dp[i][w] = max(
  dp[i-1][w],                            // skip current item
  dp[i-1][w - wt[i]] + val[i]           // take current item (if it fits)
)
```

### ✅ Base Case:

- `dp[-1][w] = 0` for all `w` (no items, no value)
    

---

### ✅ Time and Space Complexity

- **Brute force**: O(2^n) — exponential (tries every combination)
    
- **Memoized (top-down)**: O(n × W)
    
    - Where `n` = number of items, `W` = capacity
        
- **Space**: O(n × W) for `dp[][]`
    

---

Let me know if you'd like a bottom-up (iterative) version or space-optimized variant too.