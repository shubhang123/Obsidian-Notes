## Word Search Problem - Notes & Explanation
#dfs #graph #backtracking
### Problem Overview

This is the classic "Word Search" problem where you need to find if a given word exists in a 2D board of characters. The word can be formed by connecting adjacent cells (horizontally or vertically), but each cell can only be used once per word.

### Algorithm Approach: Backtracking with DFS

**Key Concepts:**

1. **Depth-First Search (DFS)**: Explores each possible path deeply before backtracking
2. **Backtracking**: Undoes choices when they don't lead to a solution
3. **Visited Marking**: Temporarily marks cells to avoid reusing them in the same path

```cpp
class Solution {
   public:
    int m, n;

    bool dfs(vector<vector<char>>& board, int i, int j, int idx, string word) {
        if (i < 0 || j < 0 || j >= n || i >= m)
            return false;
        
        // if the letter is not in word return false
        if (board[i][j] != word[idx])
            return false;

        // if the index exceeds the length of word exit
        if (idx == word.length() - 1)
            return true;

        // storing the character in order to
        // backtrack by again placing this value
        char temp = board[i][j];

        // changes the previous element to *
        // so that it doesnt interfere with the dfs
        // varna same letter ko use karke word ban skta haiu
        // which is already taken in our word in our dfs
        // aka visited letter can be used again
        board[i][j] = '*';

        bool wordExist = false;
        // down
        if (i + 1 < m && board[i + 1][j] == word[idx + 1]) {
            wordExist |= dfs(board, i + 1, j, idx + 1, word);
        }
        // up
        if (i - 1 >= 0 && board[i - 1][j] == word[idx + 1]) {
            wordExist |= dfs(board, i - 1, j, idx + 1, word);
        }
        // right
        if (j + 1 < n && board[i][j + 1] == word[idx + 1]) {
            wordExist |= dfs(board, i, j + 1, idx + 1, word);
        }
        // left
        if (j - 1 >= 0 && board[i][j - 1] == word[idx + 1]) {
            wordExist |= dfs(board, i, j - 1, idx + 1, word);
        }

        // backtracking step, keep replacing the word with *
        // for other iterations
        board[i][j] = temp;
        return wordExist;
    }

    bool exist(vector<vector<char>>& board, string word) {
        m = board.size();
        n = board[0].size();

        bool isWord = false;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == word[0])
                    isWord |= dfs(board, i, j, 0, word);
            }
        }
        return isWord;
    }
};
```

### Step-by-Step Breakdown

#### Main Function (`exist`)

```cpp
// 1. Initialize board dimensions
// 2. Try starting DFS from every cell that matches word[0]
// 3. Return true if any starting position leads to complete word
```

#### DFS Function Logic

```cpp
// Base cases:
// - Out of bounds → return false
// - Character mismatch → return false  
// - Reached end of word → return true (success!)

// Recursive case:
// 1. Mark current cell as visited (board[i][j] = '*')
// 2. Explore all 4 directions
// 3. Restore original character (backtrack)
// 4. Return if word was found in any direction
```

### Backtracking Explanation

**What is Backtracking?** Backtracking is a problem-solving technique that incrementally builds solutions and abandons partial solutions ("backtracks") when they cannot lead to a valid complete solution.

**In this problem:**

1. **Make a Choice**: Move to an adjacent cell and mark it as visited
    
    ```cpp
    char temp = board[i][j];  // Save original
    board[i][j] = '*';        // Mark as visited
    ```
    
2. **Explore Consequences**: Recursively try to complete the word from this position
    
3. **Backtrack**: If the current path doesn't work, undo the choice
    
    ```cpp
    board[i][j] = temp;  // Restore original character
    ```
    

**Why Backtracking is Needed:**

- Prevents using the same cell twice in one word path
- Allows the same cell to be used in different word attempts
- Ensures we explore all possible valid paths

### Code Improvements & Observations

**Current Issues:**

1. **Redundant Boundary Checks**: The direction checks repeat boundary validation
2. **Inefficient**: Checks character match before making recursive call

**Optimized Version:**

```cpp
bool dfs(vector<vector<char>>& board, int i, int j, int idx, string& word) {
    // Base cases
    if (idx == word.length()) return true;
    if (i < 0 || i >= m || j < 0 || j >= n || board[i][j] != word[idx])
        return false;
    
    // Mark as visited
    char temp = board[i][j];
    board[i][j] = '*';
    
    // Explore all 4 directions
    bool found = dfs(board, i+1, j, idx+1, word) ||
                 dfs(board, i-1, j, idx+1, word) ||
                 dfs(board, i, j+1, idx+1, word) ||
                 dfs(board, i, j-1, idx+1, word);
    
    // Backtrack
    board[i][j] = temp;
    return found;
}
```

### Time & Space Complexity

**Time Complexity**: O(m × n × 4^L)

- m × n: Try each cell as starting point
- 4^L: In worst case, explore 4 directions for each of L characters

**Space Complexity**: O(L)

- L: Maximum recursion depth equals word length

### Key Takeaways

1. **Backtracking Pattern**: Try → Explore → Undo
2. **State Management**: Carefully manage what represents "visited"
3. **Base Cases**: Handle success, failure, and boundary conditions
4. **Optimization**: Early termination and efficient boundary checking

The beauty of backtracking is that it systematically explores all possibilities while ensuring we don't get stuck in invalid states!