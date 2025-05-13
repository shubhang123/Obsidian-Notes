Below are three progressively optimized C++ implementations for the “Minimum Subset Sum Difference” problem:


---

1. Pure Recursion

We branch on each element: include it in subset 1 (add to sum1) or subset 2 (add to sum2), and return the best of the two.

#include <bits/stdc++.h>
using namespace std;

// Pure recursive solution: explore both choices at each index.
int findMinDiffRec(const vector<int>& arr, int i, int sum1, int sum2) {
    // Base case: all elements are placed
    if (i == arr.size()) 
        return abs(sum1 - sum2);

    // Choice 1: put arr[i] in subset1
    int take = findMinDiffRec(arr, i + 1, sum1 + arr[i], sum2);
    // Choice 2: put arr[i] in subset2
    int skip = findMinDiffRec(arr, i + 1, sum1, sum2 + arr[i]);

    return min(take, skip);
}

int minDifferenceRec(vector<int>& arr) {
    return findMinDiffRec(arr, 0, 0, 0);
}

int main() {
    vector<int> arr = {1, 6, 11, 5};
    cout << minDifferenceRec(arr) << "\n";  // Output: 1
    return 0;
}

Time Complexity: O(2ⁿ)

Why memoize? Because we recompute the same (i, sum1) states over and over.



---

2. Top-Down DP (Memoization)

We observe that at any call the only “state” that matters is (i, sum1) (since sum2 = totalSum – sum1). We store those in a table to avoid recomputation.

#include <bits/stdc++.h>
using namespace std;

// dp[i][s] = minimum difference achievable using elements from i…n-1
//           when current subset1 sum = s
vector<vector<int>> dp;
int totalSum;

// Recursive helper with memoization
int findMinDiffMemo(const vector<int>& arr, int i, int sum1) {
    if (i == arr.size()) {
        int sum2 = totalSum - sum1;
        return abs(sum1 - sum2);
    }
    // If already computed, return it
    if (dp[i][sum1] != -1) 
        return dp[i][sum1];

    // Option 1: include arr[i] in subset1
    int take = findMinDiffMemo(arr, i + 1, sum1 + arr[i]);
    // Option 2: skip it (goes into subset2)
    int skip = findMinDiffMemo(arr, i + 1, sum1);

    // Store and return best
    return dp[i][sum1] = min(take, skip);
}

int minDifferenceMemo(vector<int>& arr) {
    totalSum = accumulate(arr.begin(), arr.end(), 0);
    int n = arr.size();
    // Initialize dp with -1 (uncomputed). 
    // sum1 can range from 0…totalSum
    dp.assign(n, vector<int>(totalSum + 1, -1));
    return findMinDiffMemo(arr, 0, 0);
}

int main() {
    vector<int> arr = {1, 6, 11, 5};
    cout << minDifferenceMemo(arr) << "\n";  // Output: 1
    return 0;
}

Time Complexity: O(n · totalSum)

Space Complexity: O(n · totalSum) for the memo table.



---

3. Bottom-Up DP (Tabulation)

We translate the top-down states into a table dp[i][s] where:

i goes from n down to 0

s goes from 0 up to totalSum


dp[i][s] = best difference achievable using elements from index i onward when subset1 currently sums to s.

Steps to Derive Tabulation

1. State definition: dp[i][s] as above.


2. Base case: at i == n, difference = |s - (totalSum − s)|.


3. Transition:

// take arr[i] → new sum1 = s + arr[i]
int take = dp[i+1][s + arr[i]];
// skip arr[i] → sum1 stays s
int skip = dp[i+1][s];
dp[i][s] = min(take, skip);



Tabulated C++ Code

#include <bits/stdc++.h>
using namespace std;

int minDifferenceTab(vector<int>& arr) {
    int n = arr.size();
    int totalSum = accumulate(arr.begin(), arr.end(), 0);

    // dp[i][s]: see above. Dimensions (n+1) x (totalSum+1)
    vector<vector<int>> dp(n + 1, vector<int>(totalSum + 1));

    // Base case: i = n
    for (int s = 0; s <= totalSum; ++s) {
        dp[n][s] = abs(s - (totalSum - s));
    }

    // Fill bottom-up
    for (int i = n - 1; i >= 0; --i) {
        for (int s = 0; s <= totalSum; ++s) {
            // Option 1: include in subset1 if it fits
            int take = INT_MAX;
            if (s + arr[i] <= totalSum)
                take = dp[i + 1][s + arr[i]];
            // Option 2: skip
            int skip = dp[i + 1][s];
            dp[i][s] = min(take, skip);
        }
    }

    // Answer is dp[0][0]: starting at index 0 with sum1 = 0
    return dp[0][0];
}

int main() {
    vector<int> arr = {1, 6, 11, 5};
    cout << minDifferenceTab(arr) << "\n";  // Output: 1
    return 0;
}

Time Complexity: O(n · totalSum)

Space Complexity: O(n · totalSum)



---

Space Optimization

You can notice that dp[i] depends only on dp[i+1], so you can roll the table into two 1D arrays of length totalSum+1 (or even one, iterating s in reverse), to achieve O(totalSum) extra space.


---

Summary of the three approaches:

1. Recursion: Easy to write, exponential time.


2. Memoization (Top-Down): Same logic but caches overlapping subproblems → polynomial time.


3. Tabulation (Bottom-Up): Iteratively fills the DP table, same complexity, often faster in practice and straightforward to optimize space.



