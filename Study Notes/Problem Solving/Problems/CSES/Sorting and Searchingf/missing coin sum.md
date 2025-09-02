You have nnn coins with positive integer values. What is the smallest sum you cannot create using a subset of the coins?

# Code
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;

    vector<long long> nums(n);
    for (int i = 0; i < n; i++) {
        cin >> nums[i];
    }

    // Step 1: Sort the coins in increasing order.
    // This is important so we can build sums starting from smallest upward.
    sort(nums.begin(), nums.end());

    // Step 2: Initialize the current sum we can build to 0
    // We haven't picked any coins yet, so the smallest unreachable sum is 1
    long long currSum = 0;

    // Step 3: Traverse through the sorted coin values
    for (int i = 0; i < n; i++) {
        // If the current coin is greater than the smallest sum we *can't* form (currSum + 1),
        // it means there's a gap — we can't fill it with this or any later coin.
        if (nums[i] > currSum + 1) {
            // This is the smallest sum that cannot be formed
            cout << currSum + 1;
            return 0;
        }

        // Else, we can safely extend the range of sums we can build
        // For example: if currSum was 6 and nums[i] is 3, now we can build sums up to 6+3 = 9
        currSum += nums[i];
    }

    // If we never found a gap, then we can form all sums up to currSum
    // So the smallest sum we cannot form is currSum + 1
    cout << currSum + 1;
    return 0;
}

```