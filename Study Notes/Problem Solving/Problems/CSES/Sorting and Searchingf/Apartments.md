# Apartment Allocation Algorithm - Study Notes

## Problem Statement

- **n** applicants want apartments
- **m** apartments available
- Each applicant has a **desired apartment size**
- Each apartment has an **actual size**
- An applicant accepts an apartment if: `|desired_size - apartment_size| ≤ k`
- Goal: **Maximize the number of applicants who get apartments**

## Algorithm Overview

**Type**: Greedy Algorithm with Two Pointers  
**Time Complexity**: O(n log n + m log m) - dominated by sorting  
**Space Complexity**: O(1) - excluding input storage

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    // n = num of applicants
    // m = num of apartments
    // k = difference allowed

    int n, m, k;
    cin >> n >> m >> k;

    vector<int> desired(n);
    vector<int> apartments(m);

    for (int i = 0; i < n; i++) cin >> desired[i];
    for (int i = 0; i < m; i++) cin >> apartments[i];

    sort(desired.begin(), desired.end());
    sort(apartments.begin(), apartments.end());

    int cnt = 0;
    int up = 0, down = 0;
    // two-pointer over sorted applicants (up) and apartments (down)
    while (up < n && down < m) {
        // Case 1: apartment fits applicant’s size ±k
        if (desired[up] >= apartments[down] - k && desired[up] <= apartments[down] + k) {
            cnt++;
            up++;
            down++;
        }
        // Case 2: apartment is too large (even after subtracting k)
        // ⇒ this applicant can’t use any larger apartment, move to next applicant
        else if (apartments[down] > desired[up] + k) {
            up++;
        }
        // Case 3: apartment is too small (even after adding k)
        // ⇒ this apartment is too small for any larger applicant, skip to next apartment
        else {
            down++;
        }
    }

    cout << cnt << endl;
    return 0;
}

```
## Key Insight: Why Greedy Works

The greedy approach works because:

1. **Optimal substructure**: If we can optimally match the smallest remaining applicant, the remaining problem is independent
2. **No benefit to waiting**: Matching smaller applicants with smaller apartments never prevents better matches later
3. **Monotonic property**: Both arrays are sorted, so we can make locally optimal decisions

## Step-by-Step Algorithm

### 1. Input and Setup

```cpp
int n, m, k;  // applicants, apartments, tolerance
vector<int> desired(n);     // applicant preferences
vector<int> apartments(m);  // apartment sizes
```

### 2. Sort Both Arrays

```cpp
sort(desired.begin(), desired.end());
sort(apartments.begin(), apartments.end());
```

**Why sort?** Enables the greedy two-pointer approach by ensuring we consider smallest-to-largest matches first.

### 3. Two-Pointer Matching

```cpp
int up = 0, down = 0;  // pointers for applicants and apartments
int cnt = 0;           // successful matches
```

### 4. Three Cases in Main Loop

#### Case 1: Perfect Match ✅

```cpp
if (desired[up] >= apartments[down] - k && 
    desired[up] <= apartments[down] + k)
```

- **Condition**: `apartments[down] - k ≤ desired[up] ≤ apartments[down] + k`
- **Action**: Match them! Increment both pointers and counter
- **Logic**: This is a valid assignment, take it greedily

#### Case 2: Apartment Too Large ⬆️

```cpp
else if (apartments[down] > desired[up] + k)
```

- **Condition**: Even the smallest acceptable size for this apartment is larger than what the applicant wants
- **Action**: Move to next applicant (`up++`)
- **Logic**: This applicant can't use this or any larger apartment

#### Case 3: Apartment Too Small ⬇️

```cpp
else  // apartments[down] < desired[up] - k
```

- **Condition**: Even the largest acceptable size for this apartment is smaller than what the applicant wants
- **Action**: Move to next apartment (`down++`)
- **Logic**: This apartment is too small for this and all larger applicants

## Example Walkthrough

**Input**: n=4, m=3, k=5  
**Applicants**: [60, 45, 80, 60] → sorted: [45, 60, 60, 80]  
**Apartments**: [30, 60, 75] → sorted: [30, 60, 75]

|Step|up|down|desired[up]|apartments[down]|Range [down-k, down+k]|Action|
|---|---|---|---|---|---|---|
|1|0|0|45|30|[25, 35]|45 > 35, apartment too small, down++|
|2|0|1|45|60|[55, 65]|45 < 55, apartment too large, up++|
|3|1|1|60|60|[55, 65]|55 ≤ 60 ≤ 65, **MATCH!** cnt=1, both++|
|4|2|2|60|75|[70, 80]|60 < 70, apartment too large, up++|
|5|3|2|80|75|[70, 80]|70 ≤ 80 ≤ 80, **MATCH!** cnt=2, both++|

**Result**: 2 matches

## Why This Works (Correctness Proof Sketch)

1. **Greedy Choice Property**: When we find a match, taking it immediately is always optimal
    
    - If we skip this match, the current applicant might not get any apartment
    - The current apartment might not match any future applicant as well
2. **Optimal Substructure**: After making a greedy choice, the remaining problem has the same structure
    
3. **No Regrets**: Since arrays are sorted:
    
    - If apartment is too small for current applicant, it's too small for all remaining applicants
    - If apartment is too large for current applicant, current applicant can't use any larger apartments

## Common Mistakes to Avoid

1. **Forgetting to sort**: The two-pointer technique only works on sorted arrays
2. **Wrong boundary conditions**: Make sure the acceptance condition uses `>=` and `<=` correctly
3. **Incrementing wrong pointer**:
    - Too large apartment → move applicant pointer
    - Too small apartment → move apartment pointer
4. **Off-by-one errors**: Ensure loop continues while both pointers are valid

## Time Complexity Analysis

- **Sorting**: O(n log n + m log m)
- **Two-pointer traversal**: O(n + m) - each element visited at most once
- **Overall**: O(n log n + m log m)

## Space Complexity

- **Input storage**: O(n + m)
- **Additional space**: O(1)
- **Overall**: O(n + m)

## Related Problems

- Assignment problems with constraints
- Matching problems in bipartite graphs
- Two-pointer techniques on sorted arrays
- Greedy algorithms for optimization