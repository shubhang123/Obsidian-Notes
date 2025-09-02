# Kadane's Algorithm - Detailed Notes

## Overview

Kadane's Algorithm is a dynamic programming approach to solve the **Maximum Subarray Problem** - finding the contiguous subarray within a one-dimensional array that has the largest sum. It runs in O(n) time complexity and uses O(1) space.

## Core Algorithm Logic

The algorithm maintains two key variables:

- **max_so_far**: Maximum sum found so far (global maximum)
- **max_ending_here**: Maximum sum of subarray ending at current position (local maximum)

### Basic Implementation

```cpp
max_so_far = arr[0]
max_ending_here = arr[0]

for i = 1 to n-1:
    max_ending_here = max(arr[i], max_ending_here + arr[i])
    max_so_far = max(max_so_far, max_ending_here)

return max_so_far
```

## Key Insight

At each position, we decide whether to:

1. **Start a new subarray** from current element (if current element > sum so far)
2. **Extend the existing subarray** by including current element

This decision is made by: `max_ending_here = max(arr[i], max_ending_here + arr[i])`

## Two Important Cases

### Case 1: At Least One Non-Negative Integer Present

When the array contains at least one non-negative (≥ 0) element:

- The maximum subarray sum will be **at least 0**
- The algorithm works as described above
- We can confidently return the computed maximum

**Example**: `[-2, 1, -3, 4, -1, 2, 1, -5, 4]`

- Contains positive elements: 1, 4, 2, 1, 4
- Maximum subarray: `[4, -1, 2, 1]` with sum = 6

### Case 2: All Negative Integers

When all elements in the array are negative:

- The standard Kadane's algorithm would return the **least negative element**
- This is because the best strategy is to pick the single largest (least negative) element
- No subarray of length > 1 can have a sum greater than any individual element

**Example**: `[-8, -3, -6, -2, -5, -4]`

- All elements are negative
- Maximum subarray: `[-2]` with sum = -2 (the least negative element)

## Handling Edge Cases

### Modified Algorithm for All-Negative Case

```cpp
max_so_far = arr[0]
max_ending_here = arr[0]
all_negative = true

for i = 1 to n-1:
    if arr[i] >= 0:
        all_negative = false
    
    max_ending_here = max(arr[i], max_ending_here + arr[i])
    max_so_far = max(max_so_far, max_ending_here)

if all_negative:
    return maximum_element_in_array
else:
    return max_so_far
```

## Algorithm Walkthrough Example

Array: `[-2, 1, -3, 4, -1, 2, 1, -5, 4]`

|i|arr[i]|max_ending_here|max_so_far|Decision|
|---|---|---|---|---|
|0|-2|-2|-2|Initialize|
|1|1|1|1|Start new (1 > -2+1)|
|2|-3|-2|1|Extend (1-3 = -2)|
|3|4|4|4|Start new (4 > -2+4)|
|4|-1|3|4|Extend (4-1 = 3)|
|5|2|5|5|Extend (3+2 = 5)|
|6|1|6|6|Extend (5+1 = 6)|
|7|-5|1|6|Extend (6-5 = 1)|
|8|4|5|6|Extend (1+4 = 5)|

**Result**: Maximum subarray sum = 6, subarray = `[4, -1, 2, 1]`

## Time and Space Complexity

- **Time Complexity**: O(n) - single pass through the array
- **Space Complexity**: O(1) - only uses constant extra space

## Variations and Extensions

- **Finding actual subarray indices**: Track start and end positions
- **Circular array version**: Consider wrap-around subarrays
- **2D version**: Maximum sum rectangle in a matrix
- **K-Kadane**: Find K maximum non-overlapping subarrays

## Why It Works

The algorithm works because it maintains the optimal solution at each step using the principle of optimality: if we know the maximum subarray ending at position i-1, we can compute the maximum subarray ending at position i by either extending the previous subarray or starting fresh from the current element.