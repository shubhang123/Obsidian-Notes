#binarysearch #leetcode


## 1. The Predicate-Based Approach
explained in detail in [[Predicate function (Binary Search)]]

1. **What are we searching?**  
    We want the **minimum eating speed** `s` (bananas/hour) such that Koko can finish all banana piles within `H` hours.
    
2. **Define a predicate**
    
    ```cpp
    // Returns true if speed `s` suffices to eat all piles in ≤ H hours.
    bool canFinish(const vector<int>& piles, int H, int s);
    ```
    
    - We simulate eating at speed `s`: for each pile of size `p`, it takes `ceil(p/s)` hours.
        
    - Sum up these hours; if that total ≤ `H`, return `true`, else `false`.
        
3. **Monotonicity**
    
    - If `canFinish(s)` is `true`, then for any `s' > s`, `canFinish(s')` will also be `true` (eating faster never hurts).
        
    - Conversely, if `canFinish(s)` is `false`, then for any `s' < s`, `canFinish(s')` is also `false`.
        
4. **Binary-search on speed**
    
    - Search the integer range `[1 … maxPile]`.
        
    - At each mid-point `m`, ask `canFinish(piles, H, m)`.
        
        - If **true**, record `ans = m` and continue searching **lower** speeds (`high = m - 1`).
            
        - If **false**, move to **higher** speeds (`low = m + 1`).
            

---

## 2. Dry Run (Example)

```
piles = [3, 6, 7, 11],   H = 8
maxPile = 11
low = 1, high = 11, ans = 11
```

|Iteration|mid|canFinish(mid)?|Action|new low|new high|ans|
|:-:|:-:|:--|:--|:-:|:-:|:-:|
|1|6|ceil(3/6)+ceil(6/6)+…=6 ≤ 8 → T|ans=6; search lower (`high=5`)|1|5|6|
|2|3|1+2+3+4 =10 > 8 → F|too slow; search higher (`low=4`)|4|5|6|
|3|4|1+2+2+3 =8 ≤ 8 → T|ans=4; search lower (`high=3`)|4|3|4|
|—|—|loop ends (low>high)||||4|

**Answer = 4**

---

## 3.Code 

```cpp
class Solution {
public:
    // Predicate: can Koko finish at speed `s` within `H` hours?
    bool canFinish(const vector<int>& piles, int H, int s) {
        long long hours = 0;
        for (int p : piles) {
            // each pile costs ceil(p/s) hours
            hours += (p + s - 1) / s;
            if (hours > H) 
                return false;
        }
        return true;
    }

    int minEatingSpeed(vector<int>& piles, int H) {
        // determine upper bound for speed
        int lo = 1;
        int hi = *max_element(piles.begin(), piles.end());
        int ans = hi;

        // binary search for minimal s with canFinish == true
        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;
            if (canFinish(piles, H, mid)) {
                ans = mid;      // mid works; try even smaller
                hi = mid - 1;
            } else {
                lo = mid + 1;   // mid too slow; speed up
            }
        }
        return ans;
    }
};
```

**Key points**:

- We isolate the **predicate** `canFinish` as a separate member function.
    
- Binary search finds the **first** `s` where `canFinish(...)` transitions from `false` → `true`.