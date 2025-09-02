In a movie festival n movies will be shown. You know the starting and ending time of each movie. What is the maximum number of movies you can watch entirely?

Solution 

# Greedy Solution

### 🧠 **Key Insight:**

To fit the most movies, you must be **greedy** — always pick the movie that **ends earliest**.

This leaves the most time for future movies.

> **This is a classic "Interval Scheduling" problem.**

---

### ✅ **Greedy Strategy:**

1. **Sort** all movies by **end time `bᵢ`**.
    
2. Initialize `last_end_time = 0`.
    
3. For each movie:
    
    - If `start_time ≥ last_end_time`, watch it:
        
        - Increment count
            
        - Update `last_end_time = end_time`
            
    - Otherwise, skip.
        

---

### 💻 Pseudocode:

```cpp
sort(movies by end time);
int last_end = 0, count = 0;

for each (start, end) in movies:
    if (start >= last_end):
        count += 1
        last_end = end

return count;
```

---

### ⏱️ Time Complexity:

|Step|Complexity|
|---|---|
|Sorting|`O(n log n)`|
|Greedy loop|`O(n)`|
|**Total**|`O(n log n)`|

---

### 📦 Space Complexity:

- `O(n)` for storing movie list.
    

---

### ✅ Why It Works:

- Picking the **earliest finishing movie** always leaves the most room for future movies.
    
- It ensures **maximal scheduling** since:
    
    > If you pick a later-ending movie, it blocks you from watching more.
    

---


# DP Solution

---

## 🎯 Problem Recap

You’re given `n` movies, each with:

- Start time `a_i`
    
- End time `b_i`
    

You can watch **only one movie at a time**, and you must watch it **fully**.

Your goal: **maximize the number of non-overlapping movies you can watch**.

---

## 🧠 DP Idea

We define a DP recurrence based on **intervals**.

---

### ✅ Step-by-step plan:

1. **Sort movies by end time**.
    
2. Let `dp[i]` = **maximum number of movies you can watch using the first `i` movies**.
    
3. For each movie `i`, we have two choices:
    
    - **Skip movie `i`** → `dp[i] = dp[i-1]`
        
    - **Take movie `i`** → add 1 to the best result from the latest non-conflicting movie.
        

---

### ✅ Step 1: Sort movies by end time

This allows us to binary search the **last non-conflicting movie** for each `i`.

---

### ✅ Step 2: Binary Search Helper

We need to find the **latest movie `j < i`** such that `end[j] ≤ start[i]`.

We can store ends in a separate array for efficient `lower_bound` or `upper_bound`.

---

## ✅ C++ Code for DP

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;

    vector<pair<int, int>> movies(n);
    for (int i = 0; i < n; ++i)
        cin >> movies[i].first >> movies[i].second;

    // Sort by end time
    sort(movies.begin(), movies.end(), [](auto &a, auto &b) {
        return a.second < b.second;
    });

    // End times for binary search
    vector<int> end_times(n);
    for (int i = 0; i < n; ++i)
        end_times[i] = movies[i].second;

    // dp[i] = max movies we can watch from first i movies
    vector<int> dp(n);
    dp[0] = 1;  // Only the first movie

    for (int i = 1; i < n; ++i) {
        // Option 1: skip current movie
        dp[i] = dp[i - 1];

        // Option 2: take current movie → find latest non-conflicting
        int l = upper_bound(end_times.begin(), end_times.end(), movies[i].first) - end_times.begin() - 1;
        if (l >= 0)
            dp[i] = max(dp[i], dp[l] + 1);
        else
            dp[i] = max(dp[i], 1); // no previous movie fits
    }

    cout << dp[n - 1] << '\n';
    return 0;
}
```

---

### ⏱️ Time Complexity

- Sorting: `O(n log n)`
    
- Each DP step: `O(log n)` (binary search)
    
- Total: `O(n log n)`
    

---

### 🔍 Why DP?

- DP is useful if:
    
    - You want to **track** which movies were chosen.
        
    - You extend the problem with **weights** (e.g., each movie has a value).
        
    - You have memory for only partial overlapping allowed (e.g., watch part of a movie).
        

---

### 🧠 Summary

|Method|Complexity|Optimal|When to use|
|---|---|---|---|
|Greedy|O(n log n)|✅|Always preferred here|
|DP|O(n log n)|✅|For learning/extensions|
|Line sweep|O(n log n)|❌|Wrong logic for this case|

---

Let me know if you want the **traceback logic** to find which movies were chosen in the DP!