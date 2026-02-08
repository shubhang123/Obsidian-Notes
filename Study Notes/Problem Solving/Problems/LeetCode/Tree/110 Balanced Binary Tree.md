#graph #dfs 

a balanced binary tree is a tree where the left subtree and the right subtree have height difference of only 1 or 0

## approach:

1) just use dfs on left and right subtree and keep the track of height of each and then check at the last, but also have to check each of the height of the nodes , as they can be unbalanced as well.

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left),
 * right(right) {}
 * };
 */
class Solution {
public:
    bool isBalanced(TreeNode* root) {
        if (root == nullptr) {
            return true;
        }

        int lHeight = height(root->left);
        int rHeight = height(root->right);

        if (abs(lHeight - rHeight) > 1) {
            return false;
        }

        return isBalanced(root->left) && isBalanced(root->right);
    }

    int height(TreeNode* head) {
        if (!head) {
            return 0;
        }

        int leftHeight = height(head->left);
        int rightHeight = height(head->right);

        return max(leftHeight, rightHeight) + 1;
    }
};
```

### explaination:

here the height is calculated for each of the nodes and checked if the nodes mod value is either 1 or 0, cause those are the cases where the tree is balanced. If it doesnt match the condition then we immediately 