---
title: "Letter combination phone number"
type: "problem"
area: "study"
topic:
  - "leetcode"
  - "recursion-backtracking"
status: "draft"
created: 2026-03-28
updated: 2026-03-28
tags:
  - "area/study"
  - "type/problem"
  - "topic/leetcode"
---

#recursion #leetcode
Let’s break down the **solution and approach** for generating all possible letter combinations from a string of digits (like `"23"`) on a **phone keypad**, using **backtracking**.

---

## 🔍 Problem Statement

Given a string of digits (from `'2'` to `'9'`), each digit maps to letters like on an old mobile keypad. For example:

|Digit|Letters|
|---|---|
|2|abc|
|3|def|
|4|ghi|
|5|jkl|
|6|mno|
|7|pqrs|
|8|tuv|
|9|wxyz|

Your goal is to generate **all combinations** of these letters by taking one letter for each digit.

---

## ✅ Approach: Backtracking

### 🧠 Why Backtracking?

Backtracking is perfect here because:

- Each digit can map to multiple choices (letters).
    
- For a digit string of length `n`, the total combinations are the **cartesian product** of their letter sets → max `4^n` combinations.
    
- We build each combination character by character, backtracking when needed.
    

---

### ⚙️ Algorithm Steps

Let’s say the input is `s = "23"`:

1. **Start with an empty string `temp`** and at `index = 0` (pointing to `'2'`).
    
2. Look up all letters mapped to `s[index]` using a map:  
    `'2' → "abc"`
    
3. Loop over each letter `ch` of `"abc"`:
    
    - Append `ch` to `temp`
        
    - Recurse to the next digit: `solve(index+1, s)`
        
    - After recursion, remove the last char (`pop_back`) — this is **backtracking**.
        
4. If `index == s.length()`, the `temp` string is complete ⇒ push it into `result`.
    

---

### 📦 Data Structures

|Variable|Purpose|
|---|---|
|`unordered_map<char, string>`|digit-to-letter mapping|
|`vector<string> result`|stores all combinations|
|`string temp`|current combination during recursion|

---

### 🔁 Recursive Tree for `"23"`

We build this tree:

```
solve(0)
├─ 'a' ─ solve(1)
│     ├─ 'd' → "ad"
│     ├─ 'e' → "ae"
│     └─ 'f' → "af"
├─ 'b' ─ solve(1)
│     ├─ 'd' → "bd"
│     ├─ 'e' → "be"
│     └─ 'f' → "bf"
└─ 'c' ─ solve(1)
      ├─ 'd' → "cd"
      ├─ 'e' → "ce"
      └─ 'f' → "cf"
```

Each leaf path is a valid string.

---

### 💻 Code Overview (Your Version)

```cpp
void solve(int idx, string &s) {
    if (idx == s.size()) {
        result.push_back(temp);
        return;
    }

    for (char ch : keyboard[s[idx]]) {
        temp += ch;
        solve(idx + 1, s);
        temp.pop_back();
    }
}
```

- `temp += ch` → adds current character
    
- `solve(...)` → recursive call
    
- `temp.pop_back()` → removes last character, enabling exploration of other choices
    

---

### 🧠 Time & Space Complexity

- **Time:** `O(4^n)` (in worst case, e.g. all `'7'`s or `'9'`s which map to 4 letters each)
    
- **Space:** `O(n)` for the recursion stack and `O(4^n)` for storing all combinations
    

---

### ✅ Summary

- This is a **recursive backtracking** problem.
    
- At each index, we **explore every possibility**, and **backtrack** after trying each one.
    
- Each **path in the decision tree** represents a different letter combination.
    
- Efficient, clear, and scalable up to reasonable `n` (e.g. `n ≤ 10`).
    

Let me know if you want the **iterative version** or this explained with a real keypad!
