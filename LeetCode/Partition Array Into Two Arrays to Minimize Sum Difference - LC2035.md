
We want to **minimize** the difference between the sums of two equal-sized subsets.

Let’s say:

* `subset1` and `subset2` are the two subsets (both of size n)
* `totalSum` = sum of all elements in the array
* `sum1` = sum of elements in subset1
* `sum2` = sum of elements in subset2

---

### ✅ Key Observations:

Since all elements are split between the two subsets:

$$
\text{sum1} + \text{sum2} = \text{totalSum}
$$

So:

$$
\text{sum2} = \text{totalSum} - \text{sum1}
$$

---

### 🔍 What we want to minimize:

We want:

$$
\left| \text{sum1} - \text{sum2} \right|
$$

Now plug in the expression for `sum2`:

$$
\left| \text{sum1} - (\text{totalSum} - \text{sum1}) \right|
$$

$$
= \left| 2 \cdot \text{sum1} - \text{totalSum} \right|
$$

Or equivalently:

$$
= \left| \text{totalSum} - 2 \cdot \text{sum1} \right|
$$

---

### ✅ Final Result:

To minimize the difference between the two equal-sized subsets,
we need to find a subset of size `n` such that:

$$
\boxed{\left| \text{totalSum} - 2 \cdot \text{subsetSum} \right|}
$$

is minimized.

---

### 💡 Intuition:

If `subsetSum` is **close to half** of `totalSum`, then both subsets will have similar sums, and their difference will be small — that’s exactly what we want.


# 1st Approach(TLE)
We are given an array `nums` of even length (say `n`).
Our task is to split it into two subsets of equal size (`n/2` each) such that the **absolute difference between their sums is minimized**.

```cpp
class Solution {

public:

int minimumDifference(vector<int>& nums) {

		int n = nums.size();
		
		int half = n / 2;
		
		int totalSum = accumulate(nums.begin(), nums.end(), 0);
		
		int best = INT_MAX;
		
		  
		
		int totalMasks = 1 << n;
		
		for (int mask = 0; mask < totalMasks; mask++) {
		
			if (__builtin_popcount(mask) != half) {
		
			continue;
		
		}
		
		  
		
		int subsetSum = 0;
		
		for (int i = 0; i < n; i++) {
		
			if (mask & (1 << i)) {
		
			subsetSum += nums[i];
		
			}
		
		}
		
		  
		
		best = min(best, abs(totalSum - 2 * subsetSum));
		
		}
		
		return best;
		
		}

};
```
---

### **Step 1: Calculate the total sum**

We first calculate the sum of all elements in the array and store it as `totalSum`.

This will help us later when we need to compute the sum of the *other* subset without looping over it (since `subset2 = totalSum - subset1`).

---

### **Step 2: Generate all possible subsets**

We use bitmasking to represent all possible subsets of the array.

Each bitmask of length `n` represents a subset where:

* If the `i-th` bit is set (`1`), it means `nums[i]` is included in the subset.
* If it’s `0`, then it is not included.

This gives us `2^n` total subsets.

---

### **Step 3: Filter subsets of size `n/2`**

Out of all `2^n` subsets, we are only interested in those which contain **exactly `n/2` elements**.

This is because we want both subsets to be of equal length.
We check this using `popcount` (number of 1s in the bitmask).

---

### **Step 4: For each valid subset, calculate its sum**

For every bitmask that represents a valid subset (i.e., has exactly `n/2` set bits), we:

* Traverse through all `n` bits
* If the bit is set, we add the corresponding element from `nums` to `subsetSum`.

This gives us the total of the current subset.

---

### **Step 5: Calculate the sum of the other subset**

Since we know the total sum of the array, the sum of the other subset is simply:

$$
\text{otherSubsetSum} = \text{totalSum} - \text{subsetSum}
$$

---

### **Step 6: Compute the difference**

We want the absolute difference between the two subsets:

$$
\text{diff} = |\text{subsetSum} - \text{otherSubsetSum}|
$$

Using the formula above:

$$
\text{diff} = |\text{subsetSum} - (totalSum - subsetSum)|
= |2 \cdot subsetSum - totalSum|
= |totalSum - 2 \cdot subsetSum|
$$

This is the key formula that helps us avoid recomputing the other subset’s sum.

---

### **Step 7: Track the minimum difference**

We keep updating a variable `best` with the minimum difference found so far.

---

### **Step 8: Return the result**

After checking all valid subsets, we return the smallest difference stored in `best`.

---

### ✅ Summary

* We check all possible ways to split the array into two equal halves.
* For each way, we compute how balanced their sums are.
* The formula `abs(totalSum - 2 * subsetSum)` gives us the difference.
* We return the minimum such value.

This approach fails for n over 13 which needs us to get a better approach


# **Meet in the middle approach**
## 1 ▸ Problem Recap

> Given `2 n` integers, split them into two groups of `n` elements so that  
> `| sum(group A) – sum(group B) |` is **as small as possible**.  
> Return that minimum difference.

---

## 2 ▸ Why Meet‑in‑the‑Middle (MitM)?

