#binarysearch
Sure, let's combine the explanations for `lower_bound` and `upper_bound` and provide an implementation that works with a `std::vector<int>` and a target `int` value.

### `lower_bound` and `upper_bound` Explanation

The C++ Standard Template Library (STL) provides the `lower_bound` and `upper_bound` functions, which are powerful tools for performing efficient binary searches on sorted ranges. These functions are particularly useful when you need to quickly locate elements within a sorted container based on a target value.

1. **`lower_bound`**:
   - Finds the first position in a sorted range where the element is **greater than or equal to** a target value.
   - It returns an iterator to this position.
   - If the target value is not found in the range, `lower_bound` returns an iterator to the first element that is greater than the target.
   - If the target value is greater than all elements in the range, `lower_bound` returns an iterator to the end of the range.

2. **`upper_bound`**:
   - Finds the first position in a sorted range where the element is **strictly greater than** a target value.
   - It returns an iterator to this position.
   - If the target value is not found in the range, `upper_bound` returns an iterator to the first element that is greater than the target.
   - If the target value is greater than or equal to all elements in the range, `upper_bound` returns an iterator to the end of the range.

These functions are efficient, with a time complexity of \(O(\log n)\), making them suitable for binary searches in sorted containers like arrays, vectors, and sets.

### Syntax

```cpp
#include <algorithm>
#include <vector>

// Syntax for lower_bound and upper_bound in a std::vector<int>
auto lower = std::lower_bound(vec.begin(), vec.end(), target);
auto upper = std::upper_bound(vec.begin(), vec.end(), target);
```

- `vec.begin()`: Start of the range.
- `vec.end()`: End of the range.
- `target`: The value to compare against.

### Custom Implementation

Here's a custom implementation of `lower_bound` and `upper_bound` that works with a `std::vector<int>` and a target `int` value:

```cpp
#include <vector>

template <typename T>
typename std::vector<T>::const_iterator lower_bound(const std::vector<T>& vec, T target) {
    size_t left = 0, right = vec.size();
    while (left < right) {
        size_t mid = left + (right - left) / 2;
        if (vec[mid] < target) {
            left = mid + 1;
        } else {
            right = mid;
        }
    }
    return vec.begin() + left;
}

template <typename T>
typename std::vector<T>::const_iterator upper_bound(const std::vector<T>& vec, T target) {
    size_t left = 0, right = vec.size();
    while (left < right) {
        size_t mid = left + (right - left) / 2;
        if (!(target < vec[mid])) {
            left = mid + 1;
        } else {
            right = mid;
        }
    }
    return vec.begin() + left;
}
```

These custom implementations follow the same logic as the STL versions:

1. `lower_bound` finds the first position in the range where the element is greater than or equal to the target value.
2. `upper_bound` finds the first position in the range where the element is strictly greater than the target value.

The functions use a binary search approach to efficiently locate the desired positions within the sorted range. The time complexity of both functions is \(O(\log n)\), where `n` is the size of the range.

### Example Usage

```cpp
std::vector<int> nums = {1, 2, 4, 4, 5, 7, 8};
int target = 4;

auto lower = lower_bound(nums, target);
auto upper = upper_bound(nums, target);

// Print the results
std::cout << "Lower bound: " << *lower << " (index: " << (lower - nums.begin()) << ")" << std::endl;
std::cout << "Upper bound: " << *upper << " (index: " << (upper - nums.begin()) << ")" << std::endl;
```

This will output:

```
Lower bound: 4 (index: 2)
Upper bound: 5 (index: 4)
```

The key points to remember are:

- `lower_bound` returns an iterator to the first element that is greater than or equal to the target value.
- `upper_bound` returns an iterator to the first element that is strictly greater than the target value.
- If the target value is not found in the range, both functions return an iterator to the first element that is greater than the target (or to the end of the range if the target is greater than all elements).
- These functions are efficient, with a time complexity of \(O(\log n)\), making them suitable for binary searches in sorted containers.
