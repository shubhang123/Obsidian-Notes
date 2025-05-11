#recursion #dp 
```cpp
#include <bits/stdc++.h>
using namespace std;

// Maximum target size supported (change if needed)
const int MAXN = 1e6 + 5;

// dp[n] stores the minimum number of coins required to make sum 'n'
// Initially all values in dp[] will be set to -1
int dp[MAXN];


// ----------------------------------------
// Recursive Approach with Memoization (Top-Down DP)
// ----------------------------------------

// This function tries to make amount 'n' using the least number of coins.
// It uses recursion to try all combinations and memoizes the result in dp[n].
int solve(int n, vector<int>& coins) {
    // Base Case: if target is 0, no coins are needed
    if (n == 0) return 0;

    // Invalid Case: if target becomes negative, this path is invalid
    if (n < 0) return -1;

    // If already computed, directly return the answer
    if (dp[n] != -1) return dp[n];

    // Initialize the answer to a large number (we’ll take min over this)
    int minCoins = INT_MAX;

    // Try each coin denomination
    for (int coin : coins) {
        // Recursive call: we try to make up amount (n - coin)
        int temp = solve(n - coin, coins);

        // If subproblem was solvable, take min
        if (temp != -1) {
            minCoins = min(minCoins, temp + 1);
        }
    }

    // If no combination worked, return -1; else return computed minCoins
    return dp[n] = (minCoins == INT_MAX) ? -1 : minCoins;
}


// ----------------------------------------
// Iterative Approach (Bottom-Up DP)
// ----------------------------------------

// This function builds the dp[] array from 0 up to target 'n'
// It avoids recursion and fills the table iteratively.
int solve1(int n, vector<int>& coins) {
    // Set all dp values to -1 indicating "unreachable"
    memset(dp, -1, sizeof(dp));

    // Base Case: 0 coins needed to make sum 0
    dp[0] = 0;

    // Iterate from 1 to n to build up dp[i]
    for (int i = 1; i <= n; ++i) {
        int minCoins = INT_MAX;

        // Try each coin denomination to see if we can reach current sum
        for (int coin : coins) {
            int prev = i - coin;

            // If subproblem (i - coin) is valid and solvable
            if (prev >= 0 && dp[prev] != -1) {
                minCoins = min(minCoins, dp[prev] + 1);
            }
        }

        // If minCoins is still INF, this amount is unreachable
        if (minCoins != INT_MAX)
            dp[i] = minCoins;
    }

    // dp[n] will have the answer (or -1 if unreachable)
    return dp[n];
}


// ----------------------------------------
// Main Function
// ----------------------------------------

int main() {
    int num, target;
    cin >> num >> target;  // Read number of coins and target sum

    vector<int> coins(num);
    for (int i = 0; i < num; i++) {
        cin >> coins[i];  // Read each coin denomination
    }

    // Initialize dp[] with -1 before calling either method
    memset(dp, -1, sizeof(dp));

    // -------------------------
    // You can toggle between approaches here:
    // int ans = solve(target, coins);  // Recursive approach
    int ans = solve1(target, coins);    // Iterative approach
    // -------------------------

    cout << ans << '\n';  // Print
#
```