- **Brute force?**  
    Choose _n_ of 30 items → `C(30,15) ≈ 155 million` subsets → too slow.
    
- **MitM trick:**  
    Split into two halves of size ≤ 15.  
    Each half has only `2¹⁵ = 32 768` subsets → comfortable.
    

MitM reduces **exponential 2³⁰ → linear 2 × 2¹⁵ plus some merges**.

---

## 3 ▸ Core Observation

Let

```
total = Σ(nums)             // constant
Pick n items  →  leftSum    // sum of chosen n numbers
Other n items  →  rightSum  // = total − leftSum

Objective = | leftSum − rightSum |
           = | total − 2·leftSum |
```

So if we can make `2 × leftSum` as close as possible to `total`, we win.

---

## 4 ▸ High‑level Plan

```
         nums (length 2n)
           ┌─────────┬─────────┐
           │  left    │  right  │
           │  n ints  │  n ints │
           └─────────┴─────────┘

1️⃣  Enumerate **every** subset of each half.
2️⃣  Bucket subset sums by “how many elements were picked”.
3️⃣  For k = 0…n
        pair   k‑element subsets from left
            with (n‑k)-element subsets from right
   → guarantees total of n chosen elements.
4️⃣  Inside each pair of buckets use **binary search**
    to find the right sum that brings us closest to total/2.
5️⃣  Track the best absolute difference found.
```

---

## 5 ▸ Detailed Walk‑through of the Code

```cpp
void subsetSum(const vector<int>& nums,
               vector<vector<long long>>& sums)
```

|Line|Purpose|
|---|---|
|`int n = nums.size();`|Size of this half (≤ 15).|
|Outer loop `mask = 0 … (1<<n)-1`|Iterates over _all_ subsets (bitmask technique).|
|Inside loop|Accumulate `sum` of selected elements and count `chosen` bits.|
|`sums[chosen].push_back(sum);`|Append the subset sum to the bucket for that _chosen_ size.|
|After loop: `sort(bucket)`|Sorting each bucket enables **binary search** later.|

> **Important:** `sums` already has `n+1` inner vectors (`0 … n`) when the function is called.  
> No `resize()` or `assign()` inside—pure push‑backs.

---

```cpp
int minimumDifference(vector<int>& nums)
```

1. **Split and prepare**
    

```cpp
int n = nums.size()/2;
long long total = accumulate(nums.begin(), nums.end(), 0LL);

vector<int> leftNums(nums.begin(), nums.begin()+n);
vector<int> rightNums(nums.begin()+n, nums.end());

vector<vector<long long>> leftSums(n+1), rightSums(n+1);
subsetSum(leftNums, leftSums);
subsetSum(rightNums, rightSums);
```

- `leftSums[k]` holds _all_ sums made with exactly `k` numbers from the left half.
    
- `rightSums[k]` holds sums with `k` numbers from the right half.
    

2. **Target** we’d love each chosen side to approach:
    

```cpp
long long target = total/2;
```

3. **Merge phase – choosing k elements in detail**
    

```cpp
for (int k = 0; k <= n; ++k) {
    // pick k from left, n‑k from right
    auto& leftBucket  = leftSums[k];
    auto& rightBucket = rightSums[n-k];
```

_Why this guarantees exactly n items?_  
Left contributes `k`, right contributes `n-k` → total `n`.  
Because every subset recorded in those buckets already knows its own pick count, we never mis‑count.

4. **Binary search for the best partner**
    

For each `leftSum`:

```cpp
long long need = target - leftSum;
auto it = lower_bound(rightBucket.begin(), rightBucket.end(), need);
```

- `it` is the first right sum ≥ `need`.  
    _Two candidates_ give nearest difference: `*it` and the value just before `it`.
    

We compute:

```cpp
totalLeft = leftSum + rightSum;          // total of chosen n elements
diff      = | total - 2×totalLeft |      // objective
```

Track the minimum across all loops.

5. **Return**
    

```cpp
return static_cast<int>(bestDiff);
```

---

## 6 ▸ Dry Run – Example `[3, 9, 7, 3]`

```
n = 2           total = 22        target = 11
leftNums  = [3, 9]
rightNums = [7, 3]
```

### 6.1  Generate buckets

Left buckets:

```
k=0: [0]
k=1: [3, 9]
k=2: [12]
```

Right buckets (sorted):

```
k=0: [0]
k=1: [3, 7]
k=2: [10]
```

### 6.2  Merge

|k|leftBucket|rightBucket|key steps|bestDiff|
|---|---|---|---|---|
|0|[0]|[10]|need=11, lower_bound→10totalLeft=10, diff=2|2|
|1|[3,9]|[3,7]|left=3 → need=8, lb→? end ⇒ back 7 diff=2 (same)left=9 → need=2, lb→3 diff=2|2|
|2|[12]|[0]|need=-1, lb→0 diff=2|2|

Minimum diff `= 2`.

---

## 7 ▸ Complexity Analysis

