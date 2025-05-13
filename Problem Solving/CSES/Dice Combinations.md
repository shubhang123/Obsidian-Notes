```cpp
#include <bits/stdc++.h>
using namespace std;
 
const int mod = 1e9 + 7;
const int MAXN = 1e6 + 5; // Assumed maximum possible value of n
 
int dp[MAXN]; // C-style array for memoization
 
// Recursive function to count the number of ways to reach sum 'n'
// using dice rolls (1 to 6), with memoization
int solve(int n) {
    // Base case 1:
    // There's exactly one way to form sum 0 — by doing nothing
    if (n == 0) return 1;
 
    // Base case 2:
    // If n becomes negative, it means this path is invalid (overstepped), return 0
    if (n < 0) return 0;
 
    // Memoization check:
    // If we've already computed the answer for this 'n', return it directly
    if (dp[n] != -1) return dp[n];
 
    int sum = 0;
 
    // Recursive case:
    // Try every dice roll from 1 to 6
    for (int i = 1; i <= 6; ++i) {
        // Make the recursive call for the remaining sum (n - i)
        // and add it to the current total
        sum = (sum + solve(n - i)) % mod;
    }
 
    // Store the result in dp[n] to avoid recomputation
    return dp[n] = sum;
}
 
int main() {
    int n;
    cin >> n;
 
    // Initialize dp array with -1 to indicate uncomputed values
    memset(dp, -1, sizeof(dp));
 
    // Output the number of ways to form sum 'n'
    cout << solve(n) << '\n';
 
    return 0;
}
```