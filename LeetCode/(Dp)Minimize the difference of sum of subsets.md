/* Minimum Subset Sum Difference Problem


---

1. Pure Recursion



We branch on each element: include it in subset 1 (add to sum1) or subset 2 (add to sum2), and return the best of the two. */

#include <bits/stdc++.h> using namespace std;

// Pure recursive solution: explore both choices at each index. int findMinDiffRec(const vector<int>& arr, int i, int sum1, int sum2) { // Base case: all elements are placed if (i == arr.size()) return abs(sum1 - sum2);

// Choice 1: put arr[i] in subset1
int take = findMinDiffRec(arr, i + 1, sum1 + arr[i], sum2);
// Choice 2: put arr[i] in subset2
int skip = findMinDiffRec(arr, i + 1, sum1, sum2 + arr[i]);

return min(take, skip);

}

int minDifferenceRec(vector<int>& arr) { return findMinDiffRec(arr, 0, 0, 0); }

int main() { vector<int> arr = {1, 6, 11, 5}; cout << minDifferenceRec(arr) << "\n";  // Output: 1 return 0; }

/* Time Complexity: O(2^n) Why memoize? Because we recompute the same (i, sum1) states over and over. */

/*

2. Top-Down DP (Memoization)



We observe that at any call the only “state” that matters is (i, sum1) (since sum2 = totalSum – sum1). We store those in a table to avoid recomputation. */

#include <bits/stdc++.h> using namespace std;

vector<vector<int>> dp; int totalSum;

// Recursive helper with memoization int findMinDiffMemo(const vector<int>& arr, int i, int sum1) { if (i == arr.size()) { int sum2 = totalSum - sum1; return abs(sum1 - sum2); }

// If already computed, return it
if (dp[i][sum1] != -1)
    return dp[i][sum1];

// Option 1: include arr[i] in subset1
int take = findMinDiffMemo(arr, i + 1, sum1 + arr[i]);
// Option 2: skip it (goes into subset2)
int skip = findMinDiffMemo(arr, i + 1, sum1);

return dp[i][sum1] = min(take, skip);

}

int minDifferenceMemo(vector<int>& arr) { totalSum = accumulate(arr.begin(), arr.end(), 0); dp = vector<vector<int>>(arr.size(), vector<int>(totalSum + 1, -1)); return findMinDiffMemo(arr, 0, 0); }

int main() { vector<int> arr = {1, 6, 11, 5}; cout << minDifferenceMemo(arr) << "\n";  // Output: 1 return 0; }