|Step|Time|Space|
|---|---|---|
|Subset generation each half|`O( n · 2^n )` (≤ 500 k ops)|`O( 2^n )` (32 768 per side)|
|Merge loops|`O( 2^n · log 2^n )` (binary search)|—|
|Overall (`n ≤ 15`)|≈ `10⁵` operations → **< 1 ms**|< 1 MB|

---

## 8 ▸ Why the _k‑bucket_ idea is mandatory

Without tracking how many elements a subset uses you could:

- accidentally pair 3 elements from left with 1 from right (total 4, not `n`)
    
- need extra bookkeeping on sizes
    

Buckets encode that constraint **for free**: picking from `leftSums[k]` and `rightSums[n‑k]` always sums to `n`.

---

## 9 ▸ Common Pitfalls

1. **Not pre‑allocating buckets** → pushing to `sums[chosen]` on an empty outer vector causes UB.  
    Solution: create `n+1` vectors before calling `subsetSum`.
    
2. **Sorting the outer vector** instead of each bucket – no effect.
    
3. **Forgetting both candidates in binary search** (≥ need and `< need`) – may miss optimum.
    

---

## 10 ▸ Key Take‑aways

- **Meet‑in‑the‑middle** halves the exponent in subset problems.
    
- **Bucket by element‑count** when an exact‑size constraint exists.
    
- Two‑sided **binary search** turns `O(M²)` combination into `O(M log M)`.
    

# Code

```cpp
class Solution {
public:
    // Function to compute all subset sums for a given vector 'nums'
    // grouped by the number of elements chosen.
    // For example, if nums = [3, 9], we generate:
    //  - sum 0 using 0 elements -> sums[0] = [0]
    //  - sum 3 or 9 using 1 element -> sums[1] = [3, 9]
    //  - sum 12 using both -> sums[2] = [12]
    void subsetSum(const vector<int>& nums, vector<vector<long long>>& sums) {
        int n = nums.size();  // number of elements in this half

        // There are 2^n subsets possible
        for (int mask = 0; mask < (1 << n); mask++) {
            long long sum = 0;   // sum of current subset
            int chosen = 0;      // how many elements are chosen in this subset

            for (int i = 0; i < n; i++) {
                if (mask & (1 << i)) {
                    // i-th element is included in this subset
                    sum += nums[i];
                    chosen++;
                }
            }

            // Store sum in the list of sums with 'chosen' elements
            sums[chosen].push_back(sum);
        }

        // For each bucket (fixed # of elements chosen), sort it
        // This allows binary search later when trying to get close to the target
        for (auto& bucket : sums) {
            sort(bucket.begin(), bucket.end());
        }
    }

    int minimumDifference(vector<int>& nums) {
        int n = nums.size() / 2;  // Since nums has 2n elements

        // Total sum of all elements
        long long total = accumulate(nums.begin(), nums.end(), 0LL);

        // Split the array into two halves: left and right
        // We'll perform brute-force subset sum generation separately on each half
        vector<int> leftNums(nums.begin(), nums.begin() + n);
        vector<int> rightNums(nums.begin() + n, nums.end());

        // Each vector holds subsets grouped by how many elements are picked
        // Example: leftSums[0] → sums using 0 elements from leftNums
        //          leftSums[1] → sums using 1 element from leftNums, etc.
        vector<vector<long long>> leftSums(n + 1);   // from 0 to n elements
        vector<vector<long long>> rightSums(n + 1);  // same for right half

        // Generate subset sums for both halves
        subsetSum(leftNums, leftSums);
        subsetSum(rightNums, rightSums);

        // We are trying to make sum of n chosen elements ≈ total / 2
        long long target = total / 2;
        long long bestDiff = LLONG_MAX;  // best (smallest) absolute difference seen so far

        // Try every possible split: choose k elements from left and n - k from right
        for (int k = 0; k <= n; k++) {
            auto& leftBucket = leftSums[k];        // All subset sums choosing k from left
            auto& rightBucket = rightSums[n - k];  // All subset sums choosing (n-k) from right

            // For each leftSum in this bucket, find the best rightSum to get close to target
            for (long long leftSum : leftBucket) {
                // We want totalLeft ≈ target ⇒ rightSum ≈ target - leftSum
                long long need = target - leftSum;

                // Find the smallest rightSum ≥ need (binary search)
                auto it = lower_bound(rightBucket.begin(), rightBucket.end(), need);

                // Case 1: rightSum ≥ need
                if (it != rightBucket.end()) {
                    long long rightSum = *it;
                    long long totalLeft = leftSum + rightSum;
                    long long diff = abs(total - 2 * totalLeft);  // |S1 - S2| = |total - 2 * S1|
                    bestDiff = min(bestDiff, diff);
                }

                // Case 2: rightSum < need, check previous value for possible better match
                if (it != rightBucket.begin()) {
                    --it;
                    long long rightSum = *it;
                    long long totalLeft = leftSum + rightSum;
                    long long diff = abs(total - 2 * totalLeft);
                    bestDiff = min(bestDiff, diff);
                }
            }
        }

        // Return the best minimum difference found
        return static_cast<int>(bestDiff);
    }
};


```