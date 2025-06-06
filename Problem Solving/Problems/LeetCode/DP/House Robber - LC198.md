#dp #recursion #leetcode
Below is a comprehensive explanation of the **House Robber** problem solved by **recursion + memoization** (a top-down dynamic programming approach). We will walk through the following:

1. **Problem Statement**
2. **Recursive Formulation**
3. **Memoization**
4. **Step-by-Step Example (with a recursion tree)**
5. **Complete C++ Implementation**

Finally, we will discuss how this relates to **dynamic programming** and show why memoization avoids recomputing overlapping subproblems.

---

## 1. Problem Statement

You are a professional robber planning to rob houses along a street. Each house ii has a certain amount of money nums[i]\text{nums}[i]. The only constraint preventing you from robbing them all is that **you cannot rob two adjacent houses** on the same night (to avoid setting off alarms).

**Goal**:  
Find the maximum amount of money you can rob tonight without alerting the police.

In more formal terms, given an array `nums` where `nums[i]` is the amount of money in house ii, **return the maximum amount of money you can rob without robbing two adjacent houses**.

---

## 2. Recursive Formulation

Let robFrom(i)\text{robFrom}(i) be the **maximum** amount of money that can be robbed starting from house index ii through the end of the street. We have two choices for house ii:

1. **Rob house ii**:
    
    - You gain nums[i]\text{nums}[i] money.
    - You must skip house i+1i+1 (because you cannot rob two adjacent houses).
    - Thus, the next house you can rob from is i+2i+2.
    - The subproblem here is robFrom(i+2)\text{robFrom}(i+2).
2. **Skip house ii**:
    
    - You rob 0 money from house ii.
    - You can still rob from house i+1i+1.
    - The subproblem here is robFrom(i+1)\text{robFrom}(i+1).

Hence, the recurrence is:

robFrom(i)=max⁡(nums[i]+robFrom(i+2),robFrom(i+1))\text{robFrom}(i) = \max \Big(\text{nums}[i] + \text{robFrom}(i + 2),\quad \text{robFrom}(i + 1)\Big)

**Base cases**:

- If i≥nums.size()i \ge \text{nums.size()}, there are no houses left, so return 00.

---

## 3. Memoization

A naive recursive solution will revisit the same subproblems (e.g., robFrom(2)\text{robFrom}(2) might be computed multiple times). **Memoization** stores the result of each subproblem in an array (or map/dictionary) so that once it’s computed, we can reuse it.

- We create a memo array `memo` of size `nums.size()`, initialized to `-1` (indicating “uncomputed”).
- Before computing `robFrom(i)`, we check whether `memo[i]` is already calculated.
    - If **not** (`memo[i] == -1`), we compute it by the formula above and store the result in `memo[i]`.
    - If it **is** computed, we just return `memo[i]` immediately.

This means each subproblem `robFrom(i)` is computed **exactly once**, bringing the time complexity down to O(n)O(n) instead of O(2n)O(2^n) for the naive recursion.

---

## 4. Step-by-Step Example

Let’s take a small example to see the recursion tree, say we have **3 houses** with amounts:

nums=[2, 7, 9].\text{nums} = [2,\,7,\,9].

We want to compute robFrom(0)\text{robFrom}(0).

```
                  robFrom(0)
                /           \
     Rob house 0 (2)       Skip house 0
     => 2 + robFrom(2)       => robFrom(1)
              |                     |
         robFrom(2)           robFrom(1)
           /     \            /       \
     Rob house 2  \    Skip house 2  ...
     => 9 + robFrom(4)  => robFrom(3)
       => robFrom(4)
         (out of range, =0)
```

### Detailed Tree

1. **robFrom(0):**
    
    - **Option 1**: Rob house 0 → Gain `2` + robFrom(2)\text{robFrom}(2).
    - **Option 2**: Skip house 0 → robFrom(1)\text{robFrom}(1).
2. **robFrom(1):**
    
    - **Option 1**: Rob house 1 → Gain `7` + robFrom(3)\text{robFrom}(3).
    - **Option 2**: Skip house 1 → robFrom(2)\text{robFrom}(2).
