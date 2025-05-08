## Problem Statement

You are given an array of `n` integers. Determine the number of distinct subsets of the array that sum exactly to a target value `x`.

## Input

- The first line contains two integers `n` and `x`: the size of the array and the target sum.
    
- The second line contains `n` integers `t1, t2, ..., tn`: the elements of the array.
    

## Output

Print the number of subsets that sum to `x`.

## Constraints

- `1 ≤ n ≤ 40`
    
- `1 ≤ x ≤ 10^9`
    
- `1 ≤ ti ≤ 10^9`
    

## Example

**Input:**
`4 5 1 2 3 2`

**Output:**
3

# Algorithm

# Solving a Problem with Meet-in-the-Middle Approach

I initially analyzed this problem and realized it has an exponential time complexity. For such problems, we can only handle input sizes up to n = 20 if we want the solution to run within 1 second. However, the problem constraints specify n can be up to 40, which is twice what we can handle with a straightforward approach.

To solve this challenge, I implemented a meet-in-the-middle strategy, which divides the array into two halves and processes each half separately. This allows us to handle the larger input size efficiently.

## My Approach

1. I split the array into two halves: left and right.
2. For each half, I generated all possible subset sums.
3. Initially, I tried using unordered maps to look up sums in O(1) time, but inserting 2^n elements into maps was itself time-consuming and caused Time Limit Exceeded (TLE) errors.
4. Instead, I created arrays to store the subset sums and sorted one of them.
5. With one array sorted, I could apply binary search to find elements that would complete our target sum - similar to a 2 Sum problem.
6. I had to handle a special case: multiple elements with the same sum might exist. To account for this, I implemented binary search to find both the upper and lower bounds (first and last occurrences) of matching elements, to get the total occurences of that element and added that to the count.

This approach effectively reduced the time complexity from O(2^n) to O(2^(n/2)), allowing the solution to handle inputs up to n = 40 within the time constraints.

The meet-in-the-middle technique is particularly useful for problems that would otherwise require exponential time but can be divided into two independent subproblems that can be combined efficiently.


# Implementing Subset Sum Using Bitmasks

## Function Breakdown

```cpp
void subsetSum(const vector<int>& nums, vector<long long>& sums) {
    int n = nums.size();
    for (int mask = 0; mask < (1 << n); mask++) {
        long long sum = 0;
        for (int i = 0; i < n; i++) {
            if (mask & (1 << i)) sum += nums[i];
        }
        sums.push_back(sum);
    }
}
```

## How It Works

1. **Initialization**: First, you get the size `n` of the input array `nums`.
    
2. **Generating All Subsets with Bitmasks**: You use a for loop that iterates from 0 to 2^n - 1 (represented as `(1 << n)`). Each number in this range, when represented in binary, corresponds to a unique subset of the array.
    
3. **Interpreting the Bitmask**: For each mask value, you iterate through all positions (0 to n-1) of the array:
    
    - For each position `i`, you check if the corresponding bit in the mask is set using `mask & (1 << i)`
    - If the bit is set (non-zero result), it means the element at index `i` should be included in the current subset
    - You add this element to the running sum
4. **Storing Results**: After processing each mask (which represents one subset), you add the calculated sum to the `sums` vector.
    


# Code/Solution

```cpp
#include <bits/stdc++.h>
using namespace std;

int leftN, rightN;
vector<int> leftNums, rightNums;
vector<long long> leftSums, rightSums;

void subsetSum(const vector<int>& nums, vector<long long>& sums) {
    int n = nums.size();
    for (int mask = 0; mask < (1 << n);mask++) {
        long long sum = 0;
        for (int i = 0; i < n; i++) {
            if (mask & (1 << i)) sum += nums[i];
        }
        sums.push_back(sum);
    }
}

void divideArrays(int target, const vector<int>& nums, int n) {
    leftN = n / 2;
    rightN = n - leftN;

    leftNums.assign(nums.begin(), nums.begin() + leftN);
    rightNums.assign(nums.begin() + leftN, nums.end());

    subsetSum(leftNums, leftSums);
    subsetSum(rightNums, rightSums);
}

int main() {
    int n;
    long long target;
    cin >> n >> target;

    vector<int> nums(n);
    for (int i = 0; i < n;i++)
        cin >> nums[i];

    divideArrays(target, nums, n);

    // Sort rightSums for binary search
    sort(rightSums.begin(), rightSums.end());

    long long count = 0;
    for (long long leftSum : leftSums) {
        long long rem = target - leftSum;

        auto low = lower_bound(rightSums.begin(), rightSums.end(), rem);
        auto high = upper_bound(rightSums.begin(), rightSums.end(), rem);

        count += (high - low); 
    }

    cout << count << "\n";
    return 0;
}

```

