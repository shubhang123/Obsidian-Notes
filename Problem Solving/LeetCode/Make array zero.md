#leetcode
### 0. The problem in one sentence

“Every time you choose a sub‑array whose **minimum** is `v`, you may delete all `v`’s in that window—but _nothing bigger_—so values `< v` act like **walls** that split the array into islands.”

---

## 1. Turning that sentence into an algorithm

|Observation|Consequence in the algorithm|
|---|---|
|If an element has value `v`, you can only delete it after everything _smaller_ than `v` inside the chosen window is already 0.|Process the numbers **from smaller to larger**. When you reach value `v`, treat all indices that contain values `< v` as fixed “barriers.”|
|Between two such barriers you have a contiguous “island.” All `v`’s that live inside the same island can be wiped in **one** operation, no matter how many `v`’s there are.|For each value `v`, count how many **islands that actually contain a `v`** still remain. That is exactly the number of operations you must spend on `v`.|
|As soon as you wipe those `v`’s, their indices themselves become barriers for anything larger.|Insert every index you just processed into a structure that lets you ask: “Where’s the next barrier after position `x`?” A `std::set<int>` with `upper_bound` does this in `O(log n)`.|

---

## 2. Data structures you need

1. **Sorted list of `(value, index)` pairs** ► lets you visit positions in ascending value order (all 1’s first, then 2’s, …).
    
    - Build: one pass O(n).
        
    - Sort: O(n log n).
        
2. **Ordered set `barriers`** ► contains every index already zeroed.
    
    - Operations: `insert(i)` and `upper_bound(i)` in `O(log n)`.
        

> With these two ingredients the whole procedure is just one linear scan over the sorted pairs plus logarithmic updates.

---

## 3. Walk‑through on `[3, 1, 2, 1]`

|Step|Value being processed|Current `barriers`|Islands that contain that value|Ops added|Total ops|
|---|---|---|---|---|---|
|—start|initial zeros (none)|∅|—|—|0|
|1|all 1’s|{1, 3}|`[1,3]` is one island → 1 op|**+1**|1|
|2|the 2 at idx 2|{1, 2, 3}|`[2,2]` is one island → 1 op|**+1**|2|
|3|the 3 at idx 0|{0, 1, 2, 3}|`[0,0]` is one island → 1 op|**+1**|3|

Result = **3** operations.

Notice how each newly processed index is immediately added to `barriers`, so it splits the range for every larger value that comes later.

---

## 4. Why it’s optimal

_Greedy proof sketch_:

1. **Lower bound:** For any value `v`, two indices holding `v` that are separated by a **smaller value** must be cleared in different operations (because that smaller value would become the minimum if you tried to join them).  
    ⇒ Total ops ≥ number of such islands for each `v`.
    
2. **Algorithm achieves that bound:** We clear exactly **one** operation per island per value—never more.  
    ⇒ Total ops produced by the algorithm == theoretical minimum.
    

Thus the algorithm is optimal.

---

## 5. Code recap (no sentinels)

```cpp
int minOperations(vector<int>& nums) {
    int n = nums.size();

    // (value,index) pairs for non‑zeros
    vector<pair<int,int>> vp;
    for (int i = 0; i < n; ++i)
        if (nums[i] > 0) vp.emplace_back(nums[i], i);
    if (vp.empty()) return 0;

    sort(vp.begin(), vp.end());            // ascending value
    set<int> barriers;                     // indices already zeroed
    int ops = 0;

    for (size_t i = 0; i < vp.size(); ++i) {
        int v   = vp[i].first;
        int idx = vp[i].second;
        ++ops;                             // new value‑island → 1 op
        barriers.insert(idx);

        // try to merge further identical values in the same island
        while (i + 1 < vp.size() && vp[i+1].first == v) {
            int nextIdx = vp[i+1].second;
            auto it = barriers.upper_bound(idx);  // first barrier after idx
            if (it != barriers.end() && *it <= nextIdx) break; // blocked
            ++i;                                   // merge; no extra op
            idx = nextIdx;
            barriers.insert(nextIdx);
        }
    }
    return ops;
}
```

_Complexities_ → **O(n log n)** time, **O(n)** memory.

---

## 6. How to develop this intuition yourself

1. **Work small examples by hand.**  
    Notice that once you delete 1’s, the array breaks into pieces for 2’s; once 2’s are gone, the pieces break further for 3’s, etc.
    
2. **Phrase it as an invariant.**
    
    > “At the moment I start processing value `v`, every position holding a smaller value is permanently zero and acts as a wall.”
    
3. **Ask what exactly you must count.**  
    Realise the question reduces to:  
    _“How many contiguous runs of `v` still exist after removing smaller values?”_
    
4. **Search your toolbox for a data structure** that answers “where is the next wall after position `x`?” quickly.  
    – Balanced BST / `std::set` is the everyday choice.
    
5. **Turn the reasoning into code**: build pairs, sort, scan, maintain the set.  
    Each bullet above maps to one neat piece of the final program.
    

With practice you’ll start recognising problems where:

- Small‐to‐large (or large‐to‐small) **ordering** makes later decisions independent.
    
- Previously processed items become **barriers / blockers** for future ones.
    
- An ordered structure (`set`, `map`, Fenwick, segment tree) gives you O(log n) barrier queries.
    

Those are classic signals that this “peel layer by layer with a set” pattern will work.