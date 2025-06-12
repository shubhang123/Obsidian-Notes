Here are clean and structured notes for the **"Ferris Wheel"** problem from CSES, written in a format suitable for revision and understanding.

---

## 🌀 Problem: Ferris Wheel (CSES)

### ✅ Objective:

Assign **each child** to a **gondola**, such that:

- Each gondola can carry **at most two children**.
    
- The **sum of their weights must not exceed** `x`.
    

### 🎯 Goal:

Minimize the **number of gondolas** used.

---

## 📥 Input:

- `n` — Number of children (1 ≤ n ≤ 2⋅10⁵)
    
- `x` — Maximum allowed weight in a gondola (1 ≤ x ≤ 10⁹)
    
- `p₁, p₂, ..., pₙ` — Weights of the children (1 ≤ pᵢ ≤ x)
    

---

## 📤 Output:

- A single integer — the **minimum number of gondolas** needed.
    

---

## 🧠 Key Insight:

To **minimize gondolas**, we should try to **pair the lightest and heaviest child** who can ride together.

### 🔁 Greedy Two-Pointer Approach:

1. **Sort** the weights.
    
2. Use two pointers: `left` (start) and `right` (end).
    
3. In each iteration:
    
    - If the sum of weights at `left + right` ≤ x:
        
        - Pair them: move both pointers.
            
    - Else:
        
        - The heavier child (`right`) rides alone.
            
        - Move `right` only.
            
4. Count one gondola in each step.
    

---

## 🔂 Time Complexity:

- **O(n log n)** for sorting
    
- **O(n)** for the two-pointer loop
    
- ✅ Efficient for n ≤ 2⋅10⁵
    

---

## 🧪 Example:

**Input:**

```
4 10
7 2 3 9
```

**Sorted weights:** `[2, 3, 7, 9]`

**Pairings:**

- 2 + 9 → too heavy → 9 alone
    
- 2 + 7 = 9 → valid → pair
    
- 3 alone
    

**Total gondolas: 3**

**Output:**

```
3
```

---

## ✅ Final Algorithm (C++):

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, x;
    cin >> n >> x;
    vector<int> w(n);
    for (int i = 0; i < n; i++) cin >> w[i];

    sort(w.begin(), w.end());
    int l = 0, r = n - 1;
    int rides = 0;

    while (l <= r) {
        if (w[l] + w[r] <= x) l++;
        r--;
        rides++;
    }

    cout << rides << "\n";
    return 0;
}
```

---

Let me know if you'd like a **Python** version or **Dry Run** as well.