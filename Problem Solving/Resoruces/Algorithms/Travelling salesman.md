Below is a “zoom-out → zoom-in” tour of the Travelling Salesman Problem (TSP).  
We’ll start with the **most naïve brute-force** idea, tighten the screws until we reach the **classic optimal bit-mask DP**, then briefly mention why real-world solvers still go further (branch-and-bound, heuristics, ILP, etc.).

---

## 0. Problem Recap (sym-metric version)

_Given an undirected complete graph with `n` cities and distance matrix `dist[i][j]`, find the minimum-length tour that starts at city 0, visits every other city **exactly once**, and returns to city 0._

---

## 1. Brute Force – Enumerate All Permutations

|Item|Explanation|
|---|---|
|**Idea**|Try every ordering of the `n-1` remaining cities: `(0, p₁, p₂, …, pₙ₋₁, 0)`|
|**States searched**|`(n-1)!` permutations|
|**Time**|`O((n-1)!)`|
|**Space**|`O(1)` (track best cost so far)|
|**Why it works**|Exhaustive search; guarantees optimality|
|**Why it stinks**|Explodes after n≈10–11 (`9! = 362 880`, `11! ≈ 4 × 10⁷`)|

```cpp
double bruteForceTSP(const vector<vector<double>>& dist) {
    int n = dist.size();
    vector<int> perm;
    for (int i = 1; i < n; ++i) perm.push_back(i);

    double best = 1e100;
    do {
        double cost = dist[0][perm[0]];
        for (int i = 1; i < n-1; ++i)
            cost += dist[perm[i-1]][perm[i]];
        cost += dist[perm.back()][0];   // return home
        best = min(best, cost);
    } while (next_permutation(perm.begin(), perm.end()));

    return best;
}
```

### ☑ Take-aways

- Pure permutations = factorial blow-up.
    
- Works only for single-digit city counts.
    

---

## 2. Branch & Bound – “Still Brute, but Cut Dead Ends Early”

|Item|Explanation|
|---|---|
|**Idea**|Depth-first build the route; compute a **lower-bound** of unfinished part; abandon branches whose bound ≥ current best.|
|**Lower-bounds**|_Examples_: (1) add minimum outgoing edge for each unvisited city; (2) use a MST of unvisited nodes + two smallest links to current & start.|
|**Time**|Worst case still `(n-1)!`, **but** good instances/pruning can slash average runtime.|
|**Space**|`O(n)` on recursion stack.|
|**Why it helps**|Removes impossible winners early.|

> Not always enough for ≥20 cities, but important inside every professional TSP solver.

---

## 3. Dynamic Programming with Bitmask (Held–Karp)

### 3.1 Intuition

1. **State compression**:  
    A subset of visited cities + the last city fully describe “where we stand”.
    
2. **Optimal substructure**:  
    Shortest tour visiting `S` ending at `j` can be built from a shorter tour visiting `S−{j}` ending at `k`, plus edge `k→j`.
    

### 3.2 Recurrence

```
dp[S][j] = min over k∈S−{j}  { dp[S−{j}][k] + dist[k][j] }
```

- `S` – bitmask of visited cities (city 0 excluded: it’s always the start).
    
- Base: `dp[1<<j][j] = dist[0][j]` (route 0→j directly).
    

Answer:  
`min_j dp[ALL][j] + dist[j][0]`

### 3.3 Complexity

|Metric|Value|Practical|
|---|---|---|
|**States**|`2^(n-1) × (n-1)`||
|**Time**|`O(n² 2^n)`||
|**Space**|`O(n 2^n)` (row-wise compression possible)||

- Feasible up to `n≈20` in C++ with careful bit hacks (≈20 million states).
    

```cpp
double tspDP(const vector<vector<double>>& dist) {
    int n = dist.size(), N = 1 << (n-1);
    const double INF = 1e100;
    vector<vector<double>> dp(N, vector<double>(n, INF));

    // base cases
    for (int j = 1; j < n; ++j)
        dp[1 << (j-1)][j] = dist[0][j];

    for (int mask = 1; mask < N; ++mask) {
        for (int j = 1; j < n; ++j) if (mask & (1 << (j-1))) {
            int prev = mask ^ (1 << (j-1));
            if (prev == 0) continue;
            for (int k = 1; k < n; ++k) if (prev & (1 << (k-1))) {
                dp[mask][j] = min(dp[mask][j],
                                  dp[prev][k] + dist[k][j]);
            }
        }
    }

    double best = INF;
    int full = N-1;
    for (int j = 1; j < n; ++j)
        best = min(best, dp[full][j] + dist[j][0]);
    return best;
}
```

### ☑ Take-aways

- **Exponential** but **much smaller exponent**.
    
- Exact optimal answer for up to 20–21 cities on a laptop → good for contest problems like **LeetCode 847** (with 12 nodes) or classical **Held–Karp** questions.
    

---

## 4. From Optimal DP to “Industrial” TSP Solvers

Even `O(2^n n²)` fails for the 100-city, 1 000-city benchmarks. Pro solvers combine:

|Technique|1-liner idea|
|---|---|
|**Lin-Kernighan Heuristic (LKH)**|Local 2-Opt / 3-Opt swaps, powerful tour-improvement meta-heuristic.|
|**Iterated Local Search / Simulated Annealing**|Pop out of local minima, re-optimize.|
|**Mixed-Integer Linear Programming**|Formulate TSP as ILP + subtour-elimination constraints; let branch-and-cut engine fight it.|
|**Concorde & LKH**|World-class codes mixing branch-and-bound, cutting planes, and LK. Optimal for >10 000 cities!|

---

## 5. Why the “Optimal” DP Is Often Enough for Coding Interviews

- Interview n ≤ 15 almost always.
    
- Easy to implement & reason about.
    
- Demonstrates **bitmask DP skill**.
    
- Explains “why factorial is hopeless, why `2^n` is a win”.
    

---

## 6. Cheatsheet Comparison

|Strategy|Time|Space|Cut-off (practical)|Guarantee|
|---|---|---|---|---|
|Permutation brute|`(n-1)!`|`O(1)`|n ≤ 10|✔ Optimal|
|Branch & Bound|worst `(n-1)!`|`O(n)`|n≈15…25*|✔ Optimal*|
|Bitmask DP (Held–Karp)|`O(n² 2^n)`|`O(n 2^n)`|n ≈ 20|✔ Optimal|
|Lin-Kernighan (LKH)|~`O(n²)` per restart|`O(n)`|n ≥ 100 000|✖ Heuristic (near-opt)|
|Concorde (cutting planes)|worst exponential|large|world records|✔ Optimal|

* depends on bound quality / instance.

---

### Summary Sentences

- **Start** with permutations to feel the problem.
    
- **Graduate** to Held–Karp DP when you need exactness and `n` is small.
    
- **Scale** with branch-and-bound + good lower bounds or switch to heuristics (LK, ILP) when `n` explodes.
    

That’s the full ladder from “dumb but sure” to “smart and scalable”. If you’d like a _line-by-line_ walkthrough of the DP code or a **Worked Example** on a tiny graph, just let me know!