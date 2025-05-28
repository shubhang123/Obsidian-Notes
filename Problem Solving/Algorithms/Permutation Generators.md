
---

## 1. Backtracking with a Frequency Map

### 🤔 Idea

Rather than permuting positions, think in terms of **“which character to place next?”**. Keep a map from character → remaining count. At each recursion level, you:

1. Loop through **all distinct** characters that still have a positive count.
    
2. “Take” that character: append it to your current string, decrement its count.
    
3. Recurse.
    
4. “Undo” (backtrack): pop it off, restore the count.
    

By iterating your map’s keys in **sorted order**, you naturally generate permutations in lexicographic order, and you never revisit the same multiset arrangement twice.

---

### 🔢 Pseudocode

```text
function generate(curr):
    if curr.length == n:
        output curr
        return

    for each character c in sorted_keys(freq_map):
        if freq_map[c] == 0: continue

        // Take c
        freq_map[c] -= 1
        curr.push_back(c)

        generate(curr)

        // Backtrack
        curr.pop_back()
        freq_map[c] += 1
```

1. **Initialization**:
    
    ```cpp
    map<char,int> freq;
    for (char c : s) freq[c]++;
    
    string curr = "";
    generate(curr);
    ```
    
2. **Lexicographic order** is guaranteed by iterating the `map<char,int>` in its natural ascending order.
    
3. **Complexity**
    
    - Number of leaves ≈ number of unique permutations ≤ n!
        
    - Each leaf takes O(n) to build/print.
        
    - Total ≈ O(n · n!) in the worst case (distinct letters), but much less if many duplicates.
        

---

### 💡 C++ Sketch

```cpp
void dfs(string &curr, int n, map<char,int> &freq) {
    if (curr.size() == n) {
        cout << curr << "\n";
        return;
    }
    for (auto & [ch, count] : freq) {
        if (count == 0) continue;
        // choose
        curr.push_back(ch);
        --freq[ch];
        // recurse
        dfs(curr, n, freq);
        // undo
        curr.pop_back();
        ++freq[ch];
    }
}

int main() {
    string s;
    cin >> s;
    map<char,int> freq;
    for (char c : s) freq[c]++;
    cout << /* total_perms = product of factorials/count! */ << "\n";
    dfs(*(new string()), s.size(), freq);
}
```

---

## 2. Heap’s Algorithm

### 🤔 Idea

Heap’s algorithm generates **all** permutations of an array by doing a series of swaps. Its key property is that each recursive step generates permutations of size `k` by:

1. Recursing on `k–1`.
    
2. Swapping either the first element (if `k` odd) or the `i`-th element (if `k` even) with the `k–1` position.
    
3. Repeating for `i = 0…k–1`.
    

For a string with **distinct** characters, this will output all `n!` permutations in some order (not lexicographic). If your string has repeats, you’ll produce duplicates—but you can either:

- **Filter** them post-hoc (e.g. insert into a `set`), or
    
- **Detect and skip** identical swaps (a bit more involved).
    

---

### 🔢 Pseudocode

```text
procedure heapPermute(k):
    if k == 1:
        output current array
        return

    for i from 0 to k-1:
        heapPermute(k - 1)
        if k is even:
           swap( array[i], array[k-1] )
        else:
           swap( array[0], array[k-1] )
```

Call it as:

```text
heapPermute(n)
```

---

### 💡 C++ Sketch (with dedupe via `set`)

```cpp
void heapPermute(int k, string &s, set<string> &out) {
    if (k == 1) {
        out.insert(s);
        return;
    }
    for (int i = 0; i < k; i++) {
        heapPermute(k - 1, s, out);
        // swap rule
        if (k % 2 == 0)
            swap(s[i], s[k - 1]);
        else
            swap(s[0], s[k - 1]);
    }
}

int main() {
    string s;
    cin >> s;
    set<string> uniques;
    heapPermute(s.size(), s, uniques);
    cout << uniques.size() << "\n";
    for (auto &str : uniques)
        cout << str << "\n";
}
```

---

### 📊 Comparison

||Backtracking + freq map|Heap’s + set|
|---|---|---|
|**Duplicates**|Never generates them|Must filter (e.g. `set`)|
|**Order**|Lexicographic by design|Arbitrary (then sort/set orders)|
|**Code complexity**|Moderate (map + recursion)|Very concise recursion + swaps|
|**Memory**|O(n + #perms · n)|O(#unique_perms · n) for `set`|
|**Speed**|O(n · unique_perms)|O(n · n!) + overhead of set ops|

---

### ✅ When to use which?

- **Sorted output, no duplicates:** go with **frequency‐map backtracking**.
    
- **Teaching recursive swap patterns:** demonstrate **Heap’s algorithm**, and if needed filter by a `set`.
    

Both run easily in under 1 s for **n ≤ 8** on CSES.