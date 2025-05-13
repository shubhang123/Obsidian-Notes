## Minimum Subset Sum Difference Problem

### 1. Pure Recursion
We branch on each element: include it in subset 1 (add to sum1) or subset 2 (add to sum2), and return the best of the two.

```cpp
#include <bits/stdc++.h>
using namespace std;

// Pure recursive solution: explore both choices at each index.
int findMinDiffRec(const vector<int>& arr, int i, int sum1, int sum2) {
    if (i == arr.size())
        return abs(sum1 - sum2);

    int take = findMinDiffRec(arr, i + 1, sum1 + arr[i], sum2);
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
```

**Time Complexity**: O(2^n)

Why memoize? Because we recompute the same `(i, sum1)` states over and over.

---

### 2. Top-Down DP (Memoization)
We observe that at any call the only "state" that matters is `(i, sum1)` (since `sum2 = totalSum – sum1`). We store those in a table to avoid recomputation.

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<vector<int>> dp;
int totalSum;

int findMinDiffMemo(const vector<int>& arr, int i, int sum1) {
    if (i == arr.size()) {
        int sum2 = totalSum - sum1;
        return abs(sum1 - sum2);
    }

    if (dp[i][sum1] != -1)
        return dp[i][sum1];

    int take = findMinDiffMemo(arr, i + 1, sum1 + arr[i]);
    int skip = findMinDiffMemo(arr, i + 1, sum1);

    return dp[i][sum1] = min(take, skip);
}

int minDifferenceMemo(vector<int>& arr) {
    totalSum = accumulate(arr.begin(), arr.end(), 0);
    dp = vector<vector<int>>(arr.size(), vector<int>(totalSum + 1, -1));
    return findMinDiffMemo(arr, 0, 0);
}

int main() {
    vector<int> arr = {1, 6, 11, 5};
    cout << minDifferenceMemo(arr) << "\n";  // Output: 1
    return 0;
}
```

---

### 3. Bottom-Up DP (Tabulation)
We convert the recursive idea into an iterative DP solution. The idea is to determine all possible subset sums and find the one closest to half of the total sum.

```cpp
#include <bits/stdc++.h>
using namespace std;

int minDifferenceTab(vector<int>& arr) {
    int n = arr.size();
    int totalSum = accumulate(arr.begin(), arr.end(), 0);
    vector<vector<bool>> dp(n + 1, vector<bool>(totalSum + 1, false));

    // Base case: sum 0 is always possible
    for (int i = 0; i <= n; i++)
        dp[i][0] = true;

    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= totalSum; j++) {
            if (arr[i - 1] <= j)
                dp[i][j] = dp[i - 1][j] || dp[i - 1][j - arr[i - 1]];
            else
                dp[i][j] = dp[i - 1][j];
        }
    }

    int minDiff = INT_MAX;
    for (int s1 = 0; s1 <= totalSum / 2; s1++) {
        if (dp[n][s1]) {
            int s2 = totalSum - s1;
            minDiff = min(minDiff, abs(s2 - s1));
        }
    }
    return minDiff;
}

int main() {
    vector<int> arr = {1, 6, 11, 5};
    cout << minDifferenceTab(arr) << "\n";  // Output: 1
    return 0;
}
```

**Time Complexity**: O(n * totalSum)  
**Space Complexity**: O(n * totalSum)

