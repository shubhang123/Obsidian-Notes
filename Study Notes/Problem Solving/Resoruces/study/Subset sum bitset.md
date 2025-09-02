```cpp
#include <iostream>
#include <bitset>
#include <vector>
using namespace std;

bool subsetSumBitmask(vector<int>& arr, int target) {
    const int MAX_SUM = 10000; // Change as per your max possible sum
    bitset<MAX_SUM + 1> dp;
    dp[0] = 1; // base case: sum 0 is always possible (empty subset)

    for (int num : arr) {
        dp |= (dp << num);
    }

    return dp[target];
}

int main() {
    vector<int> arr = {3, 34, 4, 12, 5, 2};
    int target = 9;

    if (subsetSumBitmask(arr, target))
        cout << "Yes, subset exists\n";
    else
        cout << "No subset found\n";

    return 0;
}
```

Great — here's a complete theoretical explanation of solving the Subset Sum Problem using Bitmasking with bitset in C++. This includes problem definition, intuition, working, and advantages/limitations.


---

Subset Sum Problem – Theory

Definition:

Given a set of positive integers and a target value S, determine if there's a subset whose sum is exactly S.


---

Traditional DP Approach

Normally, we use a 2D or 1D DP table:

dp[i][j] = true if we can form sum j using first i elements.

Time Complexity: O(n * S)

Space Complexity: O(S) (if optimized)



---

Bitmasking Approach with bitset – Theory

Key Idea:

We use a bitset to represent all possible subset sums.

A bitset is a sequence of bits.

dp[i] = 1 means we can form a subset whose sum is i.



---

Bitset Operations Used:

1. Shift Operation dp << num

This creates new sums by adding num to all existing subset sums.

If dp[4] = 1, then dp[4 + num] = 1 in the new state.


2. OR Operation dp |= (dp << num)

We merge the new possible sums (after adding num) into the existing set.


---

Initialization:

dp[0] = 1;

We can always make a sum of 0 by choosing the empty subset.


---

Transition:

For each element num:

dp |= dp << num;

This means for all sums currently possible, we now can also form a sum by adding num.


---

Working Example

Let’s walk through an example:

arr = {3, 4, 2}
target = 9

Step-by-step:

1. Start: dp = 00000001 (only dp[0] = 1)


2. Add 3:

dp << 3 = 00001000

dp |= shifted → dp[3] = 1



3. Add 4:

now dp[0] = 1, dp[3] = 1

shift by 4 → dp[4] = 1, dp[7] = 1



4. Add 2:

now dp[0], dp[3], dp[4], dp[7] = 1

shift by 2 → adds dp[2], dp[5], dp[6], dp[9]




Final dp[9] = 1 → sum 9 is possible.


---

Time & Space Complexity

Time Complexity: O(n * S / w)

n: number of elements

S: target or max sum

w: word size (bitset is internally optimized using 64-bit chunks)


Space Complexity: O(S) bits


Bitsets are highly optimized at the hardware level, making this solution extremely fast.


---

Advantages

Speed: Bit-level operations are faster than nested loops.

Space Efficiency: Much smaller space compared to 2D DP.

Simplicity: Short, clean code once understood.



---

Limitations

Works only with non-negative integers

Target sum must be small (typically < 10^6)

Not flexible for constraints like choosing exactly k elements or negative values



---

When to Use

Use the bitmask + bitset trick when:

You just care whether a sum is possible (not the actual subset).

The array size is large but sum limits are small.

You need fast performance.



---

If you're preparing for interviews or competitions, mastering this technique can be a big time saver.

Let me know if you'd like a comparison with traditional DP, or need help modifying this to print the subset itself.

