# 📘 Notes on Binary Search Using Predicate Functions

---

### 🔹 What is a Predicate Function?

- A **predicate** is a function that returns a boolean value (`true` or `false`) for a given input.
    
- In binary search problems, the **predicate must be monotonic**:
    
    ```
    F F F F F T T T T T   → increasing
    T T T T T F F F F F   → decreasing
    ```
    
- The goal is to find the **first index where the predicate becomes `true`** (or last where it remains `false`).
    

---

### 🔹 Why Binary Search on Answer Works?

If the answer lies in a numeric range (e.g., 1 to 10^9), and for any `x`:

- `predicate(x)` tells us whether `x` is a valid solution,
    
- Then we can use binary search to shrink the range efficiently from O(n) to O(log n).
    

---

### 🔹 Template (Find Minimum Valid Answer):

```cpp
int low = 0, high = MAX;
int ans = -1;

while (low <= high) {
    int mid = (low + high) / 2;
    if (predicate(mid)) {
        ans = mid;
        high = mid - 1;  // Try to find smaller valid
    } else {
        low = mid + 1;
    }
}
return ans;
```

---

### 📦 Common Problem Types (and How Predicate is Used)

|Problem Type|Predicate Meaning|Binary Search Target|
|---|---|---|
|**Minimum Speed / Time**|“Can we finish at this speed/time?”|Minimize valid answer|
|**Koko Eating Bananas**|"Can Koko eat all bananas at speed `k`?"|Minimum eating speed|
|**Ship Capacity in D Days**|"Can we ship all packages with capacity `x`?"|Minimum capacity|
|**Aggressive Cows / Placing WiFi routers**|"Can I place cows/routers with at least distance `x`?"|Maximum minimum distance|
|**Painters Partition / Book Allocation**|"Can I divide work so max load is ≤ `x`?"|Minimum maximum load|
|**Minimum Largest Subarray Sum**|"Can I split into k parts such that max sum ≤ `x`?"|Minimize maximum sum|
|**Cutting Wood / Ropes / Gold Rods**|"Can I make `k` pieces of at least length `x`?"|Maximum length|
|**Binary Search over answer (on continuous range)**|"Does `x` satisfy a condition?"|Float/int binary search|

---

### 📌 Notes Summary

- Use binary search when:
    
    - You're looking for a **value** not a position.
        
    - You can write a **predicate** that checks validity of that value.
        
    - The predicate behaves **monotonically**.
        
- The most common goal is to find the **smallest/largest valid `x`** that satisfies the constraint.
    

---

Let me know if you want these notes as a LaTeX, Markdown, or exportable PDF version.