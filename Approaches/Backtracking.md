#recursion
# A Comprehensive Guide to Backtracking in C++

Backtracking is a general algorithmic technique that incrementally builds candidates for a solution and abandons a candidate ("backtracks") as soon as it determines that this candidate cannot lead to a valid solution. It’s especially useful for solving constraint satisfaction problems such as puzzles, combinations, permutations, and many others.

---

## Table of Contents

1. [Introduction to Backtracking](https://chatgpt.com/c/67b96660-8f58-8007-8c1a-be08a7af9781#introduction-to-backtracking)
2. [How Backtracking Works](https://chatgpt.com/c/67b96660-8f58-8007-8c1a-be08a7af9781#how-backtracking-works)
3. [Classical Backtracking Template](https://chatgpt.com/c/67b96660-8f58-8007-8c1a-be08a7af9781#classical-backtracking-template)
4. [Key Steps in a Backtracking Solution](https://chatgpt.com/c/67b96660-8f58-8007-8c1a-be08a7af9781#key-steps-in-a-backtracking-solution)
5. [Example 1: Word Search Problem](https://chatgpt.com/c/67b96660-8f58-8007-8c1a-be08a7af9781#example-1-word-search-problem)
6. [Example 2: Permutations](https://chatgpt.com/c/67b96660-8f58-8007-8c1a-be08a7af9781#example-2-permutations)
7. [Best Practices and Tips](https://chatgpt.com/c/67b96660-8f58-8007-8c1a-be08a7af9781#best-practices-and-tips)
8. [Conclusion](https://chatgpt.com/c/67b96660-8f58-8007-8c1a-be08a7af9781#conclusion)

---

## Introduction to Backtracking

Backtracking is a brute-force search technique that is refined by eliminating choices that lead to invalid solutions early. Instead of trying every possible candidate solution, backtracking incrementally builds a solution and removes ("backtracks") elements as soon as it determines that the current path cannot possibly lead to a valid solution.

This method is used in problems such as:

- Solving puzzles (e.g., Sudoku, crosswords)
- Generating permutations and combinations
- The N-Queens problem
- Pathfinding problems like the Word Search

---

## How Backtracking Works

The key idea in backtracking is to build a solution step by step and explore the potential of the current partial solution:

- **Choose:** Pick an option for the next step.
- **Explore:** Recursively explore further choices from that state.
- **Unchoose (Backtrack):** Remove the last choice and try a different option if the current path does not lead to a solution.

This depth-first search approach ensures that the algorithm does not miss any possible solutions while cutting off paths early that cannot possibly succeed.

---

## Classical Backtracking Template

A generic template for backtracking problems in C++ is as follows:

```cpp
void backtrack(/* parameters representing the state */) {
    // 1. Base Case: Check if the current state is a complete solution.
    if (isSolution(/* current state */)) {
        // Process or record the solution.
        return;
    }
    
    // 2. Iterate over all possible choices.
    for (each possible choice) {
        // 3. Check if this choice is valid.
        if (isValid(choice, /* current state */)) {
            // 4. Make the move: update the state.
            makeMove(choice, /* current state */);
            
            // 5. Recursively call backtrack with the updated state.
            backtrack(updated state);
            
            // 6. Undo the move (backtrack) to restore the previous state.
            undoMove(choice, /* current state */);
        }
    }
}
```

### Explanation of Each Step:

1. **Base Case:**  
    Determine if the current state satisfies the conditions for a complete solution. If it does, record or output the solution and terminate this recursive branch.
    
2. **Iteration Over Choices:**  
    At each step, iterate through all the possible options available for the next decision.
    
3. **Validity Check:**  
    Before committing to a choice, check if it leads to a valid state (i.e., it does not violate any constraints).
    
4. **Make the Move:**  
    Update the state to reflect that the choice has been made.
    
5. **Recursive Call:**  
    Call the backtracking function recursively to continue building the solution.
    
6. **Undo the Move (Backtrack):**  
    If the current branch fails to yield a solution, revert the state to its previous state to try a new option.
    

---

## Key Steps in a Backtracking Solution

When designing a backtracking solution, consider the following steps:

1. **Define the Problem State:**  
    Determine what constitutes a state in your problem. For instance, in a permutation problem, the state might be the current sequence of numbers; in a word search, it might be the current position and path taken on the board.
    
2. **Identify the Base Case:**  
    Decide when a valid solution is reached. This could be when all positions are filled in a puzzle or when the current partial solution meets the required conditions.
    
3. **Determine Possible Moves:**  
    Identify all the potential moves or choices available from the current state.
    
4. **Make a Choice and Update the State:**  
    Modify the current state based on the choice. This often involves marking an element as used or updating a data structure.
    
5. **Recursive Exploration:**  
    Recursively attempt to build the complete solution using the updated state.
    
6. **Backtrack:**  
    Undo the move if the recursive call does not lead to a solution. This step ensures that all possibilities are explored without interference from previous states.
    

---

## Example 1: Word Search Problem

Consider the following problem: Given a board of characters and a word, determine if the word exists in the board by traversing adjacent cells (horizontally or vertically). Here’s how backtracking is applied.

### Code Walkthrough

```cpp
class Solution {
public:
    int l, m, n;
    vector<vector<int>> directions{{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
    
    bool find(vector<vector<char>>& board, int i, int j, string &word, int idx) {
        // Base Case: All characters matched.
        if (idx >= l)
            return true;
        
        // Validity check: Ensure current position is in bounds and matches the character.
        if (i < 0 || i >= m || j < 0 || j >= n || board[i][j] != word[idx])
            return false;
        
        // Make a move: Mark the current cell to avoid reuse.
        char temp = board[i][j];
        board[i][j] = '$';
        
        // Explore: Check all four possible directions.
        for (auto& dir : directions) {
            int i_ = i + dir[0];
            int j_ = j + dir[1];
            if (find(board, i_, j_, word, idx + 1))
                return true;
        }
        
        // Backtrack: Restore the original value.
        board[i][j] = temp;
        return false;
    }
    
    bool exist(vector<vector<char>>& board, string word) {
        m = board.size();
        n = board[0].size();
        l = word.length();
        if (m * n < l)
            return false;
        
        // Try every cell as a potential starting point.
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == word[0] && find(board, i, j, word, 0)) {
                    return true;
                }
            }
        }
        return false;
    }
};
```

### Mapping to the Template:

- **Base Case:**  
    `if (idx >= l) return true;`  
    (The word has been completely found.)
    
- **Iteration Over Choices:**  
    The loop over `directions` iterates through all possible moves (right, left, down, up).
    
- **Validity Check:**  
    The condition  
    `if (i < 0 || i >= m || j < 0 || j >= n || board[i][j] != word[idx]) return false;`  
    ensures the move is valid.
    
- **Make the Move:**  
    The cell is marked with `'$'` to indicate it has been used.
    
- **Recursive Call:**  
    `if (find(board, i_, j_, word, idx + 1)) return true;`  
    continues the search.
    
- **Backtracking:**  
    Restoring the cell value with `board[i][j] = temp;` allows the algorithm to try other paths.
    

---

## Example 2: Generating Permutations

Another common backtracking problem is generating all permutations of a list of numbers.

### Code Example

```cpp
void permuteHelper(vector<int>& nums, int start, vector<vector<int>>& result) {
    // Base case: If we've reached the end, record the permutation.
    if (start == nums.size()) {
        result.push_back(nums);
        return;
    }
    
    // Iterate over all possible choices.
    for (int i = start; i < nums.size(); i++) {
        // Swap (make a move).
        swap(nums[start], nums[i]);
        
        // Recursive call: Generate all permutations from the next index.
        permuteHelper(nums, start + 1, result);
        
        // Backtrack: Undo the swap.
        swap(nums[start], nums[i]);
    }
}

vector<vector<int>> permute(vector<int>& nums) {
    vector<vector<int>> result;
    permuteHelper(nums, 0, result);
    return result;
}
```

### Explanation:

- **Base Case:**  
    When `start` equals the size of the list, a complete permutation is formed.
    
- **Iteration Over Choices:**  
    The loop iterates over possible numbers that can be swapped into the `start` position.
    
- **Make the Move:**  
    A swap is made to put a candidate number in the current position.
    
- **Recursive Call:**  
    The function calls itself with the next index to build the permutation.
    
- **Backtracking:**  
    The swap is undone to restore the original order before trying the next candidate.
    

---

## Best Practices and Tips

- **Prune Early:**  
    Always check for invalid states early to avoid unnecessary recursive calls.
    
- **Immutable vs. Mutable State:**  
    Use in-place modifications (with proper backtracking) when possible to save memory, but be careful with shared mutable state.
    
- **Clarity in Base Cases:**  
    Ensure your base case clearly represents a complete solution to prevent infinite recursion.
    
- **Debugging:**  
    Add logging or use a debugger to step through recursive calls when backtracking solutions are complex.
    
- **Template Usage:**  
    Customize the classical template to fit the problem at hand; not every problem requires all six steps explicitly if some steps are implicit in the problem's constraints.
    

---

Below is an explanation of the N-Queens problem along with its backtracking solution and how it fits into the backtracking template.

---

## The N-Queens Problem

**Problem Statement:**  
Place N queens on an N×N chessboard such that no two queens threaten each other. This means that no two queens can share the same row, column, or diagonal.

---
## Backtracking Approach for N-Queens

Backtracking is a natural fit for the N-Queens problem since you can try to place a queen in a valid position, then recursively attempt to place the next queen. If a conflict is found later, the algorithm backtracks to the previous queen and moves it to the next possible valid position.

---

## Step-by-Step Explanation Using the Backtracking Template

### 1. Define the Problem State

- **State Representation:**  
    Typically, we use a one-dimensional vector `queenPositions` where the index represents the row, and the value at that index represents the column position of the queen in that row.

### 2. Base Case

- **Base Case Check:**  
    When the number of queens placed equals N (i.e., we have filled all rows), a valid solution has been found.

### 3. Iterating Over Possible Moves

- **Choices:**  
    For each row, try placing a queen in each column one by one.

### 4. Validity Check

- **Constraints:**  
    For a queen placed at `(row, col)`, it must not share the same column or diagonal with any previously placed queen. The diagonal conflicts can be checked by ensuring that:
    - For any queen already placed at `(i, queenPositions[i])`, the current queen at `(row, col)` must satisfy:
        - `queenPositions[i] != col` (no same column)
        - `abs(queenPositions[i] - col) != abs(i - row)` (no same diagonal)

### 5. Make a Move and Update the State

- **Place the Queen:**  
    If a position `(row, col)` is valid, place the queen by recording it in `queenPositions[row] = col`.

### 6. Recursive Call

- **Recursive Exploration:**  
    Recursively attempt to place a queen in the next row.

### 7. Undo the Move (Backtrack)

- **Backtracking:**  
    If no valid placement is found in subsequent rows, remove the queen from `(row, col)` and try the next column.

---

## Sample Code in C++

Below is a sample C++ implementation that uses backtracking to solve the N-Queens problem:

```cpp
#include <iostream>
#include <vector>
#include <cmath>
using namespace std;

class NQueens {
public:
    vector<vector<string>> solveNQueens(int n) {
        vector<vector<string>> solutions;
        vector<int> queenPositions(n, -1);  // queenPositions[i] = column index for queen in row i
        backtrack(0, n, queenPositions, solutions);
        return solutions;
    }
    
private:
    void backtrack(int row, int n, vector<int>& queenPositions, vector<vector<string>>& solutions) {
        // Base Case: All queens are placed.
        if (row == n) {
            solutions.push_back(generateBoard(queenPositions, n));
            return;
        }
        
        // Iterate over all columns in the current row.
        for (int col = 0; col < n; col++) {
            if (isValid(row, col, queenPositions)) {
                // Make the move: Place the queen.
                queenPositions[row] = col;
                // Recursive call: Place queen in next row.
                backtrack(row + 1, n, queenPositions, solutions);
                // Undo the move: Remove the queen.
                queenPositions[row] = -1;
            }
        }
    }
    
    bool isValid(int row, int col, const vector<int>& queenPositions) {
        // Check previously placed queens for conflicts.
        for (int i = 0; i < row; i++) {
            // Check same column and diagonal conflicts.
            if (queenPositions[i] == col || abs(queenPositions[i] - col) == abs(i - row))
                return false;
        }
        return true;
    }
    
    vector<string> generateBoard(const vector<int>& queenPositions, int n) {
        vector<string> board;
        for (int i = 0; i < n; i++) {
            string row(n, '.');
            row[queenPositions[i]] = 'Q';
            board.push_back(row);
        }
        return board;
    }
};

int main() {
    int n = 4;
    NQueens solver;
    vector<vector<string>> solutions = solver.solveNQueens(n);
    
    cout << "Total solutions: " << solutions.size() << "\n";
    for (const auto& board : solutions) {
        for (const auto& row : board) {
            cout << row << "\n";
        }
        cout << "\n";
    }
    return 0;
}
```

### Explanation of the Code:

- **State Representation:**  
    `queenPositions` stores the column positions for queens in each row.
    
- **Base Case:**  
    When `row == n`, a complete board is constructed, and we generate the board layout with `generateBoard`.
    
- **Iterating Over Choices:**  
    The loop in the `backtrack` function goes through each column in the current row.
    
- **Validity Check:**  
    The `isValid` function checks if placing a queen at `(row, col)` would conflict with any queens placed in previous rows.
    
- **Making a Move and Recursive Call:**  
    If a valid column is found, the queen is placed, and `backtrack` is called for the next row.
    
- **Backtracking:**  
    After exploring a branch, the queen is removed (reset to `-1`) to try the next column.
    

---

## Conclusion

The N-Queens problem is an excellent example of how backtracking can systematically explore all possible configurations for placing queens on a chessboard. By applying the classical backtracking template:

- **Define the state** (positions of queens),
- **Check for base conditions** (all queens placed),
- **Iterate over all choices** (each column in the current row),
- **Validate each move** (ensuring no conflicts), and
- **Backtrack** when a dead end is reached,

you can efficiently solve the problem and generate all possible solutions. This approach not only applies to N-Queens but also provides a strong foundation for tackling other combinatorial and constraint satisfaction problems.