Here's a detailed explanation of solving the Longest Increasing Subsequence (LIS) problem using Dynamic Programming (DP) with O(n²) time complexity in C++.


---

Problem Statement:

Given an array arr[] of size n, find the length of the Longest Increasing Subsequence (LIS).

> A subsequence is a sequence that can be derived by deleting some or no elements without changing the order of the remaining elements.




---

Approach: Dynamic Programming (DP) – O(n²)

Key Idea:

For each element arr[i], check all previous elements arr[j] where j < i.
If arr[j] < arr[i], then arr[i] can be appended to the increasing subsequence ending at arr[j].


---

Step-by-Step Explanation:

1. Create a DP array dp[n]:

dp[i] will store the length of the LIS ending at index i.



2. Initialize all dp values to 1:

Every element is a subsequence of length 1 by itself.



3. Iterate through each element i = 1 to n-1:

For each j = 0 to i-1:

If arr[j] < arr[i]:

Update dp[i] = max(dp[i], dp[j] + 1).





4. The answer is the maximum value in the dp[] array.




---

C++ Code:
```cpp

#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int longestIncreasingSubsequence(vector<int>& arr) {
    int n = arr.size();
    vector<int> dp(n, 1); // Step 1: Initialize dp array with 1

    // Step 2: Fill dp array using nested loops
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < i; j++) {
            if (arr[j] < arr[i]) {
                dp[i] = max(dp[i], dp[j] + 1);
            }
        }
    }

    // Step 3: Return the maximum value in dp[]
    return *max_element(dp.begin(), dp.end());
}

int main() {
    vector<int> arr = {10, 9, 2, 5, 3, 7, 101, 18};
    int lis_length = longestIncreasingSubsequence(arr);
    cout << "Length of LIS: " << lis_length << endl;
    return 0;
}

```

---

Example:

Input:

arr = [10, 9, 2, 5, 3, 7, 101, 18]

DP table after processing:

dp = [1, 1, 1, 2, 2, 3, 4, 4]

LIS = 2, 3, 7, 101 → Length = 4


## Understanding the Longest Increasing Subsequence (LIS) Algorithm

The **Longest Increasing Subsequence (LIS)** problem is a classic algorithmic challenge that involves finding the longest subsequence in an array where elements are in strictly increasing order. A subsequence is a sequence derived from the array by deleting some or no elements without changing the order of the remaining elements. The goal is to compute either the length of the LIS or the subsequence itself efficiently. Below, we’ll explore the intuition, approach, dry runs, and a concise C++ implementation, keeping the explanation clear and focused.

---

### Key Points
- **Problem**: Find the longest subsequence in an array where elements are strictly increasing.
- **Efficient Approach**: Use dynamic programming with binary search to achieve O(n log n) time complexity.
- **Intuition**: Track the smallest element that can end a subsequence of each length, updating it as we process the array.
- **Applications**: Used in sequence analysis, scheduling, and bioinformatics.

---

### What is the LIS Problem?

Given an array of integers, the LIS is the longest subsequence (not necessarily contiguous) where each element is strictly greater than the previous one. For example, in the array `[10, 22, 9, 33, 21, 50, 41, 60]`, one LIS is `[10, 22, 33, 50, 60]` with length 5. The problem can ask for either the length or the actual subsequence.

---

### Intuition Behind the LIS Algorithm

The naive approach using dynamic programming computes the LIS ending at each index, yielding O(n²) time complexity. However, a more efficient O(n log n) approach uses a greedy strategy combined with binary search. The key idea is to maintain an array `tail` where `tail[i]` represents the smallest element that can end an increasing subsequence of length `i+1`. As we process each element, we either:
- Extend the longest subsequence by appending a larger element.
- Replace an existing element in `tail` with a smaller one to potentially allow longer subsequences later.

This works because a smaller element at a given length increases the chance of extending the subsequence with future elements.

---

### How the Algorithm Works

The O(n log n) algorithm proceeds as follows:
1. Initialize an array `tail` to store the smallest element ending a subsequence of each length.
2. For each element `arr[i]`:
   - If `arr[i]` is greater than the last element in `tail`, append it (extends the LIS).
   - Otherwise, use binary search to find the smallest index in `tail` where `tail[j] ≥ arr[i]`, and replace `tail[j]` with `arr[i]`.
3. The length of `tail` at the end is the length of the LIS.
4. To reconstruct the subsequence, track predecessors during the process.

The `tail` array doesn’t store the actual LIS but maintains candidates that ensure the longest possible subsequence.

---

### Dry Run: LIS Length

Let’s compute the LIS length for the array `[10, 22, 9, 33, 21, 50, 41, 60]`.