3. **robFrom(2):**
    
    - **Option 1**: Rob house 2 → Gain `9` + robFrom(4)\text{robFrom}(4) (but `robFrom(4)` is 0 because it’s out of range).
    - **Option 2**: Skip house 2 → robFrom(3)\text{robFrom}(3).
4. **robFrom(3)** or beyond:
    
    - Out of range, so `robFrom(3) = 0`, `robFrom(4) = 0`.

Putting it all together:

- robFrom(2)=max⁡(9+0,  0)=9\text{robFrom}(2) = \max(9 + 0,\; 0) = 9
- robFrom(1)=max⁡(7+robFrom(3),  robFrom(2))=max⁡(7+0,  9)=9\text{robFrom}(1) = \max(7 + \text{robFrom}(3),\; \text{robFrom}(2)) = \max(7 + 0,\; 9) = 9
- robFrom(0)=max⁡(2+robFrom(2),  robFrom(1))=max⁡(2+9,  9)=11\text{robFrom}(0) = \max(2 + \text{robFrom}(2),\; \text{robFrom}(1)) = \max(2 + 9,\; 9) = 11

So the maximum is **11** (rob houses 0 and 2).

**Memoization** ensures each of these calls (`robFrom(2)`, `robFrom(3)`) is computed only once.

---

## 5. Complete C++ Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int rob(vector<int>& nums) {
        // Create a memo array of size n, initialized with -1.
        // -1 indicates that the value is not yet computed.
        int n = nums.size();
        vector<int> memo(n, -1);
        
        // Start recursion from house 0
        return robFrom(nums, 0, memo);
    }
    
private:
    // Returns the maximum amount of money that can be robbed from index i to the end.
    int robFrom(const vector<int>& nums, int i, vector<int>& memo) {
        // If i is beyond the last house, return 0.
        if (i >= (int)nums.size()) {
            return 0;
        }
        
        // If we've already computed this state, return the stored result
        if (memo[i] != -1) {
            return memo[i];
        }
        
        // Option 1: Rob the current house i
        int robCurrent = nums[i] + robFrom(nums, i + 2, memo);
        
        // Option 2: Skip the current house i
        int skipCurrent = robFrom(nums, i + 1, memo);
        
        // Take the max of both options
        memo[i] = max(robCurrent, skipCurrent);
        
        return memo[i];
    }
};

int main() {
    // Example usage:
    vector<int> houses = {2, 7, 9, 3, 1};
    Solution sol;
    cout << "Maximum money robbed: " << sol.rob(houses) << endl; 
    // Expected output: 12 (rob houses 2 and 4, or houses 1 and 3, depending on indexing)
    return 0;
}
```

### How Does This Relate to Dynamic Programming?

- **Overlapping Subproblems**: Notice that robFrom(2)\text{robFrom}(2) can be triggered from multiple paths (e.g., from `robFrom(0)` if we rob house `0`, or from `robFrom(1)` if we skip house `1`). This is the hallmark of overlapping subproblems.
- **Optimal Substructure**: The maximum money robbed from any house ii depends on the optimal choices for robFrom(i+2)\text{robFrom}(i+2) or robFrom(i+1)\text{robFrom}(i+1). Hence, the problem satisfies optimal substructure: the optimal solution can be built from optimal solutions of subproblems.
- **Memoization**: We store and reuse results in `memo`. This top-down approach with caching is effectively dynamic programming. Alternatively, one can solve the same recurrence bottom-up without explicit recursion.

---

### Recap

1. We define a function `robFrom(i)` that returns the maximum money from house ii onward.
2. We decide to rob house ii (and then jump to i+2i+2) or skip house ii (and check from i+1i+1).
3. We use a `memo` array so each subproblem is computed exactly once.
4. This yields a time complexity of O(n)O(n) and space complexity of O(n)O(n) for the memo array (plus recursion stack space).

With these ideas in mind, you have a **top-down dynamic programming** solution for the House Robber problem, complete with the recursion tree and memoization approach.