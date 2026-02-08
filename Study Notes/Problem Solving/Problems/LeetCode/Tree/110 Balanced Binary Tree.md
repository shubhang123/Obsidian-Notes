#graph #dfs 
# Balanced Binary Tree (DFS)

## 1. Problem Definition

A binary tree is considered **height-balanced** if, for **every** node in the tree, the absolute difference between the height of its left subtree and the right subtree is at most 1.

Mathematically, for every node $N$:

$$|Height(N_{left}) - Height(N_{right})| \le 1$$

---

## 2. Approach 1: Top-Down DFS (Your Solution)

This is the "Brute Force" or intuitive approach. You calculate the height of the left and right children explicitly for every node, check the balance, and then recurse.

### Code Analysis

```cpp
class Solution {
public:
    bool isBalanced(TreeNode* root) {
        // Base case: An empty tree is balanced
        if (root == nullptr) return true;

        // 1. Calculate height of left and right subtrees
        int lHeight = height(root->left);
        int rHeight = height(root->right);

        // 2. Check if current node is unbalanced
        if (abs(lHeight - rHeight) > 1) return false;

        // 3. Recurse: Ensure BOTH left and right subtrees are also balanced
        return isBalanced(root->left) && isBalanced(root->right);
    }

    // Helper function to find height
    int height(TreeNode* node) {
        if (!node) return 0;
        return max(height(node->left), height(node->right)) + 1;
    }
};
```

### Critical Review (Complexity Analysis)

While this solution is correct, it is inefficient.

- **Time Complexity:** $O(N^2)$.
    
    - For every node, we call `height()`, which traverses all its children.
        
    - This results in redundant calculations (visiting nodes multiple times).
        
- **Space Complexity:** $O(N)$ due to recursion stack stack (in the worst case of a skewed tree).
    

---

## 3. Approach 2: Bottom-Up DFS (Optimized)

Instead of calling `height()` separately, we can check the balance **while** calculating the height. If a subtree is found to be unbalanced deep in the recursion, we can immediately return a specific error code (like `-1`) all the way up, avoiding further calculations.

### Logic

1. Use a DFS helper function that returns the actual height of the tree.
    
2. If a subtree is unbalanced, return `-1` (acting as a "false" flag).
    
3. If we receive `-1` from a child, we immediately return `-1` to the parent.
    
4. If the absolute difference between left and right height is $> 1$, return `-1`.
    
5. Otherwise, return the actual height: $\max(left, right) + 1$.
    

### Optimized Code ($O(N)$)

```cpp
class Solution {
public:
    bool isBalanced(TreeNode* root) {
        // If dfs returns -1, the tree is unbalanced
        return dfsHeight(root) != -1;
    }

    int dfsHeight(TreeNode* root) {
        if (root == nullptr) return 0;

        // Check left subtree
        int leftHeight = dfsHeight(root->left);
        if (leftHeight == -1) return -1; // Propagate failure immediately

        // Check right subtree
        int rightHeight = dfsHeight(root->right);
        if (rightHeight == -1) return -1; // Propagate failure immediately

        // Check current node balance
        if (abs(leftHeight - rightHeight) > 1) {
            return -1; // Current node is unbalanced
        }

        // Return actual height to parent
        return max(leftHeight, rightHeight) + 1;
    }
};
```

---

## Summary Comparison

|**Feature**|**Top-Down (Your Approach)**|**Bottom-Up (Optimized)**|
|---|---|---|
|**Traversal**|Pre-order (Check node, then children)|Post-order (Check children, then node)|
|**Redundancy**|High (Recalculates height repeatedly)|None (Calculates height once)|
|**Time Complexity**|$O(N^2)$ (Worst case)|$O(N)$ (Every node visited once)|
|**Best Use**|Simple to understand, small trees|Interview standard, large trees|

> **Key Takeaway:** In tree problems, if you find yourself calculating the same attribute (like height) repeatedly for the same nodes, try to move the logic into the return value of a **Post-Order Traversal**.

---

**Would you like me to generate a similar comparison for calculating the "Diameter of a Binary Tree," which shares this exact optimization pattern?**