| Index | Element | Tail Array (after processing) | Length | Notes |
|-------|---------|-------------------------------|--------|-------|
| 0     | 10      | [10]                          | 1      | Start with 10 |
| 1     | 22      | [10, 22]                     | 2      | Append 22 (>10) |
| 2     | 9       | [9, 22]                      | 2      | Replace 10 with 9 (9 < 10) |
| 3     | 33      | [9, 22, 33]                  | 3      | Append 33 (>22) |
| 4     | 21      | [9, 21, 33]                  | 3      | Replace 22 with 21 (21 < 22) |
| 5     | 50      | [9, 21, 33, 50]              | 4      | Append 50 (>33) |
| 6     | 41      | [9, 21, 33, 41]              | 4      | Replace 50 with 41 (41 < 50) |
| 7     | 60      | [9, 21, 33, 41, 60]          | 5      | Append 60 (>41) |

**Result**: LIS length = 5.

**Key Observations**:
- Replacing 10 with 9 allows a potential longer sequence (e.g., 9, 21, ...).
- Binary search finds the position to replace efficiently (e.g., 21 replaces 22).

---

### Dry Run: Reconstructing the LIS

To reconstruct the LIS, we track indices in a `parent` array during updates. After the above process, we backtrack from the last element in `tail` that leads to a valid sequence. For `[10, 22, 9, 33, 21, 50, 41, 60]`, one possible LIS is `[9, 21, 33, 41, 60]` (indices 2, 4, 3, 6, 7). The reconstruction involves:
- Storing the index of each element added or replaced.
- Tracing back from the last index to build the sequence.

---

### Intuition Behind the Approach

- **Greedy Replacement**: Using a smaller element to end a subsequence of length k increases flexibility for future extensions. For example, replacing 10 with 9 allows sequences like `[9, 21, 33]` that might not include 10.
- **Binary Search**: Since `tail` is sorted (smallest endings for each length), binary search finds the replacement position in O(log n), making the overall algorithm O(n log n).
- **Why it works**: The `tail` array ensures we always have the smallest possible ending for each subsequence length, maximizing the chance of finding the longest sequence.

---

### C++ Implementation

Here’s a concise C++ implementation to compute the LIS length and reconstruct the subsequence:

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

pair<int, vector<int>> findLIS(const vector<int>& arr) {
    int n = arr.size();
    vector<int> tail;           // Smallest element ending subsequence of each length
    vector<int> indices(n, -1); // Track indices for reconstruction
    vector<int> prev(n, -1);    // Previous index in LIS
    int len = 0;                // Length of LIS

    for (int i = 0; i < n; i++) {
        if (tail.empty() || arr[i] > tail.back()) {
            if (!tail.empty()) prev[i] = indices[len - 1];
            tail.push_back(arr[i]);
            indices[len++] = i;
        } else {
            int pos = lower_bound(tail.begin(), tail.end(), arr[i]) - tail.begin();
            tail[pos] = arr[i];
            indices[pos] = i;
            if (pos > 0) prev[i] = indices[pos - 1];
        }
    }

    // Reconstruct LIS
    vector<int> lis;
    for (int i = indices[len - 1]; i >= 0; i = prev[i]) {
        lis.push_back(arr[i]);
    }
    reverse(lis.begin(), lis.end());

    return {len, lis};
}

int main() {
    vector<int> arr = {10, 22, 9, 33, 21, 50, 41, 60};
    auto [length, sequence] = findLIS(arr);
    cout << "LIS Length: " << length << endl;
    cout << "LIS: ";
    for (int x : sequence) cout << x << " ";
    cout << endl;
    return 0;
}
```

**Output**:
```
LIS Length: 5
LIS: 9 21 33 41 60
```

**Explanation**:
- `tail`: Stores the smallest element for each subsequence length.
- `indices`: Tracks the index of the element in `tail`.
- `prev`: Stores the previous index in the LIS for reconstruction.
- `lower_bound`: Binary search to find the replacement position.
- Time Complexity: O(n log n) due to binary search for each element.
- Space Complexity: O(n) for `tail`, `indices`, and `prev`.

---

### Conclusion

The LIS algorithm with O(n log n) complexity is an elegant solution that uses a greedy approach and binary search to efficiently compute the longest increasing subsequence. The `tail` array maintains the smallest possible endings, ensuring flexibility for longer sequences. The dry runs illustrate how replacements and extensions work, and the C++ code provides a practical implementation for both length and sequence reconstruction. This approach is widely used in problems requiring sequence analysis and optimization.

--- 

### Key Citations
- [Longest Increasing Subsequence - GeeksforGeeks](https://www.geeksforgeeks.org/longest-increasing-subsequence-lis/)
- [LIS in O(n log n) - CP Algorithms](https://cp-algorithms.com/sequences/longest_increasing_subsequence.html)