#cses #dp #recursion


---

### ✅ **Part 1: How the recursion works**

The function:

```cpp
int solve(int n) {
    if (n == 0) return 1; 
    if (n < 0) return 0;   

    int sum = 0;
    for (int i = 1; i <= 6; i++) {
        sum = (sum + solve(n - i)) % mod;
    }
    return sum;
}
```

This function **counts the number of ways to reach sum `n` by throwing dice**, where each dice roll can give you 1 to 6. It's a variation of the **"dice combinations"** or **staircase problem**.

---

#### 🎯 What is the recurrence doing?

Let’s say you're at state `n`. From here:

- You could have come from `n-1`, if you rolled a `1`.
    
- Or from `n-2`, if you rolled a `2`.
    
- ...
    
- Or from `n-6`, if you rolled a `6`.
    

So the number of ways to reach `n` is:

```cpp
solve(n) = solve(n-1) + solve(n-2) + ... + solve(n-6)
```

And:

- `solve(0) = 1` because there's one way to make 0 sum: doing nothing.
    
- `solve(n < 0) = 0` because you can't go below 0 using positive numbers.
    

---

### 🧠 **Part 2: Tree Diagram and Making Recursive Code from It**

To build recursive code from a **recursion tree diagram**, follow these steps:

---

#### 🔹 Step 1: Draw the tree

Let’s take a small example: `solve(3)`

```
          solve(3)
        /   |   |   |   |   \
    (1)  (2) (3) (4) (5) (6)
   /      (skip n<0) ...
solve(2)
  |
  --> solve(1)
        |
        --> solve(0) → returns 1
        --> solve(-1) → returns 0
        ...
```

Each node splits into 6 children: `solve(n-1)` to `solve(n-6)`  
The base cases `solve(0)` return 1, and `solve(n < 0)` return 0.

---

#### 🔹 Step 2: Find pattern

If you observe the tree:

- Each node is the **sum of 6 previous nodes** (unless out of bounds).
    
- So `solve(n)` can be expressed in terms of `solve(n-1)` to `solve(n-6)`
    

---

#### 🔹 Step 3: Code it recursively

Now write the code by expressing this pattern:

```cpp
int solve(int n) {
    if (n == 0) return 1;       // Base case
    if (n < 0) return 0;

    int total = 0;
    for (int i = 1; i <= 6; ++i) {
        total += solve(n - i);  // Recursive step
    }
    return total;
}
```

Add `% mod` for large values, and you're done.

---

### 🚀 Optimize with Memoization (Top-Down DP)

Because this recursion repeats a lot (`solve(3)` calls `solve(2)` calls `solve(1)` ... multiple times), you can memoize:

```cpp
int solve(int n, vector<int>& dp) {
    if (n == 0) return 1;
    if (n < 0) return 0;
    if (dp[n] != -1) return dp[n];

    int total = 0;
    for (int i = 1; i <= 6; ++i) {
        total = (total + solve(n - i, dp)) % mod;
    }
    return dp[n] = total;
}
```

Call it from `main()` like this:

```cpp
int main() {
    int n;
    cin >> n;
    vector<int> dp(n+1, -1);
    cout << solve(n, dp);
}
```

---

### 🧩 Summary

- You use a **tree** to visualize all possible paths (e.g., how to break down `n`).
    
- Recursion comes from following “what could be the previous state?”
    
- Memoization avoids recomputation by storing answers of overlapping subproblems.
    

---

Would you like me to draw the tree diagram for `solve(4)` or help convert this to bottom-up DP?