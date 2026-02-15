Here is the C++ code for both approaches.

### 1. Iterative Simulation (Forward DP) - **Recommended**

This approach directly simulates the "pouring" process. It is generally preferred in C++ because it avoids recursion depth issues and is easier to optimize for space.

C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm> // for min

using namespace std;

class Solution {
public:
    double champagneTower(int poured, int query_row, int query_glass) {
        // Create a 2D table. 102 is used to handle the spill 
        // from the last row (99) to the next (100) safely without bounds checking.
        double tower[102][102] = {0.0};
        
        // Pour everything into the top glass
        tower[0][0] = (double)poured;
        
        // Simulate row by row
        for (int r = 0; r <= query_row; ++r) {
            for (int c = 0; c <= r; ++c) {
                // Calculate excess liquid in the current glass
                double excess = (tower[r][c] - 1.0) / 2.0;
                
                // If there is overflow, distribute it to the two glasses below
                if (excess > 0) {
                    tower[r+1][c] += excess;
                    tower[r+1][c+1] += excess;
                }
            }
        }
        
        // Return the amount in the target glass, capped at 1.0
        return min(1.0, tower[query_row][query_glass]);
    }
};
```

**Complexity Analysis:**

- **Time:** $O(R^2)$ — We process every glass up to the target row.
    
- **Space:** $O(R^2)$ — For the 2D array (though since $R \le 100$, this is very small).
    

---

### 2. Recursive with Memoization (Backward DP)

This approaches the problem by asking: "How much came from my parents?" This strictly follows the "Pull" logic from the notes.

C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

class Solution {
    // Memoization table initialized to -1.0 to indicate "unvisited"
    double memo[102][102];

public:
    double champagneTower(int poured, int query_row, int query_glass) {
        // Initialize memo table with -1.0
        for(int i=0; i<102; ++i) {
            for(int j=0; j<102; ++j) {
                memo[i][j] = -1.0;
            }
        }
        
        // Get the total amount poured INTO the target glass
        double total_flow = solve(poured, query_row, query_glass);
        
        // The glass can only hold 1, even if 50 flowed through it
        return min(1.0, total_flow);
    }

    double solve(int poured, int r, int c) {
        // Base Case: Top of the tower
        if (r == 0 && c == 0) {
            return (double)poured;
        }
        
        // Bounds Check: If coordinates are invalid, no liquid comes from there
        if (c < 0 || c > r) {
            return 0.0;
        }

        // Return cached result if it exists
        if (memo[r][c] != -1.0) {
            return memo[r][c];
        }

        // Recursive Step: Ask parents (Top-Left and Top-Right)
        // Parent 1: (r-1, c-1)
        double left_parent = solve(poured, r - 1, c - 1);
        // Parent 2: (r-1, c)
        double right_parent = solve(poured, r - 1, c);

        // Calculate spill from parents
        // Spill = (Parent_Amount - 1) / 2. If parent had < 1, spill is 0.
        double spill_from_left = max(0.0, (left_parent - 1.0) / 2.0);
        double spill_from_right = max(0.0, (right_parent - 1.0) / 2.0);

        // Store and return total
        return memo[r][c] = spill_from_left + spill_from_right;
    }
};
```

**Complexity Analysis:**

- **Time:** $O(R^2)$ — Each state `(r, c)` is computed exactly once.
    
- **Space:** $O(R^2)$ — For the recursion stack and memoization table.
    

### Which one should you use?

For an interview, **Code #1 (Iterative)** is safer. It is standard Dynamic Programming, easier to debug, and you don't have to write a helper function or manage a cache manually.


₹₹