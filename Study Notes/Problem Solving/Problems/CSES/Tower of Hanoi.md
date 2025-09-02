### 1 Seeing the sub-problem hiding inside the big problem

Look at the biggest (nth) disk.

- It **cannot move anywhere** until every disk that is **smaller** sits on some _other_ peg.
    
- Once the nth disk is placed on its final peg, **all smaller disks must be moved on top of it**.
    

So to move `n` disks from **A→C** you inevitably have to do three phases:

|phase|what really happens|where the `n-1` stack ends up|
|---|---|---|
|①|move the top `n-1` disks off of A|peg **B** (auxiliary)|
|②|move disk `n` (the largest)|directly **A → C**|
|③|move those `n-1` disks again|**B → C**, on top of disk n|

That _is_ the entire algorithm. It is forced by the rules; no other move order can ever finish sooner.

---

### 2 Turning the observation into a recursive routine

If we already know how to move `n-1` disks between any two pegs, the three phases translate almost verbatim into code:

```text
solve(n, A, B, C):
    solve(n-1, A, C, B)   // phase ①  (free the biggest)
    move disk n  from A to C          // phase ②
    solve(n-1, B, A, C)   // phase ③  (stack them back)
```

All that’s left is a base case:

```text
solve(1, A, B, C):  move disk 1 from A to C
```

And that is precisely what the C++ function does.

---

### 3 Why the number of moves is 2ⁿ − 1 (and why it’s minimal)

Let **T(n)** be the fewest moves needed for `n` disks.

1. The three-phase plan gives  
    `T(n) = T(n-1) + 1 + T(n-1) = 2·T(n-1) + 1`.
    
2. The base case is `T(1) = 1`.
    

Solve the recurrence (or notice the doubling pattern):

```
T(1) = 1
T(2) = 2·1 + 1 = 3
T(3) = 2·3 + 1 = 7
⋯
T(n) = 2ⁿ – 1
```

**Minimality proof (induction).**  
_Disk n must move once._  
Before that happens every smaller disk must be elsewhere ⇒ at least `T(n-1)` moves.  
After it moves, those `n-1` disks must be stacked on top of it ⇒ at least another `T(n-1)` moves.  
So **any** valid solution needs `2·T(n-1)+1` moves. By the induction hypothesis this equals `2ⁿ − 1`.  
Our algorithm achieves exactly that, so it is optimal.

---

### 4 What the recursion really does – a quick dry run for n = 3

```
solve(3,A,B,C)
└─ solve(2,A,C,B)
   ├─ solve(1,A,B,C) → move 1: 1 3
   ├─ move disk 2:     1 2
   └─ solve(1,C,A,B) → move 3: 3 2
└─ move disk 3:         1 3
└─ solve(2,B,A,C)
   ├─ solve(1,B,C,A) → move 5: 2 1
   ├─ move disk 2:     2 3
   └─ solve(1,A,B,C) → move 7: 1 3
```

The seven printed moves match `2³ − 1`.

---

### 5 Why the tester’s limits are easy

`n ≤ 16` ⇒ `2¹⁶ − 1 = 65 535` moves, perfectly fine for recursion depth and -O(2ⁿ) output.

---

### 6 Take-aways about designing the recursion

1. **Identify the bottleneck object** (the biggest disk).
    
2. **Define the pre-condition** to move it (everything above must be gone).
    
3. **Express that pre-condition as the same problem on a smaller input** (`n−1`).
    
4. **Compose**: smaller-problem → critical move → smaller-problem.
    
5. **Prove optimality** by showing each phase is unavoidable.
    

That recipe is what gives the clean, three-line recursive algorithm and its optimal move count.

---

### ✅ C++ Code:

```cpp
#include <iostream>
using namespace std;

// Recursive function to solve Tower of Hanoi
void solve(int n, int source, int auxiliary, int target) {
    if (n == 0) return;

    // Move n-1 disks from source to auxiliary
    solve(n - 1, source, target, auxiliary);

    // Move the nth disk from source to target
    cout << source << " " << target << "\n";

    // Move n-1 disks from auxiliary to target
    solve(n - 1, auxiliary, source, target);
}

int main() {
    int n;
    cin >> n;

    // Total number of moves = 2^n - 1
    cout << (1 << n) - 1 << "\n";

    // Move disks from peg 1 to peg 3 using peg 2
    solve(n, 1, 2, 3);

    return 0;
}
```

---

### 🧪 Example

**Input:**

```
2
```

**Output:**

```
3
1 2
1 3
2 3
```

---

### 📌 Explanation:

- Move disk 1 from 1 → 2
    
- Move disk 2 from 1 → 3
    
- Move disk 1 from 2 → 3
    

Total moves = `2^2 - 1 = 3`.

---

### ✅ Time & Space Complexity:

- **Time:** O(2^n)
    
- **Space:** O(n) (due to recursion stack)
    

Let me know if you'd like the **iterative version** with move tracing too.