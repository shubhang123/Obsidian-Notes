

## 📄 script.py

```py
import os

repo_dir = os.path.join(os.getcwd(), ".")
output_file = "leetcode_problems_solutions.md"

with open(output_file, "w", encoding="utf-8") as out:
    for root, dirs, files in os.walk(repo_dir):
        for file in files:
            if file.endswith(".py") or file.endswith(".java"):
                full_path = os.path.join(root, file)
                relative_path = os.path.relpath(full_path, repo_dir)

                out.write(f"\n\n## 📄 {relative_path}\n\n```{file.split('.')[-1]}\n")
                with open(full_path, "r", encoding="utf-8", errors="ignore") as f:
                    out.write(f.read())
                out.write("\n```\n")
print(f"✅ Markdown file created: {output_file}")

```


## 📄 [A]tree\[A]tree-bfs\102-binary-tree-level-order-traversal.java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        ArrayDeque<TreeNode> queue = new ArrayDeque<>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            ArrayList<Integer> cur = new ArrayList<>();
            int levelCount = queue.size();
            for (int i = 0; i < levelCount; i++) {
                TreeNode node = queue.poll();
                cur.add(node.val);
                for (TreeNode child: new TreeNode[]{node.left, node.right}) {
                    if (child != null) {
                        queue.offer(child);
                    }
                }
            }
            res.add(cur);
        }
        return res;
    }
}

// time O(n), due to traversal
// space O(n), queue can have a size of n/2 or the list's size to store nodes
// using tree and bfs
```


## 📄 [A]tree\[A]tree-bfs\102-binary-tree-level-order-traversal.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        res = []
        if not root:
            return root
        queue = deque([root])
        while queue:
            level_count = len(queue)
            cur_level = []
            for _ in range(level_count):
                node = queue.popleft()
                cur_level.append(node.val)
                for child in [node.left, node.right]:
                    if child:
                        queue.append(child)
            res.append(cur_level)
        return res
    
# time O(n), due to traversal
# space O(n), queue can have a size of n/2 or the list's size to store nodes
# using tree and bfs
```


## 📄 [A]tree\[A]tree-bfs\103-binary-tree-zigzag-level-order-traversal.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def zigzagLevelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        res = []
        if not root:
            return res
        queue = deque([root])
        while queue:
            level_count = len(queue)
            cur_level = []
            for _ in range(level_count):
                node = queue.popleft()
                cur_level.append(node.val)
                for child in [node.left, node.right]:
                    if child:
                        queue.append(child)
            if len(res) % 2 == 0:
                res.append(cur_level)
            else:
                res.append(cur_level[:: - 1])
        return res
    
# time O(n), due to traverse
# space O(n), due to queue's size (tree diameter or last level)
# using tree and bfs
```


## 📄 [A]tree\[A]tree-bfs\104-maximum-depth-of-binary-tree.java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {

    record Pair(TreeNode node, int level) { };

    public int maxDepth(TreeNode root) {
        int res = 0;
        if (root == null) {
            return 0;
        }
        ArrayDeque<Pair> queue = new ArrayDeque<>();
        queue.offer(new Pair(root, 1));
        while (!queue.isEmpty()) {
            Pair pair = queue.poll();
            TreeNode node = pair.node;
            int level = pair.level;
            res = Math.max(res, level);
            for (TreeNode child: new TreeNode[]{node.left, node.right}) {
                if (child != null) {
                    queue.offer(new Pair(child, level + 1));
                }
            }
        }
        return res;
    }
}

// time O(n), due to bfs
// space O(n), due to queue's size, it can be n/2 in a balanced tree's deepest level
// using tree and bfs
```


## 📄 [A]tree\[A]tree-bfs\104-maximum-depth-of-binary-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        queue = deque([(root, 1)])
        while queue:
            node, level = queue.popleft()
            for child in [node.left, node.right]:
                if child:
                    queue.append((child, level + 1))
        return level
    
# time O(n), due to bfs
# space O(n), due to queue's size, it can be n/2 in a balanced tree's deepest level
# using tree and bfs
```


## 📄 [A]tree\[A]tree-bfs\199-binary-tree-right-side-view.java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        
        ArrayDeque<TreeNode> queue = new ArrayDeque<>();

        if (root != null) {
            queue.offer(root);
        }

        while (!queue.isEmpty()) {
            int levelCount = queue.size();
            for (int i = 0; i < levelCount; i++) {
                TreeNode node = queue.poll();
                if (i == levelCount - 1) {
                    res.add(node.val);
                }
                for (TreeNode child: new TreeNode[]{node.left, node.right}) {
                    if (child != null) {
                        queue.offer(child);
                    }
                }
            }
        }
        return res;
    }
}

// time O(n), due to traverse
// space O(n)
// using tree and bfs
```


## 📄 [A]tree\[A]tree-bfs\199-binary-tree-right-side-view.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        res = []
        if not root:
            return res
        queue = deque([root])
        while queue:
            level_count = len(queue)
            for i in range(level_count):
                node = queue.popleft()
                if i == level_count - 1:
                    res.append(node.val)
                for child in [node.left, node.right]:
                    if child:
                        queue.append(child)
        return res
    
# time O(n), due to traverse
# space O(n)
# using tree and bfs
```


## 📄 [A]tree\[A]tree-bfs\2385-amount-of-time-for-binary-tree-to-be-infected.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def amountOfTime(self, root: Optional[TreeNode], start: int) -> int:
        start_node = None
        node_parent = {root: None}
        queue = deque([root])
        while queue:
            node = queue.popleft()
            if node.val == start:
                start_node = node
            for child in [node.left, node.right]:
                if child:
                    queue.append(child)
                    node_parent[child] = node
        
        queue = deque([(start_node, 0)])
        visited = {start_node.val}
        while queue:
            node, distance = queue.popleft()
            for next_node in [node.left, node.right, node_parent[node]]:
                if next_node and next_node.val not in visited:
                    queue.append((next_node, distance + 1))
                    visited.add(next_node.val)
        return distance

# time O(n)
# space O(n)
# using tree and bfs and build child_parent hashmap
```


## 📄 [A]tree\[A]tree-bfs\2415-reverse-odd-levels-of-binary-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def reverseOddLevels(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        queue = deque([root])
        level = 1
        while queue:
            level_count = len(queue)
            cur_level = []
            for _ in range(level_count):
                node = queue.popleft()
                if level % 2 == 0:
                    cur_level.append(node)
                for child in [node.left, node.right]:
                    if child:
                        queue.append(child)

            left, right = 0, len(cur_level) - 1
            while left < right:
                cur_level[left].val, cur_level[right].val = cur_level[right].val, cur_level[left].val
                left += 1
                right -= 1
                
            level += 1

        return root
    
# time O(n)
# space O(n)
# using tree and bfs and two pointers
```


## 📄 [A]tree\[A]tree-bfs\314-binary-tree-vertical-order-traversal.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque, defaultdict
class Solution:
    def verticalOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []
        queue = deque([(root, 0)])
        col_vals = defaultdict(list)
        min_col = float('inf')
        max_col = float('-inf')
        while queue:
            node, col = queue.popleft()
            col_vals[col].append(node.val)
            min_col = min(min_col, col)
            max_col = max(max_col, col)
            if node.left:
                queue.append((node.left, col - 1))
            if node.right:
                queue.append((node.right, col + 1))
        
        res = []
        for col in range(min_col, max_col + 1):
            res.append(col_vals[col][:])
        return res

# time O(n), due to traverse
# space O(n), due to hashmap
# using tree and bfs and hashmap and assign coordinates
```


## 📄 [A]tree\[A]tree-bfs\623-add-one-row-to-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def addOneRow(self, root: Optional[TreeNode], val: int, depth: int) -> Optional[TreeNode]:
        if not root:
            return root
            
        if depth == 1:
            return TreeNode(val=val, left=root)

        queue = deque([(root, 1)])
        while queue:
            level_count = len(queue)
            for _ in range(level_count):
                node, level = queue.popleft()
                if level == depth - 1:
                    node.left = TreeNode(val=val, left=node.left)
                    node.right = TreeNode(val=val, right=node.right)
                else:
                    for child in [node.left, node.right]:
                        if child:
                            queue.append((child, level + 1))
        return root
    
# time O(n)
# space O(n)
# using tree and bfs
```


## 📄 [A]tree\[A]tree-bfs\662-maximum-width-of-binary-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def widthOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        res = 0
        queue = deque([(root, 1)])
        while queue:
            level_count = len(queue)
            cur_level = []
            for _ in range(level_count):
                node, idx = queue.popleft()
                cur_level.append(idx)
                if node.left:
                    queue.append((node.left, idx * 2))
                if node.right:
                    queue.append((node.right, idx * 2 + 1))
            res = max(res, cur_level[- 1] - cur_level[0] + 1)
        return res
                        
# time O(n)
# space O(n), due to queue
# using tree and bfs and assign idx
```


## 📄 [A]tree\[A]tree-bfs\690-employee-importance.py

```py
"""
# Definition for Employee.
class Employee:
    def __init__(self, id: int, importance: int, subordinates: List[int]):
        self.id = id
        self.importance = importance
        self.subordinates = subordinates
"""
from collections import deque
class Solution:
    def getImportance(self, employees: List['Employee'], id: int) -> int:
        id_employee = {}
        for e in employees:
            id_employee[e.id] = e

        res = 0
        queue = deque([id_employee[id]])
        while queue:
            node = queue.popleft()
            res += node.importance
            for subordinate in node.subordinates:
                queue.append(id_employee[subordinate])
        return res
        
# time O(n)
# space O(n)
# using tree and bfs and tree's idea and building graph
```


## 📄 [A]tree\[A]tree-bfs\863-all-nodes-distance-k-in-binary-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
from collections import deque
class Solution:
    def distanceK(self, root: TreeNode, target: TreeNode, k: int) -> List[int]:
        node_parent = {root: None}
        queue = deque([root])
        while queue:
            node = queue.popleft()
            for child in [node.left, node.right]:
                if child:
                    queue.append(child)
                    node_parent[child] = node
        
        res = []
        queue = deque([(target, 0)])
        visited = {target.val}
        while queue:
            node, distance = queue.popleft()
            if distance == k:
                res.append(node.val)
            else:
                for next_node in [node.left, node.right, node_parent[node]]:
                    if next_node and next_node.val not in visited:
                        queue.append((next_node, distance + 1))
                        visited.add(next_node.val)
        return res
    
# time O(n)
# space O(n)
# using tree and bfs and build child_parent hashmap
```


## 📄 [A]tree\[A]tree-bfs\987-vertical-order-traversal-of-a-binary-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque, defaultdict
class Solution:
    def verticalTraversal(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []
        queue = deque([(root, 0, 0)])
        min_col, max_col = 0, 0
        col_rowvals = defaultdict(list)
        while queue:
            node, r, c = queue.popleft()
            min_col, max_col = min(min_col, c), max(max_col, c)
            col_rowvals[c].append((r, node.val))
            if node.left:
                queue.append((node.left, r + 1, c - 1))
            if node.right:
                queue.append((node.right, r + 1, c + 1))
        res = []
        for c in range(min_col, max_col + 1):
            res.append([v for r, v in sorted(col_rowvals[c])])
        return res
    
# time O(n + k * (n/k)log(n/k)), k is the number of cols
# space O(n), due to queue's max size (number of leaf nodes)
# using tree and bfs and hashmap and sort and assign coordinates
```


## 📄 [A]tree\[A]tree-dfs-inorder\173-binary-search-tree-iterator.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class BSTIterator:

    def __init__(self, root: Optional[TreeNode]):
        self.stack = []
        self.node = root

    def next(self) -> int:
        while self.stack or self.node:
            if self.node:
                self.stack.append(self.node)
                self.node = self.node.left
            else:
                self.node = self.stack.pop()
                val = self.node.val
                self.node = self.node.right
                return val

    def hasNext(self) -> bool:
        if self.stack or self.node:
            return True
        return False

# Your BSTIterator object will be instantiated and called as such:
# obj = BSTIterator(root)
# param_1 = obj.next()
# param_2 = obj.hasNext()

# time O(1), due to amortized
# space O(h), only store left nodes, so stack's size is tree height
# using tree and dfs (inorder and iterative) and stack to store the left nodes
```


## 📄 [A]tree\[A]tree-dfs-inorder\230-kth-smallest-element-in-a-bst.java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public int kthSmallest(TreeNode root, int k) {
        int[] idxRes = new int[2];
        dfs(root, k, idxRes);
        return idxRes[1];
    }

    public void dfs(TreeNode node, int k, int[] idxRes) {
        if (node == null) {
            return;
        }
        dfs(node.left, k, idxRes);
        idxRes[0] += 1;
        if (idxRes[0] == k) {
            idxRes[1] = node.val;
            return;
        }
        dfs(node.right, k, idxRes);
        return;
    }
}

// time O(n), for skewed tree's height
// space O(n), due to memo stack's size for skewed tree's height 
// using tree and dfs (inorder and recursive)
```


## 📄 [A]tree\[A]tree-dfs-inorder\230-kth-smallest-element-in-a-bst.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        idx = 0
        res = - 1

        def dfs(node):
            nonlocal idx, res
            if not node:
                return
            dfs(node.left)
            idx += 1
            if k == idx:
                res = node.val
                return
            dfs(node.right)

        dfs(root)
        return res
        
# time O(n), for skewed tree's height
# space O(n), due to memo stack's size for skewed tree's height 
# using tree and dfs (inorder and recursive)
```


## 📄 [A]tree\[A]tree-dfs-inorder\94-binary-tree-inorder-traversal.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        inorder = []
        def inorder_helper(root):
            if not root:
                return
            inorder_helper(root.left)
            inorder.append(root.val)
            inorder_helper(root.right)
        inorder_helper(root)
        return inorder
    
# time O(n), due to traverse
# space O(n), due to memory stack
# using tree and dfs (inorder and recursive)

class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        inorder = []
        if not root:
            return inorder
        node = root
        stack = []
        while node or stack:
            if node:
                stack.append(node)
                node = node.left
            else:
                node = stack.pop()
                inorder.append(node.val)
                node = node.right
        return inorder

# time O(n), due to traverse
# space O(n), due to stack
# using tree and dfs (inorder and iterative)

class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
				inorder = []
		    if not root:
		        return inorder
		    stack = [(root, False)]
		    while stack:
		        node, children_visited = stack.pop()
		        if children_visited:
		            inorder.append(node.val)
		        else:
		            if node.right:
		                stack.append((node.right, False))
		            stack.append((node, True))
		            if node.left:
		                stack.append((node.left, False))
		    return inorder

# time O(n), due to traverse
# space O(n), due to stack
# using tree and dfs (inorder and iterative)

class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        inorder = []
        cur = root
        while cur:
            if not cur.left:
                inorder.append(cur.val)
                cur = cur.right
            else:
                prev = cur.left
                while prev.right and prev.right != cur:
                    prev = prev.right
                if not prev.right:
                    prev.right = cur
                    cur = cur.left
                else:
                    inorder.append(cur.val)
                    prev.right = None
                    cur = cur.right
        return inorder
        
# time O(n), due to traverse
# space O(1), if don't count output list
# using tree and dfs (inorder and morris traversal)
```


## 📄 [A]tree\[A]tree-dfs-inorder\99-recover-binary-search-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def recoverTree(self, root: Optional[TreeNode]) -> None:
        """
        Do not return anything, modify root in-place instead.
        """

        first_wrong = None
        second_wrong = None
        prev = None
        cur = root

        def check():
            nonlocal first_wrong, second_wrong, prev, cur
            if prev and prev.val > cur.val:
                if not first_wrong:
                    first_wrong = prev
                second_wrong = cur
            prev = cur

        while cur:
            if not cur.left:
                check()
                cur = cur.right
            else:
                pred = cur.left
                while pred.right and pred.right != cur:
                    pred = pred.right
                
                if not pred.right:
                    pred.right = cur
                    cur = cur.left
                else:
                    check()
                    pred.right = None
                    cur = cur.right

        first_wrong.val, second_wrong.val = second_wrong.val, first_wrong.val

# time O(n), due to traverse
# space O(1)
# using tree and dfs (inorder and morris traverse)
'''
1. normal morris traversal
2. when have to add to list (not actually add), use prev_node to record
3. next time need to add to list (not actually add), take the prev_node to compare
4. there can have one pair error or two pairs error, so keep the first met error node and last met error node
'''
```


## 📄 [A]tree\[A]tree-dfs-postorder\110-balanced-binary-tree.java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public boolean isBalanced(TreeNode root) {
        int[] res = dfs(root);
        if (res[1] == 1) {
            return true;
        }
        return false;
    }

    public int[] dfs(TreeNode node) {
        if (node == null) {
            return new int[]{0, 1};
        }
        int[] left = dfs(node.left);
        int[] right = dfs(node.right);
        if (left[1] == 0 || right[1] == 0) {
            return new int[]{0, 0};
        }
        if (Math.abs(left[0] - right[0]) > 1) {
            return new int[]{0, 0};
        }
        return new int[]{Math.max(left[0], right[0]) + 1, 1};
    }
}

// time O(n), due to traverse
// space O(n), due to skewed tree's tree height (recursion stack)
// using tree and dfs (postorder and recursive)
```


## 📄 [A]tree\[A]tree-dfs-postorder\110-balanced-binary-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:

        def dfs(node):
            if not node:
                return (0, True)
            left_height, left_balance = dfs(node.left)
            right_height, right_balance = dfs(node.right)
            cur_height = max(left_height + 1, right_height + 1)
            cur_balance = left_balance and right_balance and abs(left_height - right_height) <= 1
            return (cur_height, cur_balance)

        return dfs(root)[1]
    
# time O(n), due to traverse
# space O(n), due to skewed tree's tree height (recursion stack)
# using tree and dfs (postorder and recursive)
```


## 📄 [A]tree\[A]tree-dfs-postorder\1120-maximum-average-subtree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maximumAverageSubtree(self, root: Optional[TreeNode]) -> float:
        res = float('-inf')

        def dfs(node):
            nonlocal res
            if not node:
                return (0, 0)
            left_count, left_total = dfs(node.left)
            right_count, right_total = dfs(node.right)
            cur_count = left_count + right_count + 1
            cur_total = left_total + right_total + node.val
            res = max(res, cur_total / cur_count)
            return (cur_count, cur_total)

        dfs(root)
        return res

# time O(n)
# space O(n)
# using tree and dfs (postoder, recursive)
```


## 📄 [A]tree\[A]tree-dfs-postorder\1145-binary-tree-coloring-game.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def btreeGameWinningMove(self, root: Optional[TreeNode], n: int, x: int) -> bool:
        res = False

        def dfs(node):
            nonlocal res
            if not node:
                return 0
            left_count = dfs(node.left)
            right_count = dfs(node.right)
            if node.val == x:
                upper_count = n - left_count - right_count - 1
                second_player_count = max(upper_count, left_count, right_count)
                first_player_count = n - second_player_count
                res = second_player_count > first_player_count
            return left_count + right_count + 1

        dfs(root)
        return res
        
# time O(n)
# space O(n)
# using tree and dfs (postorder and recursive)
```


## 📄 [A]tree\[A]tree-dfs-postorder\124-binary-tree-maximum-path-sum.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        res = float('-inf')

        def dfs(node):
            nonlocal res
            if not node:
                return 0
            left_path = dfs(node.left)
            right_path = dfs(node.right)
            node_as_peak_path = left_path + right_path + node.val
            res = max(res, node_as_peak_path)
            return max(left_path + node.val, right_path + node.val, 0)

        dfs(root)
        return res
        
# time O(n)
# space O(n)
# using tree and dfs (postorder and recursive)
```


## 📄 [A]tree\[A]tree-dfs-postorder\1644-lowest-common-ancestor-of-a-binary-tree-ii.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':

        def dfs(node):
            if not node:
                return None, 0
            left_cand, left_find = dfs(node.left)
            right_cand, right_find = dfs(node.right)
            if node.val == p.val or node.val == q.val:
                return node, left_find + right_find + 1
            if left_cand and right_cand:
                return node, left_find + right_find
            if left_cand:
                return left_cand, left_find
            if right_cand:
                return right_cand, right_find
            return None, 0

        res, find = dfs(root)
        return res if find == 2 else None
             
# time O(n)
# space O(n)
# using tree and dfs (postorder and recursive)
```


## 📄 [A]tree\[A]tree-dfs-postorder\2246-longest-path-with-different-adjacent-characters.py

```py
from heapq import *
class Node:
    def __init__(self, val):
        self.val = val
        self.children = []

class Solution:
    def longestPath(self, parent: List[int], s: str) -> int:
        nodes = [Node(c) for c in s]
        for i, p in enumerate(parent):
            if p == - 1:
                continue
            nodes[p].children.append(nodes[i])

        res = 0

        def dfs(node):
            nonlocal res
            if not node:
                return 0, None
            children_path = []
            for child in node.children:
                child_path, child_char = dfs(child)
                if child_char != node.val:
                    heappush(children_path, child_path)
                if len(children_path) > 2:
                    heappop(children_path)
            node_as_peak_path = sum(children_path) + 1 if children_path else 1
            res = max(res, node_as_peak_path)
            cur_path = max(children_path) + 1 if children_path else 1
            return cur_path, node.val

        dfs(nodes[0])
        return res
                    
# time O(n)
# space O(n)
# using tree and dfs (postorder and recursive) and heap
```


## 📄 [A]tree\[A]tree-dfs-postorder\236-lowest-common-ancestor-of-a-binary-tree.java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        return dfs(root, p, q);
    }

    public TreeNode dfs(TreeNode node, TreeNode p, TreeNode q) {
        if (node == null) {
            return node;
        }
        TreeNode leftCand = dfs(node.left, p, q);
        TreeNode rightCand = dfs(node.right, p, q);
        if (leftCand != null && rightCand != null) {
            return node;
        }
        if (node.val == p.val || node.val == q.val) {
            return node;
        }
        if (leftCand != null) {
            return leftCand;
        }
        if (rightCand != null) {
            return rightCand;
        }
        return null;
    }
}

// time O(n)
// space O(n)
// using tree and dfs (postorder and recursive)
/*
1. dfs postorder (bottom up approach), helps to get the potential LCA info
*/
```


## 📄 [A]tree\[A]tree-dfs-postorder\236-lowest-common-ancestor-of-a-binary-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        
        def dfs(node):
            if not node:
                return None
            left_cand = dfs(node.left)
            right_cand = dfs(node.right)
            if node.val == p.val or node.val == q.val:
                return node
            if left_cand and right_cand:
                return node
            if left_cand or right_cand:
                return left_cand or right_cand
            return None
        
        return dfs(root)
    
# time O(n)
# space O(n)
# using tree and dfs (postorder and recursive)
'''
1. dfs postorder (bottom up approach), helps to get the potential LCA info
'''
```


## 📄 [A]tree\[A]tree-dfs-postorder\298-binary-tree-longest-consecutive-sequence.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def longestConsecutive(self, root: Optional[TreeNode]) -> int:
        res = float('-inf')

        def dfs(node):
            nonlocal res
            if not node:
                return 0, float('-inf')
            left_len, left_val = dfs(node.left)
            right_len, right_val = dfs(node.right)
            cur_len = 1
            if left_val - 1 == node.val:
                cur_len = max(cur_len, left_len + 1)
            if right_val - 1 == node.val:
                cur_len = max(cur_len, right_len + 1)
            res = max(res, cur_len)
            return cur_len, node.val

        dfs(root)
        return res
    
# time O(n)
# space O(n)
# using tree and dfs (postorder and recursive)
```


## 📄 [A]tree\[A]tree-dfs-postorder\366-find-leaves-of-binary-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import defaultdict
class Solution:
    def findLeaves(self, root: Optional[TreeNode]) -> List[List[int]]:
        res = []
        if not root:
            return res
        height_nodes = defaultdict(list)
        min_height = float('inf')
        max_height = float('-inf')

        def dfs(node):
            nonlocal min_height, max_height
            if not node:
                return 0
            left_height = dfs(node.left)
            right_height = dfs(node.right)
            cur_height = max(left_height + 1, right_height + 1)
            min_height = min(min_height, cur_height)
            max_height = max(max_height, cur_height)
            height_nodes[cur_height].append(node.val)
            return cur_height

        dfs(root)

        for h in range(min_height, max_height + 1):
            res.append(height_nodes[h][:])
        return res

# time O(n)
# space O(n)
# using tree and dfs (post order and recursive) and hashmap
```


## 📄 [A]tree\[A]tree-dfs-postorder\543-diameter-of-binary-tree.java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {

    int res;

    public int diameterOfBinaryTree(TreeNode root) {
        res = 0;
        dfs(root);
        return res;
    }

    public int dfs(TreeNode node) {
        if (node == null) {
            return 0;
        }
        int leftL = dfs(node.left);
        int rightL = dfs(node.right);
        int nodeAsPeakL = leftL + rightL;
        res = Math.max(res, nodeAsPeakL);
        return Math.max(leftL + 1, rightL + 1);
    }
}

// time O(n), due to traverse
// space O(n), due to tree height for skewed tree
// using tree and dfs (postorder, recursive)
```


## 📄 [A]tree\[A]tree-dfs-postorder\543-diameter-of-binary-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        
        res = 0

        def dfs(node):
            nonlocal res
            if not node:
                return 0
            left_path = dfs(node.left)
            right_path = dfs(node.right)
            node_as_peak = left_path + right_path
            res = max(res, node_as_peak)
            return max(left_path + 1, right_path + 1)

        dfs(root)
        return res
        
# time O(n), due to traverse
# space O(n), due to tree height for skewed tree
# using tree and dfs (postorder, recursive)
```


## 📄 [A]tree\[A]tree-dfs-postorder\865-smallest-subtree-with-all-the-deepest-nodes.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def subtreeWithAllDeepest(self, root: TreeNode) -> TreeNode:

        def dfs(node):
            if not node:
                return None, 0
            left_cand, left_depth = dfs(node.left)
            right_cand, right_depth = dfs(node.right)
            cur_cand, cur_depth = None, max(left_depth + 1, right_depth + 1)
            if left_depth == right_depth:
                cur_cand = node
            elif left_depth > right_depth:
                cur_cand = left_cand
            else:
                cur_cand = right_cand
            return cur_cand, cur_depth

        return dfs(root)[0]
    
# time O(n)
# space O(n)
# using tree and dfs (postorder and recursive)
```


## 📄 [A]tree\[A]tree-dfs-preorder\1448-count-good-nodes-in-binary-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def goodNodes(self, root: TreeNode) -> int:
        res = 0

        def helper(node, cur_max):
            nonlocal res
            if not node:
                return
            if node.val >= cur_max:
                res += 1
                cur_max = node.val
            helper(node.left, cur_max)
            helper(node.right, cur_max)
        
        helper(root, float('-inf'))
        return res
    
# time O(n)
# space O(n)
# using tree and dfs (preorder and recursive)
```


## 📄 [A]tree\[A]tree-dfs-preorder\1457-pseudo-palindromic-paths-in-a-binary-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def pseudoPalindromicPaths(self, root: Optional[TreeNode]) -> int:
        res = 0

        def valid(val):
            count = 0
            for i in range(1, 10):
                if val & (1 << i) != 0:
                    count += 1
            return count <= 1

        def dfs(node, val):
            nonlocal res
            if not node:
                return
            val ^= 1 << node.val
            if not node.left and not node.right:
                res += valid(val)
                return
            dfs(node.left, val)
            dfs(node.right, val)

        dfs(root, 0)
        return res

# time O(n)
# space O(n)
# using tree and dfs (preorder and recursive) and bitmask 
# when masking notice difference of |, ^, &
```


## 📄 [A]tree\[A]tree-dfs-preorder\226-invert-binary-tree.java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode invertTree(TreeNode root) {
        return helper(root);
    }

    public TreeNode helper(TreeNode node) {
        if (node == null) {
            return node;
        }
        TreeNode newLeft = node.right;
        TreeNode newRight = node.left;
        node.left = newLeft;
        node.right = newRight;
        helper(node.left);
        helper(node.right);
        return node;
    }
}

// time O(n)
// space O(n)
// using tree and dfs (preorder and recursive)
```


## 📄 [A]tree\[A]tree-dfs-preorder\226-invert-binary-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root:
            return root
        stack = [root]
        while stack:
            node = stack.pop()
            node.left, node.right = node.right, node.left
            if node.right:
                stack.append(node.right)
            if node.left:
                stack.append(node.left)
        return root
            
# time O(n)
# space O(n)
# using tree and dfs (preorder and iterative)

class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        
        def helper(node):
            if not node:
                return node
            node.left, node.right = node.right, node.left
            helper(node.left)
            helper(node.right)
            return node
        
        return helper(root)

# time O(n)
# space O(n)
# using tree and dfs (preorder and recursive)
```


## 📄 [A]tree\[A]tree-dfs-preorder\297-serialize-and-deserialize-binary-tree.py

```py
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        def helper(node):
            if not node:
                return '#null'
            cur = '#' + str(node.val)
            left = helper(node.left)
            right = helper(node.right)
            return cur + left + right
        
        return helper(root)

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        vals = data.split('#')[1:]
        idx = 0
        def helper():
            nonlocal idx
            val = vals[idx]
            idx += 1
            if val == 'null':
                return None
            node = TreeNode(int(val))
            node.left = helper()
            node.right = helper()
            return node
        
        return helper()
        
# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# ans = deser.deserialize(ser.serialize(root))

# time O(n)
# space O(n)
# using tree and dfs (preorder and recursive) and turn tree to string
```


## 📄 [A]tree\[A]tree-dfs-preorder\449-serialize-and-deserialize-bst.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root: Optional[TreeNode]) -> str:
        """Encodes a tree to a single string.
        """
        def int_to_string(val):
            byte_array = [(val >> (i * 8)) & 0xFF for i in range(4)][:: - 1]
            char_array = [chr(byte) for byte in byte_array]
            string = ''.join(char_array)
            return string

        def build(node):
            if not node:
                return ''
            cur = int_to_string(node.val)
            left = build(node.left)
            right = build(node.right)
            return cur + left + right
        
        return build(root)
        
    def deserialize(self, data: str) -> Optional[TreeNode]:
        """Decodes your encoded data to tree.
        """
        def string_to_int(string):
            res = []
            val = 0
            for i, c in enumerate(string):
                val += ord(c) << (8 * (4 - 1 - (i % 4)))
                if i % 4 == 3:
                    res.append(val)
                    val = 0
            return res
        
        vals = string_to_int(data)
        idx = 0
        def build(lower, upper):
            nonlocal idx
            if idx >= len(vals):
                return None
            if vals[idx] <= lower or vals[idx] >= upper:
                return None
            node = TreeNode(vals[idx])
            idx += 1
            node.left = build(lower, node.val)
            node.right = build(node.val, upper)
            return node
        
        return build(float('-inf'), float('inf'))
        
# Your Codec object will be instantiated and called as such:
# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# tree = ser.serialize(root)
# ans = deser.deserialize(tree)
# return ans

# time O(n)
# space O(n)
# using tree and dfs (preorder and recursive) and turn tree to string and bst and bit manipulate
'''
1. tree is BST, so we can use comparsion of vals to avoid record null val as encoded string
2. turn every val into string (length: 4) by bit manipulation to make encoded string compact
'''
```


## 📄 [A]tree\[A]tree-dfs-preorder\545-boundary-of-binary-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def boundaryOfBinaryTree(self, root: Optional[TreeNode]) -> List[int]:

        root_list = []
        left_list = []
        leaf_list = []
        right_list = []

        def preorder(node, flag):
            if not node:
                return
            elif not node.left and not node.right:
                leaf_list.append(node.val)
            elif flag == 0:
                root_list.append(node.val)
                preorder(node.left, 1)
                preorder(node.right, 2)
            elif flag == 1:
                left_list.append(node.val)
                preorder(node.left, 1)
                preorder(node.right, 1 if not node.left else 3)
            elif flag == 2:
                right_list.append(node.val)
                preorder(node.left, 2 if not node.right else 3)
                preorder(node.right, 2)
            else:
                preorder(node.left, 3)
                preorder(node.right, 3)

        preorder(root, 0)
        return root_list + left_list + leaf_list + right_list[::- 1]

# time O(n)
# space O(n)
# using tree and dfs (preorder and recursive) and record leaves
'''
flag
0 is root
1 is left boundary
2 is right boundary
3 is others
'''
```


## 📄 [A]tree\[A]tree-dfs-preorder\572-subtree-of-another-tree.java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        StringBuffer rootSb = new StringBuffer();
        build(root, rootSb);
        String s = rootSb.toString();

        StringBuffer subRootSb = new StringBuffer();
        build(subRoot, subRootSb);
        String t = subRootSb.toString();

        int base = 131;
        int mod = 1000000007;
        long target = 0;
        for (int i = 0; i < t.length(); i++) {
            target = (target * base + t.charAt(i)) % mod;
        }
        long val = 0;
        long removeVal = 1;
        for (int i = 0; i < t.length() - 1; i++) {
            removeVal = (removeVal * base) % mod;
        }
        for (int i = 0; i < s.length(); i++) {
            if (i >= t.length()) {
                val = (val - ((removeVal * s.charAt(i - t.length())) % mod) + mod) % mod;
            }
            val = (val * base + s.charAt(i)) % mod;
            if (i >= t.length() - 1) {
                if (val == target) {
                    return true;
                }
            }
        }
        return false;
    }

    public void build(TreeNode node, StringBuffer s) {
        if (node == null) {
            s.append("#n");
            return;
        }
        s.append("#");
        s.append(node.val + "");
        build(node.left, s);
        build(node.right, s);
        return;
    }
}

// time O(n+m)
// space O(n+m)
// using tree and dfs (preorder and recursive) and turn tree to string and rabin karp (rolling hash)
```


## 📄 [A]tree\[A]tree-dfs-preorder\572-subtree-of-another-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        
        def build(node):
            if not node:
                return '#null'
            cur = '#' + str(node.val)
            left = build(node.left)
            right = build(node.right)
            return cur + left + right

        tree = build(root)
        subtree = build(subRoot)

        base = 131
        mod = 10 ** 9 + 7
        val = 0

        for i, c in enumerate(subtree):
            val = (val * base + ord(c)) % mod

        target_val = val
        val = 0
        remove_val = (base ** (len(subtree) - 1)) % mod
        for i, c in enumerate(tree):
            if i >= len(subtree):
                val -= (remove_val * ord(tree[i - len(subtree)])) % mod
            val = (val * base + ord(c)) % mod
            if i >= len(subtree) - 1:
                if val == target_val:
                    return True
        return False

# time O(n+m)
# space O(n+m)
# using tree and dfs (preorder and recursive) and turn tree to string and rabin karp (rolling hash)
```


## 📄 [A]tree\[A]tree-dfs-preorder\606-construct-string-from-binary-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def tree2str(self, root: Optional[TreeNode]) -> str:
        
        def build_helper(node):
            if not node:
                return ''
            cur = str(node.val)
            left = build_helper(node.left)
            right = build_helper(node.right)
            if not left and not right:
                return cur
            elif left and right:
                return cur + '(' + left + ')' + '(' + right + ')'
            elif not left and right:
                return cur + '()' + '(' + right + ')'
            else:
                return cur + '(' + left + ')'

        return build_helper(root)
    
# time O(n)
# space O(n)
# using tree and dfs (preorder and recursive) and turn tree to string
```


## 📄 [A]tree\[A]tree-dfs-preorder\872-leaf-similar-trees.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def leafSimilar(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> bool:
        if not root1 and not root2:
            return True
        if not root1 or not root2:
            return False
        
        def get_next_leaf(stack):
            leaf = None
            while stack:
                node = stack.pop()
                if not node.left and not node.right:
                    leaf = node
                    break
                if node.right:
                    stack.append(node.right)
                if node.left:
                    stack.append(node.left)
            return leaf

        stack1 = [root1]
        stack2 = [root2]
        while stack1 or stack2:
            leaf1 = get_next_leaf(stack1)
            leaf2 = get_next_leaf(stack2)
            if not leaf1 and not leaf2:
                continue
            if not leaf1 or not leaf2:
                return False
            if leaf1.val != leaf2.val:
                return False
        return True

# time O(n)
# space O(n)
# using tree and dfs (preorder and iterative)
```


## 📄 [A]tree\[A]tree-divide-and-conquer\100-same-tree.java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {

        if (p == null && q == null) {
            return true;
        }
        if (p == null || q == null) {
            return false;
        }
        if (p.val != q.val) {
            return false;
        }
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
}

// time O(min(p, q)), p, q is size of two trees
// space O(min(p, q)), due to tree's height
// using tree and divide and conquer and two branch top-down
/*
1. check root node
2. then check left subtree and right subtree
*/
```


## 📄 [A]tree\[A]tree-divide-and-conquer\100-same-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        
        if not p and not q:
            return True
        if not p and q:
            return False
        if p and not q:
            return False
        if p.val != q.val:
            return False
        return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
   
# time O(min(p, q)), p, q is size of two trees
# space O(min(p, q)), due to tree's height
# using tree and divide and conquer and two branch top-down
'''
1. check root node
2. then check left subtree and right subtree
'''
```


## 📄 [A]tree\[A]tree-divide-and-conquer\1008-construct-binary-search-tree-from-preorder-traversal.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def bstFromPreorder(self, preorder: List[int]) -> Optional[TreeNode]:
        idx = 0

        def build(min_val, max_val):
            nonlocal idx
            if idx == len(preorder):
                return None
            if preorder[idx] < min_val or preorder[idx] > max_val:
                return None
            node = TreeNode(preorder[idx])
            idx += 1
            node.left = build(min_val, node.val)
            node.right = build(node.val, max_val)
            return node
        
        return build(float('-inf'), float('inf'))
    
# time O(n)
# space O(n)
# using tree and divide and conquer and re-build BST (top-down approach) and dfs (preorder and recursive)
'''
1. use BST properties
2. preorder = ROOT + [LEFT SUB] + [RIGHT SUB]
            = ROOT + [ROOT OF LEFT SUB + REST ORF LEFT SUB] + [ROOT OF RIGHT SUB + REST ORF RIGHT SUB]
'''
```


## 📄 [A]tree\[A]tree-divide-and-conquer\101-symmetric-tree.java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return dfs(root.left, root.right);
    }

    public boolean dfs(TreeNode p, TreeNode q) {
        if (p == null && q == null) {
            return true;
        }
        if (p == null || q == null) {
            return false;
        }
        if (p.val != q.val) {
            return false;
        }
        return dfs(p.left, q.right) && dfs(p.right, q.left);
    }
}

// time O(n), due to traverse
// space O(n), due to tree height
// using tree and divide and conquer and two branch top-down
```


## 📄 [A]tree\[A]tree-divide-and-conquer\101-symmetric-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        
        def symmetric_helper(p, q):
            if not p and not q:
                return True
            if not p and q:
                return False
            if p and not q:
                return False
            if p.val != q.val:
                return False
            return symmetric_helper(p.left, q.right) and symmetric_helper(p.right, q.left)

        return symmetric_helper(root.left, root.right)
    
# time O(n), due to traverse
# space O(n), due to tree height
# using tree and divide and conquer and two branch top-down

from collections import deque
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        queue = deque()
        queue.append(root.left)
        queue.append(root.right)
        while queue:
            left = queue.popleft()
            right = queue.popleft()
            if not left and not right:
                continue
            elif not left or not right:
                return False
            elif left.val != right.val:
                return False
            queue.append(left.left)
            queue.append(right.right)
            queue.append(left.right)
            queue.append(right.left)
        return True
    
# time O(n)
# space O(n), due to queue and tree diameter
# using bfs (iterative)
```


## 📄 [A]tree\[A]tree-divide-and-conquer\105-construct-binary-tree-from-preorder-and-inorder-traversal.java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        Map<Integer, Integer> inValToInIdx = new HashMap<>();
        for (int i = 0; i < inorder.length; i++) {
            inValToInIdx.put(inorder[i], i);
        }
        return build(preorder, inValToInIdx, 0, preorder.length - 1, 0, inorder.length - 1, preorder.length);
    }

    public TreeNode build(int[] preorder, Map<Integer, Integer> inValToInIdx, int preLeft, int preRight, int inLeft, int inRight, int length) {
        if (length < 1) {
            return null;
        }
        TreeNode node = new TreeNode(preorder[preLeft]);
        Integer inIdx = inValToInIdx.get(preorder[preLeft]);
        int leftLength = inIdx - inLeft;
        int rightLength = length - leftLength - 1;
        node.left = build(preorder, inValToInIdx, preLeft + 1, preLeft + leftLength, inLeft, inIdx - 1, leftLength);
        node.right = build(preorder, inValToInIdx, preLeft + leftLength + 1, preRight, inIdx + 1, inRight, rightLength);
        return node;
    }
}

// time O(n), due to O(1) find in hashmap but recursion n times
// space O(n), due to hashmap or building tree or recursion
// using tree and divide and conquer and re-build tree (top-down)
/*
preorder: first value is root
inorder: every value before root is left subtree, after root is right subtree
*/
```


## 📄 [A]tree\[A]tree-divide-and-conquer\105-construct-binary-tree-from-preorder-and-inorder-traversal.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:

        n = len(preorder)
        val_inorder_idx = {}
        for i, num in enumerate(inorder):
            val_inorder_idx[num] = i

        def build_helper(preorder_left_idx, preorder_right_idx, inorder_left_idx, inorder_right_idx, node_count):
            if node_count < 1:
                return None
            val = preorder[preorder_left_idx]
            node = TreeNode(val)
            inorder_mid_idx = val_inorder_idx[val]
            left_tree_count = inorder_mid_idx - inorder_left_idx
            right_tree_count = node_count - left_tree_count - 1
            node.left = build_helper(preorder_left_idx + 1, preorder_left_idx + left_tree_count, inorder_left_idx, inorder_mid_idx - 1, left_tree_count)
            node.right = build_helper(preorder_left_idx + left_tree_count + 1, preorder_right_idx, inorder_mid_idx + 1, inorder_right_idx, right_tree_count)
            return node

        return build_helper(0, n - 1, 0, n - 1, n)     

# time O(n), due to O(1) find in hashmap but recursion n times
# space O(n), due to hashmap or building tree or recursion
# using tree and divide and conquer and re-build tree (top-down)
'''
preorder: first value is root
inorder: every value before root is left subtree, after root is right subtree
'''
```


## 📄 [A]tree\[A]tree-divide-and-conquer\106-construct-binary-tree-from-inorder-and-postorder-traversal.java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    int[] inorder;
    int[] postorder;
    int length;
    HashMap<Integer, Integer> invalToInidx;

    public TreeNode buildTree(int[] inorder, int[] postorder) {
        this.inorder = inorder;
        this.postorder = postorder;
        length = inorder.length;
        invalToInidx = new HashMap<>();
        for (int i = 0; i < inorder.length; i++) {
            invalToInidx.put(inorder[i], i);
        }
        return dfs(0, length - 1, 0, length - 1, length);
    }

    public TreeNode dfs(int inLeft, int inRight, int postLeft, int postRight, int length) {
        if (length < 1) {
            return null;
        }
        TreeNode node = new TreeNode(postorder[postRight]);
        int inidx = invalToInidx.get(postorder[postRight]);
        int leftLength = inidx - inLeft;
        int rightLength = inRight - inidx;
        node.left = dfs(inLeft, inidx - 1, postLeft, postLeft + leftLength - 1, leftLength);
        node.right = dfs(inidx + 1, inRight, postLeft + leftLength, postRight - 1, rightLength);
        return node;
    }
}

// time O(n)
// space O(n)
// using tree and divide and conquer and re-build tree (top-down)
/*
postorder: last value is root
inorder: every value before root is left subtree, after root is right subtree
*/
```


## 📄 [A]tree\[A]tree-divide-and-conquer\106-construct-binary-tree-from-inorder-and-postorder-traversal.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, inorder: List[int], postorder: List[int]) -> Optional[TreeNode]:
        n = len(inorder)
        val_inorder_idx = {}
        for i, num in enumerate(inorder):
            val_inorder_idx[num] = i

        def build_helper(postorder_left_idx, postorder_right_idx, inorder_left_idx, inorder_right_idx, node_count):
            if node_count < 1:
                return None
            val = postorder[postorder_right_idx]
            node = TreeNode(val)
            inorder_mid_idx = val_inorder_idx[val]
            left_tree_count = inorder_mid_idx - inorder_left_idx
            right_tree_count = node_count - left_tree_count - 1
            node.left = build_helper(postorder_left_idx, postorder_left_idx + left_tree_count - 1, inorder_left_idx, inorder_mid_idx - 1, left_tree_count)
            node.right = build_helper(postorder_left_idx + left_tree_count, postorder_right_idx - 1, inorder_mid_idx + 1, inorder_right_idx, right_tree_count)
            return node

        return build_helper(0, n - 1, 0, n - 1, n)

# time O(n)
# space O(n)
# using tree and divide and conquer and re-build tree (top-down)
'''
postorder: last value is root
inorder: every value before root is left subtree, after root is right subtree
'''
```


## 📄 [A]tree\[A]tree-divide-and-conquer\108-convert-sorted-array-to-binary-search-tree.java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        return build(0, nums.length - 1, nums);
    }

    public TreeNode build(int left, int right, int[] nums) {
        if (left > right) {
            return null;
        }
        int m = left + (right - left) / 2;
        TreeNode node = new TreeNode(nums[m]);
        node.left = build(left, m - 1, nums);
        node.right = build(m + 1, right, nums);
        return node;
    }
}

// time O(n), due to traverse each node once
// space O(logn), due to memo stack's size, and output is O(n)
// using tree and divide and conquer and re-build BST (top-down approach)
```


## 📄 [A]tree\[A]tree-divide-and-conquer\108-convert-sorted-array-to-binary-search-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> Optional[TreeNode]:
        n = len(nums)

        def build_helper(left, right):
            if left > right:
                return None
            mid = (left + right) // 2
            node = TreeNode(nums[mid])
            node.left = build_helper(left, mid - 1)
            node.right = build_helper(mid + 1, right)
            return node

        return build_helper(0, n - 1)

# time O(n), due to traverse each node once
# space O(logn), due to memo stack's size, and output is O(n)
# using tree and divide and conquer and re-build BST (top-down approach)

class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> Optional[TreeNode]:
        
        idx = 0

        def dfs(left, right):
            nonlocal idx
            if left > right:
                return None
            
            mid = (left + right) // 2
            left_subtree = dfs(left, mid - 1)

            node = TreeNode(nums[idx])
            idx += 1

            node.left = left_subtree

            right_subtree = dfs(mid + 1, right)
            node.right = right_subtree
            return node

        return dfs(0, len(nums) - 1)

# time O(n)
# space O(logn), due to recursion stack
# using tree and divide and conquer and re-build BST (inorder approach)
```


## 📄 [A]tree\[A]tree-divide-and-conquer\109-convert-sorted-list-to-binary-search-tree.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sortedListToBST(self, head: Optional[ListNode]) -> Optional[TreeNode]:
        
        count = 0
        cur = head
        while cur:
            count += 1
            cur = cur.next

        cur = head

        def build_helper(left, right):
            nonlocal cur
            if left > right:
                return None

            mid = (left + right) // 2
            left_subtree = build_helper(left, mid - 1)

            node = TreeNode(cur.val)
            cur = cur.next

            node.left = left_subtree

            right_subtree = build_helper(mid + 1, right)
            node.right = right_subtree
            return node

        return build_helper(0, count - 1)
    
# time O(n)
# space O(logn), due to recursion stack
# using tree and divide and conquer and re-build BST (inorder approach)
'''
1. use divide and conquer, simulate inorder traversal
2. follow linked list ptr, so build left tree first then root then right tree
'''
```


## 📄 [A]tree\[A]tree-divide-and-conquer\116-populating-next-right-pointers-in-each-node.py

```py
"""
# Definition for a Node.
class Node:
    def __init__(self, val: int = 0, left: 'Node' = None, right: 'Node' = None, next: 'Node' = None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""

class Solution:
    def connect(self, root: 'Optional[Node]') -> 'Optional[Node]':
        upper_start = root
        while upper_start:
            upper_cur = upper_start
            while upper_cur:
                if upper_cur.left:
                    upper_cur.left.next = upper_cur.right
                if upper_cur.right and upper_cur.next:
                    upper_cur.right.next = upper_cur.next.left
                upper_cur = upper_cur.next
            upper_start = upper_start.left
        return root
    
# time O(n)
# space O(1)
# using tree and divide and conquer and populate next ptr
# next ptr's two type: belong to same parent or belong to parents next to each other
```


## 📄 [A]tree\[A]tree-divide-and-conquer\117-populating-next-right-pointers-in-each-node-ii.py

```py
"""
# Definition for a Node.
class Node:
    def __init__(self, val: int = 0, left: 'Node' = None, right: 'Node' = None, next: 'Node' = None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""

class Solution:
    def connect(self, root: 'Node') -> 'Node':
        upper_start = root
        while upper_start:
            upper_cur = upper_start
            lower_start = None
            lower_end = None
            while upper_cur:
                if not lower_start:
                    lower_start = upper_cur.left or upper_cur.right
                if upper_cur.left:
                    if lower_end:
                        lower_end.next = upper_cur.left
                    lower_end = upper_cur.left
                if upper_cur.right:
                    if lower_end:
                        lower_end.next = upper_cur.right
                    lower_end = upper_cur.right
                upper_cur = upper_cur.next
            upper_start = lower_start
        return root

# time O(n)
# space O(1)
# using tree and divide and conquer and populate next ptr and multi pointers
```


## 📄 [A]tree\[A]tree-divide-and-conquer\1650-lowest-common-ancestor-of-a-binary-tree-iii.py

```py
"""
# Definition for a Node.
class Node:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None
        self.parent = None
"""

class Solution:
    def lowestCommonAncestor(self, p: 'Node', q: 'Node') -> 'Node':
        
        p1, p2 = p, q
        while p1 != p2:
            if p1:
                p1 = p1.parent
            else:
                p1 = q
            if p2:
                p2 = p2.parent
            else:
                p2 = p
        return p1
        
# time O(n)
# space O(1)
# using tree and divide and conquer and find LCA and two pointers
# p→LCA + LCA→root + q→LCA is same as q→LCA + LCA→root + p→LCA
```


## 📄 [A]tree\[A]tree-divide-and-conquer\235-lowest-common-ancestor-of-a-binary-search-tree.java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

 class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        while (root != null) {
            if (p.val < root.val && q.val < root.val) {
                root = root.left;
            } else if (p.val > root.val && q.val > root.val) {
                root = root.right;
            } else {
                break;
            }
        }
        return root;
    }
}

// time O(n), due to tree height
// space O(1)
// using tree and divide and conquer and find LCA and bst
```


## 📄 [A]tree\[A]tree-divide-and-conquer\235-lowest-common-ancestor-of-a-binary-search-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        cur = root
        while cur:
            if cur.val > p.val and cur.val > q.val:
                cur = cur.left
            elif cur.val < p.val and cur.val < q.val:
                cur = cur.right
            else:
                break
        return cur
    
# time O(n), due to tree height
# space O(1)
# using tree and divide and conquer and find LCA and bst
```


## 📄 [A]tree\[A]tree-divide-and-conquer\285-inorder-successor-in-bst.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def inorderSuccessor(self, root: TreeNode, p: TreeNode) -> Optional[TreeNode]:
        res = None
        cur = root
        while cur:
            if cur.val > p.val:
                res = cur
                cur = cur.left
            else:
                cur = cur.right
        return res
        
# time O(n)
# space O(1)
# using tree and divide and conquer and bst
```


## 📄 [A]tree\[A]tree-divide-and-conquer\450-delete-node-in-a-bst.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def deleteNode(self, root: Optional[TreeNode], key: int) -> Optional[TreeNode]:

        def delete_helper(node):
            if not node:
                return node
            if node.val == key:
                if not node.left:
                    return node.right
                pred = node.left
                while pred and pred.right:
                    pred = pred.right
                pred.right = node.right
                return node.left
            elif node.val < key:
                node.right = delete_helper(node.right)
            else:
                node.left = delete_helper(node.left)
            return node

        return delete_helper(root)
        
# time O(n), due to tree height, can be logn
# space O(n), due to recursive stack
# using tree and divide and conquer and bst
```


## 📄 [A]tree\[A]tree-divide-and-conquer\700-search-in-a-binary-search-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def searchBST(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:
        
        cur = root
        while cur:
            if cur.val == val:
                return cur
            elif cur.val > val:
                cur = cur.left
            else:
                cur = cur.right
        return None
    
# time O(n)
# space O(1)
# using tree and divide and conquer and bst
```


## 📄 [A]tree\[A]tree-divide-and-conquer\701-insert-into-a-binary-search-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def insertIntoBST(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:
        node = TreeNode(val)

        if not root:
            return node

        cur = root
        while cur:
            if cur.val > node.val:
                if not cur.left:
                    cur.left = node
                    break
                cur = cur.left
            else:
                if not cur.right:
                    cur.right = node
                    break
                cur = cur.right
        return root
            
# time O(n)
# space O(1)
# using tree and divide and conquer and bst
```


## 📄 [A]tree\[A]tree-divide-and-conquer\889-construct-binary-tree-from-preorder-and-postorder-traversal.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def constructFromPrePost(self, preorder: List[int], postorder: List[int]) -> Optional[TreeNode]:
        n = len(preorder)
        val_postorder_idx = {}
        for i, num in enumerate(postorder):
            val_postorder_idx[num] = i

        def build_helper(preorder_left_idx, preorder_right_idx, postorder_left_idx, postorder_right_idx, node_count):
            if node_count < 1:
                return None
            val = preorder[preorder_left_idx]
            node = TreeNode(val)
            if node_count == 1:
                return node
            postorder_left_tree_idx = val_postorder_idx[preorder[preorder_left_idx + 1]]
            left_tree_count = postorder_left_tree_idx - postorder_left_idx + 1
            right_tree_count = node_count - left_tree_count - 1
            node.left = build_helper(preorder_left_idx + 1, preorder_left_idx + left_tree_count, postorder_left_idx, postorder_left_tree_idx, left_tree_count)
            node.right = build_helper(preorder_left_idx + left_tree_count + 1, preorder_right_idx, postorder_left_tree_idx + 1, postorder_right_idx - 1, right_tree_count)
            return node

        return build_helper(0, n - 1, 0, n - 1, n)

# time O(n)
# space O(n)
# using tree and divide and conquer and re-build tree (top-down)
'''
1. preorder = Root + [Left Subtree] + Right Subtree
            = Root + [Left Subtree Root + Rest of Left Subtree] + Right Subtree
2. postorder = [Left Subtree] + Right Subtree + Root
             = [Rest of Left Subtree + Left Subtree Root] + Right Subtree + Root
'''
```


## 📄 [A]tree\[A]tree-divide-and-conquer\95-unique-binary-search-trees-ii.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def generateTrees(self, n: int) -> List[Optional[TreeNode]]:
        
        def copy(node):
            if not node:
                return None
            new_node = TreeNode(node.val)
            new_node.left = copy(node.left)
            new_node.right = copy(node.right)
            return new_node

        def build_helper(left, right):
            if left > right:
                return [None]
            res = []
            for root_val in range(left, right + 1):
                left_trees = build_helper(left, root_val - 1)
                right_trees = build_helper(root_val + 1, right)
                for left_tree in left_trees:
                    for right_tree in right_trees:
                        root = TreeNode(root_val)
                        root.left = copy(left_tree)
                        root.right = copy(right_tree)
                        res.append(root)
            return res

        return build_helper(1, n)
        
# time O(Catalan(n))
# space O(Catalan(n))
# using tree and divide and conquer and unique BST
```


## 📄 [A]tree\[A]tree-divide-and-conquer\96-unique-binary-search-trees.py

```py
class Solution:
    def numTrees(self, n: int) -> int:

        dp = [0 for _ in range(n + 1)]
        dp[0] = 1
        dp[1] = 1

        for total_count in range(2, n + 1):
            for left_count in range(0, total_count):
                dp[total_count] += dp[left_count] * dp[total_count - left_count - 1]
        return dp[n]
        
# time O(n**2)
# space O(n)
# using tree and divide and conquer and unique BST and dp
# dp[i] means i nodes can have how many unique binary trees

class Solution:
    def numTrees(self, n: int) -> int:

        res = 1
        for i in range(n):
            res *= ((4 * i + 2) / (i + 2))
        return int(res)

# time O(n)
# space O(1)
# using tree and divide and conquer and unique BST and math
# C0 = 1, C(n+1) = Cn * ((4n + 2) / (n + 2))
```


## 📄 [A]tree\[A]tree-divide-and-conquer\98-validate-binary-search-tree.java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public boolean isValidBST(TreeNode root) {
        return dfs(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    public boolean dfs(TreeNode node, long lower, long upper) {
        if (node == null) {
            return true;
        }
        if (node.val <= lower || node.val >= upper) {
            return false;
        }
        return dfs(node.left, lower, node.val) && dfs(node.right, node.val, upper);
    }
}

// time O(n), n is the number of nodes (traverse)
// space O(n), n is the recursive stack size (imagine an one branch tree)
// using tree and divide and conquer and two branch top-down and bst
```


## 📄 [A]tree\[A]tree-divide-and-conquer\98-validate-binary-search-tree.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        
        def valid_helper(node, lower, upper):
            if not node:
                return True
            if node.val <= lower or node.val >= upper:
                return False
            return valid_helper(node.left, lower, node.val) and valid_helper(node.right, node.val, upper)

        return valid_helper(root, float('-inf'), float('inf'))
        
# time O(n), n is the number of nodes (traverse)
# space O(n), n is the recursive stack size (imagine an one branch tree)
# using tree and divide and conquer and two branch top-down and bst
```


## 📄 [B]linked-list\[B]linked-list\1019-next-greater-node-in-linked-list.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def nextLargerNodes(self, head: Optional[ListNode]) -> List[int]:
        count = 0
        cur = head
        while cur:
            count += 1
            cur = cur.next
        res = [0 for _ in range(count)]

        stack = []
        cur = head
        for i in range(count):
            while stack and stack[- 1][1] < cur.val:
                prev_idx, prev_val = stack.pop()
                res[prev_idx] = cur.val
            stack.append((i, cur.val))
            cur = cur.next
        return res
    
# time O(n)
# space O(n)
# using linked list and counting length and monotonic stack
```


## 📄 [B]linked-list\[B]linked-list\1206-design-skiplist.py

```py
import random

class ListNode:
    def __init__(self, val=None, next=None, down=None):
        self.val = val
        self.next = next
        self.down = down

class Skiplist:

    def __init__(self):
        self.root = ListNode()

    def search(self, target: int) -> bool:
        cur = self.root
        while cur:
            if not cur.next:
                cur = cur.down
            elif target > cur.next.val:
                cur = cur.next
            elif target == cur.next.val:
                return True
            else:
                cur = cur.down
        return False

    def add(self, num: int) -> None:
        stack = []
        cur = self.root
        while cur:
            if not cur.next:
                stack.append(cur)
                cur = cur.down
            elif num > cur.next.val:
                cur = cur.next
            else:
                stack.append(cur)
                cur = cur.down
        down_node = None
        while stack:
            node = stack.pop()
            node.next = ListNode(val=num, next=node.next, down=down_node)
            down_node = node
            if random.randint(0, 1) == 0:
                break
            if not stack:
                self.root = ListNode(down=self.root)

    def erase(self, num: int) -> bool:
        stack = []
        cur = self.root
        while cur:
            if not cur.next:
                cur = cur.down
            elif num > cur.next.val:
                cur = cur.next
            elif num == cur.next.val:
                stack.append(cur)
                cur = cur.down
            else:
                cur = cur.down
        if not stack:
            return False
        while stack:
            node = stack.pop()
            node.next = node.next.next
        return True

# Your Skiplist object will be instantiated and called as such:
# obj = Skiplist()
# param_1 = obj.search(target)
# obj.add(num)
# param_3 = obj.erase(num)

# time O(logn) for all on average, worst is O(n)
# space O(n) on average, worst is O(nlogn)
# using linked list and skiplist and random
```


## 📄 [B]linked-list\[B]linked-list\138-copy-list-with-random-pointer.py

```py
"""
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random
"""

class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        if not head:
            return head

        old_node = head
        while old_node:
            next_old_node = old_node.next
            old_node.next = Node(x=old_node.val, next=next_old_node)
            old_node = next_old_node
        
        old_node = head
        while old_node:
            new_node = old_node.next
            next_old_node = old_node.next.next
            new_node.random = old_node.random.next if old_node.random else None
            old_node = next_old_node

        old_node = head
        new_list = head.next
        while old_node:
            new_node = old_node.next
            next_old_node = old_node.next.next
            old_node.next = next_old_node
            new_node.next = next_old_node.next if next_old_node else None
            old_node = next_old_node
        return new_list
        
# time O(n), due to traverse thrice
# space O(1), not count output list
# using linked list and interweaving
'''
0. OLD1 -> OLD2
1. creating and weaving: OLD1 -> NEW1 -> OLD2 -> NEW2
2. handle new_nodes' random ptr
3. unweaving and handle new_nodes' next ptr: OLD1 -> OLD2, NEW1 -> NEW2
'''
```


## 📄 [B]linked-list\[B]linked-list\141-linked-list-cycle.java

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) {
            return false;
        }
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                return true;
            }
        }
        return false;
    }
}

// time O(n), due to traverse
// space O(1)
// using linked list and two pointers (slow and fast)
```


## 📄 [B]linked-list\[B]linked-list\141-linked-list-cycle.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        if not head or not head.next:
            return False

        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                return True
        return False
        
# time O(n), due to traverse
# space O(1)
# using linked list and two pointers (slow and fast)
```


## 📄 [B]linked-list\[B]linked-list\142-linked-list-cycle-ii.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head or not head.next:
            return None
        
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                p1, p2 = head, slow
                while p1 != p2:
                    p1 = p1.next
                    p2 = p2.next
                return p1
        return None
        
# time O(n), due to traverse
# space O(1)
# using linked list and two pointers (slow and fast)
# 2 * (slow) = fast
# 2 * (p + x) = p + x + y + x
# p = y
```


## 📄 [B]linked-list\[B]linked-list\143-reorder-list.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        
        if not head or not head.next:
            return
        
        slow, fast = head, head
        while fast.next and fast.next.next:
            slow = slow.next
            fast = fast.next.next
        first_part_tail = slow
        second_part_old_head = slow.next
        first_part_tail.next = None

        prev, cur = None, second_part_old_head
        while cur:
            nxt = cur.next
            cur.next = prev
            prev = cur
            cur = nxt
        second_part_new_head = prev

        dummy = cur = ListNode()
        p1, p2 = head, second_part_new_head
        while p1 and p2:
            cur.next = p1
            p1 = p1.next
            cur = cur.next
            cur.next = p2
            p2 = p2.next
            cur = cur.next
        if p1:
            cur.next = p1
        return
        
# time O(n)
# space O(1)
# using linked lsit and two pointers (utilize symmetry property) (finding middle, reversing, combining)
```


## 📄 [B]linked-list\[B]linked-list\146-lru-cache.java

```java
class Node {
    int key;
    int val;
    Node prev;
    Node next;
    public Node(int key, int val) {
        this.key = key;
        this.val = val;
    }
}

class Dll {
    Node head;
    Node tail;
    public Dll() {
        head = new Node(- 1, - 1);
        tail = new Node(- 1, - 1);
        head.next = tail;
        tail.prev = head;
    }

    public void append(Node node) {
        Node prevNode = tail.prev;
        Node nextNode = tail;
        prevNode.next = node;
        node.prev = prevNode;
        node.next = nextNode;
        nextNode.prev = node;
        return;
    }

    public void update(Node node) {
        Node prevNode = node.prev;
        Node nextNode = node.next;
        prevNode.next = nextNode;
        nextNode.prev = prevNode;
        this.append(node);
        return;
    }

    public Node popleft() {
        Node prevNode = head;
        Node node = prevNode.next;
        Node nextNode = node.next;
        prevNode.next = nextNode;
        nextNode.prev = prevNode;
        return node;
    }
}

class LRUCache {
    int capacity;
    Dll dll;
    HashMap<Integer, Node> keyToNode;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        dll = new Dll();
        keyToNode = new HashMap<>();
    }
    
    public int get(int key) {
        if (!keyToNode.containsKey(key)) {
            return - 1;
        }
        Node node = keyToNode.get(key);
        dll.update(node);
        return node.val;
    }
    
    public void put(int key, int value) {
        if (keyToNode.containsKey(key)) {
            Node node = keyToNode.get(key);
            node.val = value;
            dll.update(node);
            return;
        }
        if (keyToNode.size() == capacity) {
            Node removeNode = dll.popleft();
            keyToNode.remove(removeNode.key);
        }
        Node node = new Node(key, value);
        keyToNode.put(key, node);
        dll.append(node);
        return;
    }
}

/**
* Your LRUCache object will be instantiated and called as such:
* LRUCache obj = new LRUCache(capacity);
* int param_1 = obj.get(key);
* obj.put(key,value);
*/

// time O(1)
// space O(capacity)
// using linked list and dll and hashmap
/*
1. maintain key_node hashmap
2. maintain dll
3. maintain capacity
4. if get() or put(), dll update the recent used node to the dll's tail or just append node to tail
5. if exceed capacity, dll popleft the least recent used node and pop it from hashmap
*/
```


## 📄 [B]linked-list\[B]linked-list\146-lru-cache.py

```py
class ListNode:
    def __init__(self, key=None, val=None):
        self.key = key
        self.val = val
        self.prev = None
        self.next = None

class Dll:
    def __init__(self):
        self.head = ListNode()
        self.tail = ListNode()
        self.head.next = self.tail
        self.tail.prev = self.head

    def append(self, node):
        prev_node = self.tail.prev
        next_node = self.tail
        prev_node.next = node
        node.prev = prev_node
        node.next = next_node
        next_node.prev = node
        return node

    def popleft(self):
        prev_node = self.head
        node = self.head.next
        next_node = node.next
        prev_node.next = next_node
        next_node.prev = prev_node
        return node

    def update(self, node):
        prev_node = node.prev
        next_node = node.next
        prev_node.next = next_node
        next_node.prev = prev_node
        self.append(node)
        return node

class LRUCache:

    def __init__(self, capacity: int):
        self.dll = Dll()
        self.key_node = {}
        self.capacity = capacity

    def get(self, key: int) -> int:
        if key not in self.key_node:
            return - 1
        node = self.key_node[key]
        self.dll.update(node)
        return node.val

    def put(self, key: int, value: int) -> None:
        if key not in self.key_node:
            if len(self.key_node) == self.capacity:
                remove_node = self.dll.popleft()
                self.key_node.pop(remove_node.key)
            node = self.dll.append(ListNode(key=key, val=value))
            self.key_node[key] = node
        else:
            node = self.key_node[key]
            node.val = value
            self.dll.update(node)

# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)

# time O(1)
# space O(capacity)
# using linked list and dll and hashmap
'''
1. maintain key_node hashmap
2. maintain dll
3. maintain capacity
4. if get() or put(), dll update the recent used node to the dll's tail or just append node to tail
5. if exceed capacity, dll popleft the least recent used node and pop it from hashmap
'''
```


## 📄 [B]linked-list\[B]linked-list\148-sort-list.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def sortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head or not head.next:
            return head

        count = 0
        cur = head
        while cur:
            count += 1
            cur = cur.next

        dummy = ListNode(next=head)
        interval_len = 1
        while interval_len < count:
            new_list = dummy
            cur = dummy.next
            while cur:
                interval1_len = 0
                interval1 = cur
                while cur and interval1_len < interval_len:
                    interval1_len += 1
                    cur = cur.next
                interval2_len = 0
                interval2 = cur
                while cur and interval2_len < interval_len:
                    interval2_len += 1
                    cur = cur.next
                while interval1_len or interval2_len:
                    if (interval1_len and interval2_len and interval1.val < interval2.val) or (interval2_len == 0):
                        new_list.next = interval1
                        new_list = new_list.next
                        interval1 = interval1.next
                        interval1_len -= 1
                    else:
                        new_list.next = interval2
                        new_list = new_list.next
                        interval2 = interval2.next
                        interval2_len -= 1
            new_list.next = None
            interval_len *= 2
        return dummy.next
                    
# time O(nlogn), due to merge sort
# space O(1)
# using linked list and iterative merge sort (bottom up)
```


## 📄 [B]linked-list\[B]linked-list\160-intersection-of-two-linked-lists.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        p1, p2 = headA, headB
        while p1 != p2:
            if not p1:
                p1 = headB
            else:
                p1 = p1.next
            if not p2:
                p2 = headA
            else:
                p2 = p2.next
        return p1

# time O(m + n), m and n are the numbers of linked lists' length
# space O(1)
# using linked list and two pointers (find LCA/intersection)
# x + p + y = y + p + x
```


## 📄 [B]linked-list\[B]linked-list\1836-remove-duplicates-from-an-unsorted-linked-list.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
from collections import defaultdict
class Solution:
    def deleteDuplicatesUnsorted(self, head: ListNode) -> ListNode:
        val_freq = defaultdict(int)
        dummy = prev = ListNode(next=head)
        cur = head
        while cur:
            val_freq[cur.val] += 1
            cur = cur.next

        cur = head
        while cur:
            if val_freq[cur.val] >= 2:
                prev.next = None
                cur = cur.next
            else:
                prev.next = cur
                prev = cur
                cur = cur.next
        return dummy.next
    
# time O(n)
# space O(n)
# using linked list and two pointers (prev and cur) and hashmap
```


## 📄 [B]linked-list\[B]linked-list\19-remove-nth-node-from-end-of-list.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = prev = cur = ListNode(next=head)
        step = n + 1
        while step:
            cur = cur.next
            step -= 1

        while cur:
            prev = prev.next
            cur = cur.next

        prev.next = prev.next.next
        return dummy.next
        
# time O(n)
# space O(1)
# using linked list and sentinel node and two pointers
'''
1. maintain two same direction pointers with n gap
2. once one ptr reach null, then another is nth from end
'''
```


## 📄 [B]linked-list\[B]linked-list\2-add-two-numbers.java

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode();
        ListNode cur = dummy;
        int carry = 0;
        while (carry > 0 || l1 != null || l2 != null) {
            if (l1 != null) {
                carry += l1.val;
                l1 = l1.next;
            }
            if (l2 != null) {
                carry += l2.val;
                l2 = l2.next;
            }
            int val = carry % 10;
            cur.next = new ListNode(val);
            cur = cur.next;
            carry /= 10;
        }
        return dummy.next;
    }
}

// time O(n)
// space O(n), creating a new linked list
// using linked list and sentinel node and two pointers
```


## 📄 [B]linked-list\[B]linked-list\2-add-two-numbers.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = cur = ListNode()
        carry = 0
        while l1 or l2 or carry:
            if l1:
                carry += l1.val
                l1 = l1.next
            if l2:
                carry += l2.val
                l2 = l2.next
            carry, digit = divmod(carry, 10)
            cur.next = ListNode(digit)
            cur = cur.next
        return dummy.next
        
# time O(n)
# space O(n), creating a new linked list
# using linked list and sentinel node and two pointers
```


## 📄 [B]linked-list\[B]linked-list\206-reverse-linked-list.java

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode prev = null;
        ListNode cur = head;
        while (cur != null) {
            ListNode nxt = cur.next;
            cur.next = prev;
            prev = cur;
            cur = nxt;
        }
        return prev;
    }
}

// time O(n)
// space O(1)
// using linked list and two pointers (prev and cur)
```


## 📄 [B]linked-list\[B]linked-list\206-reverse-linked-list.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head or not head.next:
            return head
        
        prev = None
        cur = head
        while cur:
            nxt = cur.next
            cur.next = prev
            prev = cur
            cur = nxt
        return prev
        
# time O(n)
# space O(1)
# using linked list and two pointers (prev and cur)
```


## 📄 [B]linked-list\[B]linked-list\2074-reverse-nodes-in-even-length-groups.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseEvenLengthGroups(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head or not head.next:
            return head

        dummy = prev = ListNode(next=head)
        cur = head
        count = 0
        group = 1
        while cur:
            count += 1
            if count == 1:
                prev_nodes = prev
                old_head = cur
            if count == group and group % 2:
                count = 0
                group += 1
                prev = cur
                cur = cur.next
            elif count == group and group % 2 == 0:
                old_tail = cur
                next_nodes = cur.next
                prev, cur = self.reverse(prev_nodes, old_head, old_tail, next_nodes)
                count = 0
                group += 1
            elif not cur.next and count % 2 == 0:
                old_tail = cur
                next_nodes = cur.next
                prev, cur = self.reverse(prev_nodes, old_head, old_tail, next_nodes)
            else:
                prev = cur
                cur = cur.next

        return dummy.next

    def reverse(self, prev_nodes, old_head, old_tail, next_nodes):
        prev, cur = prev_nodes, old_head
        while cur and cur != next_nodes:
            nxt = cur.next
            cur.next = prev
            prev = cur
            cur = nxt
        prev_nodes.next = prev
        old_head.next = next_nodes
        return old_head, next_nodes
    
# time O(n)
# space O(1)
# using linked list and two pointers (prev and cur) and multi pointers
```


## 📄 [B]linked-list\[B]linked-list\21-merge-two-sorted-lists.java

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummy = new ListNode();
        ListNode cur = dummy;
        while (list1 != null || list2 != null) {
            if (list1 == null) {
                cur.next = list2;
                break;
            }
            if (list2 == null) {
                cur.next = list1;
                break;
            }
            if (list1.val < list2.val) {
                cur.next = list1;
                cur = cur.next;
                list1 = list1.next;
            } else {
                cur.next = list2;
                cur = cur.next;
                list2 = list2.next;
            }
        }
        return dummy.next;
    }
}

// time O(m+n), m and n are the linked lists' size
// space O(1)
// using linked list and sentinel node
```


## 📄 [B]linked-list\[B]linked-list\21-merge-two-sorted-lists.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        dummy, p1, p2 = ListNode(), list1, list2
        cur = dummy
        while p1 or p2:
            if p1 and p2 and p1.val < p2.val:
                cur.next = p1
                p1 = p1.next
                cur = cur.next
            elif p1 and p2:
                cur.next = p2
                p2 = p2.next
                cur = cur.next
            elif p1:
                cur.next = p1
                break
            else:
                cur.next = p2
                break
        return dummy.next

# time O(m+n), m and n are the linked lists' size
# space O(1)
# using linked list and sentinel node
```


## 📄 [B]linked-list\[B]linked-list\2130-maximum-twin-sum-of-a-linked-list.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def pairSum(self, head: Optional[ListNode]) -> int:
        
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        second_part_old_head = slow

        prev, cur = None, second_part_old_head
        while cur:
            nxt = cur.next
            cur.next = prev
            prev = cur
            cur = nxt
        second_part_new_head = prev

        res = float('-inf')
        p1, p2 = head, second_part_new_head
        while p1 and p2:
            res = max(res, p1.val + p2.val)
            p1 = p1.next
            p2 = p2.next
        return res
    
# time O(n)
# space O(1)
# using linked lsit and two pointers (utilize symmetry property) (finding middle, reversing, counting)
```


## 📄 [B]linked-list\[B]linked-list\234-palindrome-linked-list.java

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) {
            return true;
        }
        ListNode slow = head;
        ListNode fast = head;
        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        ListNode firstHalfTail = slow;
        ListNode secondHalfHead = firstHalfTail.next;

        ListNode prev = null;
        ListNode cur = secondHalfHead;
        while (cur != null) {
            ListNode nxt = cur.next;
            cur.next = prev;
            prev = cur;
            cur = nxt;
        }
        ListNode newSecondHalfHead = prev;
        ListNode p1 = head;
        ListNode p2 = newSecondHalfHead;
        while (p2 != null) {
            if (p1.val != p2.val) {
                return false;
            }
            p1 = p1.next;
            p2 = p2.next;
        }
        return true;
    }
}

// time O(n)
// space O(1)
// using linked lsit and two pointers (utilize symmetry property) (finding middle, reversing, comparing)
```


## 📄 [B]linked-list\[B]linked-list\234-palindrome-linked-list.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def isPalindrome(self, head: Optional[ListNode]) -> bool:
        if not head or not head.next:
            return head

        slow = head
        fast = head
        while fast.next and fast.next.next:
            slow = slow.next
            fast = fast.next.next
        first_half_tail = slow
        second_half_head = first_half_tail.next

        prev = None
        cur = second_half_head
        while cur:
            nxt = cur.next
            cur.next = prev
            prev = cur
            cur = nxt
        new_second_half_head = prev

        p1 = head
        p2 = new_second_half_head
        while p2:
            if p1.val != p2.val:
                return False
            p1 = p1.next
            p2 = p2.next
        return True
        
# time O(n)
# space O(1)
# using linked lsit and two pointers (utilize symmetry property) (finding middle, reversing, comparing)
```


## 📄 [B]linked-list\[B]linked-list\237-delete-node-in-a-linked-list.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def deleteNode(self, node):
        """
        :type node: ListNode
        :rtype: void Do not return anything, modify node in-place instead.
        """
        node.val = node.next.val
        node.next = node.next.next
        
# time O(1)
# space O(1)
# using linked list, changing val as changing node, just let node to be like next node
```


## 📄 [B]linked-list\[B]linked-list\24-swap-nodes-in-pairs.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head or not head.next:
            return head

        dummy = prev = ListNode(next=head)
        first = head
        second = head.next
        while first and second:
            nxt = second.next
            prev.next = second
            second.next = first
            first.next = nxt
            prev = first
            first = prev.next
            second = first.next if first else None
        return dummy.next
        
# time O(n)
# space O(1)
# using linked list and two pointers (prev and cur) and dummy node
```


## 📄 [B]linked-list\[B]linked-list\25-reverse-nodes-in-k-group.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        
        def rev(prev_nodes, old_head, old_tail, next_nodes):
            prev = None
            cur = old_head
            while cur and cur != next_nodes:
                nxt = cur.next
                cur.next = prev
                prev = cur
                cur = nxt
            new_head = prev
            prev_nodes.next = new_head
            new_tail = old_head
            new_tail.next = next_nodes
            return new_tail

        dummy = ListNode(next=head)
        total = 0
        prev_nodes = dummy
        old_head = head
        cur = head
        while cur:
            total += 1
            if total == 1:
                old_head = cur
            if total == k:
                new_tail = rev(prev_nodes, old_head, cur, cur.next)
                prev_nodes = new_tail
                cur = new_tail
                total = 0
            cur = cur.next
        return dummy.next
    
# time O(n)
# space O(1)
# using linked list and two pointers (prev and cur)
```


## 📄 [B]linked-list\[B]linked-list\328-odd-even-linked-list.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def oddEvenList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head or not head.next:
            return head

        odd_dummy = odd_cur = ListNode()
        even_dummy = even_cur = ListNode()
        cur = head
        isOdd = True
        while cur:
            if isOdd:
                odd_cur.next = cur
                odd_cur = odd_cur.next
            else:
                even_cur.next = cur
                even_cur = even_cur.next
            cur = cur.next
            isOdd = not isOdd
        odd_cur.next = even_dummy.next
        even_cur.next = None
        return odd_dummy.next
        
# time O(n), due to traverse
# space (1)
# using linked list and sentinel nodes and multi pointers
```


## 📄 [B]linked-list\[B]linked-list\369-plus-one-linked-list.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def plusOne(self, head: ListNode) -> ListNode:
        dummy = ListNode(val=1, next=head)
        cur = head
        non_nine = None
        while cur:
            if cur.val != 9:
                non_nine = cur
            cur = cur.next
        
        if not non_nine:
            cur = head
            while cur:
                cur.val = 0
                cur = cur.next
            return dummy
        
        non_nine.val += 1
        while non_nine.next:
            non_nine.next.val = 0
            non_nine = non_nine.next
        return dummy.next

# time O(n)
# space O(1)
# using linked list and math and senitel node
'''
1. 999 -> 1000
2. 997 -> 998
3. 979 -> 980
'''
```


## 📄 [B]linked-list\[B]linked-list\432-all-oone-data-structure.py

```py
class ListNode:
    def __init__(self, freq=- 1):
        self.freq = freq
        self.set = set()
        self.prev = None
        self.next = None

class Dll:
    def __init__(self):
        self.head = ListNode()
        self.tail = ListNode()
        self.head.next = self.tail
        self.tail.prev = self.head

    def remove(self, node):
        prev_node = node.prev
        next_node = node.next
        prev_node.next = next_node
        next_node.prev = prev_node
    
    def insert_first(self, node):
        prev_node = self.head
        next_node = self.head.next
        prev_node.next = node
        node.prev = prev_node
        node.next = next_node
        next_node.prev = node

    def insert_before(self, old_node, new_node):
        prev_node = old_node.prev
        node = new_node
        next_node = old_node
        prev_node.next = node
        node.prev = prev_node
        node.next = next_node
        next_node.prev = node

    def insert_after(self, old_node, new_node):
        prev_node = old_node
        node = new_node
        next_node = old_node.next
        prev_node.next = node
        node.prev = prev_node
        node.next = next_node
        next_node.prev = node
    
    def get_first_node(self):
        return self.head.next

    def get_last_node(self):
        return self.tail.prev

class AllOne:

    def __init__(self):
        self.dll = Dll()
        self.key_node = {}
        self.freq_node = {}

    def inc(self, key: str) -> None:
        if key not in self.key_node:
            if 1 not in self.freq_node:
                node = ListNode(1)
                node.set.add(key)
                self.dll.insert_first(node)
                self.key_node[key] = node
                self.freq_node[1] = node
            else:
                node = self.freq_node[1]
                node.set.add(key)
                self.key_node[key] = node
        else:
            old_node = self.key_node[key]
            old_freq = old_node.freq
            old_node.set.remove(key)
            new_freq = old_freq + 1

            if new_freq not in self.freq_node:
                node = ListNode(new_freq)
                node.set.add(key)
                self.dll.insert_after(old_node, node)
                self.key_node[key] = node
                self.freq_node[new_freq] = node
            else:
                node = self.freq_node[new_freq]
                node.set.add(key)
                self.key_node[key] = node

            if len(old_node.set) == 0:
                self.dll.remove(old_node)
                self.freq_node.pop(old_freq)
                

    def dec(self, key: str) -> None:
        old_node = self.key_node[key]
        old_freq = old_node.freq
        old_node.set.remove(key)
        new_freq = old_freq - 1

        if new_freq == 0:
            self.key_node.pop(key)
        elif new_freq not in self.freq_node:
            node = ListNode(new_freq)
            node.set.add(key)
            self.dll.insert_before(old_node, node)
            self.key_node[key] = node
            self.freq_node[new_freq] = node
        else:
            node = self.freq_node[new_freq]
            node.set.add(key)
            self.key_node[key] = node

        if len(old_node.set) == 0:
            self.dll.remove(old_node)
            self.freq_node.pop(old_freq)

    def getMaxKey(self) -> str:
        node = self.dll.get_last_node()
        if node.freq == - 1:
            return ""
        hashset = node.set
        res = hashset.pop()
        hashset.add(res)
        return res

    def getMinKey(self) -> str:
        node = self.dll.get_first_node()
        if node.freq == - 1:
            return ""
        hashset = node.set
        res = hashset.pop()
        hashset.add(res)
        return res

# Your AllOne object will be instantiated and called as such:
# obj = AllOne()
# obj.inc(key)
# obj.dec(key)
# param_3 = obj.getMaxKey()
# param_4 = obj.getMinKey()

# time O(1)
# space O(n)
# using linked list and dll and hashmap
'''
1. maintain key_node hashmap
2. maintain freq_node hashmap
3. maintain dll
'''
```


## 📄 [B]linked-list\[B]linked-list\460-lfu-cache.py

```py
class ListNode:
    def __init__(self, key=None, val=None, freq=None):
        self.key = key
        self.val = val
        self.freq = freq
        self.prev = None
        self.next = None

class Dll:
    def __init__(self):
        self.head = ListNode()
        self.tail = ListNode()
        self.head.next = self.tail
        self.tail.prev = self.head
        self.size = 0

    def append(self, node):
        prev_node = self.tail.prev
        next_node = self.tail
        prev_node.next = node
        node.prev = prev_node
        node.next = next_node
        next_node.prev = node
        self.size += 1
        return node

    def popleft(self):
        prev_node = self.head
        node = self.head.next
        next_node = node.next
        prev_node.next = next_node
        next_node.prev = prev_node
        self.size -= 1
        return node

    def remove(self, node):
        prev_node = node.prev
        next_node = node.next
        prev_node.next = next_node
        next_node.prev = prev_node
        self.size -= 1
        return node

    def is_empty(self):
        return self.size == 0

class LFUCache:

    def __init__(self, capacity: int):
        self.key_node = {}
        self.freq_dll = {}
        self.capacity = capacity
        self.min_freq = 0

    def get(self, key: int) -> int:
        if key not in self.key_node:
            return - 1
        node = self.key_node[key]
        self.add_freq(node)
        return node.val

    def put(self, key: int, value: int) -> None:
        if self.capacity == 0:
            return
        if key not in self.key_node:
            if len(self.key_node) == self.capacity:
                dll_for_pop = self.freq_dll[self.min_freq]
                remove_node = dll_for_pop.popleft()
                self.key_node.pop(remove_node.key)
                if dll_for_pop.is_empty():
                    self.freq_dll.pop(self.min_freq)
            self.min_freq = 1
            node = ListNode(key, value, 1)
            self.key_node[key] = node
            if 1 not in self.freq_dll:
                self.freq_dll[1] = Dll()
            dll = self.freq_dll[1]
            dll.append(node)
        else:
            node = self.key_node[key]
            node.val = value
            self.add_freq(node)

    def add_freq(self, node):
        old_freq = node.freq
        new_freq = old_freq + 1
        node.freq = new_freq
        old_dll = self.freq_dll[old_freq]
        old_dll.remove(node)
        if old_dll.is_empty():
            self.freq_dll.pop(old_freq)
            if old_freq == self.min_freq:
                self.min_freq = new_freq
        if new_freq not in self.freq_dll:
            self.freq_dll[new_freq] = Dll()
        new_dll = self.freq_dll[new_freq]
        new_dll.append(node)

# Your LFUCache object will be instantiated and called as such:
# obj = LFUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)

# time O(1)
# space O(capacity)
# using linked list and dll and hashmap
'''
1. maintain key_node hashmap
2. maintain freq_dll hashmap
3. maintain min_freq variable (modify when add new node or add freq for node)
4. maintain capacity
5. if get() or put(), dll of cur freq remove used node, and append node to tail in another dll which belongs freq + 1
6. if exceed capacity, dll of min_freq popleft the least recent used node and pop it from hashmap
'''
```


## 📄 [B]linked-list\[B]linked-list\61-rotate-list.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def rotateRight(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        if not head or not head.next:
            return head
        prev, cur, old_head = None, head, head
        count = 0
        while cur:
            count += 1
            prev = cur
            cur = cur.next
        old_tail = prev

        k %= count
        if k == 0:
            return head
            
        step = k + 1
        dummy = prev = cur = ListNode(next=head)
        while step:
            cur = cur.next
            step -= 1
        while cur:
            prev = prev.next
            cur = cur.next
        new_tail = prev
        new_head = prev.next
        old_tail.next = old_head
        new_tail.next = None
        return new_head
        
# time O(n)
# space O(1)
# using linked list and counting length and two pointers
```


## 📄 [B]linked-list\[B]linked-list\82-remove-duplicates-from-sorted-list-ii.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy = prev = ListNode(val=float('-inf'), next=head)
        cur = head
        while cur:
            if cur.next and cur.val == cur.next.val:
                while cur.next and cur.val == cur.next.val:
                    cur = cur.next
                prev.next = None
                cur = cur.next
            else:
                prev.next = cur
                prev = cur
                cur = cur.next
                
        return dummy.next
    
# time O(n)
# space O(1)
# using linked lsit and two pointers (prev and cur) and sentinel node
```


## 📄 [B]linked-list\[B]linked-list\83-remove-duplicates-from-sorted-list.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy = prev = ListNode(val= float('-inf'), next=head)
        cur = head
        while cur:
            if prev.val == cur.val:
                prev.next = None
                cur = cur.next
            else:
                prev.next = cur
                prev = cur
                cur = cur.next
        return dummy.next
    
# time O(n)
# space O(1)
# using linked list and two pointers (prev and cur)
```


## 📄 [B]linked-list\[B]linked-list\876-middle-of-the-linked-list.java

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
}

// time O(n), due to traverse
// space O(1)
// using linked list and two pointers (slow and fast)
/*
1. If there are two middle nodes, return the second middle node: use 'while fast and fast.next'
2. If there are two middle nodes, return the first middle node: use 'while fast.next and fast.next.next'
*/
```


## 📄 [B]linked-list\[B]linked-list\876-middle-of-the-linked-list.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head or not head.next:
            return head
        
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        return slow
        
# time O(n), due to traverse
# space O(1)
# using linked list and two pointers (slow and fast)
'''
1. If there are two middle nodes, return the second middle node: use 'while fast and fast.next'
2. If there are two middle nodes, return the first middle node: use 'while fast.next and fast.next.next'
'''
```


## 📄 [B]linked-list\[B]linked-list\92-reverse-linked-list-ii.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseBetween(self, head: Optional[ListNode], left: int, right: int) -> Optional[ListNode]:
        if not head or not head.next:
            return head

        dummy = ListNode(next=head)
        count = 0
        prev, cur = dummy, head
        prev_nodes, old_head, old_tail, next_nodes = None, None, None, None
        while cur:
            count += 1
            if left <= count <= right:
                if count == left:
                    prev_nodes = prev
                    old_head = cur
                if count == right:
                    old_tail = cur
                    next_nodes = cur.next
                nxt = cur.next
                cur.next = prev
                prev = cur
                cur = nxt
            else:
                prev = cur
                cur = cur.next
                
        prev_nodes.next = old_tail
        old_head.next = next_nodes
        return dummy.next
    
# time O(n)
# space O(1)
# using linked list and two pointers (prev and cur) and multi pointers
```


## 📄 [C]hashmap\[C]hashmap\1-two-sum.java

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> valToIdx = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (valToIdx.containsKey(target - nums[i])) {
                return new int[]{valToIdx.get(target - nums[i]), i};
            }
            valToIdx.put(nums[i], i);
        }
        return null;
    }
}

// time O(n), due to traverse
// space O(n), due to hashmap
// using hashmap and store val
```


## 📄 [C]hashmap\[C]hashmap\1-two-sum.py

```py
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        num_idx = {}
        for i, num in enumerate(nums):
            if target - num in num_idx:
                return [i, num_idx[target - num]]
            num_idx[num] = i
        return []
        
# time O(n), due to traverse
# space O(n), due to hashmap
# using hashmap and store val
```


## 📄 [C]hashmap\[C]hashmap\1010-pairs-of-songs-with-total-durations-divisible-by-60.py

```py
from collections import defaultdict
class Solution:
    def numPairsDivisibleBy60(self, time: List[int]) -> int:
        res = 0
        val_freq = defaultdict(int)
        for t in time:
            target = (60 - (t % 60)) % 60
            res += val_freq[target]
            val_freq[t % 60] += 1
        return res
        
# time O(n), due to traverse
# space O(1)
# using hashmap and store valid val’s freq for finding pairs
```


## 📄 [C]hashmap\[C]hashmap\1055-shortest-way-to-form-string.py

```py
from collections import defaultdict
class Solution:
    def shortestWay(self, source: str, target: str) -> int:
        schar_set = set(source)
        tchar_set = set(target)
        for c in tchar_set:
            if c not in schar_set:
                return - 1

        idx_nextindices = defaultdict(list)
        nextindices = [- 1 for _ in range(26)]
        for i in range(len(source) - 1, - 1, - 1):
            idx_nextindices[i] = nextindices[:]
            nextindices[ord(source[i]) - ord('a')] = i
        idx_nextindices[- 1] = nextindices[:]

        idx = - 1
        res = 1
        for c in target:
            idx = idx_nextindices[idx][ord(c) - ord('a')]
            if idx == - 1:
                idx = idx_nextindices[idx][ord(c) - ord('a')]
                res += 1
        return res
    
# time O(n + m)
# space O(n), due to hashmap
# using hashmap and snapshot of hashmap
```


## 📄 [C]hashmap\[C]hashmap\1152-analyze-user-website-visit-pattern.py

```py
from collections import defaultdict
class Solution:
    def mostVisitedPattern(self, username: List[str], timestamp: List[int], website: List[str]) -> List[str]:
        user_visits = defaultdict(list)
        for u, t, w in zip(username, timestamp, website):
            user_visits[u].append((t, w))

        pattern_freq = defaultdict(int)
        for u, visits in user_visits.items():
            sort_visits = sorted(visits)
            pattern_set = set()
            for i in range(len(sort_visits) - 2):
                for j in range(i + 1, len(sort_visits) - 1):
                    for k in range(j + 1, len(sort_visits)):
                        pattern = (sort_visits[i][1], sort_visits[j][1], sort_visits[k][1])
                        if pattern in pattern_set:
                            continue
                        pattern_set.add(pattern)
                        pattern_freq[pattern] += 1
        
        res = []
        max_freq = max(pattern_freq.values())
        for p, f in pattern_freq.items():
            if f == max_freq:
                res.append(p)
        res.sort()
        
        return list(res[0])
                        
# time O(m * n**3), m is the number of users and n is the number of websites, not count sorting the potential res
# space O(m * n**3), due to combinations
# using hashmap and store sth’s freq and sort and combinations
'''
1. same user can only contribute to one pattern once
'''
```


## 📄 [C]hashmap\[C]hashmap\128-longest-consecutive-sequence.java

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        HashSet<Integer> set = new HashSet<>();
        for (int num: nums) {
            set.add(num);
        }
        int res = 0;
        for (int num: nums) {
            if (set.contains(num - 1)) {
                continue;
            }
            int left = num;
            int right = num;
            if (!set.contains(left + res)) {
                continue;
            }
            while (set.contains(right + 1)) {
                right += 1;
            }
            res = Math.max(res, right - left + 1);
        }
        return res;
    }
}

// time O(n)
// sapce O(n)
// using hashmap and store val and hashset and pruning
/*
1. find every sequence's start point
*/
```


## 📄 [C]hashmap\[C]hashmap\128-longest-consecutive-sequence.py

```py
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        hashset = set(nums)

        res = 0
        for num in hashset:
            if num - 1 in hashset:
                continue
            if num + res not in hashset:
                continue
            cur = num
            while cur + 1 in hashset:
                cur = cur + 1
            res = max(res, cur - num + 1)
        return res
    
# time O(n)
# sapce O(n)
# using hashmap and store val and hashset and pruning
'''
1. find every sequence's start point
'''
```


## 📄 [C]hashmap\[C]hashmap\13-roman-to-integer.java

```java
class Solution {
    public int romanToInt(String s) {
        HashMap<Character, Integer> charToWeight = new HashMap<>();
        charToWeight.put('I', 1);
        charToWeight.put('V', 5);
        charToWeight.put('X', 10);
        charToWeight.put('L', 50);
        charToWeight.put('C', 100);
        charToWeight.put('D', 500);
        charToWeight.put('M', 1000);
        int res = 0;
        for (int i = 0; i < s.length(); i++) {
            Character c = s.charAt(i);
            int w = charToWeight.get(c);
            if (i + 1 < s.length() && charToWeight.get(s.charAt(i + 1)) > w) {
                res -= w;
            } else {
                res += w;
            }
        }
        return res;
    }
}

// time O(n), due to traverse, n is the length of input string
// space O(1), hashmap's size is O(7)
// using hashmap and store val
```


## 📄 [C]hashmap\[C]hashmap\13-roman-to-integer.py

```py
class Solution:
    def romanToInt(self, s: str) -> int:
        char_val = {'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000}
        res = 0
        for i, c in enumerate(s):
            if i + 1 < len(s) and char_val[c] < char_val[s[i + 1]]:
                res -= char_val[c]
            else:
                res += char_val[c]
        return res
        
# time O(n), due to traverse, n is the length of input string
# space O(1), hashmap's size is O(7)
# using hashmap and store val
```


## 📄 [C]hashmap\[C]hashmap\1805-number-of-different-integers-in-a-string.py

```py
class Solution:
    def numDifferentIntegers(self, word: str) -> int:
        hashset = set()
        string = ''
        for c in word + ' ':
            if c.isdigit():
                string += c
            else:
                if string:
                    hashset.add(int(string))
                    string = ''
        
        return len(hashset)
    
# time O(n)
# space O(n)
# using hashmap and store val and string and hashset
```


## 📄 [C]hashmap\[C]hashmap\2013-detect-squares.py

```py
from collections import defaultdict
class DetectSquares:

    def __init__(self):
        self.x_points = defaultdict(set)
        self.point_freq = defaultdict(int)

    def add(self, point: List[int]) -> None:
        self.x_points[point[0]].add((point[0], point[1]))
        self.point_freq[(point[0], point[1])] += 1

    def count(self, point: List[int]) -> int:
        res = 0
        points = self.x_points[point[0]]
        for x, y in points:
            if y == point[1]:
                continue
            edge = abs(y - point[1])
            res += self.point_freq[(x - edge, y)] * self.point_freq[(x - edge, point[1])] * self.point_freq[(x, y)]
            res += self.point_freq[(x + edge, y)] * self.point_freq[(x + edge, point[1])] * self.point_freq[(x, y)]
        return res

# Your DetectSquares object will be instantiated and called as such:
# obj = DetectSquares()
# obj.add(point)
# param_2 = obj.count(point)

# time O(1) for init and add(), O(n) for count
# space O(n)
# using hashmap and store valid val’s freq for finding pairs
```


## 📄 [C]hashmap\[C]hashmap\205-isomorphic-strings.java

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        HashMap<Character, Character> scToTc = new HashMap<>();
        HashMap<Character, Character> tcToSc = new HashMap<>();

        for (int i = 0; i < s.length(); i++) {
            Character sc = s.charAt(i);
            Character tc = t.charAt(i);
            if (!scToTc.containsKey(sc)) {
                scToTc.put(sc, tc);
            }
            if (!tcToSc.containsKey(tc)) {
                tcToSc.put(tc, sc);
            }
            if (!Objects.equals(sc, tcToSc.get(tc))) {
                return false;
            }
            if (!Objects.equals(tc, scToTc.get(sc))) {
                return false;
            }
        }
        return true;
    }
}

// time O(n), due to traverse
// space O(n), can be O(1) since char's number is limited
// using hashmap and build bijection mapping relation
```


## 📄 [C]hashmap\[C]hashmap\205-isomorphic-strings.py

```py
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        sc_tc = {}
        tc_sc = {}
        for sc, tc in zip(s, t):
            if sc not in sc_tc:
                sc_tc[sc] = tc
            if tc not in tc_sc:
                tc_sc[tc] = sc
            if sc_tc[sc] != tc or tc_sc[tc] != sc:
                return False
        return True
            
# time O(n), due to traverse
# space O(n), can be O(1) since char's number is limited
# using hashmap and build bijection mapping relation
```


## 📄 [C]hashmap\[C]hashmap\217-contains-duplicate.java

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashSet<Integer> set = new HashSet<>();
        for (int num: nums) {
            if (set.contains(num)) {
                return true;
            }
            set.add(num);
        }
        return false;
    }
}

// time O(n)
// space O(n)
// using hashmap and store val and hashset
```


## 📄 [C]hashmap\[C]hashmap\217-contains-duplicate.py

```py
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        hashset = set()
        for num in nums:
            if num in hashset:
                return True
            hashset.add(num)
        return False
    
# time O(n)
# space O(n)
# using hashmap and store val and hashset
```


## 📄 [C]hashmap\[C]hashmap\2342-max-sum-of-a-pair-with-equal-sum-of-digits.py

```py
class Solution:
    def maximumSum(self, nums: List[int]) -> int:
        total_num = {}
        res = - 1
        for num in nums:
            total, val = 0, num
            while val:
                d, m = divmod(val, 10)
                total += m
                val = d
            if total not in total_num:
                total_num[total] = num
            else:
                res = max(res, total_num[total] + num)
                total_num[total] = max(total_num[total], num)
        return res
    
# time O(nL), can treat L as constant
# space O(n)
# using hashmap and store val
```


## 📄 [C]hashmap\[C]hashmap\2364-count-number-of-bad-pairs.py

```py
from collections import defaultdict
class Solution:
    def countBadPairs(self, nums: List[int]) -> int:
        good_pairs = 0
        val_freq = defaultdict(int)
        for i, num in enumerate(nums):
            good_pairs += val_freq[num - i]
            val_freq[num - i] += 1
        total_pairs = (len(nums) * (len(nums) - 1)) // (2 * 1)
        return total_pairs - good_pairs

# time O(n)
# space O(n)
# using hashmap and store valid val’s freq for finding pairs
'''
1. j - i == nums[j] - nums[i] => nums[j] - j == nums[i] - i
'''
```


## 📄 [C]hashmap\[C]hashmap\242-valid-anagram.java

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }
        HashMap<Character, Integer> sCharToFreq = new HashMap<>();
        HashMap<Character, Integer> tCharToFreq = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            Character sc = s.charAt(i);
            sCharToFreq.compute(sc, (k, v) -> v == null ? 1 : v + 1);
            Character tc = t.charAt(i);
            tCharToFreq.compute(tc, (k, v) -> v == null ? 1 : v + 1);
        }
        for (Character c: sCharToFreq.keySet()) {
            if (!Objects.equals(sCharToFreq.get(c), tCharToFreq.get(c))) {
                return false;
            }
        }
        return true;
    }
}

// time O(n)
// space O(26) == O(1), constant
// using hashmap and store sth’s freq
```


## 📄 [C]hashmap\[C]hashmap\242-valid-anagram.py

```py
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        schar_freq = [0 for _ in range(26)]
        tchar_freq = [0 for _ in range(26)]
        for c in s:
            schar_freq[ord(c) - ord('a')] += 1
        for c in t:
            tchar_freq[ord(c) - ord('a')] += 1
        for i in range(26):
            if schar_freq[i] != tchar_freq[i]:
                return False
        return True

# time O(n)
# space O(26) == O(1), constant
# using hashmap and store sth’s freq
```


## 📄 [C]hashmap\[C]hashmap\2423-remove-letter-to-equalize-frequency.py

```py
from collections import defaultdict
class Solution:
    def equalFrequency(self, word: str) -> bool:
        char_freq = defaultdict(int)
        for c in word:
            char_freq[c] += 1
        freq_freq = defaultdict(int)
        for f in char_freq.values():
            freq_freq[f] += 1
        min_freqkey = min(freq_freq.keys())
        max_freqkey = max(freq_freq.keys())
        if len(freq_freq) == 1 and min_freqkey == 1:
            return True
        if len(freq_freq) == 1 and freq_freq[min_freqkey] == 1:
            return True
        if len(freq_freq) != 2:
            return False
        if min_freqkey == 1 and freq_freq[min_freqkey] == 1:
            return True
        if max_freqkey - min_freqkey == 1 and freq_freq[max_freqkey] == 1:
            return True
        return False

# time O(n)
# space O(1)
# using hashmap and store sth’s freq
'''
valid: 1 freq, all freq == 1
valid: 1 freq, (freq) count == 1
valid: 2 freq, small freq == 1 and (small freq) count == 1
valid: 2 freq, large freq == small freq + 1, and (large freq) count == 1
'''
```


## 📄 [C]hashmap\[C]hashmap\249-group-shifted-strings.py

```py
from collections import defaultdict
class Solution:
    def groupStrings(self, strings: List[str]) -> List[List[str]]:
        pattern_strings = defaultdict(list)

        for s in strings:
            new_s = ''
            shift = ord(s[0]) - ord('a')
            for c in s:
                new_c = chr((ord(c) - ord('a') - shift + 26) % 26 + ord('a'))
                new_s += new_c
            pattern_strings[new_s].append(s)

        return list(pattern_strings.values())

# time O(nL)
# space O(nL)
# using hashmap and store val
```


## 📄 [C]hashmap\[C]hashmap\266-palindrome-permutation.py

```py
from collections import defaultdict
class Solution:
    def canPermutePalindrome(self, s: str) -> bool:
        char_freq = defaultdict(int)
        for c in s:
            char_freq[c] += 1
        
        res = 0
        for c, f in char_freq.items():
            if f % 2 and res % 2:
                return False
            res += f
        return True
    
# time O(n)
# space O(1), due to the number of unique letters
# using hashmap and store sth’s freq
```


## 📄 [C]hashmap\[C]hashmap\299-bulls-and-cows.py

```py
from collections import defaultdict
class Solution:
    def getHint(self, secret: str, guess: str) -> str:
        char_freq = defaultdict(int)
        bulls, cows = 0, 0
        for sc, gc in zip(secret, guess):
            if sc == gc:
                bulls += 1
                continue
            if char_freq[sc] < 0:
                cows += 1
            if char_freq[gc] > 0:
                cows += 1
            char_freq[sc] += 1
            char_freq[gc] -= 1

        return f'{bulls}A{cows}B'
    
# time O(n)
# space O(1)
# using hashmap and store sth’s freq
'''
1. positive freq means it appeared more times in the secret
2. negative freq means it appeared more times in the guess
'''
```


## 📄 [C]hashmap\[C]hashmap\336-palindrome-pairs.py

```py
class Solution:
    def palindromePairs(self, words: List[str]) -> List[List[int]]:
        word_idx = {}
        for i, word in enumerate(words):
            word_idx[word] = i

        res = []
        for i, word in enumerate(words):
            rev_word = word[:: - 1]

            if word and word == rev_word and "" in word_idx:
                res.append([i, word_idx[""]])
                res.append([word_idx[""], i])

            if word and rev_word in word_idx and i != word_idx[rev_word]:
                res.append([i, word_idx[rev_word]])

            for cut in range(1, len(word)):
                prefix = word[0: cut]
                suffix = word[cut:]
                rev_prefix = prefix[:: - 1]
                rev_suffix = suffix[:: - 1]
                if suffix == rev_suffix and rev_prefix in word_idx:
                    res.append([i, word_idx[rev_prefix]])
                if prefix == rev_prefix and rev_suffix in word_idx:
                    res.append([word_idx[rev_suffix], i])
        
        return res
                    
# time O(n * (L**2))
# space O(nL), due to hashmap
# using hashmap and store val and palindrome
'''
we got 5 situations:
(notice word, prefix, suffix cannot be empty)
1. pal_word + ""
2. "" + pal_word
3. word + word[:: - 1]
4. prefix + pal_suffix + prefix[:: - 1]
5. suffix[:: - 1] + pal_prefix + suffix

how to check palindrome:
approach 1: use two pointers
approach 2: use word == word[:: - 1]
'''
```


## 📄 [C]hashmap\[C]hashmap\380-insert-delete-getrandom-o1.py

```py
import random
class RandomizedSet:

    def __init__(self):
        self.nums = []
        self.num_idx = {}

    def insert(self, val: int) -> bool:
        if val in self.num_idx:
            return False
        else:
            self.nums.append(val)
            self.num_idx[val] = len(self.nums) - 1 
            return True

    def remove(self, val: int) -> bool:
        if val in self.num_idx:
            old_val = val
            old_idx = self.num_idx[old_val]
            last_val = self.nums[- 1]
            last_idx = len(self.nums) - 1
            self.nums[old_idx] = last_val
            self.nums[last_idx] = old_val
            self.nums.pop()
            self.num_idx[last_val] = old_idx
            self.num_idx[old_val] = last_idx
            self.num_idx.pop(old_val)
            return True
        else:
            return False

    def getRandom(self) -> int:
        return random.choice(self.nums)

# Your RandomizedSet object will be instantiated and called as such:
# obj = RandomizedSet()
# param_1 = obj.insert(val)
# param_2 = obj.remove(val)
# param_3 = obj.getRandom()

# time O(1)
# space O(n), due to hashmap and list
# using hashmap and store val and list
```


## 📄 [C]hashmap\[C]hashmap\381-insert-delete-getrandom-o1-duplicates-allowed.py

```py
from collections import defaultdict
import random
class RandomizedCollection:
    def __init__(self):
        self.nums = []
        self.num_indices = defaultdict(set)

    def insert(self, val: int) -> bool:
        if val in self.num_indices:
            self.nums.append(val)
            self.num_indices[val].add(len(self.nums) - 1)
            return False
        else:
            self.nums.append(val)
            self.num_indices[val].add(len(self.nums) - 1)
            return True

    def remove(self, val: int) -> bool:
        if val in self.num_indices:
            old_val = val
            old_idx = self.num_indices[old_val].pop()
            self.num_indices[old_val].add(old_idx)
            last_val = self.nums[- 1]
            last_idx = len(self.nums) - 1

            self.nums[old_idx] = last_val
            self.nums[last_idx] = old_val
            self.nums.pop()
            
            if old_val != last_val:
                self.num_indices[last_val].remove(last_idx)
                self.num_indices[last_val].add(old_idx)
                self.num_indices[old_val].remove(old_idx)
            else:
                self.num_indices[last_val].remove(last_idx)

            if not self.num_indices[old_val]:
                self.num_indices.pop(old_val)
            
            return True
        else:
            return False

    def getRandom(self) -> int:
        return random.choice(self.nums)


# Your RandomizedCollection object will be instantiated and called as such:
# obj = RandomizedCollection()
# param_1 = obj.insert(val)
# param_2 = obj.remove(val)
# param_3 = obj.getRandom()

# time O(1)
# space O(n), due to hashmap and list
# using hashmap and store val and list and hashset
```


## 📄 [C]hashmap\[C]hashmap\383-ransom-note.java

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        HashMap<Character, Integer> rCharToFreq = new HashMap<>();
        HashMap<Character, Integer> mCharToFreq = new HashMap<>();
        for (int i = 0; i < ransomNote.length(); i++) {
            Character c = ransomNote.charAt(i);
            rCharToFreq.compute(c, (k, v) -> v == null ? 1 : v + 1);
        }
        for (int i = 0; i < magazine.length(); i++) {
            Character c = magazine.charAt(i);
            mCharToFreq.compute(c, (k, v) -> v == null ? 1 : v + 1);
        }
        for (Character c: rCharToFreq.keySet()) {
            if (mCharToFreq.containsKey(c) && rCharToFreq.get(c) <= mCharToFreq.get(c)) {
                continue;
            }
            return false;
        }
        return true;
    }
}

// time O(n+m)
// space O(26) == O(1), constant
// using hashmap and store sth’s freq
```


## 📄 [C]hashmap\[C]hashmap\383-ransom-note.py

```py
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        if len(ransomNote) > len(magazine):
            return False
        rchar_freq = [0 for _ in range(26)]
        mchar_freq = [0 for _ in range(26)]
        for c in ransomNote:
            rchar_freq[ord(c) - ord('a')] += 1
        for c in magazine:
            mchar_freq[ord(c) - ord('a')] += 1
        for i in range(26):
            if rchar_freq[i] > mchar_freq[i]:
                return False
        return True
    
# time O(n+m)
# space O(26) == O(1), constant
# using hashmap and store sth’s freq
```


## 📄 [C]hashmap\[C]hashmap\387-first-unique-character-in-a-string.java

```java
class Solution {
    public int firstUniqChar(String s) {
        HashMap<Character, Integer> charToFreq = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            charToFreq.compute(s.charAt(i), (k, v) -> v == null ? 1 : v + 1);
        }
        for (int i = 0; i < s.length(); i++) {
            if (Objects.equals(charToFreq.get(s.charAt(i)), 1)) {
                return i;
            }
        }
        return - 1;
    }
}

// time O(n), due to traverse twice
// space O(1), due to hashmap (26 letters)
// using hashmap and store sth’s freq
```


## 📄 [C]hashmap\[C]hashmap\387-first-unique-character-in-a-string.py

```py
from collections import defaultdict
class Solution:
    def firstUniqChar(self, s: str) -> int:
        char_freq = defaultdict(int)
        for c in s:
            char_freq[c] += 1
        for i, c in enumerate(s):
            if char_freq[c] == 1:
                return i
        return - 1
        
# time O(n), due to traverse twice
# space O(1), due to hashmap (26 letters)
# using hashmap and store sth’s freq
```


## 📄 [C]hashmap\[C]hashmap\409-longest-palindrome.java

```java
class Solution {
    public int longestPalindrome(String s) {
        HashMap<Character, Integer> charToFreq = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            Character c = s.charAt(i);
            charToFreq.compute(c, (k, v) -> v == null ? 1 : v + 1);
        }

        int res = 0;
        for (Map.Entry<Character, Integer> kv: charToFreq.entrySet()) {
            Character k = kv.getKey();
            Integer v = kv.getValue();
            if (res % 2 == 0) {
                res += v;
            } else {
                if (v % 2 == 1) {
                    v -= 1;
                }
                res += v;
            }
        }
        return res;
    }
}

// time O(n)
// space O(1)
// using hashmap and store sth’s freq
```


## 📄 [C]hashmap\[C]hashmap\409-longest-palindrome.py

```py
from collections import defaultdict
class Solution:
    def longestPalindrome(self, s: str) -> int:
        char_freq = defaultdict(int)
        for c in s:
            char_freq[c] += 1
        
        res = 0
        for f in char_freq.values():
            if res % 2:
                res += f - (f % 2)
            else:
                res += f
        return res
    
# time O(n)
# space O(1)
# using hashmap and store sth’s freq
```


## 📄 [C]hashmap\[C]hashmap\49-group-anagrams.java

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        HashMap<String, ArrayList<String>> patternToStrings = new HashMap<>();
        for (String s: strs) {
            int[] charToFreq = new int[26];
            for (int i = 0; i < s.length(); i++) {
                charToFreq[s.charAt(i) - 'a'] += 1;
            }
            StringBuffer sb = new StringBuffer();
            for (int i = 0; i < 26; i++) {
                sb.append("#");
                sb.append(charToFreq[i]);
            }
            patternToStrings.computeIfAbsent(sb.toString(), k -> new ArrayList<>()).add(s);
        }
        List<List<String>> res = new ArrayList<>();
        for (ArrayList<String> val: patternToStrings.values()) {
            res.add(val);
        }
        return res;
    }
}

// time O(nL)
// space O(nL)
// using hashmap and store sth’s freq
```


## 📄 [C]hashmap\[C]hashmap\49-group-anagrams.py

```py
from collections import defaultdict
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        pattern_words = defaultdict(list)
        for word in strs:
            char_freq = [0 for _ in range(26)]
            for c in word:
                char_freq[ord(c) - ord('a')] += 1
            pattern_words[tuple(char_freq)].append(word)
        return list(pattern_words.values())

# time O(nL)
# space O(nL)
# using hashmap and store sth’s freq
```


## 📄 [C]hashmap\[C]hashmap\609-find-duplicate-file-in-system.py

```py
from collections import defaultdict
class Solution:
    def findDuplicate(self, paths: List[str]) -> List[List[str]]:
        content_path = defaultdict(list)
        
        for p in paths:
            files = p.split(' ')
            root_path = files[0]
            for i in range(1, len(files)):
                data = files[i].split('(')
                file_path = data[0]
                content = data[1][: - 1]
                content_path[content].append(root_path + "/" + file_path)

        return [v for v in content_path.values() if len(v) > 1]

# time O(nL)
# space O(nL)
# using hashmap and store val and string
```


## 📄 [C]hashmap\[C]hashmap\705-design-hashset.py

```py
class ListNode:
    def __init__(self, val, next=None):
        self.val = val
        self.next = next

class MyHashSet:

    def __init__(self):
        self.hash = 1009
        self.buckets = [None for _ in range(self.hash)]

    def add(self, key: int) -> None:
        idx = key % self.hash
        if self.buckets[idx] != None:
            node = self.buckets[idx]
            prev, cur, find = self.check(key, node)
            if not find:
                self.buckets[idx] = ListNode(key, node)
        else:
            self.buckets[idx] = ListNode(key)

    def remove(self, key: int) -> None:
        idx = key % self.hash
        if self.buckets[idx] != None:
            node = self.buckets[idx]
            prev, cur, find = self.check(key, node)
            if find:
                if prev:
                    prev.next = cur.next
                else:
                    self.buckets[idx] = cur.next

    def contains(self, key: int) -> bool:
        idx = key % self.hash
        if self.buckets[idx] != None:
            node = self.buckets[idx]
            prev, cur, find = self.check(key, node)
            return find
        else:
            return False
        
    def check(self, val, node):
        prev, cur, find = None, node, False
        while cur:
            if cur.val == val:
                find = True
                break
            prev = cur
            cur = cur.next
        return prev, cur, find

# Your MyHashSet object will be instantiated and called as such:
# obj = MyHashSet()
# obj.add(key)
# obj.remove(key)
# param_3 = obj.contains(key)

# time O(n/k), k is the number of buckets, n/k is the length of linked list in bucket
# space O(n + k)
# using hahsmap and separate chaining and linked list and two pointers
```


## 📄 [C]hashmap\[C]hashmap\706-design-hashmap.py

```py
class ListNode:
    def __init__(self, key=None, val=None, next=None):
        self.key = key
        self.val = val
        self.next = next

class MyHashMap:

    def __init__(self):
        self.hash = 1009
        self.buckets = [None for _ in range(self.hash)]

    def put(self, key: int, value: int) -> None:
        idx = key % self.hash
        if self.buckets[idx] != None:
            node = self.buckets[idx]
            prev, cur, find = self.check(key, node)
            if find:
                cur.val = value
            else:
                self.buckets[idx] = ListNode(key, value, node)
        else:
            self.buckets[idx] = ListNode(key, value)

    def get(self, key: int) -> int:
        idx = key % self.hash
        if self.buckets[idx] != None:
            node = self.buckets[idx]
            prev, cur, find = self.check(key, node)
            if find:
                return cur.val
        return - 1

    def remove(self, key: int) -> None:
        idx = key % self.hash
        if self.buckets[idx] != None:
            node = self.buckets[idx]
            prev, cur, find = self.check(key, node)
            if find:
                if prev:
                    prev.next = cur.next
                else:
                    self.buckets[idx] = cur.next

    def check(self, key, node):
        prev, cur, find = None, node, False
        while cur:
            if cur.key == key:
                find = True
                break
            prev = cur
            cur = cur.next
        return prev, cur, find

# Your MyHashMap object will be instantiated and called as such:
# obj = MyHashMap()
# obj.put(key,value)
# param_2 = obj.get(key)
# obj.remove(key)

# time O(n/k), k is the number of buckets, n/k is the length of linked list in bucket
# space O(n + k)
# using hahsmap and separate chaining and linked list and two pointers
```


## 📄 [C]hashmap\[C]hashmap\734-sentence-similarity.py

```py
from collections import defaultdict
class Solution:
    def areSentencesSimilar(self, sentence1: List[str], sentence2: List[str], similarPairs: List[List[str]]) -> bool:
        if len(sentence1) != len(sentence2):
            return False

        word_simword = defaultdict(set)
        for w1, w2 in similarPairs:
            word_simword[w1].add(w2)

        for w1, w2 in zip(sentence1, sentence2):
            if w1 == w2 or w2 in word_simword[w1] or w1 in word_simword[w2]:
                continue
            else:
                return False
        return True
    
# time O((p + n) * L), L is the avg length of words
# space O(p), p is the length of pairs (also the hashmap's size)
# using hashmap and store val and hashset
```


## 📄 [C]hashmap\[C]hashmap\767-reorganize-string.py

```py
from collections import defaultdict
class Solution:
    def reorganizeString(self, s: str) -> str:
        char_freq = defaultdict(int)
        for c in s:
            char_freq[c] += 1

        char_with_max_freq = max(char_freq.keys(), key=char_freq.get)
        max_freq = char_freq[char_with_max_freq]
        if max_freq > (len(s) + 1) // 2:
            return ''

        res = [None for _ in range(len(s))]
        idx = 0

        def put(char, freq):
            nonlocal idx
            while freq:
                res[idx] = char
                freq -= 1
                idx += 2
                if idx >= len(res):
                    idx = 1
        
        put(char_with_max_freq, max_freq)
        
        for c, f in char_freq.items():
            if c != char_with_max_freq:
                put(c, f)

        return ''.join(res)
        
# time O(n)
# space O(n), due to output list
# using hashmap and store sth’s freq and greedy
'''
1. deal with max freq char first
'''
```


## 📄 [C]hashmap\[C]hashmap\819-most-common-word.py

```py
from collections import defaultdict
import string
class Solution:
    def mostCommonWord(self, paragraph: str, banned: List[str]) -> str:
        ban_set = set(banned)
        word_freq = defaultdict(int)
        word = ''
        res = ''
        res_freq = 0
        for c in paragraph + ' ':
            if c in string.ascii_letters:
                word += c.lower()
            elif word:
                if word in ban_set:
                    word = ''
                    continue
                word_freq[word] += 1
                if word_freq[word] > res_freq:
                    res = word
                    res_freq = word_freq[word]
                word = ''

        return res

# time O(n+m)
# space O(n+m)
# using hashmap and store sth’s freq
```


## 📄 [C]hashmap\[C]hashmap\828-count-unique-characters-of-all-substrings-of-a-given-string.py

```py
from collections import defaultdict
class Solution:
    def uniqueLetterString(self, s: str) -> int:
        char_leftappear = [None for _ in range(len(s))]
        leftappear = [- 1 for _ in range(26)]
        for i, c in enumerate(s):
            char_leftappear[i] = leftappear[:]
            leftappear[ord(c) - ord('A')] = i

        char_rightappear = [None for _ in range(len(s))]
        rightappear = [len(s) for _ in range(26)]
        for i in range(len(s) - 1, - 1, - 1):
            char_rightappear[i] = rightappear[:]
            rightappear[ord(s[i]) - ord('A')] = i
        
        res = 0
        for i, c in enumerate(s):
            left_bound = char_leftappear[i][ord(c) - ord('A')]
            left_choices = i - left_bound
            right_bound = char_rightappear[i][ord(c) - ord('A')] 
            right_choices = right_bound - i
            res += left_choices * right_choices

        return res

# time O(n)
# space O(n)
# using hashmap and snapshot of hashmap
'''
1. think about only consider one char, eg. "AXX'A'XA"
2. use list to sotre the snapshot of hashmap
3. subarray/substring can form by each element's left and right bound/choices
'''
```


## 📄 [C]hashmap\[C]hashmap\890-find-and-replace-pattern.py

```py
class Solution:
    def findAndReplacePattern(self, words: List[str], pattern: str) -> List[str]:
        
        def check(p, q):
            pc_qc = {}
            qc_pc = {}
            for pc, qc in zip(p, q):
                if pc not in pc_qc:
                    pc_qc[pc] = qc
                if qc not in qc_pc:
                    qc_pc[qc] = pc
                if pc_qc[pc] != qc or qc_pc[qc] != pc:
                    return False
            return True

        return [w for w in words if check(w, pattern)]
    
# time O(nL), n is the number of words
# space O(1), not counting output
# using hashmap and build bijection mapping relation
```


## 📄 [C]hashmap\[C]hashmap\953-verifying-an-alien-dictionary.py

```py
class Solution:
    def isAlienSorted(self, words: List[str], order: str) -> bool:
        char_val = {}
        for i, c in enumerate(order):
            char_val[c] = i

        for i in range(len(words)):
            if i + 1 < len(words):
                cur_word = words[i]
                next_word = words[i + 1]
                j = 0
                while j < len(cur_word) and j < len(next_word):
                    if char_val[cur_word[j]] < char_val[next_word[j]]:
                        break
                    elif char_val[cur_word[j]] == char_val[next_word[j]]:
                        j += 1
                        if j < len(cur_word) and j >= len(next_word):
                            return False
                    else:
                        return False
        return True
        
# time O(nL), n is the number of words and L is the average length of words
# space O(1), hashmap's size is 26
# using hashmap and store val
```


## 📄 [D]binary-search\[D]binary-search\1011-capacity-to-ship-packages-within-d-days.py

```py
class Solution:
    def shipWithinDays(self, weights: List[int], days: int) -> int:
        
        def valid(bound):
            total = 0
            day = 1
            for w in weights:
                if w > bound:
                    return False
                if total + w > bound:
                    total = w
                    day += 1
                else:
                    total += w
            return day <= days

        left, right, boundary = 1, sum(weights), - 1
        while left <= right:
            m = (left + right) // 2
            if valid(m):
                boundary = m
                right = m - 1
            else:
                left = m + 1
        return boundary

# time O(nlogm), n is the number of weights for the traversion's cost, and m is the sum of weights for binary search's cost
# space O(1)
# using binary search and search in sth’s range
```


## 📄 [D]binary-search\[D]binary-search\1062-longest-repeating-substring.py

```py
class Solution:
    def longestRepeatingSubstring(self, s: str) -> int:
        
        def valid(k):
            base = 27
            mod = 10**9 + 7
            hashval_set = set()
            hashval = 0
            remove_base = (base ** (k - 1)) % mod
            for i, c in enumerate(s):
                if i >= k:
                    hashval -= (remove_base * ord(s[i - k])) % mod
                hashval = (hashval * base + ord(c)) % mod
                if i >= k - 1:
                    if hashval in hashval_set:
                        return True
                    hashval_set.add(hashval)
            return False

        left, right, boundary = 1, len(s) - 1, 0
        while left <= right:
            m = (left + right) // 2
            if valid(m):
                boundary = m
                left = m + 1
            else:
                right = m - 1
        return boundary
    
# time O(nlogn), valid() costs O(n) by rolling hash method
# space O(n), due to list and hashset
# using binary search and search in sth’s range and rabin karp
```


## 📄 [D]binary-search\[D]binary-search\1201-ugly-number-iii.py

```py
from math import lcm
class Solution:
    def nthUglyNumber(self, n: int, a: int, b: int, c: int) -> int:
        
        def valid(val):
            return (val // a + val // b + val // c - val // lcm(a, b) - val // lcm(b, c) - val // lcm(c, a) + val // lcm(a, b, c)) >= n

        left, right, boundary = min(a, b, c), n * min(a, b, c), - 1
        while left <= right:
            m = (left + right) // 2
            if valid(m):
                boundary = m
                right = m - 1
            else:
                left = m + 1
        return boundary
    
# time O(log(n * min(a, b, c))), due to the search range of binary search
# space O(1)
# using binary search and search in sth’s range
```


## 📄 [D]binary-search\[D]binary-search\1428-leftmost-column-with-at-least-a-one.py

```py
# """
# This is BinaryMatrix's API interface.
# You should not implement it, or speculate about its implementation
# """
#class BinaryMatrix(object):
#    def get(self, row: int, col: int) -> int:
#    def dimensions(self) -> list[]:

class Solution:
    def leftMostColumnWithOne(self, binaryMatrix: 'BinaryMatrix') -> int:
        mat = binaryMatrix
        rows, cols = mat.dimensions()
        res = - 1
        row = 0
        while row < rows:
            left = 0
            right = res - 1 if res != - 1 else cols - 1
            while left <= right:
                m = (left + right) // 2
                if mat.get(row, m) == 1:
                    res = m
                    right = m - 1
                else:
                    left = m + 1
            row += 1
        return res
        
# time O(RlogC)
# space O(1)
# using binary search and search in a sorted array for most close val
```


## 📄 [D]binary-search\[D]binary-search\153-find-minimum-in-rotated-sorted-array.py

```py
class Solution:
    def findMin(self, nums: List[int]) -> int:
        left, right, boundary = 0, len(nums) - 1, len(nums) - 1
        while left <= right:
            m = (left + right) // 2
            if nums[m] < nums[boundary]:
                boundary = m
            if nums[m] > nums[right]:
                left = m + 1
            else:
                right = m - 1
        return nums[boundary]

# time O(logn)
# space O(1)
# using binary search and rotated sorted array
'''
notice above soltion depends on all elements are unique
if elements are not unique, then:

left, right, boundary = 0, len(nums) - 1, len(nums) - 1
while left <= right:
    m = (left + right) // 2
    if nums[m] < nums[boundary]:
        boundary = m
    if nums[m] > nums[right]:
        left = m + 1
    elif nums[m] < nums[right]:
        right = m - 1
    else:
        right -= 1
return nums[boundary]

# time O(n)
# space O(1)
# using binary search and rotated sorted array
'''
```


## 📄 [D]binary-search\[D]binary-search\162-find-peak-element.py

```py
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        left, right, boundary = 0, len(nums) - 2, len(nums) - 1
        while left <= right:
            m = (left + right) // 2
            if nums[m] > nums[m + 1]:
                boundary = m
                right = m - 1
            else:
                left = m + 1
        return boundary
    
# time O(logn), due to binary search
# space O(1)
# using binary search and use boundary to record
```


## 📄 [D]binary-search\[D]binary-search\222-count-complete-tree-nodes.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def countNodes(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        cur = root
        level = 0
        while cur:
            level += 1
            cur = cur.left

        def valid(idx):
            cur = root
            for i in range(level - 2, - 1, - 1):
                if idx & (1 << i):
                    cur = cur.right
                else:
                    cur = cur.left
            return cur != None
        
        left, right, boundary = 1 << (level - 1), (1 << level) - 1, - 1
        while left <= right:
            m = (left + right) // 2
            if valid(m):
                boundary = m
                left = m + 1
            else:
                right = m - 1
        return boundary
        
# time O(logn * logn)
# space O(1)
# using binary search and search in sth’s range and complete tree
'''
1. last level can have at most 2**(h-1) or 2**h - 2**(h-1) nodes
2. tree height in complete tree is logn
'''
```


## 📄 [D]binary-search\[D]binary-search\278-first-bad-version.java

```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int left = 1;
        int right = n;
        int boundary = - 1;
        while (left <= right) {
            int m = left + (right - left) / 2;
            if (isBadVersion(m)) {
                boundary = m;
                right = m - 1;
            } else {
                left = m + 1;
            }
        }
        return boundary;
    }
}

// time O(logn)
// space O(1)
// using binary search and search in sth’s range
```


## 📄 [D]binary-search\[D]binary-search\278-first-bad-version.py

```py
# The isBadVersion API is already defined for you.
# def isBadVersion(version: int) -> bool:

class Solution:
    def firstBadVersion(self, n: int) -> int:
        left, right, boundary = 1, n, - 1
        while left <= right:
            m = (left + right) // 2
            if isBadVersion(m):
                boundary = m
                right = m - 1
            else:
                left = m + 1
        return boundary
    
# time O(logn)
# space O(1)
# using binary search and search in sth’s range
```


## 📄 [D]binary-search\[D]binary-search\33-search-in-rotated-sorted-array.java

```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        int boundary = - 1;
        while (left <= right) {
            int m = left + (right - left) / 2;
            if (nums[m] == target) {
                boundary = m;
                break;
            }
            if (nums[m] > nums[right]) {
                if (nums[left] <= target && target < nums[m]) {
                    right = m - 1;
                } else {
                    left = m + 1;
                }
            } else {
                if (nums[m] < target && target <= nums[right]) {
                    left = m + 1;
                } else {
                    right = m - 1;
                }
            }
        }
        return boundary;
    }
}

// time O(logn)
// space O(1)
// using binary search and rotated sorted array
/*
1. compare to right ptr
2. if m ptr val larger than right ptr val, means the left side of m ptr has order
3. if m ptr val less than right ptr val, means the right side of m ptr has order
*/
```


## 📄 [D]binary-search\[D]binary-search\33-search-in-rotated-sorted-array.py

```py
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right, boundary = 0, len(nums) - 1, - 1
        while left <= right:
            m = (left + right) // 2
            if nums[m] == target:
                boundary = m
                break
            elif nums[m] > nums[right]:
                if nums[left] <= target < nums[m]:
                    right = m - 1
                else:
                    left = m + 1
            else:
                if nums[m] < target <= nums[right]:
                    left = m + 1
                else:
                    right = m - 1
        return boundary
        
# time O(logn)
# space O(1)
# using binary search and rotated sorted array
'''
1. compare to right ptr
2. if m ptr val larger than right ptr val, means the left side of m ptr has order
3. if m ptr val less than right ptr val, means the right side of m ptr has order
'''
```


## 📄 [D]binary-search\[D]binary-search\34-find-first-and-last-position-of-element-in-sorted-array.java

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] res = new int[2];

        int left = 0;
        int right = nums.length - 1;
        int boundary = - 1;
        while (left <= right) {
            int m = left + (right - left) / 2;
            if (nums[m] == target) {
                boundary = m;
                right = m - 1;
            } else if (nums[m] > target) {
                right = m - 1;
            } else {
                left = m + 1;
            }
        }
        res[0] = boundary;

        left = 0;
        right = nums.length - 1;
        boundary = - 1;
        while (left <= right) {
            int m = left + (right - left) / 2;
            if (nums[m] == target) {
                boundary = m;
                left = m + 1;
            } else if (nums[m] > target) {
                right = m - 1;
            } else {
                left = m + 1;
            }
        }
        res[1] = boundary;
        return res;
    }
}

// time O(logn)
// space O(1)
// using binary search and search in a sorted array for specific val
```


## 📄 [D]binary-search\[D]binary-search\34-find-first-and-last-position-of-element-in-sorted-array.py

```py
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        res = []
        left, right, boundary = 0, len(nums) - 1, - 1
        while left <= right:
            m = (left + right) // 2
            if nums[m] == target:
                boundary = m
                right = m - 1
            elif nums[m] > target:
                right = m - 1
            else:
                left = m + 1
        res.append(boundary)

        left, right, boundary = 0, len(nums) - 1, - 1
        while left <= right:
            m = (left + right) // 2
            if nums[m] == target:
                boundary = m
                left = m + 1
            elif nums[m] > target:
                right = m - 1
            else:
                left = m + 1
        res.append(boundary)
        return res
    
# time O(logn)
# space O(1)
# using binary search and search in a sorted array for specific val
```


## 📄 [D]binary-search\[D]binary-search\35-search-insert-position.java

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        int boundary = - 1;
        while (left <= right) {
            int m = left + (right - left) / 2;
            if (nums[m] >= target) {
                boundary = m;
                right = m - 1;
            } else {
                left = m + 1;
            }
        }
        return boundary != - 1 ? boundary : nums.length;
    }
}

// time O(logn)
// space O(1)
// using binary search and search in a sorted array for most close val
```


## 📄 [D]binary-search\[D]binary-search\35-search-insert-position.py

```py
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left, right, boundary = 0, len(nums) - 1, len(nums)
        while left <= right:
            m = (left + right) // 2
            if nums[m] >= target:
                boundary = m
                right = m - 1
            else:
                left = m + 1
        return boundary

# time O(logn)
# space O(1)
# using binary search and search in a sorted array for most close val
```


## 📄 [D]binary-search\[D]binary-search\367-valid-perfect-square.py

```py
class Solution:
    def isPerfectSquare(self, num: int) -> bool:
        left, right, boundary = 1, num, - 1
        while left <= right:
            m = (left + right) // 2
            if m ** 2 == num:
                boundary = m
                break
            elif m ** 2 < num:
                left = m + 1
            else:
                right = m - 1
        return boundary != - 1
    
# time O(logn)
# space O(1)
# using binary search and search in a sorted array for specific val
```


## 📄 [D]binary-search\[D]binary-search\4-median-of-two-sorted-arrays.py

```py
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
       
        A, B = nums1, nums2
        if len(A) > len(B):
            A, B = B, A

        total = len(A) + len(B)
        
        left, right = 0, len(A)
        while left <= right:
            m = (left + right) // 2
            lenA = m
            lenB = total // 2 - lenA
            leftA = A[lenA - 1] if lenA - 1 >= 0 else float('-inf')
            rightA = A[lenA] if lenA < len(A) else float('inf')
            leftB = B[lenB - 1] if lenB - 1 >= 0 else float('-inf')
            rightB = B[lenB] if lenB < len(B) else float('inf')
            if leftA > rightB:
                right = m - 1
            elif leftB > rightA:
                left = m + 1
            else:
                break

        return min(rightA, rightB) if total % 2 else (max(leftA, leftB) + min(rightA, rightB)) / 2

# time O(log(min(m, n))), due to binary search
# space O(1)
# using binary search and search in sth’s range
'''
1. median can divide a sorted array(listA + listB) to two part with same length
2. use binary search to find the length of listA to contribute into the first part of sorted array, 
   will get the length of listB to contribute into the first part of sorted array at the same time
3. then we use these two length to get the cut points inside listA and listB, 
   will get 4 nums before/after the cut points
4. compare them, if the condition is not correct, 
   then keep search the correct length of listA to contribute into the first part of sorted array
5. if condition is correct, just deal with two situation of getting median
'''
```


## 📄 [D]binary-search\[D]binary-search\528-random-pick-with-weight.py

```py
import random
class Solution:

    def __init__(self, w: List[int]):
        self.prefix = [0 for _ in range(len(w) + 1)]
        total = 0
        for i, weight in enumerate(w):
            total += weight
            self.prefix[i + 1] = total

    def pickIndex(self) -> int:
        target = random.randint(1, self.prefix[- 1])
        left, right, boundary = 1, len(self.prefix) - 1, - 1
        while left <= right:
            m = (left + right) // 2
            if self.prefix[m] >= target:
                boundary = m
                right = m - 1
            else:
                left = m + 1
        return boundary - 1

# Your Solution object will be instantiated and called as such:
# obj = Solution(w)
# param_1 = obj.pickIndex()

# time O(logn), for pickIndex() using binary search and initiation is O(n) due to prefix sum list
# space O(n), due to prefix sum list
# using binary search and search in a sorted array for most close val and prefix sum and random

'''
nums = [2, 8, 5]
prefix = [0, 2, 10, 15]
[1 2] [3 4 5 6 7 8 9 10] [11 12 13 14 15]
'''
```


## 📄 [D]binary-search\[D]binary-search\658-find-k-closest-elements.py

```py
class Solution:
    def findClosestElements(self, arr: List[int], k: int, x: int) -> List[int]:
        
        left, right, boundary = 0, len(arr) - k - 1, len(arr) - k
        while left <= right:
            m = (left + right) // 2
            if arr[m] > x:
                boundary = m
                right = m - 1
            elif arr[m + k] < x:
                left = m + 1
            elif abs(arr[m] - x) <= abs(arr[m + k] - x):
                boundary = m
                right = m - 1
            else:
                left = m + 1
        return arr[boundary: boundary + k]

# time O(log(n - k) + k)
# space O(1), not counting output
# using binary search and use boundary to record
'''
1. make sure to record the rightest choice as first potential res
2. use binary search to find left bound of subarray which is k length
3. if 'mid' is a better choice, then record it and shrink the search range
   (if any choice is better than 'mid', then we can not record it)

4. there are 3 scenarios:

x O O O O O O O O O O  
   [our subarray]      (x is in our left side)

O O O O O O O O O O x  
   [our subarray]      (x is in our right side)

O O O O O x O O O O O
   [our subarray]      (x is inside our subarray)

5. how to decide:

 X                     (x = 5)
[5, 15, 20, 22, 23, 50]
            E   E   E  (begin)
    m   E   E          (1st branch, record it, then keep find LEFT side)

                    X  (x = 50)
[5, 15, 20, 22, 23, 50]
            E   E   E  (begin)
    m   E   E          (2nd branch)
    O   O   O            (choice 1)
        O   O   O        (choice 2 won, so go find RIGHT side)

        X              (x = 20)
[5, 15, 20, 22, 23, 50]
            E   E   E  (begin)
    m   E   E          (3rd branch)
    O   O   O            (choice 1 won, record it, then keep find LEFT side)
        O   O   O        (choice 2)

            X          (x = 22)
[5, 15, 20, 22, 23, 50]
            E   E   E  (begin)
    m   E   E          (3rd branch)
    O   O   O            (choice 1)
        O   O   O        (choice 2 won, so go to 4th branch (go find RIGHT side))
'''
```


## 📄 [D]binary-search\[D]binary-search\702-search-in-a-sorted-array-of-unknown-size.py

```py
# """
# This is ArrayReader's API interface.
# You should not implement it, or speculate about its implementation
# """
#class ArrayReader:
#    def get(self, index: int) -> int:

class Solution:
    def search(self, reader: 'ArrayReader', target: int) -> int:
        left, right, boundary = 0, target - reader.get(0), - 1
        while left <= right:
            m = (left + right) // 2
            val = reader.get(m)
            if val == 2** 31 - 1:
                right = m - 1
            elif val > target:
                right = m - 1
            elif val == target:
                boundary = m
                break
            else:
                left = m + 1
        return boundary
    
# time O(logn)
# space O(1)
# using binary search and search in a sorted array for specific val
'''
1. notice that problem says the array contains unique elements
'''
```


## 📄 [D]binary-search\[D]binary-search\704-binary-search.java

```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        int boundary = - 1;
        while (left <= right) {
            int m = left + (right - left) / 2;
            if (nums[m] == target) {
                boundary = m;
                break;
            } else if (nums[m] > target) {
                right = m - 1;
            } else {
                left = m + 1;
            }
        }
        return boundary;
    }
}

// time O(logn), n is the length of nums
// space O(1)
// using binary search and search in a sorted array for specific val
```


## 📄 [D]binary-search\[D]binary-search\704-binary-search.py

```py
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right, boundary = 0, len(nums) - 1, - 1
        while left <= right:
            m = (left + right) // 2
            if nums[m] == target:
                boundary = m
                break
            elif nums[m] < target:
                left = m + 1
            else:
                right = m - 1
        return boundary
    
# time O(logn), n is the length of nums
# space O(1)
# using binary search and search in a sorted array for specific val
```


## 📄 [D]binary-search\[D]binary-search\719-find-k-th-smallest-pair-distance.py

```py
class Solution:
    def smallestDistancePair(self, nums: List[int], k: int) -> int:
        
        nums.sort()

        def valid(diff):
            pairs = 0
            left = 0
            for right in range(len(nums)):
                while nums[right] - nums[left] > diff:
                    left += 1
                left_choices = right - left
                right_choices = 1
                pairs += left_choices * right_choices
            return pairs >= k

        left, right, boundary = 0, max(nums) - min(nums), - 1
        while left <= right:
            m = (left + right) // 2
            if valid(m):
                boundary = m
                right = m - 1
            else:
                left = m + 1
        return boundary
    
# time O(nlogn + nlogD), D is the max distance in nums
# space O(1)
# using binary search and search in sth’s range and sort and sliding window
```


## 📄 [D]binary-search\[D]binary-search\74-search-a-2d-matrix.java

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int rows = matrix.length;
        int cols = matrix[0].length;
        int left = 0;
        int right = rows * cols - 1;
        while (left <= right) {
            int m = left + (right - left) / 2;
            int r = m / cols;
            int c = m % cols;
            if (matrix[r][c] > target) {
                right = m - 1;
            } else if (matrix[r][c] == target) {
                return true;
            } else {
                left = m + 1;
            }
        }
        return false;
    }
}

// time O(log(mn))
// space O(1)
// using binary search and search in a sorted array for specific val
```


## 📄 [D]binary-search\[D]binary-search\74-search-a-2d-matrix.py

```py
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        rows, cols = len(matrix), len(matrix[0])

        def get_num(idx):
            r, c = divmod(idx, cols)
            return matrix[r][c]

        left, right, boundary = 0, rows * cols - 1, - 1
        while left <= right:
            m = (left + right) // 2
            num = get_num(m)
            if num == target:
                boundary = m
                break
            elif num > target:
                right = m - 1
            else:
                left = m + 1
        return boundary != - 1
    
# time O(log(mn))
# space O(1)
# using binary search and search in a sorted array for specific val
```


## 📄 [D]binary-search\[D]binary-search\744-find-smallest-letter-greater-than-target.py

```py
class Solution:
    def nextGreatestLetter(self, letters: List[str], target: str) -> str:
        left, right, boundary = 0, len(letters) - 1, 0
        while left <= right:
            m = (left + right) // 2
            if letters[m] > target:
                boundary = m
                right = m - 1
            else:
                left = m + 1
        return letters[boundary]

# time O(logn), due to binary search
# space O(1)
# using binary search and search in a sorted array for most close val
```


## 📄 [D]binary-search\[D]binary-search\81-search-in-rotated-sorted-array-ii.py

```py
class Solution:
    def search(self, nums: List[int], target: int) -> bool:
        left, right, boundary = 0, len(nums) - 1, - 1
        while left <= right:
            m = (left + right) // 2
            if nums[m] == target:
                boundary = m
                break
            elif nums[m] > nums[right]:
                if nums[left] <= target < nums[m]:
                    right = m - 1
                else:
                    left = m + 1
            elif nums[m] < nums[right]:
                if nums[m] < target <= nums[right]:
                    left = m + 1
                else:
                    right = m - 1
            else:
                right -= 1
        return True if boundary != - 1 else False

# time O(n), best case O(logn)
# space O(1)
# using binary search and rotated sorted array
'''
1. if we cannot decide which side could be sorted, we can only wipe out one element
2. think about [1,1,1,2,1]
'''
```


## 📄 [D]binary-search\[D]binary-search\852-peak-index-in-a-mountain-array.py

```py
class Solution:
    def peakIndexInMountainArray(self, arr: List[int]) -> int:
        
        left, right, boundary = 1, len(arr) - 2, - 1
        while left <= right:
            m = (left + right) // 2
            if arr[m - 1] < arr[m]:
                boundary = m
                left = m + 1
            else:
                right = m - 1
        return boundary

# time O(logn), due to binary search
# space O(1)
# using binary search and use boundary to record
```


## 📄 [D]binary-search\[D]binary-search\875-koko-eating-bananas.py

```py
from math import ceil
class Solution:
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        
        def valid(speed):
            hour = 0
            for p in piles:
                hour += ceil(p / speed)
            return hour <= h
        
        left, right, boundary = 1, sum(piles), - 1
        while left <= right:
            m = (left + right) // 2
            if valid(m):
                boundary = m
                right = m - 1
            else:
                left = m + 1
        return boundary
    
# time O(nlogm), n is the number of piles and m is the size of max pile 
# space O(1)
# using binary search and search in sth’s range
```


## 📄 [D]binary-search\[D]binary-search\878-nth-magical-number.py

```py
from math import lcm
class Solution:
    def nthMagicalNumber(self, n: int, a: int, b: int) -> int:
        
        def valid(val):
            l = lcm(a, b)
            return (val // a + val // b - val // l) >= n

        left, right, boundary = min(a, b), n * min(a, b), - 1
        while left <= right:
            m = (left + right) // 2
            if valid(m):
                boundary = m
                right = m - 1
            else:
                left = m + 1
        return boundary % (10**9 + 7)

# time O(log(min(a, b)*n))
# space O(1)
# using binary search and search in sth’s range
```


## 📄 [D]binary-search\[D]binary-search\981-time-based-key-value-store.java

```java
class TimeMap {
    HashMap<String, ArrayList<Pair>> map;

    record Pair(String value, int timestamp) { }

    public TimeMap() {
        map = new HashMap<>();
    }
    
    public void set(String key, String value, int timestamp) {
        map.computeIfAbsent(key, k -> new ArrayList<>()).add(new Pair(value, timestamp));
    }
    
    public String get(String key, int timestamp) {
        if (!map.containsKey(key)) {
            return "";
        }
        ArrayList<Pair> list = map.get(key);
        int left = 0;
        int right = list.size() - 1;
        int boundary = - 1;
        while (left <= right) {
            int m = left + (right - left) / 2;
            if (list.get(m).timestamp <= timestamp) {
                boundary = m;
                left = m + 1;
            } else {
                right = m - 1;
            }
        }
        if (boundary == - 1) {
            return "";
        }
        return list.get(boundary).value;
    }
}

/**
* Your TimeMap object will be instantiated and called as such:
* TimeMap obj = new TimeMap();
* obj.set(key,value,timestamp);
* String param_2 = obj.get(key,timestamp);
*/

// time O(logn) for get()
// space O(n), due to hashmap, n is the number of calling set()
// using binary search and search in a sorted array for most close val and hashmap
```


## 📄 [D]binary-search\[D]binary-search\981-time-based-key-value-store.py

```py
from collections import defaultdict
class TimeMap:

    def __init__(self):
        self.store = defaultdict(list)

    def set(self, key: str, value: str, timestamp: int) -> None:
        self.store[key].append((value, timestamp))

    def get(self, key: str, timestamp: int) -> str:
        if key not in self.store:
            return ''
        vals = self.store[key]
        left, right, boundary = 0, len(vals) - 1, - 1
        while left <= right:
            m = (left + right) // 2
            if vals[m][1] <= timestamp:
                boundary = m
                left = m + 1
            else:
                right = m - 1
        return vals[boundary][0] if boundary != - 1 else ''

# Your TimeMap object will be instantiated and called as such:
# obj = TimeMap()
# obj.set(key,value,timestamp)
# param_2 = obj.get(key,timestamp)

# time O(logn) for get()
# space O(n), due to hashmap, n is the number of calling set()
# using binary search and search in a sorted array for most close val and hashmap
```


## 📄 [E]heap\[E]heap\1094-car-pooling.py

```py
from heapq import *
class Solution:
    def carPooling(self, trips: List[List[int]], capacity: int) -> bool:
        trips.sort(key = lambda x: x[1])
        
        seats = capacity
        heap = []
        for p, s, e in trips:
            while heap and heap[0][0] <= s:
                prev_e, prev_p = heappop(heap)
                seats += prev_p
            if seats < p:
                return False
            heappush(heap, (e, p))
            seats -= p
        return True
        
# time O(nlogn), due to sort, and traverse and perform heap operations
# space O(n), due to heap
# using heap and storing and popping out elements and sort
'''
1. sort by start time
2. store (end, passengers) in heap
3. when new passengers come, let old passengers leave (with smallest end time)
'''
```


## 📄 [E]heap\[E]heap\1235-maximum-profit-in-job-scheduling.py

```py
from heapq import *
class Solution:
    def jobScheduling(self, startTime: List[int], endTime: List[int], profit: List[int]) -> int:
        jobs = [(s, e, p) for s, e, p in zip(startTime, endTime, profit)]
        jobs.sort()

        heap = []
        prev_best = 0
        all_time_best = 0
        for s, e, p in jobs:
            while heap and heap[0][0] <= s:
                _, prev_p = heappop(heap)
                prev_best = max(prev_best, prev_p)
            heappush(heap, (e, prev_best + p))
            all_time_best = max(all_time_best, prev_best + p)
        return all_time_best
        
# time O(nlogn), due to heap operation is O(logn) and sort is O(nlogn)
# space O(n), due to heap
# using heap and greedily schedule tasks (start/end/val) and sort and greedy
'''
- sort every task by their start time
- use heap to quickly find the most recent finished task according to cur task
- use pop out elements to keep recording the previous best result
  - the previous best result is according to cur task (also applicable for future tasks to use)
- push the cur end time and cur result in heap for future tasks
  - when pushing also treat this profit as a candidate of best result
  - we need to keep recording the all time best result
'''
```


## 📄 [E]heap\[E]heap\1383-maximum-performance-of-a-team.py

```py
from heapq import *
class Solution:
    def maxPerformance(self, n: int, speed: List[int], efficiency: List[int], k: int) -> int:
        
        engineers = [(s, e) for s, e in zip(speed, efficiency)]
        engineers.sort(key = lambda x: - x[1])

        res = 0
        total = 0
        heap = []
        for s, e in engineers:
            total += s
            heappush(heap, s)
            if len(heap) > k:
                total -= heappop(heap)
            res = max(res, total * e)

        return res % (10**9+7)
        
# time O(nlogn)
# space O(n + k)
# using heap and storing and popping out elements and sort and greedy
'''
two factors in problem, need to handle ony by one
1. we traverse every possible team effi (from high to low), and keep recording the best perf
2. we handle the effi factor by sort, so we can guarantee the effi we use is monotonic dec
3. we handle the spee factor by heap, so we can only store the higher spee and pop the smallest
'''
```


## 📄 [E]heap\[E]heap\1705-maximum-number-of-eaten-apples.py

```py
from heapq import *
class Solution:
    def eatenApples(self, apples: List[int], days: List[int]) -> int:
        heap = []
        res = 0
        for i in range(len(apples)):
            while heap and heap[0][0] <= i:
                heappop(heap)
            if apples[i] != 0:
                heappush(heap, [i + days[i], apples[i]])
            if heap and heap[0][1] > 0:
                res += 1
                heap[0][1] -= 1
                if heap[0][1] == 0:
                    heappop(heap)

        cur = len(apples)
        while heap:
            while heap and heap[0][0] <= cur:
                heappop(heap)
            if heap:
                end, count = heappop(heap)
                res += min(end - cur, count)
                cur += min(end - cur, count)

        return res
    
# time O(nlogn)
# space O(n)
# using heap and storing and popping out elements
```


## 📄 [E]heap\[E]heap\1792-maximum-average-pass-ratio.py

```py
from heapq import *
class Solution:
    def maxAverageRatio(self, classes: List[List[int]], extraStudents: int) -> float:
        heap = [(-((p+1)/(t+1) - p/t), p, t) for p, t in classes]
        heapify(heap)

        while extraStudents:
            _, p, t = heappop(heap)
            heappush(heap, (-((p+2)/(t+2) - (p+1)/(t+1)), p + 1, t + 1))
            extraStudents -= 1
        
        ratio = 0
        for _, p, t in heap:
            ratio += p/t
        return ratio / len(classes)

# time O(n + mlogn)
# space O(n)
# using heap and storing and popping out elements
```


## 📄 [E]heap\[E]heap\2008-maximum-earnings-from-taxi.py

```py
from heapq import *
class Solution:
    def maxTaxiEarnings(self, n: int, rides: List[List[int]]) -> int:
        rides.sort()

        heap = []
        prev_best = 0
        all_time_best = 0
        for s, e, t in rides:
            while heap and heap[0][0] <= s:
                prev_end, prev_profit = heappop(heap)
                prev_best = max(prev_best, prev_profit)
            heappush(heap, (e, prev_best + e - s + t))
            all_time_best = max(all_time_best, prev_best + e - s + t)
        return all_time_best

# time O(nlogn), due to heap operation is O(logn) and sort is O(nlogn)
# space O(n), due to heap
# using heap and greedily schedule tasks (start/end/val) and sort and greedy
```


## 📄 [E]heap\[E]heap\2054-two-best-non-overlapping-events.py

```py
from heapq import *
class Solution:
    def maxTwoEvents(self, events: List[List[int]]) -> int:
        events.sort()
        heap = []
        prev_best = 0
        all_time_best = 0
        for s, e, v in events:
            while heap and heap[0][0] < s:
                prev_end, prev_profit, event_count = heappop(heap)
                if event_count == 1:
                    prev_best = max(prev_best, prev_profit)
            heappush(heap, (e, v, 1))
            heappush(heap, (e, prev_best + v, 2))
            all_time_best = max(all_time_best, prev_best + v)
        return all_time_best
    
# time O(nlogn), due to heap operation is O(logn) and sort is O(nlogn)
# space O(n), due to heap
# using heap and greedily schedule tasks (start/end/val) and sort and greedy
```


## 📄 [E]heap\[E]heap\23-merge-k-sorted-lists.py

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
from heapq import *
class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        heap = []
        for i, node in enumerate(lists):
            if node:
                heappush(heap, (node.val, i))
        dummy = cur = ListNode()
        while heap:
            val, i = heappop(heap)
            cur.next = ListNode(val)
            cur = cur.next
            if lists[i].next:
                lists[i] = lists[i].next
                heappush(heap, (lists[i].val, i))

        return dummy.next

# time O(nlogk), n is the number of nodes, k is the number of lists
# space O(k)
# using heap and k way merge problem and linked list
```


## 📄 [E]heap\[E]heap\264-ugly-number-ii.py

```py
from heapq import *
class Solution:
    def nthUglyNumber(self, n: int) -> int:
        res = [1]
        primes = [2, 3, 5]
        heap = [(res[0] * primes[i], 0, i) for i in range(len(primes))]
        while len(res) < n:
            val, res_idx, primes_idx = heappop(heap)
            if val > res[- 1]:
                res.append(val)
            heappush(heap, (res[res_idx + 1] * primes[primes_idx], res_idx + 1, primes_idx))
        return res[- 1]
    
# time O(nklog(k)), k is 3
# space O(n + k)
# using heap and k way merge problem
'''
1. imagine 3 virtual sorted lists to do merging
2. we dynamically generate these 3 sorted lists from our current res list
'''
```


## 📄 [E]heap\[E]heap\295-find-median-from-data-stream.py

```py
from heapq import *
class MedianFinder:

    def __init__(self):
        self.smallhalf_maxheap = []
        self.largehalf_minheap = []

    def addNum(self, num: int) -> None:
        heappush(self.smallhalf_maxheap, - num)
        heappush(self.largehalf_minheap, - heappop(self.smallhalf_maxheap))
        if len(self.largehalf_minheap) > len(self.smallhalf_maxheap) + 1:
            heappush(self.smallhalf_maxheap, - heappop(self.largehalf_minheap))

    def findMedian(self) -> float:
        if len(self.largehalf_minheap) > len(self.smallhalf_maxheap):
            return self.largehalf_minheap[0]
        return (self.largehalf_minheap[0] + (- self.smallhalf_maxheap[0])) / 2

# Your MedianFinder object will be instantiated and called as such:
# obj = MedianFinder()
# obj.addNum(num)
# param_2 = obj.findMedian()

# time O(logn) for addNum(), O(1) for findMedian()
# space O(n), due to heap
# using heap and two heap problem
'''
follow up
bucket sort's idea
if input are in some small range, just build an array to record each number's count, then iterate over array to get median
also if most input are in some small range, will need build two counters to record number beyond range
'''

```


## 📄 [E]heap\[E]heap\313-super-ugly-number.py

```py
from heapq import *
class Solution:
    def nthSuperUglyNumber(self, n: int, primes: List[int]) -> int:
        res = [1]
        heap = [(res[0] * primes[i], 0, i) for i in range(len(primes))]
        while len(res) < n:
            val, res_idx, primes_idx = heappop(heap)
            if val > res[- 1]:
                res.append(val)
            heappush(heap, (res[res_idx + 1] * primes[primes_idx], res_idx + 1, primes_idx))
        return res[- 1]

# time O(nklog(k)), k is length of primes
# space O(n + k)
# using heap and k way merge problem
```


## 📄 [E]heap\[E]heap\355-design-twitter.py

```py
from heapq import *
class ListNode:
    def __init__(self, id=- 1, timestamp=- 1, next=None):
        self.id = id
        self.timestamp = timestamp
        self.next = next

class Twitter:

    def __init__(self):
        self.id_tweets = defaultdict(ListNode)
        self.timestamp = 0
        self.id_follows = defaultdict(set)

    def postTweet(self, userId: int, tweetId: int) -> None:
        tweets = self.id_tweets[userId]
        self.id_tweets[userId] = ListNode(tweetId, self.timestamp, tweets)
        self.timestamp += 1

    def getNewsFeed(self, userId: int) -> List[int]:
        nodes = [self.id_tweets[userId]]
        for id in self.id_follows[userId]:
            nodes.append(self.id_tweets[id])
        heap = []
        for i, node in enumerate(nodes):
            if node.id != - 1:
                heap.append((- node.timestamp, i))
        heapify(heap)
        res = []
        while len(res) < 10 and heap:
            _, i = heappop(heap)
            res.append(nodes[i].id)
            nodes[i] = nodes[i].next
            if nodes[i].id != - 1:
                heappush(heap, (- nodes[i].timestamp, i))
        return res

    def follow(self, followerId: int, followeeId: int) -> None:
        self.id_follows[followerId].add(followeeId)

    def unfollow(self, followerId: int, followeeId: int) -> None:
        if followeeId in self.id_follows[followerId]:
            self.id_follows[followerId].remove(followeeId)

# Your Twitter object will be instantiated and called as such:
# obj = Twitter()
# obj.postTweet(userId,tweetId)
# param_2 = obj.getNewsFeed(userId)
# obj.follow(followerId,followeeId)
# obj.unfollow(followerId,followeeId)

# time O(k + 10logk) for getNewsFeed(), others are O(1)
# space O(n), n is total tweets
# using heap and k way merge problem and hashmap
```


## 📄 [E]heap\[E]heap\373-find-k-pairs-with-smallest-sums.py

```py
from heapq import *
class Solution:
    def kSmallestPairs(self, nums1: List[int], nums2: List[int], k: int) -> List[List[int]]:
        heap = []
        visited = set()
        heappush(heap, (nums1[0] + nums2[0], 0, 0))
        visited.add((0, 0))
        res = []
        while len(res) < k:
            val, i, j = heappop(heap)
            res.append([nums1[i], nums2[j]])
            if i + 1 < len(nums1) and (i + 1, j) not in visited:
                heappush(heap, (nums1[i + 1] + nums2[j], i + 1, j))
                visited.add((i + 1, j))
            if j + 1 < len(nums2) and (i, j + 1) not in visited:
                heappush(heap, (nums1[i] + nums2[j + 1], i, j + 1))
                visited.add((i, j + 1))
        return res

# time O(klogk)
# space O(k)
# using heap and bfs
```


## 📄 [E]heap\[E]heap\378-kth-smallest-element-in-a-sorted-matrix.py

```py
from heapq import *
class Solution:
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        rows, cols = len(matrix), len(matrix[0])
        heap = []
        visited = set()
        heappush(heap, (matrix[0][0], 0, 0))
        visited.add((0, 0))
        while k:
            val, r, c = heappop(heap)
            k -= 1
            if r + 1 < rows and (r + 1, c) not in visited:
                heappush(heap, (matrix[r+1][c], r + 1, c))
                visited.add((r + 1, c))
            if c + 1 < cols and (r, c + 1) not in visited:
                heappush(heap, (matrix[r][c+1], r, c + 1))
                visited.add((r, c + 1))
        return val

# time O(klogk)
# space O(k)
# using heap and bfs
```


## 📄 [E]heap\[E]heap\407-trapping-rain-water-ii.py

```py
from heapq import *
class Solution:
    def trapRainWater(self, heightMap: List[List[int]]) -> int:
        h = heightMap
        rows, cols = len(h), len(h[0])
        heap = []
        visited = set()
        for r in range(rows):
            for c in range(cols):
                if (r == 0 or r == rows - 1) and (r, c) not in visited:
                    heappush(heap, (h[r][c], r, c))
                    visited.add((r, c))
                if (c == 0 or c == cols - 1) and (r, c) not in visited:
                    heappush(heap, (h[r][c], r, c))
                    visited.add((r, c))
        
        res = 0
        while heap:
            height, r, c = heappop(heap)
            for next_r, next_c in [(r+1, c), (r-1, c), (r, c+1), (r, c-1)]:
                if next_r not in range(rows) or next_c not in range(cols):
                    continue
                if (next_r, next_c) in visited:
                    continue
                res += max(height - h[next_r][next_c], 0)
                heappush(heap, (max(height, h[next_r][next_c]), next_r, next_c))
                visited.add((next_r, next_c))
        return res
        
# time O(RClog(RC)), heap size is RC
# space O(RC), due to hashset
# using heap and bfs
```


## 📄 [E]heap\[E]heap\480-sliding-window-median.py

```py
from heapq import *
from collections import defaultdict
class TwoHeap:
    def __init__(self):
        self.smallhalf_maxheap = []
        self.largehalf_minheap = []
        self.removeval_freq = defaultdict(int)
        self.smallhalf_size = 0
        self.largehalf_size = 0

    def insert(self, val):
        if self.smallhalf_maxheap and - self.smallhalf_maxheap[0] >= val:
            heappush(self.smallhalf_maxheap, - val)
            self.smallhalf_size += 1
        else:
            heappush(self.largehalf_minheap, val)
            self.largehalf_size += 1
        
        self.balance()
        self.lazy_remove()
    
    def remove(self, val):
        if self.smallhalf_maxheap and - self.smallhalf_maxheap[0] == val:
            heappop(self.smallhalf_maxheap)
            self.smallhalf_size -= 1
        elif self.largehalf_minheap and self.largehalf_minheap[0] == val:
            heappop(self.largehalf_minheap)
            self.largehalf_size -= 1
        elif self.smallhalf_maxheap and - self.smallhalf_maxheap[0] > val:
            self.smallhalf_size -= 1
            self.removeval_freq[val] += 1
        else:
            self.largehalf_size -= 1
            self.removeval_freq[val] += 1
        
        self.balance()
        self.lazy_remove()

    def balance(self):
        if self.smallhalf_size > self.largehalf_size + 1:
            heappush(self.largehalf_minheap, - heappop(self.smallhalf_maxheap))
            self.smallhalf_size -= 1
            self.largehalf_size += 1
        if self.largehalf_size > self.smallhalf_size + 1:
            heappush(self.smallhalf_maxheap, - heappop(self.largehalf_minheap))
            self.largehalf_size -= 1
            self.smallhalf_size += 1

    def lazy_remove(self):
        while self.smallhalf_maxheap and self.removeval_freq[- self.smallhalf_maxheap[0]]:
            neg_val = heappop(self.smallhalf_maxheap)
            self.removeval_freq[- neg_val] -= 1
        while self.largehalf_minheap and self.removeval_freq[self.largehalf_minheap[0]]:
            val = heappop(self.largehalf_minheap)
            self.removeval_freq[val] -= 1

    def get_median(self):
        if self.smallhalf_size == self.largehalf_size:
            return (- self.smallhalf_maxheap[0] + self.largehalf_minheap[0]) / 2
        elif self.smallhalf_size > self.largehalf_size:
            return - self.smallhalf_maxheap[0]
        else:
            return self.largehalf_minheap[0]

class Solution:
    def medianSlidingWindow(self, nums: List[int], k: int) -> List[float]:
        twoheap = TwoHeap()
        res = []
        left = 0
        for right, num in enumerate(nums):
            twoheap.insert(nums[right])
            if right - left + 1 == k:
                res.append(twoheap.get_median())
                twoheap.remove(nums[left])
                left += 1
        return res
    
# time O(nlogn)
# space O(n)
# using heap and two heap problem and lazy removal and sliding window
```


## 📄 [E]heap\[E]heap\502-ipo.py

```py
from heapq import *
class Solution:
    def findMaximizedCapital(self, k: int, w: int, profits: List[int], capital: List[int]) -> int:
        minheap_validate = []
        for p, c in zip(profits, capital):
            minheap_validate.append((c, p))
        heapify(minheap_validate)

        maxheap_profitable = []
        while k:
            while minheap_validate and minheap_validate[0][0] <= w:
                c, p = heappop(minheap_validate)
                heappush(maxheap_profitable, - p)
            if maxheap_profitable:
                neg_p = heappop(maxheap_profitable)
                w += - neg_p
                k -= 1
            else:
                break
        return w

# time O(nlogn)
# space O(n)
# using heap and two heap problem
```


## 📄 [E]heap\[E]heap\630-course-schedule-iii.py

```py
from heapq import *
class Solution:
    def scheduleCourse(self, courses: List[List[int]]) -> int:
        courses.sort(key = lambda x: x[1])

        heap = []
        cur_day = 0
        for duration, lastday in courses:
            if cur_day + duration <= lastday:
                heappush(heap, - duration)
                cur_day += duration
            elif heap and - heap[0] > duration:
                cur_day -= - (heappop(heap))
                heappush(heap, - duration)
                cur_day += duration

        return len(heap)
        
# time O(nlogn)
# space O(n)
# using heap and storing and popping out elements and sort and greedy
'''
1. greedy strategy
2. we consider the course with earilier deadline first
3. if we can take, we push in heap
4. if we can not take, we should check any prev course can be replaced or not
5. if so, we pop out that course with longest time, then take cur course (cur course is better choice)
6. if not, we discard cur course
'''
```


## 📄 [E]heap\[E]heap\632-smallest-range-covering-elements-from-k-lists.py

```py
from heapq import *
class Solution:
    def smallestRange(self, nums: List[List[int]]) -> List[int]:
        heap = []
        min_val, max_val = float('inf'), float('-inf')
        for i, vals in enumerate(nums):
            heappush(heap, (vals[0], i, 0))
            min_val = min(min_val, vals[0])
            max_val = max(max_val, vals[0])

        res = [min_val, max_val]

        while len(heap) == len(nums):
            val, list_idx, val_idx = heappop(heap)
            if val_idx + 1 < len(nums[list_idx]):
                next_val = nums[list_idx][val_idx + 1]
                heappush(heap, (next_val, list_idx, val_idx + 1))

                max_val = max(max_val, next_val)
                min_val = heap[0][0]
                diff = max_val - min_val
                if diff < res[1] - res[0]:
                    res = [min_val, max_val]
               
        return res
    
# time O(nlogk)
# space O(k)
# using heap and k way merge problem and greedy
'''
1. changing the smallest num (start point) can greedily find the small range
'''
```


## 📄 [E]heap\[E]heap\646-maximum-length-of-pair-chain.py

```py
from heapq import *
class Solution:
    def findLongestChain(self, pairs: List[List[int]]) -> int:
        pairs.sort()
        heap = []
        prev_best = 0
        all_time_best = 0
        for s, e in pairs:
            while heap and heap[0][0] < s:
                _, prev_len = heappop(heap)
                prev_best = max(prev_best, prev_len)
            heappush(heap, (e, prev_best + 1))
            all_time_best = max(all_time_best, prev_best + 1)
        return all_time_best
    
# time O(nlogn), due to heap operation is O(logn) and sort is O(nlogn)
# space O(n), due to heap
# using heap and greedily schedule tasks (start/end/val) and sort and greedy
```


## 📄 [E]heap\[E]heap\692-top-k-frequent-words.py

```py
from collections import defaultdict
from heapq import *

class FreqWord:
    def __init__(self, f, w):
        self.f = f
        self.w = w

    def __lt__(self, other):
        if self.f == other.f:
            return self.w > other.w
        return self.f < other.f

class Solution:
    def topKFrequent(self, words: List[str], k: int) -> List[str]:
        word_freq = defaultdict(int)
        for w in words:
            word_freq[w] += 1

        heap = []
        for w, f in word_freq.items():
            heappush(heap, FreqWord(f, w))
            if len(heap) > k:
                heappop(heap)
        return [fw.w for fw in sorted(heap, key = lambda x: (- x.f, x.w))]

# time O(nlogk), n is number of words, due to iterate frequency to heap operate
# space O(n + k), due to hashmap to store frequency and heap
# using heap and top k problem (based on heap) and min heap and sort and hashmap
'''
1. use min heap
2. inside heap, we want to pop out the low freq word
3. if same freq, we pop out the large word (so large word must be treated as smaller)
'''
```


## 📄 [E]heap\[E]heap\759-employee-free-time.py

```py
"""
# Definition for an Interval.
class Interval:
    def __init__(self, start: int = None, end: int = None):
        self.start = start
        self.end = end
"""
from heapq import *
class Solution:
    def employeeFreeTime(self, schedule: '[[Interval]]') -> '[Interval]':
        heap = []
        for i, employee in enumerate(schedule):
            heappush(heap, (schedule[i][0].start, schedule[i][0].end, i, 0))

        res = []
        prev_end = 0
        while heap:
            s, e, employee_id, interval_id = heappop(heap)
            if prev_end and prev_end < s:
                res.append(Interval(prev_end, s))
            prev_end = max(prev_end, e)
            if interval_id + 1 < len(schedule[employee_id]):
                interval = schedule[employee_id][interval_id + 1]
                heappush(heap, (interval.start, interval.end, employee_id, interval_id + 1))
        return res
    
# time O(nlogk)
# space O(k), due to heap
# using heap and k way merge problem and interval
```


## 📄 [E]heap\[E]heap\973-k-closest-points-to-origin.java

```java
class Solution {
    public int[][] kClosest(int[][] points, int k) {
        PriorityQueue<int[]> heap = new PriorityQueue<>((a, b) -> Integer.compare(b[0], a[0]));
        int[][] res = new int[k][2];
        for (int[] p: points) {
            heap.offer(new int[]{p[0] * p[0] + p[1] * p[1], p[0], p[1]});
            if (heap.size() > k) {
                heap.poll();
            }
        }
        while (!heap.isEmpty()) {
            int idx = heap.size() - 1;
            int[] p = heap.poll();
            res[idx][0] = p[1];
            res[idx][1] = p[2];
        }
        return res;
    }
}

// time O(nlogk)
// space O(k)
// using heap and top k problem (based on heap) and max heap
```


## 📄 [E]heap\[E]heap\973-k-closest-points-to-origin.py

```py
from heapq import *
class Solution:
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
        heap = []
        for x, y in points:
            distance = (x**2 + y**2) ** 0.5
            heappush(heap, (- distance, x, y))
            if len(heap) > k:
                heappop(heap)
                
        return [[x, y] for _, x, y in heap]

# time O(nlogk)
# space O(k)
# using heap and top k problem (based on heap) and max heap
```


## 📄 [F]string\[F]string\1044-longest-duplicate-substring.py

```py
class Solution:
    def longestDupSubstring(self, s: str) -> str:
        
        def find(k):
            base = 27
            base2 = 13
            mod = 10**9+7
            hashval_set = set()
            hashval = 0
            hashval2 = 0
            remove_base = (base ** (k - 1)) % mod
            remove_base2 = (base2 ** (k - 1)) % mod
            for i, c in enumerate(s):
                if i >= k:
                    hashval -= (remove_base * ord(s[i - k])) % mod
                    hashval2 -= (remove_base2 * ord(s[i - k])) % mod
                hashval = (hashval * base + ord(c)) % mod
                hashval2 = (hashval2 * base2 + ord(c)) % mod
                if i >= k - 1:
                    if (hashval, hashval2) in hashval_set:
                        return i - (k - 1)
                    hashval_set.add((hashval, hashval2))
            return - 1

        left, right, boundary = 1, len(s) - 1, - 1
        res_idx = - 1
        while left <= right:
            m = (left + right) // 2
            idx = find(m)
            if idx != - 1:
                boundary = m
                res_idx = idx
                left = m + 1
            else:
                right = m - 1
        return s[res_idx: res_idx + boundary] if res_idx != - 1 else ""
        
# time O(nlogn), find() costs O(n) by rolling hash method
# space O(n), due to hashset
# using string and rabin karp and binary search
'''
1. use binary search to guess the length of substring
2. use rolling hash to record is any substring repeated
3. change the length of substring to keep seraching
'''
```


## 📄 [F]string\[F]string\14-longest-common-prefix.java

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        String prefix = strs[0];
        for (String s: strs) {
            if (s.length() < prefix.length()) {
                prefix = s;
            }
        }
        for (int i = 0; i < prefix.length(); i++) {
            for (String s: strs) {
                if (prefix.charAt(i) != s.charAt(i)) {
                    return prefix.substring(0, i);
                }
            }
        }
        return prefix;
    }
}

// time O(nL)
// space O(1)
// using string and string composition
/*
1. notice the order of for loop
*/
```


## 📄 [F]string\[F]string\14-longest-common-prefix.py

```py
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        prefix = min(strs, key = len)
        for i, c in enumerate(prefix):
            for s in strs:
                if c != s[i]:
                    return prefix[:i]
        return prefix
    
# time O(nL)
# space O(1)
# using string and string composition
'''
1. notice the order of for loop
'''
```


## 📄 [F]string\[F]string\187-repeated-dna-sequences.py

```py
class Solution:
    def findRepeatedDnaSequences(self, s: str) -> List[str]:
        val_map = {'A':0, 'C':1, 'G':2, 'T':3}
        res = set()
        length = 10
        base = 27
        hashval_set = set()
        hashval = 0
        remove_base = base ** (length - 1)
        for i, c in enumerate(s):
            if i >= length:
                hashval -= remove_base * val_map[s[i - length]]
            hashval = hashval * base + val_map[c]
            if i >= length - 1:
                if hashval in hashval_set:
                    res.add(s[i - (length - 1): i + 1])
                hashval_set.add(hashval)
        return list(res)
    
# time O(n)
# space O(n)
# using string and rabin krap and hashset
```


## 📄 [F]string\[F]string\271-encode-and-decode-strings.py

```py
class Codec:
    def encode(self, strs: List[str]) -> str:
        """Encodes a list of strings to a single string.
        """
        def int_to_string(val):
            byte_array = [(val >> (8 * i)) & 0xFF for i in range(4)][:: - 1]
            char_array = [chr(byte) for byte in byte_array]
            string = ''.join(char_array)
            return string
        
        res = ''
        for s in strs:
            res += int_to_string(len(s)) + s
        return res

    def decode(self, s: str) -> List[str]:
        """Decodes a single string to a list of strings.
        """
        def string_to_int(string):
            val = 0
            for i, c in enumerate(string):
                val += ord(c) << (8 * (4 - 1 - i))
            return val

        res = []
        i = 0
        while i < len(s):
            chunk_len = string_to_int(s[i: i + 4])
            i += 4
            res.append(s[i: i + chunk_len])
            i += chunk_len
        return res

# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.decode(codec.encode(strs))

# time O(n)
# space O(1), not counting output
# using string and chunk and bit manipulation
```


## 📄 [F]string\[F]string\273-integer-to-english-words.py

```py
class Solution:
    def numberToWords(self, num: int) -> str:
        singles = ["", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"]
        tens = ["", "", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"]
        bases = ["", "", "Hundred", "Thousand", "", "", "Million", "", "", "Billion"]

        if num == 0:
            return "Zero"

        def helper(num):
            res = ""
            if num >= 10 ** 2:
                d, m = divmod(num, 10 ** 2)
                res += singles[d] + " " + bases[2] + " "
                num = m
            if num >= 10 * 2:
                d, m = divmod(num, 10)
                res += tens[d] + " "
                num = m
            res += singles[num] + " "
            return res.strip()

        res = ""
        for i in range(3, - 1, - 1):
            if num >= 10 ** (3 * i):
                d, m = divmod(num, 10 ** (3 * i))
                res += helper(d) + " " + bases[3 * i] + " "
                num = m
        return res.strip()
        
# time O(1)
# space O(1)
# using string and string composition
```


## 📄 [F]string\[F]string\28-find-the-index-of-the-first-occurrence-in-a-string.py

```py
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        base = 27
        hashval_set = set()
        hashval = 0
        for i, c in enumerate(needle):
            hashval = hashval * base + ord(c)
        hashval_set.add(hashval)

        hashval = 0
        remove_base = base ** (len(needle) - 1)
        for i, c in enumerate(haystack):
            if i >= len(needle):
                hashval -= remove_base * ord(haystack[i - len(needle)])
            hashval = hashval * base + ord(c)
            if i >= len(needle) - 1:
                if hashval in hashval_set:
                    return i - (len(needle) - 1)
        return - 1

# time O(n+m)
# space O(1)
# using hashmap and rabin karp
```


## 📄 [F]string\[F]string\43-multiply-strings.py

```py
class Solution:
    def multiply(self, num1: str, num2: str) -> str:
        res = [0 for _ in range(len(num1) + len(num2))]

        for i in range(len(num1) - 1, - 1, - 1):
            for j in range(len(num2) - 1, - 1, - 1):
                val = (ord(num1[i]) - ord('0')) * (ord(num2[j]) - ord('0'))
                idx = len(res) - 1 - (len(num1) - 1 - i + len(num2) - 1 - j)
                res[idx] += val

        carry = 0
        for i in range(len(res) - 1, - 1, - 1):
            carry, res[i] = divmod(res[i] + carry, 10)
        
        num = ''
        for val in res:
            if not val and not num:
                continue
            num += chr(val + ord('0'))
        return num if num else '0'
    
# time O(nm)
# space O(n+m)
# using string and traverse from end and math
```


## 📄 [F]string\[F]string\58-length-of-last-word.py

```py
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        res = 0

        for i in range(len(s) - 1, - 1, -1):
            if not res and s[i] == ' ':
                continue
            if s[i] == ' ':
                break
            res += 1
        return res
                
# time O(n)
# space O(1)
# using string and traverse from end
```


## 📄 [F]string\[F]string\6-zigzag-conversion.py

```py
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if numRows == 1 or numRows == len(s):
            return s

        rows = [[] for _ in range(numRows)]
        flag = 1
        idx = 0
        for c in s:
            rows[idx].append(c)
            if not (0 <= idx + flag < len(rows)):
                flag *= - 1
            idx += flag

        res = ''
        for row in rows:
            res += ''.join(row)
        return res

# time O(n)
# space O(n)
# using string and string composition
```


## 📄 [F]string\[F]string\65-valid-number.py

```py
class Solution:
    def isNumber(self, s: str) -> bool:
        met_sign = False
        met_dot = False
        met_num = False
        met_e = False

        for c in s:
            if c in '+-':
                if met_sign or met_dot or met_num:
                    return False
                met_sign = True
            elif c == '.':
                if met_dot or met_e:
                    return False
                met_dot = True
            elif c in 'eE':
                if not met_num or met_e:
                    return False
                met_sign = False
                met_dot = False
                met_num = False
                met_e = True
            elif c.isdigit():
                met_num = True
            else:
                return False
        return met_num

# time O(n)
# space O(1)
# using string and string composition
'''
1. (+/-) (num).num (e/E (+/-) num)
2. (+/-) num (e/E (+/-) num)
'''
```


## 📄 [F]string\[F]string\68-text-justification.py

```py
class Solution:
    def fullJustify(self, words: List[str], maxWidth: int) -> List[str]:
        
        res = []
        cur_words = []
        cur_len = 0
        for i, word in enumerate(words):
            if not cur_words or (cur_len + len(cur_words) + len(word) <= maxWidth):
                cur_words.append(word)
                cur_len += len(word)
            else:
                blank = maxWidth - cur_len
                if len(cur_words) > 1:
                    d, m = divmod(blank, len(cur_words) - 1)
                    tail = 0
                else:
                    d, m = 0, 0
                    tail = blank
                text = ''
                for j, w in enumerate(cur_words):
                    text += w
                    if j < len(cur_words) - 1:
                        text += ' ' * d
                        if m:
                            text += ' '
                            m -= 1
                    else:
                        text += ' ' * tail
                res.append(text)
                cur_words = [word]
                cur_len = len(word)
            if i == len(words) - 1:
                blank = maxWidth - cur_len
                text = ''
                for j, w in enumerate(cur_words):
                    text += w
                    if j < len(cur_words) - 1:
                        text += ' '
                        blank -= 1
                    else:
                        text += ' ' * blank
                res.append(text)
            
        return res

# time O(nL)
# space O(nL)
# using string and string composition
'''
1. fully justified: 
   contain >= 2 words: [word + blank + word]
   contain only 1 word: [word + blank] (blank can be empty here)
2. left justified: 
   contain >= 2 words: [word + 1 + word + blank] (blank can be empty here)
   contain only 1 word: [word + blank] (blank can be empty here)
'''
```


## 📄 [F]string\[F]string\718-maximum-length-of-repeated-subarray.py

```py
class Solution:
    def findLength(self, nums1: List[int], nums2: List[int]) -> int:
        if len(nums1) > len(nums2):
            nums1, nums2 = nums2, nums1

        def find(k):
            base = 109
            mod = 10**9+7
            hashval_set = set()
            hashval = 0
            remove_base = (base ** (k - 1)) % mod
            for i, num in enumerate(nums1):
                if i >= k:
                    hashval -= (remove_base * nums1[i - k]) % mod
                hashval = (hashval * base + nums1[i]) % mod
                if i >= k - 1:
                    hashval_set.add(hashval)
            
            hashval = 0
            for i, num in enumerate(nums2):
                if i >= k:
                    hashval -= (remove_base * nums2[i - k]) % mod
                hashval = (hashval * base + nums2[i]) % mod
                if i >= k - 1:
                    if hashval in hashval_set:
                        return True
            return False

        left, right, boundary = 1, len(nums1), 0
        while left <= right:
            m = (left + right) // 2
            if find(m):
                boundary = m
                left = m + 1
            else:
                right = m - 1
        return boundary

# time O((n+m) * log(min(n, m))
# space O(n)
# using string and rabin krap and binary search
```


## 📄 [F]string\[F]string\8-string-to-integer-atoi.java

```java
class Solution {
    public int myAtoi(String s) {
        boolean metSign = false;
        boolean metNum = false;
        int sign = 1;
        int num = 0;
        int min = Integer.MIN_VALUE;
        int max = Integer.MAX_VALUE;

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == ' ') {
                if (metSign || metNum) {
                    return sign * num;
                } else {
                    continue;
                }
            } else if (c == '-' || c == '+') {
                if (metSign || metNum) {
                    return sign * num;
                }
                metSign = true;
                if (c == '-') {
                    sign = - 1;
                }
            } else if (Character.isDigit(c)) {
                metNum = true;
                int val = c - '0';
                if (sign * num > max / 10 || (sign * num == max / 10 && sign * val > max % 10)) {
                    return max;
                } else if (sign * num < min / 10 || (sign * num == min / 10 && sign * val < min % 10)) {
                    return min;
                } else {
                    num = num * 10 + val;
                }
            } else {
                return sign * num;
            }
        }
        return sign * num;
    }
}

// time O(n), due to traverse
// space O(1)
// using string and handle value’s bound
```


## 📄 [F]string\[F]string\8-string-to-integer-atoi.py

```py
class Solution:
    def myAtoi(self, s: str) -> int:
        sign = 0
        num = 0
        max_int = 2**31 - 1
        min_int = - (2**31)

        for c in s:
            if c == ' ' and not sign:
                continue
            elif sign == 0 and c == '+':
                sign = 1
            elif sign == 0 and c == '-':
                sign = - 1
            elif not c.isdigit():
                break
            else:
                if sign == 0:
                    sign = 1
                if sign * num > max_int // 10 or \
                   (sign * num == max_int // 10 and int(c) > max_int % 10):
                    return max_int
                if sign * num < int(min_int / 10) or \
                     (sign * num == int(min_int / 10) and int(c) > 10 - min_int % 10):
                    return min_int
                num = num * 10 + int(c)
            
        return sign * num
        
# time O(n), due to traverse
# space O(1)
# using string and handle value’s bound
'''
-25//10 == -3
int(-25/10) == -2
-102 % 10 == 8
2 == 10 - (-102 % 10)
'''
```


## 📄 [F]string\[F]string\844-backspace-string-compare.java

```java
class Solution {
    public boolean backspaceCompare(String s, String t) {
        int i = s.length() - 1;
        int j = t.length() - 1;
        int iBack = 0;
        int jBack = 0;
        while (i >= 0 || j >= 0) {
            Character iChar = null;
            Character jChar = null;
            while (i >= 0) {
                if (s.charAt(i) == '#') {
                    iBack += 1;
                    i -= 1;
                }
                else if (iBack > 0) {
                    iBack -= 1;
                    i -= 1;
                } else {
                    iChar = s.charAt(i);
                    i -= 1;
                    break;
                }
            }
            while (j >= 0) {
                if (t.charAt(j) == '#') {
                    jBack += 1;
                    j -= 1;
                }
                else if (jBack > 0) {
                    jBack -= 1;
                    j -= 1;
                } else {
                    jChar = t.charAt(j);
                    j -= 1;
                    break;
                }
            }
            if (!Objects.equals(iChar, jChar)) {
                return false;
            }
        }
        return true;
    }
}

// time O(n+m)
// space O(1)
// using string and traverse from end and two pointers
```


## 📄 [F]string\[F]string\844-backspace-string-compare.py

```py
class Solution:
    def backspaceCompare(self, s: str, t: str) -> bool:
        i, j = len(s) - 1, len(t) - 1
        s_delete, t_delete = 0, 0
        
        while i >= 0 or j >= 0:
            s_char, t_char = None, None

            while i >= 0:
                if s[i] == '#':
                    s_delete += 1
                    i -= 1
                elif s_delete:
                    s_delete -= 1
                    i -= 1
                else:
                    s_char = s[i]
                    i -= 1
                    break

            while j >= 0:
                if t[j] == '#':
                    t_delete += 1
                    j -= 1
                elif t_delete:
                    t_delete -= 1
                    j -= 1
                else:
                    t_char = t[j]
                    j -= 1
                    break

            if s_char != t_char:
                return False
        return True
            
# time O(n+m)
# space O(1)
# using string and traverse from end and two pointers
```


## 📄 [G]trie\[G]trie\1166-design-file-system.py

```py
class TrieNode:
    def __init__(self):
        self.children = {}
        self.val = - 1

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, path, val):
        path = path.split('/')[1:]
        node = self.root
        for i, p in enumerate(path):
            if p not in node.children:
                if i == len(path) - 1:
                    node.children[p] = TrieNode()
                else:
                    return False
            node = node.children[p]
        if node.val == - 1:
            node.val = val
            return True
        else:
            return False

    def search(self, path):
        path = path.split('/')[1:]
        node = self.root
        for p in path:
            if p not in node.children:
                return - 1
            node = node.children[p]
        return node.val

class FileSystem:
    def __init__(self):
        self.trie = Trie()

    def createPath(self, path: str, value: int) -> bool:
        return self.trie.insert(path, value)

    def get(self, path: str) -> int:
        return self.trie.search(path)

# Your FileSystem object will be instantiated and called as such:
# obj = FileSystem()
# param_1 = obj.createPath(path,value)
# param_2 = obj.get(path)

# time O(1) for init, O(L) for createPath() and get()
# space O(nL)
# using trie and custom trie node
```


## 📄 [G]trie\[G]trie\1268-search-suggestions-system.py

```py
class TrieNode:
    def __init__(self):
        self.children = {}
        self.suggests = []

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, s):
        node = self.root
        for c in s:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
            node.suggests.append(s)
            node.suggests = sorted(node.suggests)[:3]
    
    def search(self, s):
        res = []
        node = self.root
        for i, c in enumerate(s):
            if c not in node.children:
                res.extend([[] for _ in range(len(s) - i)])
                break
            node = node.children[c]
            res.append(node.suggests)
        return res

class Solution:
    def suggestedProducts(self, products: List[str], searchWord: str) -> List[List[str]]:
        trie = Trie()
        for p in products:
            trie.insert(p)
        return trie.search(searchWord)

# time O(nL)
# space O(nL), nL nodes in trie, not counting suggests list storage in node
# using trie and custom trie node and sort
```


## 📄 [G]trie\[G]trie\208-implement-trie-prefix-tree.java

```java
class Trie {

    TrieNode root;

    public Trie() {
        root = new TrieNode();
    }
    
    public void insert(String word) {
        TrieNode node = root;
        for (int i = 0; i < word.length(); i++) {
            Character c = word.charAt(i);
            if (!node.children.containsKey(c)) {
                node.children.put(c, new TrieNode());
            }
            node = node.children.get(c);
        }
        node.isWord = true;
    }
    
    public boolean search(String word) {
        TrieNode node = root;
        for (int i = 0; i < word.length(); i++) {
            Character c = word.charAt(i);
            if (!node.children.containsKey(c)) {
                return false;
            }
            node = node.children.get(c);
        }
        return node.isWord;
    }
    
    public boolean startsWith(String prefix) {
        TrieNode node = root;
        for (int i = 0; i < prefix.length(); i++) {
            Character c = prefix.charAt(i);
            if (!node.children.containsKey(c)) {
                return false;
            }
            node = node.children.get(c);
        }
        return true;
    }
}

class TrieNode {
    HashMap<Character, TrieNode> children;
    boolean isWord;

    public TrieNode() {
        children = new HashMap<>();
        isWord = false;
    }
}

/**
* Your Trie object will be instantiated and called as such:
* Trie obj = new Trie();
* obj.insert(word);
* boolean param_2 = obj.search(word);
* boolean param_3 = obj.startsWith(prefix);
*/

// time O(L) for insert(), search(), startsWith(), L is the word's length
// space O(nL), n is the number of words, L is the max len
// using trie and standard trie
```


## 📄 [G]trie\[G]trie\208-implement-trie-prefix-tree.py

```py
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        node = self.root
        for c in word:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
        node.is_word = True

    def search(self, word: str) -> bool:
        node = self.root
        for c in word:
            if c not in node.children:
                return False
            node = node.children[c]
        return node.is_word

    def startsWith(self, prefix: str) -> bool:
        node = self.root
        for c in prefix:
            if c not in node.children:
                return False
            node = node.children[c]
        return True

# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)

# time O(L) for insert(), search(), startsWith(), L is the word's length
# space O(nL), n is the number of words, L is the max len
# using trie and standard trie
```


## 📄 [G]trie\[G]trie\211-design-add-and-search-words-data-structure.py

```py
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, s):
        node = self.root
        for c in s:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
        node.is_word = True

    def search(self, s):
        return self.search_helper(s, self.root, 0)

    def search_helper(self, s, node, idx):
        for i in range(idx, len(s)):
            if s[i] == '.':
                for child in node.children.values():
                    if self.search_helper(s, child, i + 1):
                        return True
                return False
            if s[i] not in node.children:
                return False
            node = node.children[s[i]]
        return node.is_word

class WordDictionary:
    def __init__(self):
        self.trie = Trie()
        self.len_set = set()

    def addWord(self, word: str) -> None:
        self.len_set.add(len(word))
        self.trie.insert(word)

    def search(self, word: str) -> bool:
        if len(word) not in self.len_set:
            return False
        return self.trie.search(word)

# Your WordDictionary object will be instantiated and called as such:
# obj = WordDictionary()
# obj.addWord(word)
# param_2 = obj.search(word)

# time O(nL or 26**L) for search(), O(L) for addWord()
# space O(nL), n is the number of words, L is the max len
# using trie and perform dfs inside trie and prune
```


## 📄 [G]trie\[G]trie\2185-counting-words-with-a-given-prefix.py

```py
class TrieNode:
    def __init__(self):
        self.children = {}
        self.count = 0

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, s):
        node = self.root
        for c in s:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
            node.count += 1
    
    def search(self, s):
        node = self.root
        for c in s:
            if c not in node.children:
                return 0
            node = node.children[c]
        return node.count

class Solution:
    def prefixCount(self, words: List[str], pref: str) -> int:
        trie = Trie()
        for w in words:
            trie.insert(w)
        return trie.search(pref)

# time O(nL)
# space O(nL)
# using trie and custom trie node
'''
1. using trie allows we change requested prefix frequently
2. if prefix is fixed, and words are sorted. try binary search (O(klogn)))
'''
```


## 📄 [G]trie\[G]trie\2416-sum-of-prefix-scores-of-strings.py

```py
class TrieNode:
    def __init__(self):
        self.children = {}
        self.count = 0
        self.length = 0

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, s):
        node = self.root
        for i, c in enumerate(s):
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
            node.count += 1
            node.length = i + 1

    def search(self, s):
        res = 0
        node = self.root
        for c in s:
            node = node.children[c]
            res += node.count
            if node.count == 1:
                res += len(s) - node.length
                break
        return res

class Solution:
    def sumPrefixScores(self, words: List[str]) -> List[int]:
        trie = Trie()
        for w in words:
            trie.insert(w)
        res = []
        for w in words:
            res.append(trie.search(w))
        return res
    
# time O(nL)
# space O(nL)
# using trie and custom trie node and prune
```


## 📄 [G]trie\[G]trie\472-concatenated-words.py

```py
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, s):
        node = self.root
        for c in s:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
        node.is_word = True
    
    def search(self, s):
        return self.search_helper(s, self.root, 0)

    def search_helper(self, s, node, idx):
        for i in range(idx, len(s)):
            if node.is_word:
                if self.search_helper(s, self.root, i):
                    return True
            if s[i] not in node.children:
                return False
            node = node.children[s[i]]
        return node.is_word

class Solution:
    def findAllConcatenatedWordsInADict(self, words: List[str]) -> List[str]:
        res = []
        trie = Trie()
        words.sort(key=len)
        for w in words:
            if trie.search(w):
                res.append(w)
            else:
                trie.insert(w)
            
        return res
        
# time O(nlogn + nL + n * L**2), search is O(L**2) here not O(2**L), due to cost is L + L-1 + L-2 + ... + 1
# space O(nL), n is the number of words, L is the max len
# using trie and perform dfs inside trie and sort
'''
1. long word can only be consisted from short words, so we sort at first
2. if certain word can be consisted from short words then no need to add in trie
'''
```


## 📄 [G]trie\[G]trie\588-design-in-memory-file-system.py

```py
class TrieNode:
    def __init__(self):
        self.children = {}
        self.content = ''

class FileSystem:
    def __init__(self):
        self.root = TrieNode()

    def ls(self, path: str) -> List[str]:
        node = self.get_node(path)
        if node.content:
            return [path.split('/')[- 1]]
        return sorted(list(node.children.keys()))

    def mkdir(self, path: str) -> None:
        self.get_node(path)

    def addContentToFile(self, filePath: str, content: str) -> None:
        node = self.get_node(filePath)
        node.content += content

    def readContentFromFile(self, filePath: str) -> str:
        node = self.get_node(filePath)
        return node.content

    def get_node(self, path):
        if path == '/':
            return self.root
        path = path.split('/')[1:]
        node = self.root
        for p in path:
            if p not in node.children:
                node.children[p] = TrieNode()
            node = node.children[p]
        return node

# Your FileSystem object will be instantiated and called as such:
# obj = FileSystem()
# param_1 = obj.ls(path)
# obj.mkdir(path)
# obj.addContentToFile(filePath,content)
# param_4 = obj.readContentFromFile(filePath)

# time O(L), most operation is O(L), and ls() can be O(L + klogk), k is the number of files
# space O(nL), n is the number of paths and files, L is the path's length
# using trie and custom trie node
```


## 📄 [G]trie\[G]trie\642-design-search-autocomplete-system.py

```py
class TrieNode:
    def __init__(self):
        self.children = {}
        self.sentence = ''
        self.count = 0

class Trie:
    def __init__(self):
        self.root = TrieNode()
        self.cur = self.root
        self.sentence = ''

    def insert(self, s, count):
        node = self.root
        for c in s:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
        node.sentence = s
        node.count += count

    def search(self, char):
        if char == '#':
            self.insert(self.sentence, 1)
            self.cur = self.root
            self.sentence = ''
            return []
        elif not self.cur or char not in self.cur.children:
            self.cur = None
            self.sentence += char
            return []
        else:
            self.cur = self.cur.children[char]
            self.sentence += char
            res = self.search_helper(self.cur)
            res.sort(key = lambda x: (- x[0], x[1]))
            return [sentence for _, sentence in res[:3]]

    def search_helper(self, node):
        res = []
        if node.sentence:
            res.append((node.count, node.sentence))
        for child in node.children.values():
            res.extend(self.search_helper(child))
        return res

class AutocompleteSystem:
    def __init__(self, sentences: List[str], times: List[int]):
        self.trie = Trie()
        for s, t in zip(sentences, times):
            self.trie.insert(s, t)

    def input(self, c: str) -> List[str]:
        return self.trie.search(c)

# Your AutocompleteSystem object will be instantiated and called as such:
# obj = AutocompleteSystem(sentences, times)
# param_1 = obj.input(c)

# time O(nL) for init(), O(nL + nlogn) or O(L) for input()
# space O(nL+s), s is the number of calling input(), we can store more info inside trie node for improving time complexity
# using trie and perform dfs inside trie and sort
```


## 📄 [G]trie\[G]trie\745-prefix-and-suffix-search.py

```py
class TrieNode:
    def __init__(self):
        self.children = {}
        self.idx = - 1

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, s, idx):
        node = self.root
        for c in s:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
            node.idx = idx

    def search(self, s):
        node = self.root
        for c in s:
            if c not in node.children:
                return - 1
            node = node.children[c]
        return node.idx

class WordFilter:
    def __init__(self, words: List[str]):
        self.trie = Trie()
        for i, w in enumerate(words):
            for start in range(len(w)):
                self.trie.insert(w[start:] + '#' + w, i)

    def f(self, pref: str, suff: str) -> int:
        return self.trie.search(suff + '#' + pref)

# Your WordFilter object will be instantiated and called as such:
# obj = WordFilter(words)
# param_1 = obj.f(pref,suff)

# time O(n(L**2)) for init, O(L) for f()
# space O(n(L**2))
# using trie and custom trie node
'''
1. search suffix first than prefix
2. because we don't know the chars between them
3. so we cannot search prefix first
'''
```


## 📄 [H]array\[H]array\1472-design-browser-history.py

```py
class BrowserHistory:

    def __init__(self, homepage: str):
        self.pages = [homepage]
        self.start = 0
        self.cur = 0
        self.end = 0
        
    def visit(self, url: str) -> None:
        if self.cur + 1 == len(self.pages):
            self.pages.append(url)
            self.cur += 1
            self.end = self.cur
        else:
            self.pages[self.cur + 1] = url
            self.cur += 1
            self.end = self.cur

    def back(self, steps: int) -> str:
        if self.cur - steps >= self.start:
            self.cur -= steps
            return self.pages[self.cur]
        else:
            self.cur = self.start
            return self.pages[self.cur]

    def forward(self, steps: int) -> str:
        if self.cur + steps <= self.end:
            self.cur += steps
            return self.pages[self.cur]
        else:
            self.cur = self.end
            return self.pages[self.cur]

# Your BrowserHistory object will be instantiated and called as such:
# obj = BrowserHistory(homepage)
# obj.visit(url)
# param_2 = obj.back(steps)
# param_3 = obj.forward(steps)

# time O(1) for all
# space O(n)
# using array and maintain array's range dynamically
```


## 📄 [H]array\[H]array\1535-find-the-winner-of-an-array-game.py

```py
class Solution:
    def getWinner(self, arr: List[int], k: int) -> int:
        max_num = max(arr)
        
        cur = None
        count = 0
        for i, num in enumerate(arr):
            if num == max_num:
                cur = num
                break
            if not cur:
                cur = num
            elif cur < num:
                cur = num
                count = 1
            else:
                count += 1
            if count == k:
                break
        return cur
                
# time O(n)
# space O(1)
# using array and simulation
'''
1. we can use queue to simulate the game
2. but actually if we met max num, max num will always be res
3. so, we do not need to consider element behind max num (involves the elements which were moved to end)
'''
```


## 📄 [H]array\[H]array\163-missing-ranges.py

```py
class Solution:
    def findMissingRanges(self, nums: List[int], lower: int, upper: int) -> List[List[int]]:
        nums = [lower - 1] + nums + [upper + 1]
        res = []
        for i in range(1, len(nums)):
            prev = nums[i - 1]
            cur = nums[i]
            if cur - prev >= 2:
                res.append([prev + 1, cur - 1])
        return res
    
# time O(n)
# space O(n)
# using array and pre-process
```


## 📄 [H]array\[H]array\169-majority-element.java

```java
class Solution {
    public int majorityElement(int[] nums) {
        Integer cand = null;
        int vote = 0;
        for (int i = 0; i < nums.length; i++) {
            if (cand != null && cand == nums[i]) {
                vote += 1;
            } else if (cand == null) {
                cand = nums[i];
                vote = 1;
            } else {
                vote -= 1;
                if (vote == 0) {
                    cand = null;
                }
            }
        }
        return cand;
    }
}

// time O(n)
// space O(1)
// using array and boyer moore vote algorithm
```


## 📄 [H]array\[H]array\169-majority-element.py

```py
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        cand = None
        vote = 0
        for num in nums:
            if num == cand:
                vote += 1
            elif cand == None:
                cand = num
                vote = 1
            else:
                vote -= 1
                if vote == 0:
                    cand = None
        return cand

# time O(n)
# space O(1)
# using array and boyer moore vote algorithm
```


## 📄 [H]array\[H]array\189-rotate-array.py

```py
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        
        def helper(left, right):
            while left < right:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1
        
        k %= len(nums)
        helper(0, len(nums) - 1)
        helper(0, k - 1)
        helper(k, len(nums) - 1)
        
# time O(n)
# space O(1)
# using array and reverse technique
'''
1. after rotate, can divide array into two part
2. rotate them again
'''
```


## 📄 [H]array\[H]array\229-majority-element-ii.py

```py
class Solution:
    def majorityElement(self, nums: List[int]) -> List[int]:
        
        def get_top_k_majority(k):
            cand_vote = {}
            for num in nums:
                if num in cand_vote:
                    cand_vote[num] += 1
                elif len(cand_vote) < k:
                    cand_vote[num] = 1
                else:
                    for c in list(cand_vote.keys()):
                        cand_vote[c] -= 1
                        if cand_vote[c] == 0:
                            cand_vote.pop(c)

            for c in cand_vote.keys():
                cand_vote[c] = 0
            for num in nums:
                if num in cand_vote:
                    cand_vote[num] += 1
            return [c for c, v in cand_vote.items() if v * (k + 1) > len(nums)]

        return get_top_k_majority(2)
    
# time O(nk), k is 2 here
# space O(k)
# using array and boyer moore vote algorithm
```


## 📄 [H]array\[H]array\243-shortest-word-distance.py

```py
class Solution:
    def shortestDistance(self, wordsDict: List[str], word1: str, word2: str) -> int:
        res = len(wordsDict)
        i, j = - 1, - 1
        for k, word in enumerate(wordsDict):
            if word == word1:
                i = k
            if word == word2:
                j = k
            if i != - 1 and j != - 1:
                res = min(res, abs(i - j))
            if res == 1:
                break
        return res
    
# time O(nL)
# space O(1)
# using array and traverse
```


## 📄 [H]array\[H]array\280-wiggle-sort.py

```py
class Solution:
    def wiggleSort(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        
        for i in range(len(nums)):
            if i + 1 < len(nums):
                if i % 2 == 0:
                    if nums[i] > nums[i + 1]:
                        nums[i], nums[i + 1] = nums[i + 1], nums[i]
                else:
                    if nums[i] < nums[i + 1]:
                        nums[i], nums[i + 1] = nums[i + 1], nums[i]

# time O(n)
# space O(1)
# using array and swap
'''
1. swap won't affect the relationship of nums[i - 1] and nums[i]
'''
```


## 📄 [H]array\[H]array\287-find-the-duplicate-number.py

```py
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        slow, fast = 0, 0
        while True:
            slow = nums[slow]
            fast = nums[nums[fast]]
            if slow == fast:
                break
        
        p1, p2 = 0, slow
        while True:
            p1 = nums[p1]
            p2 = nums[p2]
            if p1 == p2:
                break
        
        return p1
            
# time O(n)
# space O(1)
# using array and specific range array (cycle detection)
'''
1. (L + P ) * 2 = L + P + Q + P
2. L = Q
'''
```


## 📄 [H]array\[H]array\362-design-hit-counter.py

```py
class HitCounter:
    def __init__(self):
        self.limit = 300
        self.timestamp_count = [[0, 0] for _ in range(self.limit)]

    def hit(self, timestamp: int) -> None:
        idx = timestamp % self.limit
        if self.timestamp_count[idx][0] == timestamp:
            self.timestamp_count[idx][1] += 1
        else:
            self.timestamp_count[idx] = [timestamp, 1]

    def getHits(self, timestamp: int) -> int:
        res = 0
        idx = timestamp % self.limit
        for t, c in self.timestamp_count:
            if timestamp - self.limit < t <= timestamp:
                res += c
        return res

# Your HitCounter object will be instantiated and called as such:
# obj = HitCounter()
# obj.hit(timestamp)
# param_2 = obj.getHits(timestamp)

# time O(1)
# space O(s), s is 300
# using array and circular array
```


## 📄 [H]array\[H]array\370-range-addition.py

```py
class Solution:
    def getModifiedArray(self, length: int, updates: List[List[int]]) -> List[int]:
        
        diffs = [0 for _ in range(length)]
        for s, e, inc in updates:
            diffs[s] += inc
            if e + 1 < length:
                diffs[e + 1] -= inc
        
        total = 0
        for i, d in enumerate(diffs):
            total += d
            diffs[i] = total
        return diffs
        
# time O(n+k), k is the length of updates
# space O(1), if not counting output list
# using array and difference array
```


## 📄 [H]array\[H]array\384-shuffle-an-array.py

```py
import random
class Solution:

    def __init__(self, nums: List[int]):
        self.nums = nums
        self.origin_nums = nums[:]

    def reset(self) -> List[int]:
        self.nums = self.origin_nums[:]
        return self.nums

    def shuffle(self) -> List[int]:
        for i in range(len(self.nums) - 1, - 1, - 1):
            target_idx = random.randint(0, i)
            self.nums[i], self.nums[target_idx] = self.nums[target_idx], self.nums[i]
        return self.nums

# Your Solution object will be instantiated and called as such:
# obj = Solution(nums)
# param_1 = obj.reset()
# param_2 = obj.shuffle()

# time O(n)
# space O(n)
# using array and knuth shuffle
```


## 📄 [H]array\[H]array\398-random-pick-index.py

```py
from collections import defaultdict
import random
class Solution:

    def __init__(self, nums: List[int]):
        self.num_indices = defaultdict(list)
        for i, num in enumerate(nums):
            self.num_indices[num].append(i)

    def pick(self, target: int) -> int:
        indices = self.num_indices[target]
        return random.choice(indices)

# Your Solution object will be instantiated and called as such:
# obj = Solution(nums)
# param_1 = obj.pick(target)

# time O(1) for pick()
# space O(n), due to hashmap
# using hashmap

import random
class Solution:
    def __init__(self, nums: List[int]):
        self.nums = nums

    def pick(self, target: int) -> int:
        stream = 0
        res = None
        for i, num in enumerate(self.nums):
            if num == target:
                if 0 == random.randint(0, stream):
                    res = i
                stream += 1
        return res
        
# time O(n) for pick()
# space O(1)
# using array and reservoir sampling
```


## 📄 [H]array\[H]array\41-first-missing-positive.py

```py
class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        for i, num in enumerate(nums):
            while 1 <= nums[i] <= len(nums):
                target_idx = nums[i] - 1
                if nums[i] == nums[target_idx]:
                    break
                nums[i], nums[target_idx] = nums[target_idx], nums[i]

        for i, num in enumerate(nums):
            if num != i + 1:
                return i + 1
        return len(nums) + 1
        
# time O(n)
# space O(1)
# using array and specific range array (cyclic sort)
'''
1. we want to restore array like below
idx:
    0, 1, 2, 3 ..., n-1
val:
    1, 2, 3, 4 ..., n 
2. then we can find out the missing val 
'''
```


## 📄 [H]array\[H]array\442-find-all-duplicates-in-an-array.py

```py
class Solution:
    def findDuplicates(self, nums: List[int]) -> List[int]:
        for i, num in enumerate(nums):
            while 1 <= nums[i] <= len(nums):
                target_idx = nums[i] - 1
                if nums[i] == nums[target_idx]:
                    break
                nums[i], nums[target_idx] = nums[target_idx], nums[i]

        res = []
        for i, num in enumerate(nums):
            if i != num - 1:
                res.append(num)
        return res
        
# time O(n)
# space O(1), not counting output list
# using array and specific range array (cyclic sort)
```


## 📄 [H]array\[H]array\448-find-all-numbers-disappeared-in-an-array.py

```py
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        for i, num in enumerate(nums):
            while 1 <= nums[i] <= len(nums):
                target_idx = nums[i] - 1
                if nums[i] == nums[target_idx]:
                    break
                nums[i], nums[target_idx] = nums[target_idx], nums[i]
        
        res = []
        for i, num in enumerate(nums):
            if num != i + 1:
                res.append(i + 1)
        return res
    
# time O(n)
# space O(1), if not count output list
# using array and specific range array (cyclic sort)
```


## 📄 [H]array\[H]array\845-longest-mountain-in-array.py

```py
class Solution:
    def longestMountain(self, arr: List[int]) -> int:
        state = 0
        start = 0
        res = 0

        for i in range(1, len(arr)):
            if state == 0:
                if arr[i - 1] < arr[i]:
                    state = 1
                    start = i - 1
            elif state == 1:
                if arr[i - 1] == arr[i]:
                    state = 0
                elif arr[i - 1] > arr[i]:
                    state = 2
                    res = max(res, i - start + 1)
            else:
                if arr[i - 1] < arr[i]:
                    state = 1
                    start = i - 1
                elif arr[i - 1] == arr[i]:
                    state = 0
                else:
                    res = max(res, i - start + 1)
        
        return res

# time O(n)
# space O(1)
# using array and finite state machine
'''
1. state 0 for undefined, 1 for uphill, 2 for downhill
'''
```


## 📄 [H]array\[H]array\849-maximize-distance-to-closest-person.py

```py
class Solution:
    def maxDistToClosest(self, seats: List[int]) -> int:
        
        res = 0
        zero = 0
        edge_zero = False

        for i, s in enumerate(seats):
            if s == 0:
                zero += 1
                if i == 0 or i == len(seats) - 1:
                    edge_zero = True
                if edge_zero:
                    res = max(res, zero)
                else:
                    res = max(res, (zero + 1) // 2)
            else:
                zero = 0
                edge_zero = False
        
        return res
    
# time O(n)
# space O(1)
# using array and count continuous elements
```


## 📄 [H]array\[H]array-line-sweep\1229-meeting-scheduler.py

```py
class Solution:
    def minAvailableDuration(self, slots1: List[List[int]], slots2: List[List[int]], duration: int) -> List[int]:
        slots1.sort()
        slots2.sort()
        i, j = 0, 0
        res = []
        while i < len(slots1) and j < len(slots2):
            s1, e1 = slots1[i]
            s2, e2 = slots2[j]
            if e1 < s2:
                i += 1
            elif e2 < s1:
                j += 1
            else:
                interval = [max(s1, s2), min(e1, e2)]
                if interval[1] - interval[0] >= duration:
                    res.append(interval[0])
                    res.append(interval[0] + duration)
                    break
                elif e1 < e2:
                    i += 1
                else:
                    j += 1
        
        return res
    
# time O(mlogm + nlogn)
# space O(1), not counting built in sort cost
# using array and line sweep and compare two intervals each round and two pointers and greedy and sort

class Solution:
    def minAvailableDuration(self, slots1: List[List[int]], slots2: List[List[int]], duration: int) -> List[int]:
        
        intervals = []
        for s, e in slots1:
            if e - s >= duration:
                intervals.append([s, e])
        for s, e in slots2:
            if e - s >= duration:
                intervals.append([s, e])
        intervals.sort()

        res = []
        if intervals:
            prev_s, prev_e = intervals[0]
        for i in range(1, len(intervals)):
            cur_s, cur_e = intervals[i]
            if prev_e < cur_s:
                prev_s, prev_e = cur_s, cur_e
            else:
                interval = [max(prev_s, cur_s), min(prev_e, cur_e)]
                if interval[1] - interval[0] >= duration:
                    res.append(interval[0])
                    res.append(interval[0] + duration)
                    break
                if cur_e > prev_e:
                    prev_s, prev_e = cur_s, cur_e
        return res

# time O((m+n)log(m+n))
# space O(m+n)
# using array and line sweep and compare two intervals each round and greedy and sort and prune

from heapq import *
class Solution:
    def minAvailableDuration(self, slots1: List[List[int]], slots2: List[List[int]], duration: int) -> List[int]:
        
        events = []
        for s, e in slots1:
            if e - s >= duration:
                events.append((s, 1))
                events.append((e, - 1))
        for s, e in slots2:
            if e - s >= duration:
                events.append((s, 1))
                events.append((e, - 1))

        heapify(events)
        status = 0
        prev_timestamp = 0
        res = []
        while events:
            timestamp, weight = heappop(events)
            if status == 2:
                interval = [prev_timestamp, timestamp]
                if interval[1] - interval[0] >= duration:
                    res.append(interval[0])
                    res.append(interval[0] + duration)
                    break
            prev_timestamp = timestamp
            status += weight
        return res

# time O((m+n)log(m+n))
# space O(m+n)
# using array and line sweep and and greedy and heap and prune
```


## 📄 [H]array\[H]array-line-sweep\1272-remove-interval.py

```py
class Solution:
    def removeInterval(self, intervals: List[List[int]], toBeRemoved: List[int]) -> List[List[int]]:
        
        res = []
        prev_s, prev_e = toBeRemoved
        for i, (cur_s, cur_e) in enumerate(intervals):
            if cur_s >= prev_e:
                res.extend(intervals[i:])
                return res
            elif cur_e <= prev_s:
                res.append([cur_s, cur_e])
            else:
                if cur_s < prev_s:
                    res.append([cur_s, prev_s])
                if cur_e > prev_e:
                    res.append([prev_e, cur_e])
        
        return res
    
# time O(n)
# space O(n), due to output list
# using array and line sweep and compare two intervals each round
```


## 📄 [H]array\[H]array-line-sweep\1288-remove-covered-intervals.py

```py
class Solution:
    def removeCoveredIntervals(self, intervals: List[List[int]]) -> int:
        intervals.sort(key = lambda x: (x[0], - x[1]))

        res = 0
        prev_s, prev_e = intervals[0]
        for i in range(1, len(intervals)):
            cur_s, cur_e = intervals[i]
            if prev_e >= cur_e:
                res += 1
            else:
                prev_s, prev_e = cur_s, cur_e

        return len(intervals) - res
        
# time O(nlogn)
# space O(1) or consider the built in sort's cost
# using array and line sweep and compare two intervals each round and sort and greedy
```


## 📄 [H]array\[H]array-line-sweep\1851-minimum-interval-to-include-each-query.py

```py
from heapq import *
class Solution:
    def minInterval(self, intervals: List[List[int]], queries: List[int]) -> List[int]:

        intervals.sort()
        queries = [(q, i) for i, q in enumerate(queries)]
        queries.sort()
        res = [- 1 for _ in range(len(queries))]

        heap = []
        idx = 0
        for q, i in queries:
            while idx < len(intervals):
                s, e = intervals[idx]
                if q < s:
                    break
                elif e < q:
                    idx += 1
                else:
                    heappush(heap, (e - s + 1, s, e))
                    idx += 1
            
            while heap:
                length, s, e = heap[0]
                if e < q:
                    heappop(heap)
                else:
                    res[i] = length
                    break
        return res
    
# time O(nlogn + qlogq)
# space O(n + q)
# using array and line sweep and heap to store previous intervals’ states and greedy and sort
```


## 📄 [H]array\[H]array-line-sweep\252-meeting-rooms.java

```java
class Solution {
    public boolean canAttendMeetings(int[][] intervals) {
        if (intervals.length == 0) {
            return true;
        }
        Arrays.sort(intervals, (a, b) -> a[0] == b[0] ? Integer.compare(a[1], b[1]) : Integer.compare(a[0], b[0]));
        int prevE = intervals[0][1];
        for (int i = 1; i < intervals.length; i++) {
            int curS = intervals[i][0];
            int curE = intervals[i][1];
            if (prevE > curS) {
                return false;
            }
            prevE = Math.max(prevE, curE);
        }
        return true;
    }
}

// time O(nlogn)
// space O(1), or consider sort's cost
// using array and line sweep and compare two intervals each round
```


## 📄 [H]array\[H]array-line-sweep\252-meeting-rooms.py

```py
class Solution:
    def canAttendMeetings(self, intervals: List[List[int]]) -> bool:
        if not intervals:
            return True
        
        intervals.sort()

        prev_s, prev_e = intervals[0]
        for i in range(1, len(intervals)):
            cur_s, cur_e = intervals[i]
            if prev_e <= cur_s:
                prev_s, prev_e = cur_s, cur_e
                continue
            return False

        return True

# time O(nlogn)
# space O(1), or consider sort's cost
# using array and line sweep and compare two intervals each round
```


## 📄 [H]array\[H]array-line-sweep\253-meeting-rooms-ii.py

```py
from heapq import *
class Solution:
    def minMeetingRooms(self, intervals: List[List[int]]) -> int:
        
        intervals.sort()

        heap = []
        for s, e in intervals:
            if heap and heap[0] <= s:
                heappop(heap)
            heappush(heap, e)
        return len(heap)

# time O(nlogn)
# space O(n)
# using array and line sweep and heap to store previous intervals’ states

from heapq import *
class Solution:
    def minMeetingRooms(self, intervals: List[List[int]]) -> int:
        
        intervals.sort()

        heap = []
        res = 0
        for s, e in intervals:
            while heap and heap[0] <= s:
                heappop(heap)
            heappush(heap, e)
            res = max(res, len(heap))
        return res

# time O(nlogn)
# space O(n)
# using array and line sweep and heap to store previous intervals’ states

class Solution:
    def minMeetingRooms(self, intervals: List[List[int]]) -> int:
        
        events = []

        for s, e in intervals:
            events.append((s, 1))
            events.append((e, - 1))
        events.sort()

        status = 0
        res = 0
        for timestamp, weight in events:
            status += weight
            res = max(res, status)
        return res

# time O(nlogn)
# space O(n)
# using array and line sweep and sort
```


## 📄 [H]array\[H]array-line-sweep\435-non-overlapping-intervals.py

```py
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        
        intervals.sort()

        res = 0
        prev_s, prev_e = intervals[0]
        for i in range(1, len(intervals)):
            cur_s, cur_e = intervals[i]
            if prev_e <= cur_s:
                prev_s, prev_e = cur_s, cur_e
            else:
                if cur_e < prev_e:
                    prev_s, prev_e = cur_s, cur_e
                res += 1
        
        return res

# time O(nlogn)
# space O(1), or due to built in sort's cost
# using array and line sweep and compare two intervals each round and sort and greedy
```


## 📄 [H]array\[H]array-line-sweep\452-minimum-number-of-arrows-to-burst-balloons.py

```py
class Solution:
    def findMinArrowShots(self, points: List[List[int]]) -> int:
        
        points.sort()

        res = 0
        prev_e = points[0][1]
        for i in range(1, len(points)):
            cur_s, cur_e = points[i]
            if prev_e < cur_s:
                res += 1
                prev_e = cur_e
            else:
                prev_e = min(prev_e, cur_e)
            
        res += 1

        return res
    
# time O(nlogn)
# space O(1), not counting built in sort cost
# using array and line sweep and compare two intervals each round and sort and greedy
'''
1. only end ptr matters
'''

class Solution:
    def findMinArrowShots(self, points: List[List[int]]) -> int:
        
        points.sort(key = lambda x: x[1])

        res = 0
        prev_e = points[0][1]
        for i in range(1, len(points)):
            cur_s, cur_e = points[i]
            if prev_e < cur_s:
                res += 1
                prev_e = cur_e
            
        res += 1

        return res

# time O(nlogn)
# space O(1), not counting built in sort cost
# using array and line sweep and compare two intervals each round and sort and greedy
'''
1. only end ptr matters
'''
```


## 📄 [H]array\[H]array-line-sweep\56-merge-intervals.java

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> a[0] == b[0] ? Integer.compare(a[1], b[1]) : Integer.compare(a[0], b[0]));
        ArrayList<int[]> res = new ArrayList<>();
        int prevS = intervals[0][0];
        int prevE = intervals[0][1];
        for (int i = 1; i < intervals.length; i++) {
            int curS = intervals[i][0];
            int curE = intervals[i][1];
            if (prevE < curS) {
                res.add(new int[]{prevS, prevE});
                prevS = curS;
                prevE = curE;
            } else {
                prevE = Math.max(prevE, curE);
            }
        }
        res.add(new int[]{prevS, prevE});
        return res.toArray(new int[res.size()][2]);
    }
}

// time O(nlogn)
// space O(n), due to output and sort
// using array and line sweep and compare two intervals each round and sort
```


## 📄 [H]array\[H]array-line-sweep\56-merge-intervals.py

```py
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        
        intervals.sort()

        res = []
        prev_s, prev_e = intervals[0]
        for i in range(1, len(intervals)):
            cur_s, cur_e = intervals[i]
            if prev_e < cur_s:
                res.append([prev_s, prev_e])
                prev_s, prev_e = cur_s, cur_e
            else:
                prev_e = max(prev_e, cur_e)

        res.append([prev_s, prev_e])

        return res
        
# time O(nlogn)
# space O(n), due to output and sort
# using array and line sweep and compare two intervals each round and sort

class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        
        events = []
        for s, e in intervals:
            events.append((s, 1))
            events.append((e, - 1))
        events.sort(key = lambda x: (x[0], - x[1]))

        res = []
        status = 0
        prev_timestamp = 0

        for timestamp, weight in events:
            if status == 0 and weight == 1:
                prev_timestamp = timestamp
            if status == 1 and weight == - 1:
                res.append([prev_timestamp, timestamp])
            status += weight

        return res
                
# time O(nlogn)
# space O(n), due to output and sort
# using array and line sweep and sort
'''
1. if certain timestamp have both start and end event, let start event become first
'''

```


## 📄 [H]array\[H]array-line-sweep\57-insert-interval.java

```java
class Solution {
  public int[][] insert(int[][] intervals, int[] newInterval) {
      int prevS = newInterval[0];
      int prevE = newInterval[1];
      ArrayList<int[]> res = new ArrayList<>();

      for (int i = 0; i < intervals.length; i++) {
          int curS = intervals[i][0];
          int curE = intervals[i][1];
          if (prevE < curS) {
              res.add(new int[]{prevS, prevE});
              res.addAll(Arrays.asList(Arrays.copyOfRange(intervals, i, intervals.length)));
              return res.toArray(new int[res.size()][2]);
          } else if (prevS > curE) {
              res.add(new int[]{curS, curE});
          } else {
              prevS = Math.min(prevS, curS);
              prevE = Math.max(prevE, curE);
          }
      }
      res.add(new int[]{prevS, prevE});
      return res.toArray(new int[res.size()][2]);
  }
}

// time O(n)
// space O(n), due to output list
// using array and line sweep and compare two intervals each round
```


## 📄 [H]array\[H]array-line-sweep\57-insert-interval.py

```py
class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:

        res = []
        prev_s, prev_e = newInterval
        for i, (cur_s, cur_e) in enumerate(intervals):
            if prev_e < cur_s:
                res.append([prev_s, prev_e])
                res.extend(intervals[i:])
                return res
            elif prev_s > cur_e:
                res.append([cur_s, cur_e])
            else:
                prev_s, prev_e = min(prev_s, cur_s), max(prev_e, cur_e)

        res.append([prev_s, prev_e])

        return res

# time O(n)
# space O(n), due to output list
# using array and line sweep and compare two intervals each round
```


## 📄 [H]array\[H]array-line-sweep\757-set-intersection-size-at-least-two.py

```py
class Solution:
    def intersectionSizeTwo(self, intervals: List[List[int]]) -> int:
        
        intervals.sort(key = lambda x: x[1])

        res = 0
        prev_s, prev_e = intervals[0][1] - 1, intervals[0][1]
        for i in range(1, len(intervals)):
            cur_s, cur_e = intervals[i]
            if prev_e < cur_s:
                res += 2
                prev_s, prev_e = cur_e - 1, cur_e
            elif prev_s < cur_s:
                res += 1
                if prev_e != cur_e:
                    prev_s, prev_e = prev_e, cur_e
                else:
                    prev_s, prev_e = cur_e - 1, cur_e
                
        res += 2
            
        return res

# time O(nlogn)
# space O(1), or due to built in sort's cost
# using array and line sweep and compare two intervals each round and sort and greedy
'''
1. sort by end, so we can handle early end's interval first
2-1. greedly choose last two number because they get better chance to overlap with others
2-2. if we are not sorting by end, then we cannot decide how to choose the best two number
3-1. totally miss
3-2-1. only cover one number (one num remain, one num is new interval end)
3-2-2. only cover one number (one num remain, but collision with new interval end)
'''
```


## 📄 [H]array\[H]array-line-sweep\986-interval-list-intersections.py

```py
class Solution:
    def intervalIntersection(self, firstList: List[List[int]], secondList: List[List[int]]) -> List[List[int]]:
        i, j = 0, 0
        res = []
        while i < len(firstList) and j < len(secondList):
            s1, e1 = firstList[i]
            s2, e2 = secondList[j]
            if e1 < s2:
                i += 1
            elif e2 < s1:
                j += 1
            else:
                res.append([max(s1, s2), min(e1, e2)])
                if e1 > e2:
                    j += 1
                else:
                    i += 1

        return res
    
# time O(m+n)
# space O(m+n), for output list
# using array and line sweep and compare two intervals each round and two pointers and greedy
```


## 📄 [H]array\[H]array-prefix-sum\1031-maximum-sum-of-two-non-overlapping-subarrays.py

```py
class Solution:
    def maxSumTwoNoOverlap(self, nums: List[int], firstLen: int, secondLen: int) -> int:
        
        prefix = [0 for _ in range(len(nums) + 1)]
        total = 0
        for i, num in enumerate(nums):
            total += num
            prefix[i + 1] = total

        def get_sum(p, q):
            max_p = prefix[p]
            max_pq = prefix[p + q]
            for i in range(p + q, len(nums)):
                cur_p = prefix[i - q + 1] - prefix[i - p - q + 1]
                cur_q = prefix[i + 1] - prefix[i - q + 1]
                max_p = max(max_p, cur_p)
                max_pq = max(max_pq, cur_q + max_p)
            return max_pq

        return max(get_sum(firstLen, secondLen), get_sum(secondLen, firstLen))

# time O(n)
# space O(n)
# using array and prefix sum and standard prefix sum and sliding window
'''
1. subarrayA is before subarrayB
2. subarrayB is before subarrayA
3. prefix sum is just for simplify calc, can solve by sliding window only
'''
```


## 📄 [H]array\[H]array-prefix-sum\1248-count-number-of-nice-subarrays.py

```py
from collections import defaultdict
class Solution:
    def numberOfSubarrays(self, nums: List[int], k: int) -> int:
        prefix_count = defaultdict(int)
        prefix_count[0] = 1

        total = 0
        res = 0
        for num in nums:
            if num % 2:
                total += 1
            res += prefix_count[total - k]
            prefix_count[total] += 1
        return res
    
# time O(n)
# space O(n)
# using array and prefix sum and hashmap to validate the gap subarray
```


## 📄 [H]array\[H]array-prefix-sum\2055-plates-between-candles.py

```py
class Solution:
    def platesBetweenCandles(self, s: str, queries: List[List[int]]) -> List[int]:
        
        right_cand = [len(s) for _ in range(len(s))]
        left_cand = [0 for _ in range(len(s))]

        idx = 0
        for i in range(len(s)):
            if s[i] == '|':
                idx = i
            left_cand[i] = idx
        idx = len(s)
        for i in range(len(s) - 1, - 1, - 1):
            if s[i] == '|':
                idx = i
            right_cand[i] = idx
        
        prefix = [0 for _ in range(len(s) + 1)]
        total = 0
        for i, c in enumerate(s):
            if c == '*':
                total += 1
            prefix[i + 1] = total
        
        res = []
        for s, e in queries:
            left_bound = right_cand[s]
            right_bound = left_cand[e]
            if left_bound <= right_bound:
                res.append(prefix[right_bound + 1] - prefix[left_bound])
            else:
                res.append(0)
        return res
            
# time O(n+q)
# space O(n), due to preprocessing lists, not counting output
# using array and prefix sum and standard prefix sum
'''
1. boundary processing
2. prefix sum
'''
```


## 📄 [H]array\[H]array-prefix-sum\2100-find-good-days-to-rob-the-bank.py

```py
class Solution:
    def goodDaysToRobBank(self, security: List[int], time: int) -> List[int]:
        inc_prefix = [0 for _ in range(len(security))]
        dec_prefix = [0 for _ in range(len(security))]

        inc = 0
        dec = 0
        for i in range(1, len(security)):
            if security[i - 1] > security[i]:
                dec += 1
            elif security[i - 1] < security[i]:
                inc += 1
            dec_prefix[i] = dec
            inc_prefix[i] = inc

        res = []
        for i in range(time, len(security) - time):
            inc_before = inc_prefix[i] - inc_prefix[i - time]
            dec_after = dec_prefix[i + time] - dec_prefix[i]

            if inc_before == 0 and dec_after == 0:
                res.append(i)

        return res
    
# time O(n)
# space O(n)
# using array and prefix sum and standard prefix sum
```


## 📄 [H]array\[H]array-prefix-sum\2256-minimum-average-difference.py

```py
class Solution:
    def minimumAverageDifference(self, nums: List[int]) -> int:
        
        prefix = [0 for _ in range(len(nums) + 1)]
        total = 0
        for i, num in enumerate(nums):
            total += num
            prefix[i + 1] = total

        res = float('inf')
        res_idx = - 1
        for i in range(len(nums)):
            first_avg = prefix[i + 1] // (i + 1)
            second_avg = (prefix[- 1] - prefix[i + 1]) // (len(nums) - i - 1) if len(nums) - i - 1 != 0 else 0
            diff = abs(first_avg - second_avg)
            if diff < res:
                res = diff
                res_idx = i
        return res_idx
    
# time O(n)
# space O(n)
# using array and prefix sum and standard prefix sum
```


## 📄 [H]array\[H]array-prefix-sum\238-product-of-array-except-self.java

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int[] res = new int[nums.length];
        Arrays.fill(res, 1);
        int total = 1;
        for (int i = 0; i < nums.length; i++) {
            res[i] = total;
            total *= nums[i];
        }
        total = 1;
        for (int i = nums.length - 1; i >= 0; i--) {
            res[i] *= total;
            total *= nums[i];
        }
        return res;
    }
}

// time O(n)
// space O(1), not counting output list
// using array and prefix sum and standard prefix sum
```


## 📄 [H]array\[H]array-prefix-sum\238-product-of-array-except-self.py

```py
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        res = [1 for _ in range(len(nums))]

        total = 1
        for i, num in enumerate(nums):
            res[i] = total
            total *= num
        
        total = 1
        for i in range(len(nums) - 1, - 1, - 1):
            res[i] *= total
            total *= nums[i]

        return res
    
# time O(n)
# space O(1), not counting output list
# using array and prefix sum and standard prefix sum
```


## 📄 [H]array\[H]array-prefix-sum\303-range-sum-query-immutable.py

```py
class NumArray:
    def __init__(self, nums: List[int]):
        self.prefix = [0 for _ in range(len(nums) + 1)]
        total = 0
        for i, num in enumerate(nums):
            total += num
            self.prefix[i + 1] = total

    def sumRange(self, left: int, right: int) -> int:
        return self.prefix[right + 1] - self.prefix[left]

# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# param_1 = obj.sumRange(left,right)

# time O(1) for sumRange(), O(n) for initiation
# space O(n)
# using array and prefix sum and standard prefix sum
```


## 📄 [H]array\[H]array-prefix-sum\304-range-sum-query-2d-immutable.py

```py
class NumMatrix:

    def __init__(self, matrix: List[List[int]]):
        rows, cols = len(matrix), len(matrix[0])
        self.prefix = [[0 for _ in range(cols + 1)] for _ in range(rows + 1)]
        for r in range(rows):
            total = 0
            for c in range(cols):
                total += matrix[r][c]
                self.prefix[r + 1][c + 1] = self.prefix[r][c + 1] + total

    def sumRegion(self, row1: int, col1: int, row2: int, col2: int) -> int:
        return self.prefix[row2 + 1][col2 + 1] - self.prefix[row1][col2 + 1] - self.prefix[row2 + 1][col1] + self.prefix[row1][col1]


# Your NumMatrix object will be instantiated and called as such:
# obj = NumMatrix(matrix)
# param_1 = obj.sumRegion(row1,col1,row2,col2)

# time O(1) for sumRegion(), O(RC) for init
# space O(RC)
# using array and prefix sum and standard prefix sum
```


## 📄 [H]array\[H]array-prefix-sum\325-maximum-size-subarray-sum-equals-k.py

```py
class Solution:
    def maxSubArrayLen(self, nums: List[int], k: int) -> int:
        prefix_idx = {}
        prefix_idx[0] = - 1

        total = 0
        res = 0
        for i, num in enumerate(nums):
            total += num
            if total - k in prefix_idx:
                res = max(res, i - prefix_idx[total - k])
            if total not in prefix_idx:
                prefix_idx[total] = i
        return res
    
# time O(n)
# space O(n)
# using array and prefix sum and hashmap to validate the gap subarray
```


## 📄 [H]array\[H]array-prefix-sum\363-max-sum-of-rectangle-no-larger-than-k.py

```py
from sortedcontainers import SortedDict
class Solution:
    def maxSumSubmatrix(self, matrix: List[List[int]], k: int) -> int:
        rows, cols = len(matrix), len(matrix[0])

        prefix = [[0 for _ in range(cols + 1)] for _ in range(rows + 1)]
        for r in range(rows):
            total = 0
            for c in range(cols):
                total += matrix[r][c]
                prefix[r + 1][c + 1] = total
        
        def get_sum(part_rows):
            prefix_dict = SortedDict()
            prefix_dict[0] = - 1
            total = 0
            res = float('-inf')
            for r, part_row in enumerate(part_rows):
                total += part_row
                idx = prefix_dict.bisect_left(total - k)
                if idx < len(prefix_dict):
                    res = max(res, total - prefix_dict.peekitem(idx)[0])
                if total not in prefix_dict:
                    prefix_dict[total] = r
            return res

        res = float('-inf')
        for lc in range(cols):
            for rc in range(lc, cols):
                part_rows = [row[rc + 1] - row[lc] for i, row in enumerate(prefix) if i > 0]
                res = max(res, get_sum(part_rows))
        return res
    
# time O(C**2 * RlogR)
# space O(RC)
# using array and prefix sum and hashmap to validate the gap subarray and binary search
```


## 📄 [H]array\[H]array-prefix-sum\523-continuous-subarray-sum.py

```py
class Solution:
    def checkSubarraySum(self, nums: List[int], k: int) -> bool:
        prefix_idx = {}
        prefix_idx[0] = - 1

        total = 0
        for i, num in enumerate(nums):
            total += num
            total %= k
            if total in prefix_idx and i - prefix_idx[total] >= 2:
                return True
            if total not in prefix_idx:
                prefix_idx[total] = i
        return False
    
# time O(n)
# space O(n)
# using array and prefix sum and hashmap to validate the gap subarray
```


## 📄 [H]array\[H]array-prefix-sum\525-contiguous-array.py

```py
class Solution:
    def findMaxLength(self, nums: List[int]) -> int:
        nums = [- 1 if num == 0 else 1 for num in nums]

        prefix_idx = {}
        prefix_idx[0] = - 1
        total = 0
        res = 0
        for i, num in enumerate(nums):
            total += num
            if total in prefix_idx:
                res = max(res, i - prefix_idx[total])
            else:
                prefix_idx[total] = i
        return res

# time O(n)
# space O(n)
# using array and prefix sum and hashmap to validate the gap subarray
'''
1. if meet the same prefix in hashmap means the gap is balanced
'''
```


## 📄 [H]array\[H]array-prefix-sum\548-split-array-with-equal-sum.py

```py
class Solution:
    def splitArray(self, nums: List[int]) -> bool:
        prefix = [0 for _ in range(len(nums) + 1)]
        total = 0
        for i, num in enumerate(nums):
            total += num
            prefix[i + 1] = total

        for j in range(3, len(nums) - 3):
            prefix_set = set()
            for i in range(1, j - 1):
                if prefix[i] == prefix[j] - prefix[i + 1]:
                    prefix_set.add(prefix[i])
            for k in range(j + 2, len(nums) - 1):
                if prefix[k] - prefix[j + 1] == prefix[- 1] - prefix[k + 1]:
                    if prefix[k] - prefix[j + 1] in prefix_set:
                        return True
        return False
        
# time O(n**2)
# space O(n)
# using array and prefix sum and hashmap to validate the gap subarray       
'''
1. xixjxkx
   0123456
'''
```


## 📄 [H]array\[H]array-prefix-sum\560-subarray-sum-equals-k.java

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int res = 0;
        HashMap<Integer, Integer> valToFreq = new HashMap<>();
        valToFreq.put(0, 1);
        int total = 0;
        for (int num: nums) {
            total += num;
            if (valToFreq.containsKey(total - k)) {
                res += valToFreq.get(total - k);
            }
            valToFreq.compute(total, (key, v) -> v == null ? 1 : v + 1);
        }
        return res;
    }
}

// time O(n)
// space O(n)
// using array and prefix sum and hashmap to validate the gap subarray
/*
1. if meet the prefix - k in hashmap means the gap is valid
*/
```


## 📄 [H]array\[H]array-prefix-sum\560-subarray-sum-equals-k.py

```py
from collections import defaultdict
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        prefix_count = defaultdict(int)
        prefix_count[0] = 1
        total = 0
        res = 0
        for num in nums:
            total += num
            res += prefix_count[total - k]
            prefix_count[total] += 1
        return res
    
# time O(n)
# space O(n)
# using array and prefix sum and hashmap to validate the gap subarray
'''
1. if meet the prefix - k in hashmap means the gap is valid
'''
```


## 📄 [H]array\[H]array-prefix-sum\724-find-pivot-index.py

```py
class Solution:
    def pivotIndex(self, nums: List[int]) -> int:
        prefix = [0 for _ in range(len(nums) + 1)]
        total = 0
        for i, num in enumerate(nums):
            total += num
            prefix[i + 1] = total

        for i in range(len(nums)):
            if prefix[i] == prefix[len(nums)] - prefix[i + 1]:
                return i
        return - 1
    
# time O(n)
# space O(n)
# using array and prefix sum and standard prefix sum
```


## 📄 [H]array\[H]array-prefix-sum\974-subarray-sums-divisible-by-k.py

```py
from collections import defaultdict
class Solution:
    def subarraysDivByK(self, nums: List[int], k: int) -> int:
        prefix_count = defaultdict(int)
        prefix_count[0] = 1

        total = 0
        res = 0
        for num in nums:
            total += num
            total %= k
            res += prefix_count[total]
            prefix_count[total] += 1
        return res
    
# time O(n), due to traverse
# space O(n)
# using array and prefix sum and hashmap to validate the gap subarray
```


## 📄 [H]array\[H]array-sliding-window\1100-find-k-length-substrings-with-no-repeated-characters.py

```py
from collections import defaultdict
class Solution:
    def numKLenSubstrNoRepeats(self, s: str, k: int) -> int:
        char_freq = defaultdict(int)
        res = 0
        left = 0
        for right in range(len(s)):
            char_freq[s[right]] += 1
            while right - left + 1 > k or char_freq[s[right]] > 1:
                char_freq[s[left]] -= 1
                if char_freq[s[left]] == 0:
                    char_freq.pop(s[left])
                left += 1
            if len(char_freq) == k:
                res += 1
        return res
    
# time O(n)
# space O(k)
# using array and standard sliding window and hashmap
```


## 📄 [H]array\[H]array-sliding-window\1151-minimum-swaps-to-group-all-1s-together.py

```py
class Solution:
    def minSwaps(self, data: List[int]) -> int:
        count_total = 0
        for num in data:
            if num == 1:
                count_total += 1
        
        res = count_total
        count = 0
        left = 0
        for right in range(len(data)):
            if data[right] == 1:
                count += 1
            while right - left + 1 > count_total:
                if data[left] == 1:
                    count -= 1
                left += 1
            if right - left + 1 == count_total:
                res = min(res, right - left + 1 - count)
        return res

# time O(n)
# space O(1)
# using array and standard sliding window
```


## 📄 [H]array\[H]array-sliding-window\1423-maximum-points-you-can-obtain-from-cards.py

```py
class Solution:
    def maxScore(self, cardPoints: List[int], k: int) -> int:
        res = float('inf')
        total = 0
        left = 0
        for right in range(len(cardPoints)):
            total += cardPoints[right]
            while right - left + 1 > len(cardPoints) - k:
                total -= cardPoints[left]
                left += 1
            if right - left + 1 == len(cardPoints) - k:
                res = min(res, total)
        return sum(cardPoints) - res

# time O(n)
# space O(1)
# using array and standard sliding window
```


## 📄 [H]array\[H]array-sliding-window\209-minimum-size-subarray-sum.py

```py
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        res = float('inf')
        total = 0
        left = 0
        for right in range(len(nums)):
            total += nums[right]
            while total >= target:
                res = min(res, right - left + 1)
                total -= nums[left]
                left += 1
        return res if res != float('inf') else 0

# time O(n)
# space O(1)
# using array and shrink type sliding window
'''
1. notice: only works for positive elements
2. if num can be negative then use monotonic queue and prefix sum and sliding window
3. think about [20, -30, 20, 10] and 30, correct res should be 2
'''

class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        
        def valid(length):
            total = 0
            for i in range(len(nums)):
                total += nums[i]
                if i >= length:
                    total -= nums[i - length]
                if total >= target:
                    return True
            return False
        
        left, right, boundary = 1, len(nums), 0
        while left <= right:
            m = (left + right) // 2
            if valid(m):
                boundary = m
                right = m - 1
            else:
                left = m + 1
        return boundary
    
# time O(nlogn)
# space O(1)
# using binary search and search in sth’s range
'''
1. notice: only works for positive elements
2. if num can be negative then use monotonic queue and prefix sum and sliding window
3. think about [-10, -10, -10, 20] and 20, correct res should be 1
'''

class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        prefix = [0 for _ in range(len(nums) + 1)]
        total = 0
        for i, num in enumerate(nums):
            total += num
            prefix[i + 1] = total
        
        res = float('inf')
        mono_queue = deque([])
        for i in range(len(prefix)):
            while mono_queue and prefix[i] - prefix[mono_queue[0]] >= target:
                idx = mono_queue.popleft()
                res = min(res, i - idx)
            while mono_queue and prefix[i] <= prefix[mono_queue[- 1]]:
                mono_queue.pop()
            mono_queue.append(i)
        return res if res != float('inf') else 0

# time O(n)
# space O(n)
# using monotonic queue and prefix sum and sliding window
```


## 📄 [H]array\[H]array-sliding-window\2134-minimum-swaps-to-group-all-1s-together-ii.py

```py
class Solution:
    def minSwaps(self, nums: List[int]) -> int:
        count_total = 0
        for num in nums:
            if num == 1:
                count_total += 1
        
        res = count_total
        count = 0
        left = 0
        for right in range(len(nums) * 2):
            mod_right = right % len(nums)
            if nums[mod_right] == 1:
                count += 1
            while right - left + 1 > count_total:
                mod_left = left % len(nums)
                if nums[mod_left] == 1:
                    count -= 1
                left += 1
            if right - left + 1 == count_total:
                res = min(res, right - left + 1 - count)
        return res

# time O(n)
# space O(1)
# using array and standard sliding window
```


## 📄 [H]array\[H]array-sliding-window\3-longest-substring-without-repeating-characters.java

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        HashMap<Character, Integer> charToFreq = new HashMap<>();
        int res = 0;
        int left = 0;
        for (int right = 0; right < s.length(); right++) {
            Character c = s.charAt(right);
            charToFreq.compute(c, (k, v) -> v == null ? 1 : v + 1);
            while (charToFreq.get(c) > 1) {
                Character removeC = s.charAt(left);
                charToFreq.put(removeC, charToFreq.get(removeC) - 1);
                if (Objects.equals(charToFreq.get(removeC), 0)) {
                    charToFreq.remove(removeC);
                }
                left += 1;
            }
            res = Math.max(res, right - left + 1);
        }
        return res;
    }
}

// time O(n)
// space O(1), due to the hashmap could contain all unique chars
// using array and standard sliding window and hashmap
```


## 📄 [H]array\[H]array-sliding-window\3-longest-substring-without-repeating-characters.py

```py
from collections import defaultdict
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        char_freq = defaultdict(int)
        res = 0
        left = 0
        for right in range(len(s)):
            char_freq[s[right]] += 1
            while char_freq[s[right]] > 1:
                char_freq[s[left]] -= 1
                if char_freq[s[left]] == 0:
                    char_freq.pop(s[left])
                left += 1
            res = max(res, right - left + 1)
        return res
        
# time O(n)
# space O(1), due to the hashmap could contain all unique chars
# using array and standard sliding window and hashmap
```


## 📄 [H]array\[H]array-sliding-window\30-substring-with-concatenation-of-all-words.py

```py
from collections import defaultdict
class Solution:
    def findSubstring(self, s: str, words: List[str]) -> List[int]:
        word_freq = defaultdict(int)
        for w in words:
            word_freq[w] += 1
        count_total = len(word_freq)
        
        res = []
        L = len(words[0])
        M = len(words)
        for start in range(L):
            sword_freq = defaultdict(int)
            count = 0
            left = start
            for right in range(start, len(s), L):
                w = s[right: right + L]
                sword_freq[w] += 1
                if sword_freq[w] == word_freq[w]:
                    count += 1
                while right - left + L > L * M or sword_freq[w] > word_freq[w]:
                    remove_w = s[left: left + L]
                    if sword_freq[remove_w] == word_freq[remove_w]:
                        count -= 1
                    sword_freq[remove_w] -= 1
                    if sword_freq[remove_w] == 0:
                        sword_freq.pop(remove_w)
                    left += L
                if count == count_total:
                    res.append(left)
        return res
    
# time O(L * n + m), L is the length of word in words, n is the length of s, and m is the length of words
# space O(m)
# using array and standard sliding window and hashmap
'''
1. enumerate each possible starting point
'''
```


## 📄 [H]array\[H]array-sliding-window\340-longest-substring-with-at-most-k-distinct-characters.py

```py
from collections import defaultdict
class Solution:
    def lengthOfLongestSubstringKDistinct(self, s: str, k: int) -> int:
        char_freq = defaultdict(int)
        res = 0
        left = 0
        for right in range(len(s)):
            char_freq[s[right]] += 1
            while len(char_freq) > k:
                char_freq[s[left]] -= 1
                if char_freq[s[left]] == 0:
                    char_freq.pop(s[left])
                left += 1
            res = max(res, right - left + 1)
        return res
                
# time O(n), due to traverse
# space O(k), due to hashmap
# using array and standard sliding window and hashmap
```


## 📄 [H]array\[H]array-sliding-window\395-longest-substring-with-at-least-k-repeating-characters.py

```py
from collections import defaultdict
class Solution:
    def longestSubstring(self, s: str, k: int) -> int:
        res = 0

        for unique_char_count in range(1, 27):
            char_freq = defaultdict(int)
            count = 0
            left = 0
            for right in range(len(s)):
                char_freq[s[right]] += 1
                if char_freq[s[right]] == k:
                    count += 1
                while len(char_freq) > unique_char_count:
                    if char_freq[s[left]] == k:
                        count -= 1
                    char_freq[s[left]] -= 1
                    if char_freq[s[left]] == 0:
                        char_freq.pop(s[left])
                    left += 1
                if count == unique_char_count:
                    res = max(res, right - left + 1)
        return res
    
# time O(n)
# space O(1), due to hashmap
# using array and standard sliding window and hashmap
'''
1-1. when perform naive sliding window, we cannot decide when to move left ptr
1-2. because we do not know how to define the invalid state
2-1. by enumerate how many unique chars should inside the windwow,
2-2. now we know when is valid or invalid (when to move left ptr)
'''
```


## 📄 [H]array\[H]array-sliding-window\424-longest-repeating-character-replacement.java

```java
class Solution {
    public int characterReplacement(String s, int k) {
        HashMap<Character, Integer> charToFreq = new HashMap<>();
        int max = 0;
        int res = 0;
        int left = 0;
        for (int right = 0; right < s.length(); right++) {
            Character c = s.charAt(right);
            charToFreq.compute(c, (key, v) -> v == null ? 1 : v + 1);
            if (charToFreq.get(c) > max) {
                max = charToFreq.get(c);
            }
            while (max + k < right - left + 1) {
                Character remove_c = s.charAt(left);
                charToFreq.put(remove_c, charToFreq.get(remove_c) - 1);
                if (charToFreq.get(remove_c) == 0) {
                    charToFreq.remove(remove_c);
                }
                left += 1;
            }
            res = Math.max(res, right - left + 1);
        }
        return res;
    }
}

// time O(n)
// space O(1)
// using array and standard sliding window and hashmap and greedy
```


## 📄 [H]array\[H]array-sliding-window\424-longest-repeating-character-replacement.py

```py
from collections import defaultdict
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        char_freq = defaultdict(int)
        res = 0
        max_freq = 0
        left = 0
        for right in range(len(s)):
            char_freq[s[right]] += 1
            if char_freq[s[right]] > max_freq:
                max_freq = char_freq[s[right]]
            while max_freq + k < right - left + 1:
                char_freq[s[left]] -= 1
                if char_freq[s[left]] == 0:
                    char_freq.pop(s[left])
                left += 1
            res = max(res, right - left + 1)
        return res
    
# time O(n)
# space O(1)
# using array and standard sliding window and hashmap and greedy
```


## 📄 [H]array\[H]array-sliding-window\438-find-all-anagrams-in-a-string.java

```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> res = new ArrayList<>();
        HashMap<Character, Integer> pcharToFreq = new HashMap<>();
        for (int i = 0; i < p.length(); i++) {
            pcharToFreq.compute(p.charAt(i), (k, v) -> v == null ? 1 : v + 1);
        }
        HashMap<Character, Integer> subcharToFreq = new HashMap<>();
        int total = pcharToFreq.size();
        int match = 0;
        int left = 0;
        for (int right = 0; right < s.length(); right++) {
            subcharToFreq.compute(s.charAt(right), (k, v) -> v == null ? 1 : v + 1);
            if (Objects.equals(subcharToFreq.get(s.charAt(right)), pcharToFreq.get(s.charAt(right)))) {
                match += 1;
            }
            while (right - left + 1 > p.length()) {
                Character c = s.charAt(left);
                if (Objects.equals(subcharToFreq.get(c), pcharToFreq.get(c))) {
                    match -= 1;
                }
                subcharToFreq.put(c, subcharToFreq.get(c) - 1);
                if (Objects.equals(subcharToFreq.get(c), 0)) {
                    subcharToFreq.remove(c);
                }
                left += 1;
            }
            if (match == total) {
                res.add(left);
            }
        }
        return res;
    }
}

// time O(m+n), due to traverse
// space O(1), not counting output
// using array and standard sliding window and hashmap
```


## 📄 [H]array\[H]array-sliding-window\438-find-all-anagrams-in-a-string.py

```py
from collections import defaultdict
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        pchar_freq = defaultdict(int)
        for c in p:
            pchar_freq[c] += 1
        
        res = []
        match_total = len(pchar_freq)
        match = 0
        schar_freq = defaultdict(int)
        left = 0
        for right in range(len(s)):
            schar_freq[s[right]] += 1
            if schar_freq[s[right]] == pchar_freq[s[right]]:
                match += 1
            while right - left + 1 > len(p):
                if schar_freq[s[left]] == pchar_freq[s[left]]:
                    match -= 1
                schar_freq[s[left]] -= 1
                if schar_freq[s[left]] == 0:
                    schar_freq.pop(s[left])
                left += 1
            if match == match_total:
                res.append(left)
        return res

# time O(m+n), due to traverse
# space O(1), not counting output
# using array and standard sliding window and hashmap
```


## 📄 [H]array\[H]array-sliding-window\567-permutation-in-string.py

```py
from collections import defaultdict
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        tchar_freq = defaultdict(int)
        for c in s1:
            tchar_freq[c] += 1

        match_total = len(tchar_freq)
        match = 0
        schar_freq = defaultdict(int)
        left = 0
        for right in range(len(s2)):
            schar_freq[s2[right]] += 1
            if schar_freq[s2[right]] == tchar_freq[s2[right]]:
                match += 1
            while right - left + 1 > len(s1):
                if schar_freq[s2[left]] == tchar_freq[s2[left]]:
                    match -= 1
                schar_freq[s2[left]] -= 1
                if schar_freq[s2[left]] == 0:
                    schar_freq.pop(s2[left])
                left += 1
            if match == match_total:
                return True
        return False
    
# time O(m+n)
# space O(1)
# using array and standard sliding window and hashmap
```


## 📄 [H]array\[H]array-sliding-window\76-minimum-window-substring.py

```py
from collections import defaultdict
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        tchar_freq = defaultdict(int)
        for c in t:
            tchar_freq[c] += 1
        count_total = len(tchar_freq)

        res = float('inf')
        res_idx = - 1
        schar_freq = defaultdict(int)
        count = 0
        left = 0
        for right in range(len(s)):
            schar_freq[s[right]] += 1
            if schar_freq[s[right]] == tchar_freq[s[right]]:
                count += 1
            while count == count_total:
                if right - left + 1 < res:
                    res = right - left + 1
                    res_idx = left
                if schar_freq[s[left]] == tchar_freq[s[left]]:
                    count -= 1
                schar_freq[s[left]] -= 1
                if schar_freq[s[left]] == 0:
                    schar_freq.pop(s[left])
                left += 1
        return s[res_idx: res_idx + res] if res != float('inf') else ''

# time O(m+n)
# space O(1)
# using array and shrink type sliding window and hashmap
```


## 📄 [H]array\[H]array-sliding-window\904-fruit-into-baskets.py

```py
from collections import defaultdict
class Solution:
    def totalFruit(self, fruits: List[int]) -> int:
        type_freq = defaultdict(int)
        res = 0
        left = 0
        for right in range(len(fruits)):
            type_freq[fruits[right]] += 1
            while len(type_freq) > 2:
                type_freq[fruits[left]] -= 1
                if type_freq[fruits[left]] == 0:
                    type_freq.pop(fruits[left])
                left += 1
            res = max(res, right - left + 1)
        return res
    
# time O(n)
# space O(1)
# using array and standard sliding window and hashmap
```


## 📄 [H]array\[H]array-sort\1099-two-sum-less-than-k.py

```py
class Solution:
    def twoSumLessThanK(self, nums: List[int], k: int) -> int:
        min_num = min(nums)
        max_num = max(nums)
        buckets = [0 for _ in range(max_num - min_num + 1)]
        for num in nums:
            buckets[num - min_num] += 1

        res = - 1
        left, right = 0, len(buckets) - 1
        while left <= right:
            cur = left + min_num + right + min_num
            if buckets[left] == 0:
                left += 1
            elif buckets[right] == 0:
                right -= 1
            elif left == right and buckets[left] < 2:
                break
            elif cur < k:
                res = max(res, cur)
                left += 1
            else:
                right -= 1
        return res

# time O(n + b)
# space O(b)
# using array and sort and bucket sort and two pointers
```


## 📄 [H]array\[H]array-sort\164-maximum-gap.py

```py
class Solution:
    def maximumGap(self, nums: List[int]) -> int:
        min_num = min(nums)
        max_num = max(nums)
        if min_num == max_num or len(nums) < 2:
            return 0

        interval = max(1, (max_num - min_num) // len(nums))
        buckets_count = (max_num - min_num) // interval + 1
        buckets = [[False, float('inf'), float('-inf')] for _ in range(buckets_count)]
        for num in nums:
            idx = (num - min_num) // interval
            buckets[idx] = [True, min(buckets[idx][1], num), max(buckets[idx][2], num)]
        
        buckets = [[min_val, max_val] for filled, min_val, max_val in buckets if filled]
        res = 0
        for i in range(1, len(buckets)):
            res = max(res, buckets[i][0] - buckets[i - 1][1])

        return res
    
# time O(n + b)
# space O(b)
# using array and sort and bucket sort and pigeonhole principle
'''
1. pigeonhole principle
2. n+1 pigeons live in n holes, at least one hole have two or more pigeons
3. n pigeons live in n+1 holes, at least one hole is empty
4. so we need to make buckets more than length of nums
5. if there is a empty hole, 
   the maximum difference cannot be within a single bucket but between the numbers in different buckets
6. even if all buckets are filled, 
   the maximum gap is still likely to occur between the maximum value of one bucket and the minimum value of an adjacent bucket
   this is because the numbers within each bucket are relatively close to each other, given the way the interval size is determined
'''
```


## 📄 [H]array\[H]array-sort\1710-maximum-units-on-a-truck.py

```py
class Solution:
    def maximumUnits(self, boxTypes: List[List[int]], truckSize: int) -> int:
        
        max_box_size = max(boxTypes, key = lambda x: x[1])[1]
        min_box_size = min(boxTypes,  key = lambda x: x[1])[1]

        buckets = [0 for _ in range(max_box_size - min_box_size + 1)]
        for count, size in boxTypes:
            buckets[size - min_box_size] += count
        
        res = 0
        for i in range(len(buckets) - 1, - 1, - 1):
            if buckets[i] <= truckSize:
                res += buckets[i] * (i + min_box_size)
                truckSize -= buckets[i]
            elif truckSize:
                res += truckSize * (i + min_box_size)
                truckSize -= truckSize
            else:
                break
        return res

# time O(n+b)
# space O(b)
# using array and sort and bucket sort and greedy
```


## 📄 [H]array\[H]array-sort\179-largest-number.py

```py
class Solution:
    def largestNumber(self, nums: List[int]) -> str:

        nums = [str(num) for num in nums]
        
        def merge_sort(nums):
            n = len(nums)
            if n <= 1:
                return nums
            m = n // 2
            left_part = merge_sort(nums[: m])
            right_part = merge_sort(nums[m:])
            res = []
            left, right = 0, 0
            while left < m or right < n - m:
                if left == m:
                    res.append(right_part[right])
                    right += 1
                elif right == n- m:
                    res.append(left_part[left])
                    left += 1
                elif left_part[left] + right_part[right] >= right_part[right] + left_part[left]:
                    res.append(left_part[left])
                    left += 1
                else:
                    res.append(right_part[right])
                    right += 1
            return res

        nums = merge_sort(nums)
        res = ''.join(nums)
        return res if res[0] != '0' else '0'

# time O(nlogn), logn recursion layers and each layer costs O(n)
# space O(n), due to new list, recursion stack is O(logn)
# using array and sort and self defined merge sort
# stable

import random
class Solution:
    def largestNumber(self, nums: List[int]) -> str:

        nums = [str(num) for num in nums]
        
        def quick_sort(left, right):
            if left >= right:
                return
            pivot_idx = random.randint(left, right)
            pivot_val = nums[pivot_idx]
            nums[right], nums[pivot_idx] = nums[pivot_idx], nums[right]
            partition_idx = left
            for i in range(left, right):
                if nums[i] + pivot_val > pivot_val + nums[i]:
                    nums[i], nums[partition_idx] = nums[partition_idx], nums[i]
                    partition_idx += 1
            nums[right], nums[partition_idx] = nums[partition_idx], nums[right]
            quick_sort(left, partition_idx - 1)
            quick_sort(partition_idx + 1, right)
            return

        quick_sort(0, len(nums) - 1)
        res = ''.join(nums)
        return res if res[0] != '0' else '0'

# time O(n**2), when the list is almost sorted, and the average time is O(nlogn)
# space O(n), due to recursion layers, O(logn) in average
# using array and sort and self defined quick sort
# unstable
```


## 📄 [H]array\[H]array-sort\1985-find-the-kth-largest-integer-in-the-array.py

```py
from collections import defaultdict
import random
class Solution:
    def kthLargestNumber(self, nums: List[str], k: int) -> str:

        nums = [int(num) for num in nums]

        num_freq = defaultdict(int)
        for num in nums:
            num_freq[num] += 1
        num_with_max_freq = max(num_freq, key=num_freq.get)
        max_freq = max(num_freq.values())
        if max_freq > k and max_freq > len(nums) - k:
            return str(num_with_max_freq)
        
        def quick_select(left, right):
            pivot_idx = random.randint(left, right)
            pivot_val = nums[pivot_idx]
            nums[right], nums[pivot_idx] = nums[pivot_idx], nums[right]
            partition_idx = left
            for i in range(left, right):
                if nums[i] < pivot_val:
                    nums[i], nums[partition_idx] = nums[partition_idx], nums[i]
                    partition_idx += 1
            nums[right], nums[partition_idx] = nums[partition_idx], nums[right]
            return partition_idx

        left, right = 0, len(nums) - 1
        while left <= right:
            idx = quick_select(left, right)
            if idx == len(nums) - k:
                return str(nums[idx])
            elif idx > len(nums) - k:
                right = idx - 1
            else:
                left = idx + 1

# time O(n**2), quick select can be O(n) in average (O(n**2) in worst) (notice that quick sort is O(nlogn) in average)
# space O(n)
# using array and sort and top k problem (based on sort) and quick select and prune
```


## 📄 [H]array\[H]array-sort\215-kth-largest-element-in-an-array.java

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {

        HashMap<Integer, Integer> valToFreq = new HashMap<>();
        for (int num: nums) {
            valToFreq.compute(num, (key, v) -> v == null ? 1 : v + 1);
        }
        int maxFreq = Collections.max(valToFreq.values());
        if (maxFreq > k && maxFreq > nums.length - k) {
            for (Integer key: valToFreq.keySet()) {
                if (Objects.equals(valToFreq.get(key), maxFreq)) {
                    return key;
                }
            }
        }

        int left = 0;
        int right = nums.length - 1;
        int idx = 0;
        while (left <= right) {
            idx = quickSelect(nums, left, right);
            if (idx == nums.length - k) {
                break;
            } else if (idx > nums.length - k) {
                right = idx - 1;
            } else {
                left = idx + 1;
            }
        }
        return nums[idx];
    }

    public int quickSelect(int[] nums, int left, int right) {
        Random random = new Random();
        int pivotIdx = random.nextInt(right - left + 1) + left;
        int pivotVal = nums[pivotIdx];
        swap(nums, pivotIdx, right);
        int partitionIdx = left;
        for (int i = left; i < right; i++) {
            if (nums[i] < pivotVal) {
                swap(nums, partitionIdx, i);
                partitionIdx += 1;
            }
        }
        swap(nums, partitionIdx, right);
        return partitionIdx;
    }

    public void swap(int[] nums, int left, int right) {
        int temp = nums[left];
        nums[left] = nums[right];
        nums[right] = temp;
        return;
    }
}

// time O(n**2) in worst, O(n) in average (notice that quick sort is O(nlogn) in average)
// space O(n), due to hashmap
// using array and sort and top k problem (based on sort) and quick select and prune
```


## 📄 [H]array\[H]array-sort\215-kth-largest-element-in-an-array.py

```py
import random
from collections import defaultdict
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:

        num_freq = defaultdict(int)
        for num in nums:
            num_freq[num] += 1
        key_with_max_freq = max(num_freq, key=num_freq.get)
        max_freq = max(num_freq.values())
        if max_freq > k and max_freq > len(nums) - k:
            return key_with_max_freq
        
        def quick_select(left, right):
            pivot_idx = random.randint(left, right)
            pivot_val = nums[pivot_idx]
            nums[right], nums[pivot_idx] = nums[pivot_idx], nums[right]
            partition_idx = left
            for i in range(left, right):
                if nums[i] < pivot_val:
                    nums[i], nums[partition_idx] = nums[partition_idx], nums[i]
                    partition_idx += 1
            nums[right], nums[partition_idx] = nums[partition_idx], nums[right]
            return partition_idx

        left, right = 0, len(nums) - 1
        while left <= right:
            idx = quick_select(left, right)
            if idx == len(nums) - k:
                return nums[idx]
            elif idx > len(nums) - k:
                right = idx - 1
            else:
                left = idx + 1
        
# time O(n**2) in worst, O(n) in average (notice that quick sort is O(nlogn) in average)
# space O(n), due to hashmap
# using array and sort and top k problem (based on sort) and quick select and prune

class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        min_num = min(nums)
        max_num = max(nums)
        num_freq = [0 for _ in range(max_num - min_num + 1)]
        for num in nums:
            num_freq[num - min_num] += 1
        for i in range(len(num_freq) - 1, - 1, - 1):
            if num_freq[i] >= k:
                return i + min_num
            k -= num_freq[i]

# time O(n+b)
# space O(b), b is the range of min_num and max_num
# using array and sort and top k problem (based on sort) and bucket sort
```


## 📄 [H]array\[H]array-sort\315-count-of-smaller-numbers-after-self.py

```py
class Solution:
    def countSmaller(self, nums: List[int]) -> List[int]:

        counts = [0 for _ in range(len(nums))]
        nums = [(num, i) for i, num in enumerate(nums)]
        
        def merge_sort(nums):
            n = len(nums)
            if n <= 1:
                return nums
            m = n // 2
            left_part = merge_sort(nums[: m])
            right_part = merge_sort(nums[m:])
            res = []
            left, right = 0, 0
            while left < m or right < n - m:
                if left == m:
                    res.append(right_part[right])
                    right += 1
                elif right == n - m:
                    res.append(left_part[left])
                    counts[left_part[left][1]] += right
                    left += 1
                elif left_part[left][0] <= right_part[right][0]:
                    res.append(left_part[left])
                    counts[left_part[left][1]] += right
                    left += 1
                else:
                    res.append(right_part[right])
                    right += 1
            return res

        merge_sort(nums)
        return counts

# time O(nlogn), each layer to merge cost O(n)
# space O(n), due to new list, merge sort has logn stack layers
# using array and sort and merge sort
'''
1. the count is updated for each element from the left part during merging
   (think about how many elements from right part and place before cur element)
   (means these elements are smaller than cur element and locate at cur elements right side before sorting)
'''
```


## 📄 [H]array\[H]array-sort\324-wiggle-sort-ii.py

```py
import random
class Solution:
    def wiggleSort(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        
        def quick_select(left, right):
            pivot_idx = random.randint(left, right)
            pivot_val = nums[pivot_idx]
            nums[pivot_idx], nums[right] = nums[right], nums[pivot_idx]
            partition_idx = left
            for i in range(left, right):
                if nums[i] < pivot_val:
                    nums[i], nums[partition_idx] = nums[partition_idx], nums[i]
                    partition_idx += 1
            nums[partition_idx], nums[right] = nums[right], nums[partition_idx]
            return partition_idx

        left, right = 0, len(nums) - 1
        middle_idx = (left + right) // 2
        while left <= right:
            idx = quick_select(left, right)
            if idx == middle_idx:
                break
            elif idx > middle_idx:
                right = idx - 1
            else:
                left = idx + 1
        median = nums[middle_idx]

        left, right = 0, len(nums) - 1
        cur = 0
        while cur <= right:
            if nums[cur] < median:
                nums[cur], nums[left] = nums[left], nums[cur]
                left += 1
                cur += 1
            elif nums[cur] == median:
                cur += 1
            else:
                nums[cur], nums[right] = nums[right], nums[cur]
                right -= 1
        
        clone_nums = nums[:]
        left, right = middle_idx, len(clone_nums) - 1
        for i in range(len(nums)):
            if i % 2 == 0:
                nums[i] = clone_nums[left]
                left -= 1
            else:
                nums[i] = clone_nums[right]
                right -= 1

# time O(n), due to quick select (average), worst is O(n**2)
# space O(n)
# using array and sort and quick select and three way partitioning
'''
1. quick select to get median
2. three way partitioning
3. notice: how to avoid vals equal median place in neighbor
'''

import random
class Solution:
    def wiggleSort(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        
        def quick_select(left, right):
            pivot_idx = random.randint(left, right)
            pivot_val = nums[pivot_idx]
            nums[right], nums[pivot_idx] = nums[pivot_idx], nums[right]
            partition_idx = left
            for i in range(left, right):
                if nums[i] < pivot_val:
                    nums[i], nums[partition_idx] = nums[partition_idx], nums[i]
                    partition_idx += 1
            nums[right], nums[partition_idx] = nums[partition_idx], nums[right]
            return partition_idx

        left, right = 0, len(nums) - 1
        mid_val = None
        while left <= right:
            idx = quick_select(left, right)
            if idx == len(nums) // 2:
                mid_val = nums[idx]
                break
            elif idx > len(nums) // 2:
                right = idx - 1
            else:
                left = idx + 1
        
        n = len(nums)
        small = n - 1 if (n - 1) % 2 == 0 else n - 2 # largest even idx (even idx for small val)
        i = small # for traversing whole array
        large = 1 # smallest odd idx (odd idx for large val)
        for _ in range(n):
            if nums[i] < mid_val:
                nums[small], nums[i] = nums[i], nums[small]
                small -= 2
                i -= 2
                if i < 0:
                    i = n - 1 if (n - 1) % 2 == 1 else n - 2 # reset to the largest odd idx
            elif nums[i] > mid_val:
                nums[large], nums[i] = nums[i], nums[large]
                large += 2
            else:
                i -= 2
                if i < 0:
                    j = n - 1 if (n - 1) % 2 == 1 else n - 2 # reset to the largest odd idx

# time O(n), due to quick select (average), worst is O(n**2)
# space O(1)
# using array and sort and quick select and three way partitioning
'''
1. quick select to get median
2. three way partitioning
3. notice: how to avoid vals equal median place in neighbor
'''
```


## 📄 [H]array\[H]array-sort\347-top-k-frequent-elements.java

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> valToFreq = new HashMap<>();
        for (int num: nums) {
            valToFreq.compute(num, (key, v) -> v == null ? 1 : v + 1);
        }
        PriorityQueue<int[]> heap = new PriorityQueue<>((a, b) -> Integer.compare(a[0], b[0]));
        for (Map.Entry<Integer, Integer> entry: valToFreq.entrySet()) {
            Integer val = entry.getKey();
            Integer freq = entry.getValue();
            heap.offer(new int[]{freq, val});
            if (heap.size() > k) {
                heap.poll();
            }
        }
        int[] res = new int[heap.size()];
        int i = 0;
        for (int[] element: heap) {
            res[i] = element[1];
            i += 1;
        }
        return res;
    }
}

// time O(n + nlogk)
// space O(n + k), due to hashmap and heap
// using heap and top k problem (based on heap) and min heap and hashmap
```


## 📄 [H]array\[H]array-sort\347-top-k-frequent-elements.py

```py
from collections import defaultdict
from heapq import *
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        num_freq = defaultdict(int)
        for num in nums:
            num_freq[num] += 1
        
        heap = []
        for num, freq in num_freq.items():
            heappush(heap, (freq, num))
            if len(heap) > k:
                heappop(heap)
        return [num for freq, num in heap]

# time O(n + nlogk)
# space O(n + k), due to hashmap and heap
# using heap and top k problem (based on heap) and min heap and hashmap

from collections import defaultdict
from heapq import *
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        num_freq = defaultdict(int)
        for num in nums:
            num_freq[num] += 1
        
        heap = [(- freq, num) for num, freq in num_freq.items()]
        heapify(heap)
        res = []
        for _ in range(k):
            res.append(heappop(heap)[1])
        return res

# time O(n + n + klogn)
# space O(n), due to hashmap and heap
# using heap and top k problem (based on heap) and max heap and hashmap

from collections import defaultdict
import random
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        
        num_freq = defaultdict(int)
        for num in nums:
            num_freq[num] += 1
        
        vals = [(f, n) for n, f in num_freq.items()]
        
        def quick_select(left, right):
            pivot_idx = random.randint(left, right)
            pivot_val = vals[pivot_idx]
            vals[right], vals[pivot_idx] = vals[pivot_idx], vals[right]
            partition_idx = left
            for i in range(left, right):
                if vals[i][0] < pivot_val[0]:
                    vals[i], vals[partition_idx] = vals[partition_idx], vals[i]
                    partition_idx += 1
            vals[right], vals[partition_idx] = vals[partition_idx], vals[right]
            return partition_idx

        left, right = 0, len(vals) - 1
        while left <= right:
            idx = quick_select(left, right)
            if idx == len(vals) - k:
                return [n for f, n in vals[idx:]]
            elif idx > len(vals) - k:
                right = idx - 1
            else:
                left = idx + 1
        
# time O(n**2) in worst, O(n) in average (notice that quick sort is O(nlogn) in average)
# space O(n), due to hashmap and list
# using array and sort and top k problem (based on sort) and quick select and hashmap

from collections import defaultdict
import random
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        
        num_freq = defaultdict(int)
        for num in nums:
            num_freq[num] += 1
        
        min_freq = min(num_freq.values())
        max_freq = max(num_freq.values())
        buckets = [[] for _ in range(max_freq - min_freq + 1)]
        for n, f in num_freq.items():
            buckets[f - min_freq].append(n)
        
        res = []
        for i in range(len(buckets) - 1, - 1, - 1):
            vals = buckets[i]
            if len(vals) <= k:
                res.extend(vals)
                k -= len(vals)
            else:
                break
        return res

# time O(n + b)
# space O(n + b)
# using array and sort and top k problem (based on sort) and bucket sort and hashmap
```


## 📄 [H]array\[H]array-sort\451-sort-characters-by-frequency.py

```py
from collections import defaultdict
class Solution:
    def frequencySort(self, s: str) -> str:
        char_freq = defaultdict(int)
        for c in s:
            char_freq[c] += 1
        
        max_freq = max(char_freq.values())
        min_freq = min(char_freq.values())
        buckets = [[] for _ in range(max_freq - min_freq + 1)]
        for c, f in char_freq.items():
            buckets[f - min_freq].append(c)
        
        res = ''
        for i in range(len(buckets) - 1, - 1, - 1):
            chars = buckets[i]
            for c in chars:
                res += c * (i + min_freq)
        return res

# time O(n + b)
# space O(n + b)
# using array and sort and bucket sort and hashmap
```


## 📄 [H]array\[H]array-sort\462-minimum-moves-to-equal-array-elements-ii.py

```py
import random
class Solution:
    def minMoves2(self, nums: List[int]) -> int:
        
        def quick_select(left, right):
            pivot_idx = random.randint(left, right)
            pivot_val = nums[pivot_idx]
            nums[right], nums[pivot_idx] = nums[pivot_idx], nums[right]
            partition_idx = left
            for i in range(left, right):
                if nums[i] < pivot_val:
                    nums[i], nums[partition_idx] = nums[partition_idx], nums[i]
                    partition_idx += 1
            nums[right], nums[partition_idx] = nums[partition_idx], nums[right]
            return partition_idx

        left, right = 0, len(nums) - 1
        while left <= right:
            idx = quick_select(left, right)
            if idx == len(nums) // 2:
                mid_val = nums[idx]
                res = 0
                for num in nums:
                    res += abs(num - mid_val)
                return res
            elif idx > len(nums) // 2:
                right = idx - 1
            else:
                left = idx + 1
    
# time O(n), due to quick select (average), worst is O(n**2)
# space O(1)
# using array and sort and quick select and math
'''
1. find median
2. if length is odd, then just use median
3. if length is even, choose any one of the two numbers in the median calculation
'''
```


## 📄 [H]array\[H]array-sort\493-reverse-pairs.py

```py
class Solution:
    def reversePairs(self, nums: List[int]) -> int:
        
        count = 0
        
        def merge_sort(nums):
            nonlocal count
            n = len(nums)
            if n <= 1:
                return nums
            m = n // 2
            left_part = merge_sort(nums[: m])
            right_part = merge_sort(nums[m:])

            left, right = 0, 0
            while left < m and right < n - m:
                if left_part[left] > right_part[right] * 2:
                    count += m - left
                    right += 1
                else:
                    left += 1

            res = []
            left, right = 0, 0
            while left < m or right < n - m:
                if left == m:
                    res.append(right_part[right])
                    right += 1
                elif right == n - m:
                    res.append(left_part[left])
                    left += 1
                elif left_part[left] <= right_part[right]:
                    res.append(left_part[left])
                    left += 1
                else:
                    res.append(right_part[right])
                    right += 1
            return res

        merge_sort(nums)
        return count
            
# time O(nlogn), each layer to merge cost O(n)
# space O(n), due to new list, merge sort has logn stack layers
# using array and sort and merge sort and two pointers
'''
1. the count is updated if left part element is twice larger than right part element
'''
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\11-container-with-most-water.java

```java
class Solution {
    public int maxArea(int[] height) {
        int res = 0;
        int left = 0;
        int right = height.length - 1;
        while (left <= right) {
            int cur = Math.min(height[left], height[right]) * (right - left);
            res = Math.max(res, cur);
            if (height[left] > height[right]) {
                right -= 1;
            } else {
                left += 1;
            }
        }
        return res;
    }
}

// time O(n)
// space O(1)
// using array and two pointers opposite direction and shrink type and greedy
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\11-container-with-most-water.py

```py
class Solution:
    def maxArea(self, height: List[int]) -> int:
        res = 0
        left, right = 0, len(height) - 1
        while left < right:
            if height[left] < height[right]:
                res = max(res, height[left] * (right - left))
                left += 1
            else:
                res = max(res, height[right] * (right - left))
                right -= 1
        return res
    
# time O(n)
# space O(1)
# using array and two pointers opposite direction and shrink type and greedy
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\125-valid-palindrome.java

```java
class Solution {
    public boolean isPalindrome(String s) {
        int left = 0;
        int right = s.length() - 1;
        while (left < right) {
            char lc = s.charAt(left);
            char rc = s.charAt(right);
            if (!Character.isLetterOrDigit(lc)) {
                left += 1;
            } else if (!Character.isLetterOrDigit(rc)) {
                right -= 1;
            } else {
                if (Character.toLowerCase(lc) == Character.toLowerCase(rc)) {
                    left += 1;
                    right -= 1;
                } else {
                    return false;
                }
            }
        }
        return true;
    }
}

// time O(n), due to traverse
// space O(1)
// using array and two pointers opposite direction and shrink type
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\125-valid-palindrome.py

```py
class Solution:
    def isPalindrome(self, s: str) -> bool:
        left, right = 0, len(s) - 1
        while left < right:
            if not s[left].isalnum():
                left += 1
            elif not s[right].isalnum():
                right -= 1
            elif s[left].lower() == s[right].lower():
                left += 1
                right -= 1
            else:
                return False
        return True
    
# time O(n), due to traverse
# space O(1)
# using array and two pointers opposite direction and shrink type
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\15-3sum.java

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        for (int i = 0; i < nums.length - 2; i++) {
            if (i - 1 >= 0 && nums[i - 1] == nums[i]) {
                continue;
            }
            int j = i + 1;
            int k = nums.length - 1;
            int target = 0 - nums[i];
            if (nums[j] + nums[j + 1] > target) {
                break;
            }
            if (nums[k - 1] + nums[k] < target) {
                continue;
            }
            while (j < k) {
                int total = nums[j] + nums[k];
                if (total == target) {
                    res.add(new ArrayList<>(Arrays.asList(nums[i], nums[j], nums[k])));
                    j += 1;
                    k -= 1;
                } else if (total > target) {
                    k -= 1;
                } else {
                    j += 1;
                }
                while (j < k && j - 1 > i && nums[j - 1] == nums[j]) {
                    j += 1;
                }
                while (j < k && k + 1 < nums.length && nums[k] == nums[k + 1]) {
                    k -= 1;
                }
            }
        }
        return res;
    }
}

// time O(n**2)
// space O(1), or due to built in sort's cost
// using array and two pointers opposite direction and shrink type and sort
/*
1. be aware of handling duplicate
*/
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\15-3sum.py

```py
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:

        nums.sort()

        res = []
        for i in range(len(nums) - 2):
            if i - 1 >= 0 and nums[i - 1] == nums[i]:
                continue
            left, right = i + 1, len(nums) - 1
            target = - nums[i]
            while left < right:
                cur = nums[left] + nums[right]
                if cur == target:
                    res.append([nums[i], nums[left], nums[right]])
                    left += 1
                    while left < right and nums[left - 1] == nums[left]:
                        left += 1
                elif cur > target:
                    right -= 1
                    while left < right and nums[right + 1] == nums[right]:
                        right -= 1
                else:
                    left += 1
                    while left < right and nums[left - 1] == nums[left]:
                        left += 1
        return res
    
# time O(n**2)
# space O(1), or due to built in sort's cost
# using array and two pointers opposite direction and shrink type and sort
'''
1. be aware of handling duplicate
'''
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\151-reverse-words-in-a-string.py

```py
class Solution:
    def reverseWords(self, s: str) -> str:

        chars = list(' ' + s + ' ')

        def rev(left, right):
            while left < right:
                chars[left], chars[right] = chars[right], chars[left]
                left += 1
                right -= 1
        
        rev(0, len(chars) - 1)

        word = False
        left = 0
        for right in range(len(chars)):
            if chars[right] == ' ' and word:
                rev(left, right)
                word = False
            elif chars[right] != ' ' and not word:
                left = right
                word = True
        
        res = ''
        for c in chars:
            if c != ' ':
                res += c
            elif res and res[- 1] != ' ':
                res += ' '
        return res.rstrip()

# time O(n)
# space O(n)
# using array and two pointers opposite direction and shrink type
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\16-3sum-closest.py

```py
class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:

        nums.sort()
        res_diff = float('inf')
        res = None

        for i in range(len(nums) - 2):
            left, right = i + 1, len(nums) - 1
            
            small_three = nums[i] + nums[left] + nums[left + 1]
            if small_three > target:
                if abs(small_three - target) < res_diff:
                    res_diff = abs(small_three - target)
                    res = small_three
                break
            large_three = nums[i] + nums[right - 1] + nums[right]
            if large_three < target:
                if abs(large_three - target) < res_diff:
                    res_diff = abs(large_three - target)
                    res = large_three
                continue
            
            while left < right:
                cur = nums[i] + nums[left] + nums[right]
                if abs(cur - target) < res_diff:
                    res_diff = abs(cur - target)
                    res = cur
                if cur == target:
                    return target
                elif cur > target:
                    right -= 1
                else:
                    left += 1
        return res

# time O(n**2)
# space O(1), not count built in sort's cost
# using array and two pointers opposite direction and shrink type and sort and prune
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\167-two-sum-ii-input-array-is-sorted.py

```py
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        left, right = 0, len(numbers) - 1
        while left < right:
            if numbers[left] + numbers[right] == target:
                break
            elif numbers[left] + numbers[right] > target:
                right -= 1
            else:
                left += 1
        return [left + 1, right + 1]

# time O(n), due to traverse
# space O(1)
# using array and two pointers opposite direction and shrink type
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\18-4sum.py

```py
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        nums.sort()
        res = []
        for i in range(len(nums) - 3):
            if i - 1 >= 0 and nums[i - 1] == nums[i]:
                continue
            for j in range(i + 1, len(nums) - 2):
                if j - 1 >= i + 1 and nums[j - 1] == nums[j]:
                    continue
                left, right = j + 1, len(nums) - 1
                while left < right:
                    cur = nums[i] + nums[j] + nums[left] + nums[right]
                    if cur == target:
                        res.append([nums[i], nums[j], nums[left], nums[right]])
                        left += 1
                        while left < right and nums[left - 1] == nums[left]:
                            left += 1
                    elif cur > target:
                        right -= 1
                        while left < right and nums[right + 1] == nums[right]:
                            right -= 1
                    else:
                        left += 1
                        while left < right and nums[left - 1] == nums[left]:
                            left += 1
        return res
    
# time O(n**3)
# space O(1), not count output list
# using array and two pointers opposite direction and shrink type and sort
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\344-reverse-string.java

```java
class Solution {
    public void reverseString(char[] s) {
        int left = 0;
        int right = s.length - 1;
        while (left < right) {
            char temp = s[left];
            s[left] = s[right];
            s[right] = temp;
            left += 1;
            right -= 1;
        }
        return;
    }
}

// time O(n)
// space O(1)
// using array and two pointers opposite direction and shrink type
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\344-reverse-string.py

```py
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        left, right = 0, len(s) - 1
        while left < right:
            s[left], s[right] = s[right], s[left]
            left += 1
            right -= 1

# time O(n)
# space O(1)
# using array and two pointers opposite direction and shrink type
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\42-trapping-rain-water.py

```py
class Solution:
    def trap(self, height: List[int]) -> int:
        res = 0
        left, right = 0, len(height) - 1
        left_wall, right_wall = height[left], height[right]
        while left < right:
            left_wall = max(left_wall, height[left])
            right_wall = max(right_wall, height[right])
            if left_wall < right_wall:
                res += left_wall - height[left]
                left += 1
            else:
                res += right_wall - height[right]
                right -= 1
        return res
        
# tiem O(n), due to traverse
# space O(1)
# using array and two pointers opposite direction and shrink type and greedy
'''
1. count the water with lower wall's side first
'''
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\5-longest-palindromic-substring.java

```java
class Solution {
    public String longestPalindrome(String s) {
        int resLen = 1;
        int resIdx = 0;

        for (int i = 0; i < s.length(); i++) {
            int[] cur = valid(s, i, i);
            if (cur[1] > resLen) {
                resIdx = cur[0];
                resLen = cur[1];
            }
            cur = valid(s, i, i + 1);
            if (cur[1] > resLen) {
                resIdx = cur[0];
                resLen = cur[1];
            }
    }
        return s.substring(resIdx, resIdx + resLen);
    }

    public int[] valid(String s, int left, int right) {
        int[] res = new int[]{left, 1};
        while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
            res[0] = left;
            res[1] = right - left + 1;
            left -= 1;
            right += 1;
        }
        return res;
    }
}

// time O(n**2), traversal costs O(n), and each time need to using two pointers to expand
// space O(1)
// using array and two pointers opposite direction and expand type
/*
1. this is not optimal solution
*/
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\5-longest-palindromic-substring.py

```py
class Solution:
    def longestPalindrome(self, s: str) -> str:

        res_len = 0
        res = - 1
        
        for i in range(len(s)):

            left, right = i, i
            while left >= 0 and right < len(s):
                if s[left] == s[right]:
                    if right - left + 1 > res_len:
                        res_len = right - left + 1
                        res = left
                    left -= 1
                    right += 1
                else:
                    break
            
            left, right = i, i + 1
            while left >= 0 and right < len(s):
                if s[left] == s[right]:
                    if right - left + 1 > res_len:
                        res_len = right - left + 1
                        res = left
                    left -= 1
                    right += 1
                else:
                    break
            
        return s[res: res + res_len]

# time O(n**2), traversal costs O(n), and each time need to using two pointers to expand
# space O(1)
# using array and two pointers opposite direction and expand type
'''
1. this is not optimal solution
'''
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\680-valid-palindrome-ii.py

```py
class Solution:
    def validPalindrome(self, s: str) -> bool:
        
        def helper(left, right, count):
            while left < right:
                if s[left] != s[right]:
                    if count == 0:
                        return helper(left + 1, right, 1) or helper(left, right - 1, 1)
                    return False
                left += 1
                right -= 1
            return True

        return helper(0, len(s) - 1, 0)

# time O(n), due to traverse
# space O(1)
# using array and two pointers opposite direction and shrink type
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\948-bag-of-tokens.py

```py
class Solution:
    def bagOfTokensScore(self, tokens: List[int], power: int) -> int:

        tokens.sort()

        res = 0
        score = 0
        left, right = 0, len(tokens) - 1
        while left <= right:
            if power >= tokens[left]:
                power -= tokens[left]
                score += 1
                left += 1
                res = max(res, score)
            elif score >= 1:
                power += tokens[right]
                score -= 1
                right -= 1
            else:
                break
        return res
        
# time O(nlogn)
# space O(1), or due to built in sort
# using array and two pointers opposite direction and shrink type and sort and greedy
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\977-squares-of-a-sorted-array.java

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        List<Integer> list = new ArrayList<>();
        int left = 0;
        int right = nums.length - 1;
        while (left <= right) {
            if (Math.abs(nums[left]) > Math.abs(nums[right])) {
                list.add(nums[left] * nums[left]);
                left += 1;
            } else {
                list.add(nums[right] * nums[right]);
                right -= 1;
            }
        }
        Collections.reverse(list);
        return list.stream().mapToInt(i -> i).toArray();
    }
}

// time O(n)
// space O(n)
// using array and two pointers opposite direction and shrink type
```


## 📄 [H]array\[H]array-two-pointers-opposite-direction\977-squares-of-a-sorted-array.py

```py
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        res = []
        left, right = 0, len(nums) - 1
        while left <= right:
            if nums[left] ** 2 < nums[right] ** 2:
                res.append(nums[right] ** 2)
                right -= 1
            else:
                res.append(nums[left] ** 2)
                left += 1
        return res[:: - 1]
        
# time O(n)
# space O(n)
# using array and two pointers opposite direction and shrink type
```


## 📄 [H]array\[H]array-two-pointers-same-direction\121-best-time-to-buy-and-sell-stock.java

```java
class Solution {
    public int maxProfit(int[] prices) {
        int res = 0;
        int left = 0;
        for (int right = 0; right < prices.length; right++) {
            if (prices[right] > prices[left]) {
                res = Math.max(res, prices[right] - prices[left]);
            } else {
                left = right;
            }
        }
        return res;
    }
}

// time O(n)
// space O(1)
// using array and two pointers same direction and left ptr to record and greedy
```


## 📄 [H]array\[H]array-two-pointers-same-direction\121-best-time-to-buy-and-sell-stock.py

```py
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        res = 0
        left = 0
        for right in range(len(prices)):
            if prices[right] > prices[left]:
                res = max(res, prices[right] - prices[left])
            else:
                left = right
        return res
        
# time O(n)
# space O(1)
# using array and two pointers same direction and left ptr to record and greedy
```


## 📄 [H]array\[H]array-two-pointers-same-direction\122-best-time-to-buy-and-sell-stock-ii.py

```py
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        res = 0
        left = 0
        for right in range(len(prices)):
            if prices[right] > prices[left]:
                res += prices[right] - prices[left]
                left = right
            else:
                left = right
        return res
        
# time O(n)
# space O(1)
# using array and two pointers same direction and left ptr to record and greedy
```


## 📄 [H]array\[H]array-two-pointers-same-direction\1574-shortest-subarray-to-be-removed-to-make-array-sorted.py

```py
class Solution:
    def findLengthOfShortestSubarray(self, arr: List[int]) -> int:
        left = None
        for i in range(len(arr)):
            if i - 1 >= 0 and arr[i - 1] > arr[i]:
                left = i - 1
                break
        right = None
        for i in range(len(arr) - 1, - 1, - 1):
            if i + 1 < len(arr) and arr[i] > arr[i + 1]:
                right = i + 1
                break
        if left == None:
            return 0

        res = min(right, len(arr) - (left + 1))
        
        p1, p2 = 0, right
        while p1 < left + 1 and p2 < len(arr):
            if arr[p1] <= arr[p2]:
                res = min(res, p2 - p1 - 1)
                p1 += 1
            else:
                p2 += 1
        return res
        
# time O(n)
# space O(1)
# using array and two pointers same direction and traverse two sequences
'''
1. find valid left subarray
2. find valid right subarray
3. record res: discard whole rest array of valid left subarray or whole rest array of valid right subarray
4-1. start from discard whole rest array of valid right subarray
4-2. consider restore one element at leftest side, this might make us to discard some elements in origin valid right subarray
4-3. keep trying to restore elements
'''
```


## 📄 [H]array\[H]array-two-pointers-same-direction\165-compare-version-numbers.py

```py
class Solution:
    def compareVersion(self, version1: str, version2: str) -> int:
        p1, p2 = 0, 0
        while p1 < len(version1) or p2 < len(version2):
            v1, v2 = 0, 0
            while p1 < len(version1) and version1[p1] != '.':
                v1 *= 10
                v1 += int(version1[p1])
                p1 += 1
            while p2 < len(version2) and version2[p2] != '.':
                v2 *= 10
                v2 += int(version2[p2])
                p2 += 1
            if v1 < v2:
                return - 1
            elif v1 > v2:
                return 1
            if p1 < len(version1) and version1[p1] == '.':
                p1 += 1
            if p2 < len(version2) and version2[p2] == '.':
                p2 += 1
        return 0

# time O(n+m)
# space O(1)
# using array and two pointers same direction and traverse two sequences
```


## 📄 [H]array\[H]array-two-pointers-same-direction\2337-move-pieces-to-obtain-a-string.py

```py
class Solution:
    def canChange(self, start: str, target: str) -> bool:
        p1, p2 = 0, 0
        while p1 < len(start) or p2 < len(target):
            c1 = None
            while p1 < len(start):
                if start[p1] == 'L' or start[p1] == 'R':
                    c1 = start[p1]
                    break
                p1 += 1
            c2 = None
            while p2 < len(target):
                if target[p2] == 'L' or target[p2] == 'R':
                    c2 = target[p2]
                    break
                p2 += 1
            if c1 != c2:
                return False
            elif c1 == 'L' and p1 < p2:
                return False
            elif c1 == 'R' and p1 > p2:
                return False
            p1 += 1
            p2 += 1
        return True
    
# time O(n)
# space O(1)
# using array and two pointers same direction and traverse two sequences
```


## 📄 [H]array\[H]array-two-pointers-same-direction\2414-length-of-the-longest-alphabetical-continuous-substring.py

```py
class Solution:
    def longestContinuousSubstring(self, s: str) -> int:
        
        res = 0
        left = 0
        for right in range(len(s)):
            if ord(s[right]) - ord(s[left]) == right - left:
                res = max(res, right - left + 1)
            else:
                left = right
        return res
    
# time O(n)
# space O(1)
# using array and two pointers same direction and left ptr to record
```


## 📄 [H]array\[H]array-two-pointers-same-direction\244-shortest-word-distance-ii.py

```py
from collections import defaultdict
class WordDistance:

    def __init__(self, wordsDict: List[str]):
        self.word_indices = defaultdict(list)
        for i, w in enumerate(wordsDict):
            self.word_indices[w].append(i)

    def shortest(self, word1: str, word2: str) -> int:
        indices1 = self.word_indices[word1]
        indices2 = self.word_indices[word2]

        res = float('inf')
        p1, p2 = 0, 0
        while p1 < len(indices1) and p2 < len(indices2):
            res = min(res, abs(indices1[p1] - indices2[p2]))
            if indices1[p1] < indices2[p2]:
                p1 += 1
            else:
                p2 += 1
        return res

# Your WordDistance object will be instantiated and called as such:
# obj = WordDistance(wordsDict)
# param_1 = obj.shortest(word1,word2)

# time O(n) for init, O(f1 +f2) for shortest(), f1 and f2 is the freqence of word1 and word2
# space O(n)
# using array and two pointers same direction and traverse two sequences and hashmap
```


## 📄 [H]array\[H]array-two-pointers-same-direction\26-remove-duplicates-from-sorted-array.py

```py
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        left = 0
        for right in range(len(nums)):
            if left - 1 >= 0 and nums[right] == nums[left - 1]:
                continue
            nums[right], nums[left] = nums[left], nums[right]
            left += 1
        return left

# time O(n), due to traverse
# space O(1)
# using array and two pointers same direction and left ptr to record
```


## 📄 [H]array\[H]array-two-pointers-same-direction\27-remove-element.py

```py
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        left = 0
        for right in range(len(nums)):
            if nums[right] != val:
                nums[right], nums[left] = nums[left], nums[right]
                left += 1
        return left
    
# time O(n)
# space O(1)
# using array and two pointers same direction and left ptr to record
```


## 📄 [H]array\[H]array-two-pointers-same-direction\283-move-zeroes.java

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int left = 0;
        for (int right = 0; right < nums.length; right++) {
            if (nums[right] == 0) {
                continue;
            }
            int temp = nums[left];
            nums[left] = nums[right];
            nums[right] = temp;
            left += 1;
        }
    }
}

// time O(n)
// space O(1)
// using array and two pointers same direction and left ptr to record
```


## 📄 [H]array\[H]array-two-pointers-same-direction\283-move-zeroes.py

```py
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        left = 0
        for right in range(len(nums)):
            if nums[right] != 0:
                nums[right], nums[left] = nums[left], nums[right]
                left += 1

# time O(n)
# space O(1)
# using array and two pointers same direction and left ptr to record
```


## 📄 [H]array\[H]array-two-pointers-same-direction\31-next-permutation.py

```py
class Solution:
    def nextPermutation(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        a = None
        for i in range(len(nums) - 1, - 1, - 1):
            if i - 1 >= 0 and nums[i - 1] < nums[i]:
                a = i - 1
                break
        if a == None:
            left, right = 0, len(nums) - 1
            while left < right:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1
            return
        
        b = a + 1
        for i in range(len(nums) - 1, a, - 1):
            if nums[a] < nums[i]:
                b = i
                break
        
        nums[a], nums[b] = nums[b], nums[a]

        left, right = a + 1, len(nums) - 1
        while left < right:
            nums[left], nums[right] = nums[right], nums[left]
            left += 1
            right -= 1

# time O(n), worst case traverse all list
# space O(1)
# using array and two pointers same direction and find next permutation
'''
1. find first relative small (left neighbor < cur element) num a in right side (if can not find a, then we are already in the largest permutation)
2. find first relative large num b (to that relative small num a) in right side
3. swap a and b
4. let second half subarray (after that swap idx (b's new idx)) become monotonic increasing (reverse them)
'''
```


## 📄 [H]array\[H]array-two-pointers-same-direction\556-next-greater-element-iii.py

```py
class Solution:
    def nextGreaterElement(self, n: int) -> int:
        nums = list(str(n))
        
        a = None
        for i in range(len(nums) - 1, - 1, - 1):
            if i - 1 >= 0 and nums[i - 1] < nums[i]:
                a = i - 1
                break
        if a == None:
            return - 1
        
        b = a + 1
        for i in range(len(nums) - 1, a, - 1):
            if nums[a] < nums[i]:
                b = i
                break
        
        nums[a], nums[b] = nums[b], nums[a]

        left, right = a + 1, len(nums) - 1
        while left < right:
            nums[left], nums[right] = nums[right], nums[left]
            left += 1
            right -= 1
        res = 0
        max_num = 2**31 - 1
        for num in nums:
            if res > max_num // 10 or (res == max_num // 10 and int(num) > max_num % 10):
                return - 1
            res *= 10
            res += int(num)
        return res

# time O(n)
# space O(n)
# using array and two pointers same direction and find next permutation
```


## 📄 [H]array\[H]array-two-pointers-same-direction\75-sort-colors.java

```java
class Solution {
    public void sortColors(int[] nums) {
        int red = 0;
        int blue = nums.length - 1;
        int i = 0;

        while (i < blue + 1) {
            if (nums[i] == 0) {
                int temp = nums[i];
                nums[i] = nums[red];
                nums[red] = temp;
                i += 1;
                red += 1;
            } else if (nums[i] == 1) {
                i += 1;
            } else {
                int temp = nums[i];
                nums[i] = nums[blue];
                nums[blue] = temp;
                blue -= 1;
            }
        }
    }
}

// time O(n)
// space O(1)
// using array and two pointers same direction and left ptr to record and three way partitioning
/*
1. when swap with left ptr, cur ptr with only get 1 or 0
2. most time is 1. And 0 is when cur ptr swap with left ptr at same idx
3. so cur need plus 1
*/
```


## 📄 [H]array\[H]array-two-pointers-same-direction\75-sort-colors.py

```py
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        left, right = 0, len(nums) - 1
        cur = 0
        while cur <= right:
            if nums[cur] == 0:
                nums[cur], nums[left] = nums[left], nums[cur]
                left += 1
                cur += 1
            elif nums[cur] == 1:
                cur += 1
            else:
                nums[cur], nums[right] = nums[right], nums[cur]
                right -= 1
                
# time O(n)
# space O(1)
# using array and two pointers same direction and left ptr to record and three way partitioning
'''
1. when swap with left ptr, cur ptr with only get 1 or 0
2. most time is 1. And 0 is when cur ptr swap with left ptr at same idx
3. so cur need plus 1
'''
```


## 📄 [H]array\[H]array-two-pointers-same-direction\80-remove-duplicates-from-sorted-array-ii.py

```py
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        cur = [None, 0]
        left = 0
        for right in range(len(nums)):
            if cur[0] == None or cur[0] != nums[right]:
                cur[0] = nums[right]
                cur[1] = 1
            elif cur[0] == nums[right] and cur[1] == 1:
                cur[1] = 2
            else:
                continue
            
            nums[right], nums[left] = nums[left], nums[right]
            left += 1
        
        return left
    
# time O(n)
# space O(1)
# using array and two pointers same direction and left ptr to record
```


## 📄 [I]stack-queue\[I]stack-queue\1209-remove-all-adjacent-duplicates-in-string-ii.py

```py
class Solution:
    def removeDuplicates(self, s: str, k: int) -> str:
        stack = []
        for c in s:
            if not stack or stack[- 1][0] != c:
                stack.append([c, 1])
            else:
                stack[- 1][1] += 1
                if stack[- 1][1] == k:
                    stack.pop()
        res = ''
        while stack:
            c, f = stack.pop()
            res = c * f + res
        return res
    
# time O(n), n is the string's length
# space O(n), due to stack
# using stack and queue and use stack to store the last states
```


## 📄 [I]stack-queue\[I]stack-queue\1249-minimum-remove-to-make-valid-parentheses.py

```py
class Solution:
    def minRemoveToMakeValid(self, s: str) -> str:
        res = []
        balance = 0
        for c in s:
            if c == '(':
                balance += 1
                res.append(c)
            elif c == ')':
                if balance > 0:
                    balance -= 1
                    res.append(c)
            else:
                res.append(c)

        balance = 0
        for i in range(len(res) - 1, - 1, - 1):
            if res[i] == ')':
                balance += 1
            elif res[i] == '(':
                if balance > 0:
                    balance -= 1
                else:
                    res[i] = ''
            else:
                continue

        return ''.join(res)
    
# time O(n), due to traverse twice
# space O(n)
# using stack and queue and variables to simulate stack
```


## 📄 [I]stack-queue\[I]stack-queue\150-evaluate-reverse-polish-notation.java

```java
class Solution {
    public int evalRPN(String[] tokens) {
        ArrayDeque<Integer> stack = new ArrayDeque<>();
        for (String token: tokens) {
            if ("+-*/".contains(token)) {
                Integer second = stack.pop();
                Integer first = stack.pop();
                if (Objects.equals(token, "+")){
                    stack.push(first + second);
                } else if (Objects.equals(token, "-")) {
                    stack.push(first - second);
                } else if (Objects.equals(token, "*")) {
                    stack.push(first * second);
                } else {
                    stack.push(first / second);
                }
            } else {
                stack.push(Integer.parseInt(token));
            }
        }
        return stack.peek();
    }
}

// time O(n), due to traverse
// space O(n), due to stack
// using stack and queue and use stack to store the last states
```


## 📄 [I]stack-queue\[I]stack-queue\150-evaluate-reverse-polish-notation.py

```py
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        num_stack = []
        cal_stack = []
        for t in tokens:
            if t in '+-*/':
                num2 = num_stack.pop()
                num1 = num_stack.pop()
                if t == '+':
                    num_stack.append(num1 + num2)
                elif t == '-':
                    num_stack.append(num1 - num2)
                elif t == '*':
                    num_stack.append(num1 * num2)
                else:
                    num_stack.append(int(num1 / num2))
            else:
                num_stack.append(int(t))
        return num_stack[- 1]
    
# time O(n), due to traverse
# space O(n), due to stack
# using stack and queue and use stack to store the last states
```


## 📄 [I]stack-queue\[I]stack-queue\155-min-stack.java

```java
class MinStack {
    ArrayDeque<Long> stack;
    long min;

    public MinStack() {
        stack = new ArrayDeque<>();
        min = 0;
    }
    
    public void push(int val) {
        if (stack.isEmpty()) {
            min = val;
            stack.push(0L);
        } else {
            long diff = val - min;
            if (diff < 0) {
                min = val;
                stack.push(diff);
            } else {
                stack.push(diff);
            }
        }
    }
    
    public void pop() {
        Long diff = stack.peek();
        if (diff < 0) {
            min += Math.abs(diff);
            stack.pop();
        } else {
            stack.pop();
        }
        if (stack.isEmpty()) {
            min = 0;
        }
    }
    
    public int top() {
        Long diff = stack.peek();
        if (diff < 0) {
            return (int) min;
        }
        return (int) (min + diff);
    }
    
    public int getMin() {
        return (int) min;
    }
}

/**
* Your MinStack object will be instantiated and called as such:
* MinStack obj = new MinStack();
* obj.push(val);
* obj.pop();
* int param_3 = obj.top();
* int param_4 = obj.getMin();
*/

// time O(1)
// space O(n)
// using stack and queue and implement stack/queue and one stack
```


## 📄 [I]stack-queue\[I]stack-queue\155-min-stack.py

```py
class MinStack:

    def __init__(self):
        self.stack = []
        self.min_num = None

    def push(self, val: int) -> None:
        if self.min_num == None:
            self.stack.append(0)
            self.min_num = val
        elif val < self.min_num:
            self.stack.append(val - self.min_num)
            self.min_num = val
        else:
            self.stack.append(val - self.min_num)

    def pop(self) -> None:
        diff = self.stack.pop()
        if len(self.stack) == 0:
            self.min_num = None
        elif diff < 0:
            self.min_num += abs(diff)

    def top(self) -> int:
        diff = self.stack[- 1]
        if diff < 0:
            return self.min_num
        return self.min_num + diff

    def getMin(self) -> int:
        return self.min_num

# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(val)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()

# time O(1)
# space O(n)
# using stack and queue and implement stack/queue and one stack
```


## 📄 [I]stack-queue\[I]stack-queue\20-valid-parentheses.java

```java
class Solution {
    public boolean isValid(String s) {
        HashMap<Character, Character> closeOpen = new HashMap<>();
        closeOpen.put(')', '(');
        closeOpen.put('}', '{');
        closeOpen.put(']', '[');
        ArrayDeque<Character> stack = new ArrayDeque<>();
        for (Character c: s.toCharArray()) {
            if (closeOpen.containsKey(c)) {
                if (!Objects.equals(stack.peek(), closeOpen.get(c))) {
                    return false;
                }
                stack.pop();
            } else {
                stack.push(c);
            }
        }
        return stack.isEmpty();
    }
}

// time O(n)
// space O(n)
// using stack and queue and use stack to store the last states and hashmap
```


## 📄 [I]stack-queue\[I]stack-queue\20-valid-parentheses.py

```py
class Solution:
    def isValid(self, s: str) -> bool:
        close_open = {')': '(', '}': '{', ']': '['}
        stack = []
        for c in s:
            if c not in close_open:
                stack.append(c)
            else:
                if not stack or stack[- 1] != close_open[c]:
                    return False
                stack.pop()
        return not stack

# time O(n)
# space O(n)
# using stack and queue and use stack to store the last states and hashmap
```


## 📄 [I]stack-queue\[I]stack-queue\224-basic-calculator.py

```py
class Solution:
    def calculate(self, s: str) -> int:
        s = '(' + s + ')'
        s = s.replace(' ', '')
        s = s.replace('(-', '(0-')

        num_stack = []
        cal_stack = []

        def calc():
            num2 = num_stack.pop()
            num1 = num_stack.pop()
            cal = cal_stack.pop()
            if cal == '+':
                num_stack.append(num1 + num2)
            else:
                num_stack.append(num1 - num2)
        
        num = ''
        for i in range(len(s)):
            if s[i] == '(':
                cal_stack.append(s[i])
            elif s[i] == ')':
                while cal_stack and cal_stack[- 1] != '(':
                    calc()
                cal_stack.pop()
            elif s[i] in '+-':
                while cal_stack and cal_stack[- 1] != '(':
                    calc()
                cal_stack.append(s[i])
            else:
                num += s[i]
                if not s[i + 1].isdigit():
                    num_stack.append(int(num))
                    num = ''

        return num_stack[- 1]
    
# time O(n)
# space O(n)
# using stack and queue and use stack to store the last states
```


## 📄 [I]stack-queue\[I]stack-queue\225-implement-stack-using-queues.py

```py
from collections import deque
class MyStack:

    def __init__(self):
        self.queue = deque([])

    def push(self, x: int) -> None:
        old_element_count = len(self.queue)
        self.queue.append(x)
        for _ in range(old_element_count):
            self.queue.append(self.queue.popleft())

    def pop(self) -> int:
        return self.queue.popleft()

    def top(self) -> int:
        return self.queue[0]

    def empty(self) -> bool:
        return len(self.queue) == 0

# Your MyStack object will be instantiated and called as such:
# obj = MyStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.empty()

# time O(n), due to push, and others are O(1)
# space O(n), due to queue
# using stack and queue and implement stack/queue and one queue
```


## 📄 [I]stack-queue\[I]stack-queue\227-basic-calculator-ii.py

```py
class Solution:
    def calculate(self, s: str) -> int:
        s = s.replace(' ', '')

        num_stack = []
        cal_stack = []

        def calc():
            num2 = num_stack.pop()
            num1 = num_stack.pop()
            cal = cal_stack.pop()
            if cal == '+':
                num_stack.append(num1 + num2)
            elif cal == '-':
                num_stack.append(num1 - num2)
            elif cal == '*':
                num_stack.append(num1 * num2)
            else:
                num_stack.append(int(num1 / num2))
        
        cal_weight = {'+': 0, '-': 0, '*': 1, '/': 1}
        num = ''
        for i in range(len(s)):
            if s[i] in '+-*/':
                while cal_stack and cal_weight[cal_stack[- 1]] >= cal_weight[s[i]]:
                    calc()
                cal_stack.append(s[i])
            else:
                num += s[i]
                if i == len(s) - 1 or (i + 1 < len(s) and not s[i + 1].isdigit()):
                    num_stack.append(int(num))
                    num = ''
        
        while cal_stack:
            calc()

        return num_stack[- 1]
    
# time O(n)
# space O(n)
# using stack and queue and use stack to store the last states
```


## 📄 [I]stack-queue\[I]stack-queue\2296-design-a-text-editor.py

```py
class TextEditor:

    def __init__(self):
        self.left = []
        self.right = []

    def addText(self, text: str) -> None:
        for c in text:
            self.left.append(c)

    def deleteText(self, k: int) -> int:
        res = 0
        while self.left and k:
            self.left.pop()
            k -= 1
            res += 1
        return res

    def cursorLeft(self, k: int) -> str:
        while self.left and k:
            self.right.append(self.left.pop())
            k -= 1
        res = ''
        for i in range(len(self.left) - 1, - 1, - 1):
            res = self.left[i] + res
            if len(res) == 10:
                break
        return res

    def cursorRight(self, k: int) -> str:
        while self.right and k:
            self.left.append(self.right.pop())
            k -= 1
        res = ''
        for i in range(len(self.left) - 1, - 1, - 1):
            res = self.left[i] + res
            if len(res) == 10:
                break
        return res

# Your TextEditor object will be instantiated and called as such:
# obj = TextEditor()
# obj.addText(text)
# param_2 = obj.deleteText(k)
# param_3 = obj.cursorLeft(k)
# param_4 = obj.cursorRight(k)
                       
# time O(s) for add, O(1) for init, others are O(k)
# space O(n)
# using stack and queue and stack to simulate and two stacks
```


## 📄 [I]stack-queue\[I]stack-queue\232-implement-queue-using-stacks.java

```java
class MyQueue {
    ArrayDeque<Integer> stack1;
    ArrayDeque<Integer> stack2;

    public MyQueue() {
        stack1 = new ArrayDeque<>();
        stack2 = new ArrayDeque<>();
    }
    
    public void push(int x) {
        stack1.push(x);
    }
    
    public int pop() {
        peek();
        return stack2.pop();
    }
    
    public int peek() {
        if (!stack2.isEmpty()) {
            return stack2.peek();
        }
        while (!stack1.isEmpty()) {
            stack2.push(stack1.pop());
        }
        return stack2.peek();
    }
    
    public boolean empty() {
        return stack1.isEmpty() && stack2.isEmpty();
    }
}

/**
* Your MyQueue object will be instantiated and called as such:
* MyQueue obj = new MyQueue();
* obj.push(x);
* int param_2 = obj.pop();
* int param_3 = obj.peek();
* boolean param_4 = obj.empty();
*/

// time O(1) for push(), empty() ,and initiation, amortized O(1) for pop(), peek()
// space O(n), due to two stacks
// using stack and queue and implement stack/queue and two stacks
```


## 📄 [I]stack-queue\[I]stack-queue\232-implement-queue-using-stacks.py

```py
class MyQueue:

    def __init__(self):
        self.stack1 = []
        self.stack2 = []

    def push(self, x: int) -> None:
        self.stack1.append(x)

    def pop(self) -> int:
        self.peek()
        return self.stack2.pop()

    def peek(self) -> int:
        if self.stack2:
            return self.stack2[- 1]
        while self.stack1:
            self.stack2.append(self.stack1.pop())
        return self.stack2[- 1]

    def empty(self) -> bool:
        return len(self.stack1) == 0 and len(self.stack2) == 0

# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()

# time O(1) for push(), empty() ,and initiation, amortized O(1) for pop(), peek()
# space O(n), due to two stacks
# using stack and queue and implement stack/queue and two stacks
```


## 📄 [I]stack-queue\[I]stack-queue\32-longest-valid-parentheses.py

```py
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        res = 0
        left, right = 0, 0
        for c in s:
            if c == '(':
                left += 1
            else:
                right += 1
            if left == right:
                res = max(res, left + right)
            elif left < right:
                left, right = 0, 0
        
        left, right = 0, 0
        for i in range(len(s) - 1, - 1, - 1):
            if s[i] == ')':
                right += 1
            else:
                left += 1
            if right == left:
                res = max(res, right + left)
            elif right < left:
                left, right = 0, 0

        return res
    
# time O(n)
# space O(1)
# using stack and queue and variables to simulate stack
'''
1. first traversal we cannot deal with the potential answer when left > right
2. to fix this, we traverse back to front
'''
```


## 📄 [I]stack-queue\[I]stack-queue\341-flatten-nested-list-iterator.py

```py
# """
# This is the interface that allows for creating nested lists.
# You should not implement it, or speculate about its implementation
# """
#class NestedInteger:
#    def isInteger(self) -> bool:
#        """
#        @return True if this NestedInteger holds a single integer, rather than a nested list.
#        """
#
#    def getInteger(self) -> int:
#        """
#        @return the single integer that this NestedInteger holds, if it holds a single integer
#        Return None if this NestedInteger holds a nested list
#        """
#
#    def getList(self) -> [NestedInteger]:
#        """
#        @return the nested list that this NestedInteger holds, if it holds a nested list
#        Return None if this NestedInteger holds a single integer
#        """

class NestedIterator:
    def __init__(self, nestedList: [NestedInteger]):
        self.stack = []
        while nestedList:
            self.stack.append(nestedList.pop())

    def next(self) -> int:
        return self.stack.pop().getInteger()
        
    def hasNext(self) -> bool:
        while self.stack:
            if self.stack[- 1].isInteger():
                return True
            vals = self.stack.pop().getList()
            while vals:
                self.stack.append(vals.pop())
        return False

# Your NestedIterator object will be instantiated and called as such:
# i, v = NestedIterator(nestedList), []
# while i.hasNext(): v.append(i.next())

# time O(1) for init and next(), and O(1) for hasNext() (amortized)
# space O(n)
# using stack and queue and stack to simulate and stack
```


## 📄 [I]stack-queue\[I]stack-queue\346-moving-average-from-data-stream.py

```py
from collections import deque
class MovingAverage:

    def __init__(self, size: int):
        self.queue = deque([])
        self.size = size
        self.total = 0

    def next(self, val: int) -> float:
        if len(self.queue) == self.size:
            self.total -= self.queue.popleft()
        self.queue.append(val)
        self.total += val
        return self.total / len(self.queue)

# Your MovingAverage object will be instantiated and called as such:
# obj = MovingAverage(size)
# param_1 = obj.next(val)

# time O(1)
# space O(n)
# using stack and queue and use queue to simulate
```


## 📄 [I]stack-queue\[I]stack-queue\394-decode-string.py

```py
class Solution:
    def decodeString(self, s: str) -> str:
        stack = []

        cur = ''
        num = ''
        for i in range(len(s)):
            if s[i] == '[':
                stack.append((int(num), cur))
                num = ''
                cur = ''
            elif s[i] == ']':
                mul, prev = stack.pop()
                cur = prev + mul * cur
            elif s[i].isdigit():
                num += s[i]
            else:
                cur += s[i]
        return cur
    
# time O(n), not precisely (only true if max freq is small)
# space O(n), not precisely (only true if max freq is small)
# using stack and queue and use stack to store the last states
```


## 📄 [I]stack-queue\[I]stack-queue\71-simplify-path.py

```py
class Solution:
    def simplifyPath(self, path: str) -> str:
        
        stack = []
        path = path.split('/')[1:]

        for c in path:
            if not c or c == '.':
                continue
            elif c == '..':
                if stack:
                    stack.pop()
            else:
                stack.append(c)
        
        return '/' + '/'.join(stack)
    
# time O(n), due to traverse and split
# space O(n), due to stack and split
# using stack and queue and use stack to store the last states
```


## 📄 [I]stack-queue\[I]stack-queue\716-max-stack.py

```py
from heapq import *
class MaxStack:

    def __init__(self):
        self.stack = []
        self.max_heap = []
        self.remove_set = set()
        self.id = 0

    def push(self, x: int) -> None:
        self.stack.append((x, self.id))
        heappush(self.max_heap, (- x, - self.id))
        self.id += 1

    def pop(self) -> int:
        val, idx = self.stack.pop()
        self.remove_set.add(idx)
        self.lazy_remove()
        return val

    def top(self) -> int:
        return self.stack[- 1][0]

    def peekMax(self) -> int:
        return - self.max_heap[0][0]

    def popMax(self) -> int:
        neg_val, neg_idx = heappop(self.max_heap)
        self.remove_set.add(- neg_idx)
        self.lazy_remove()
        return - neg_val
    
    def lazy_remove(self):
        while self.stack and self.stack[- 1][1] in self.remove_set:
            _, idx = self.stack.pop()
            self.remove_set.remove(idx)
        while self.max_heap and - self.max_heap[0][1] in self.remove_set:
            _, neg_idx = heappop(self.max_heap)
            self.remove_set.remove(- neg_idx)

# Your MaxStack object will be instantiated and called as such:
# obj = MaxStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.peekMax()
# param_5 = obj.popMax()

# time O(logn) for push(), amortized O(logn) for pop(), popmax(), O(1) for init, top(), peekMax()
# space O(n)
# using stack and queue and implement stack/queue and stack and heap and hashmap
```


## 📄 [I]stack-queue\[I]stack-queue\726-number-of-atoms.py

```py
from collections import defaultdict
import string
class Solution:
    def countOfAtoms(self, formula: str) -> str:
        element_freq = defaultdict(int)
        mul_stack = []
        num = ''
        element = ''
        mul = 1
        for i in range(len(formula) - 1, - 1, - 1):
            c = formula[i]
            if c == ')':
                mul *= int(num) if num else 1
                mul_stack.append(int(num) if num else 1)
                num = ''
            elif c == '(':
                mul //= mul_stack.pop()
            elif c.isdigit():
                num = c + num
            else:
                element = c + element
                if c in string.ascii_uppercase:
                    element_freq[element] += mul * (int(num) if num else 1) 
                    element = ''
                    num = ''

        res = ''
        for e, f in sorted(element_freq.items()):
            res += e + (str(f) if f != 1 else '')
        return res
        
# time O(nlogn)
# space O(n), due to stack and hashmap
# using stack and queue and use stack to store the last states and hashmap and sort
```


## 📄 [I]stack-queue\[I]stack-queue\735-asteroid-collision.py

```py
class Solution:
    def asteroidCollision(self, asteroids: List[int]) -> List[int]:
        stack = []

        for weight in asteroids:
            if not stack:
                stack.append(weight)
            elif stack[- 1] < 0:
                stack.append(weight)
            elif stack[- 1] > 0 and weight > 0:
                stack.append(weight)
            else:
                while stack and stack[- 1] > 0 and weight < 0:
                    if stack[- 1] > abs(weight):
                        weight = 0
                        break
                    elif stack[- 1] == abs(weight):
                        weight = 0
                        stack.pop()
                        break
                    else:
                        stack.pop()
                if weight:
                    stack.append(weight)
        return stack
                  
# time O(n), each asteroid push and pop at most once
# space O(n), due to stack
# using stack and queue and use stack to store the last states
```


## 📄 [I]stack-queue\[I]stack-queue\772-basic-calculator-iii.py

```py
class Solution:
    def calculate(self, s: str) -> int:
        s = '(' + s + ')'

        num_stack = []
        cal_stack = []

        def calc():
            num2 = num_stack.pop()
            num1 = num_stack.pop()
            cal = cal_stack.pop()
            if cal == '+':
                num_stack.append(num1 + num2)
            elif cal == '-':
                num_stack.append(num1 - num2)
            elif cal == '*':
                num_stack.append(num1 * num2)
            else:
                num_stack.append(int(num1 / num2))

        cal_weight = {'+': 0, '-': 0, '*': 1, '/': 1}
        num = ''
        for i in range(len(s)):
            if s[i] == '(':
                cal_stack.append(s[i])
            elif s[i] == ')':
                while cal_stack and cal_stack[- 1] != '(':
                    calc()
                cal_stack.pop()
            elif s[i] in '+-*/':
                while cal_stack and cal_stack[- 1] != '(' and cal_weight[cal_stack[- 1]] >= cal_weight[s[i]]:
                    calc()
                cal_stack.append(s[i])
            else:
                num += s[i]
                if not s[i + 1].isdigit():
                    num_stack.append(int(num))
                    num = ''
        return num_stack[- 1]
    
# time O(n)
# space O(n)
# using stack and queue and use stack to store the last states
```


## 📄 [I]stack-queue\[I]stack-queue\895-maximum-frequency-stack.py

```py
from collections import defaultdict
class FreqStack:

    def __init__(self):
        self.max_freq = 0
        self.val_freq = defaultdict(int)
        self.freq_stack = defaultdict(list)

    def push(self, val: int) -> None:
        self.val_freq[val] += 1
        freq = self.val_freq[val]
        if freq > self.max_freq:
            self.max_freq = freq
        self.freq_stack[freq].append(val)

    def pop(self) -> int:
        vals = self.freq_stack[self.max_freq]
        val = vals.pop()
        if len(vals) == 0:
            self.freq_stack.pop(self.max_freq)
            self.max_freq -= 1
        self.val_freq[val] -= 1
        if self.val_freq[val] == 0:
            self.val_freq.pop(val)
        return val

# Your FreqStack object will be instantiated and called as such:
# obj = FreqStack()
# obj.push(val)
# param_2 = obj.pop()

# time O(1)
# space O(n)
# using stack and queue and implement stack/queue and stack and hashmap
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\1438-longest-continuous-subarray-with-absolute-diff-less-than-or-equal-to-limit.py

```py
from collections import deque
class Solution:
    def longestSubarray(self, nums: List[int], limit: int) -> int:
        res = 0
        min_queue = deque([])
        max_queue = deque([])
        left = 0
        for right in range(len(nums)):
            while min_queue and nums[min_queue[- 1]] >= nums[right]:
                min_queue.pop()
            min_queue.append(right)
            while max_queue and nums[max_queue[- 1]] <= nums[right]:
                max_queue.pop()
            max_queue.append(right)
            while nums[max_queue[0]] - nums[min_queue[0]] > limit:
                left += 1
                if min_queue[0] < left:
                    min_queue.popleft()
                if max_queue[0] < left:
                    max_queue.popleft()
            res = max(res, right - left + 1)
        return res
    
# time O(n), each num will only pop and push twice and both cost O(1)
# space O(n), due to deque's size
# using stack and queue and montonic and monotonic queue and sliding window
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\1696-jump-game-vi.py

```py
class Solution:
    def maxResult(self, nums: List[int], k: int) -> int:
        dp = [float('-inf') for _ in range(len(nums))]
        dp[0] = nums[0]

        for right in range(1, len(nums)):
            for left in range(max(0, right - k), right):
                dp[right] = max(dp[right], dp[left] + nums[right])
        return dp[- 1]

# time O(nk)
# space O(n)
# using dp (this will TLE)

from collections import deque
class Solution:
    def maxResult(self, nums: List[int], k: int) -> int:
        dp = [float('-inf') for _ in range(len(nums))]
        dp[0] = nums[0]
        queue = deque([])

        for right in range(len(nums)):
            left = right - k
            while queue and queue[0] < left:
                queue.popleft()
            if queue:
                dp[right] = dp[queue[0]] + nums[right]
            while queue and dp[queue[- 1]] <= dp[right]:
                queue.pop()
            queue.append(right)

        return dp[- 1]
    
# time O(n)
# space O(n)
# using stack and queue and montonic and monotonic queue and sliding window and dp
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\1762-buildings-with-an-ocean-view.py

```py
class Solution:
    def findBuildings(self, heights: List[int]) -> List[int]:
        stack = []
        for i, h in enumerate(heights):
            while stack and heights[stack[- 1]] <= h:
                stack.pop()
            stack.append(i)
        return stack
    
# time O(n)
# space O(n)
# using stack and queue and montonic and monotonic stack (consider one side’s relationship)
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\1856-maximum-subarray-min-product.py

```py
class Solution:
    def maxSumMinProduct(self, nums: List[int]) -> int:
        prefix = [0 for _ in range(len(nums) + 1)]
        total = 0
        for i, num in enumerate(nums):
            total += num
            prefix[i + 1] = total
        
        res = 0
        stack = []
        for i in range(len(nums)):
            while stack and nums[stack[- 1]] > nums[i]:
                idx = stack.pop()
                left_bound = stack[- 1] if stack else - 1
                right_bound = i
                res = max(res, nums[idx] * (prefix[right_bound] - prefix[left_bound + 1]))
            stack.append(i)
        while stack:
            idx = stack.pop()
            left_bound = stack[- 1] if stack else - 1
            right_bound = len(nums)
            res = max(res, nums[idx] * (prefix[right_bound] - prefix[left_bound + 1]))

        return res % (10**9+7)

# time O(n)
# space O(n), due to lists
# using stack and queue and montonic and monotonic stack (consider two side’s relationship) and prefix sum
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\1944-number-of-visible-people-in-a-queue.py

```py
class Solution:
    def canSeePersonsCount(self, heights: List[int]) -> List[int]:
        stack = []
        res = [0 for _ in range(len(heights))]
        for i in range(len(heights) - 1, - 1, - 1):
            while stack and heights[stack[- 1]] <= heights[i]:
                stack.pop()
                res[i] += 1
            if stack:
                res[i] += 1
            stack.append(i)
        return res

# time O(n)
# space O(n)
# using stack and queue and montonic and monotonic stack (consider one side’s relationship)
'''
1. person can see people in right (monotonic increasing height)
'''
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\2104-sum-of-subarray-ranges.py

```py
class Solution:
    def subArrayRanges(self, nums: List[int]) -> int:
        res = 0
        temp = [float('inf')] + nums + [float('inf')]
        stack = []
        for i in range(len(temp)):
            while stack and temp[stack[- 1]] < temp[i]:
                idx = stack.pop()
                left_bound = stack[- 1]
                right_bound = i
                res += (idx - left_bound) * (right_bound - idx) * temp[idx]
            stack.append(i)
        temp = [float('-inf')] + nums + [float('-inf')]
        stack = []
        for i in range(len(temp)):
            while stack and temp[stack[- 1]] > temp[i]:
                idx = stack.pop()
                left_bound = stack[- 1]
                right_bound = i
                res -= (idx - left_bound) * (right_bound - idx) * temp[idx]
            stack.append(i)
        return res
            
# time O(n), due to traverse twice
# space O(n), due to stack
# using stack and queue and montonic and monotonic stack (consider two side’s relationship)
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\2289-steps-to-make-array-non-decreasing.py

```py
class Solution:
    def totalSteps(self, nums: List[int]) -> int:
        stack = []
        res = 0
        for i in range(len(nums) - 1, - 1, - 1):
            step = 0
            while stack and nums[stack[- 1][0]] < nums[i]:
                _, step_cost = stack.pop()
                step = max(step + 1, step_cost)
            stack.append((i, step))
            res = max(res, step)
        return res
    
# time O(n)
# space O(n)
# using stack and queue and montonic and monotonic stack (consider one side’s relationship)
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\2345-finding-the-number-of-visible-mountains.py

```py
from collections import defaultdict
class Solution:
    def visibleMountains(self, peaks: List[List[int]]) -> int:
        peaks.sort()
        stack = []
        for i in range(len(peaks)):
            x, y = peaks[i]
            while stack and stack[- 1][1] <= y - (x - stack[- 1][0]):
                stack.pop()
            if not stack or (stack[- 1][1] - (x - stack[- 1][0]) < y):
                stack.append((x, y))

        peak_count = defaultdict(int)
        for x, y in peaks:
            peak_count[(x, y)] += 1
        same_peak = 0
        for p in stack:
            if peak_count[p] > 1:
                same_peak += 1
            
        return len(stack) - same_peak
    
# time O(nlogn)
# space O(n)
# using stack and queue and montonic and monotonic stack (consider one side’s relationship) and hashmap and sort
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\239-sliding-window-maximum.py

```py
from collections import deque
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        res = []
        queue = deque([])
        for right, num in enumerate(nums):
            left = right - k + 1
            while queue and nums[queue[- 1]] <= num:
                queue.pop()
            queue.append(right)
            while queue and queue[0] < left:
                queue.popleft()
            if left >= 0:
                res.append(nums[queue[0]])
        return res
    
# time O(n)
# space O(k)
# using stack and queue and montonic and monotonic queue and sliding window
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\316-remove-duplicate-letters.py

```py
from collections import defaultdict
class Solution:
    def removeDuplicateLetters(self, s: str) -> str:
        char_freq = defaultdict(int)
        for c in s:
            char_freq[c] += 1
        stack = []
        visited = set()
        for c in s:
            while stack and char_freq[stack[- 1]] and stack[- 1] > c and c not in visited:
                remove_c = stack.pop()
                visited.remove(remove_c)
            if c not in visited:
                stack.append(c)
                visited.add(c)
            char_freq[c] -= 1
        return ''.join(stack)
    
# time O(n)
# space O(n), or O(1) consider the number of letters
# using stack and queue and montonic and monotonic stack (consider one side’s relationship) and hashmap and hashset
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\402-remove-k-digits.py

```py
class Solution:
    def removeKdigits(self, num: str, k: int) -> str:
        stack = []
        for c in num:
            while stack and stack[- 1] > c and k:
                stack.pop()
                k -= 1
            stack.append(c)
        
        while stack and k:
            stack.pop()
            k -= 1

        res = ''.join(stack).lstrip('0')
        return res if res else '0'

# time O(n)
# space O(n)
# using stack and queue and montonic and monotonic stack (consider one side’s relationship)
'''
1. 21: when met 1, we pop 2 out and choose 1 to make num smaller
2. 12: when met 1, we cannot pop 1 cause it will make num larger
'''

```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\496-next-greater-element-i.py

```py
class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        
        val_idx = {}
        for i, num in enumerate(nums1):
            val_idx[num] = i

        res = [- 1 for _ in range(len(nums1))]
        stack = []
        for i in range(len(nums2)):
            while stack and nums2[stack[- 1]] < nums2[i]:
                idx = stack.pop()
                if nums2[idx] in val_idx:
                    res[val_idx[nums2[idx]]] = nums2[i]
            stack.append(i)
        return res
    
# time O(n)
# space O(n), due to stack and hashmap
# using stack and queue and montonic and monotonic stack (consider one side’s relationship) and hashmap
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\503-next-greater-element-ii.py

```py
class Solution:
    def nextGreaterElements(self, nums: List[int]) -> List[int]:
        res = [- 1 for _ in range(len(nums))]
        stack = []
        for i in range(2 * len(nums)):
            j = i % len(nums)
            while stack and nums[stack[- 1]] < nums[j]:
                idx = stack.pop()
                res[idx] = nums[j]
            if i < len(nums):
                stack.append(i)
        return res

# time O(n), each num will only pop and push once and both cost O(1)
# space O(n), due to deque's size
# using stack and queue and montonic and monotonic stack (consider one side’s relationship)
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\739-daily-temperatures.java

```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int[] res = new int[temperatures.length];
        ArrayDeque<Integer> stack = new ArrayDeque<>();
        for (int i = 0; i < temperatures.length; i++) {
            while (!stack.isEmpty() && temperatures[stack.peek()] < temperatures[i]) {
                int idx = stack.pop();
                res[idx] = i - idx;
            }
            stack.push(i);
        }
        return res;
    }
}

// time O(n), each temperature will only pop and push once and both cost O(1)
// space O(n), due to stack's size
// using stack and queue and montonic and monotonic stack (consider one side’s relationship)
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\739-daily-temperatures.py

```py
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        res = [0 for _ in range(len(temperatures))]
        stack = []
        for i in range(len(temperatures)):
            while stack and temperatures[stack[- 1]] < temperatures[i]:
                idx = stack.pop()
                res[idx] = i - idx
            stack.append(i)
        return res
    
# time O(n), each temperature will only pop and push once and both cost O(1)
# space O(n), due to stack's size
# using stack and queue and montonic and monotonic stack (consider one side’s relationship)
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\768-max-chunks-to-make-sorted-ii.py

```py
class Solution:
    def maxChunksToSorted(self, arr: List[int]) -> int:
        stack = []
        for num in arr:
            chunk_max = num
            while stack and stack[- 1] > num:
                chunk_max = max(chunk_max, stack.pop())
            stack.append(chunk_max)
        return len(stack)
    
# time O(n)
# space O(n)
# using stack and queue and montonic and monotonic stack (consider one side’s relationship)
'''
1. [0, 0, 3, 5, 4, 2]
2. [0] [0] [2, 3, 4, 5]
3. we should maintain each chunk's max in stack
'''
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\84-largest-rectangle-in-histogram.py

```py
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        heights = [0] + heights + [0]
        res = 0
        stack = []
        for i in range(len(heights)):
            while stack and heights[stack[- 1]] > heights[i]:
                idx = stack.pop()
                height = heights[idx]
                left_bound = stack[- 1]
                right_bound = i
                width = right_bound - left_bound - 1
                res = max(res, height * width)
            stack.append(i)
        return res
        
# time O(n)
# space O(n), due to stack
# using stack and queue and montonic and monotonic stack (consider two side’s relationship)
'''
1. decide height
2. then find the left smaller element and right smaller element
3. count the area between these two bound
'''
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\85-maximal-rectangle.py

```py
class Solution:
    def maximalRectangle(self, matrix: List[List[str]]) -> int:
        
        def helper(heights):
            heights = [0] + heights + [0]
            stack = []
            res = 0
            for i in range(len(heights)):
                while stack and heights[stack[- 1]] > heights[i]:
                    idx = stack.pop()
                    res = max(res, heights[idx] * (i - stack[- 1] - 1))
                stack.append(i)
            return res

        res = 0
        rows, cols = len(matrix), len(matrix[0])
        prefix = [0 for _ in range(cols)]
        for r in range(rows):
            for c in range(cols):
                if matrix[r][c] == "1":
                    prefix[c] += 1
                else:
                    prefix[c] = 0
            res = max(res, helper(prefix))
        return res
    
# time O(RC)
# space O(C)
# using stack and queue and montonic and monotonic stack (consider two side’s relationship) and prefix
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\862-shortest-subarray-with-sum-at-least-k.py

```py
from collections import deque
class Solution:
    def shortestSubarray(self, nums: List[int], k: int) -> int:
        prefix = [0 for _ in range(len(nums) + 1)]
        total = 0
        for i, num in enumerate(nums):
            total += num
            prefix[i + 1] = total

        res = float('inf')
        queue = deque([])
        for i in range(len(prefix)):
            while queue and prefix[i] - prefix[queue[0]] >= k:
                idx = queue.popleft()
                res = min(res, i - idx)
            while queue and prefix[queue[- 1]] >= prefix[i]:
                queue.pop()
            queue.append(i)
        return res if res != float('inf') else - 1

# time O(n)
# space O(n)
# using stack and queue and montonic and monotonic queue and sliding window and prefix
'''
1. monotonic queue store the potential subarray's head idices
2. monotonic queue needs to store the smallest prefix sum at queue's head
3. because smaller prefix gets more chance to fulfill the condition
4. once it met condition, record it, then popleft it (cur round is the best condition for shortest)
5. if cur idx's prefix sum is smaller than queue's tail, then pop from queue (using cur idx is shorter)
6. append cur idx in queue
'''
```


## 📄 [I]stack-queue\[I]stack-queue-monotonic\907-sum-of-subarray-minimums.py

```py
class Solution:
    def sumSubarrayMins(self, arr: List[int]) -> int:
        arr = [0] + arr + [0]
        stack = []
        res = 0
        for i in range(len(arr)):
            while stack and arr[stack[- 1]] > arr[i]:
                idx = stack.pop()
                left_bound = stack[- 1]
                right_bound = i
                left_choices = idx - left_bound
                right_choices = i - idx
                res += left_choices * right_choices * arr[idx]
            stack.append(i)
        return res % (10**9+7)
                   
# time O(n)
# space O(n)
# using stack and queue and montonic and monotonic stack (consider two side’s relationship)

class Solution:
    def sumSubarrayMins(self, arr: List[int]) -> int:
        smaller_in_right = [len(arr) for _ in range(len(arr))]
        stack = []
        for i, num in enumerate(arr):
            while stack and arr[stack[- 1]] >= num:
                idx = stack.pop()
                smaller_in_right[idx] = i
            stack.append(i)

        smaller_in_left = [- 1 for _ in range(len(arr))]
        stack = []
        for i in range(len(arr) - 1, - 1, - 1):
            while stack and arr[stack[- 1]] > arr[i]:
                idx = stack.pop()
                smaller_in_left[idx] = i
            stack.append(i)

        res = 0
        for i in range(len(arr)):
            left_bound = smaller_in_left[i]
            right_bound = smaller_in_right[i]
            left_choices = i - left_bound
            right_choices = right_bound - i
            res += left_choices * right_choices * arr[i]
        return res % (10**9+7)

# time O(n)
# space O(n)
# using stack and queue and montonic and monotonic stack (consider two side’s relationship)
```


## 📄 [J]backtracking\[J]backtracking\113-path-sum-ii.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
        
        res = []

        def dfs(path, total, node):
            if not node.left and not node.right:
                if total == targetSum:
                    res.append(path[:])
                return
            for child in [node.left, node.right]:
                if child:
                    path.append(child.val)
                    dfs(path, total + child.val, child)
                    path.pop()
        
        if root:
            dfs([root.val], root.val, root)
        return res
        
# time O(n**2), traversal costs O(n) and every leaf performs O(n) to append path to res
# space O(n**2), due to output list
# using dfs and backtracking and backtracking with constraints
```


## 📄 [J]backtracking\[J]backtracking\131-palindrome-partitioning.py

```py
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        res = []
        
        def valid(left, right):
            while left < right:
                if s[left] != s[right]:
                    return False
                left += 1
                right -= 1
            return True

        def dfs(path, idx):
            if idx == len(s):
                res.append(path[:])
                return
            w = ''
            for end in range(idx, len(s)):
                w += s[end]
                if valid(idx, end):
                    path.append(w)
                    dfs(path, end + 1)
                    path.pop()
        
        dfs([], 0)
        return res
    
# time O(2**n * n)
# space O(n)
# using dfs and backtracking and two pointers and backtracking with constraints
```


## 📄 [J]backtracking\[J]backtracking\140-word-break-ii.py

```py
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:
        word_set = set(wordDict)
        res = []
        memo = [True for _ in range(len(s))]

        def dfs(path, idx):
            if idx == len(s):
                res.append(' '.join(path))
                return
            if memo[idx] == False:
                return
            old_res_len = len(res)
            w = ''
            for end in range(idx, len(s)):
                w += s[end]
                if w not in word_set:
                    continue
                path.append(w)
                dfs(path, end + 1)
                path.pop()
            if old_res_len == len(res):
                memo[idx] = False
        
        dfs([], 0)
        return res
    
# time O(2**n), there is 2**n ways to divide input string
# space O(2**n), due to output list
# using dfs and backtracking and backtracking with constraints and prune
'''
1. use memo to prune
2. memo[idx] == False, means substring s[idx:] cannot generate any valid ans
'''
```


## 📄 [J]backtracking\[J]backtracking\17-letter-combinations-of-a-phone-number.java

```java
class Solution {

    HashMap<Character, ArrayList<Character>> map;
    List<String> res;

    public List<String> letterCombinations(String digits) {
        map = new HashMap<>();
        int cur = 0;
        for (int i = 2; i < 10; i++) {
            char c = (char) (i + '0');
            int total = 3;
            if (i == 7 || i == 9) {
                total += 1;
            }
            for (int j = 0; j < total; j++) {
                map.computeIfAbsent(c, k -> new ArrayList<>()).add((char) (cur + 'a'));
                cur += 1;
            }
        }
        res = new ArrayList<>();
        if (digits.length() > 0) {
            dfs(digits, new StringBuffer(), 0);
        }
        return res;
    }

    public void dfs(String digits, StringBuffer sb, int idx) {
        if (idx == digits.length()) {
            res.add(sb.toString());
            return;
        }
        for (int i = 0; i < map.get(digits.charAt(idx)).size(); i++) {
            Character c = map.get(digits.charAt(idx)).get(i);
            sb.append(c);
            dfs(digits, sb, idx + 1);
            sb.deleteCharAt(sb.length() - 1);
        }
        return;
    }
}

// time O(4**n), n is the length of digits
// space O(n), due to recursion stack, output is O(4**n)
// using dfs and backtracking and backtracking with constraints
```


## 📄 [J]backtracking\[J]backtracking\17-letter-combinations-of-a-phone-number.py

```py
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if not digits:
            return []
        res = []
        num_chars = {'2': 'abc', '3': 'def', '4':'ghi', '5':'jkl', '6':'mno', '7':'pqrs', '8':'tuv', '9':'wxyz'}

        def dfs(path, idx):
            if len(path) == len(digits):
                res.append(''.join(path))
                return
            for c in num_chars[digits[idx]]:
                path.append(c)
                dfs(path, idx + 1)
                path.pop()

        dfs([], 0)
        return res
                
# time O(4**n), n is the length of digits
# space O(n), due to recursion stack, output is O(4**n)
# using dfs and backtracking and backtracking with constraints
```


## 📄 [J]backtracking\[J]backtracking\212-word-search-ii.py

```py
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, word):
        node = self.root
        for c in word:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
        node.is_word = True

class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        trie = Trie()
        for w in words:
            trie.insert(w)

        rows, cols = len(board), len(board[0])
        res = []

        def dfs(path, r, c, visited, node, parent_node):
            if node.is_word:
                res.append(''.join(path))
                node.is_word = False
            if len(node.children) == 0:
                parent_node.children.pop(board[r][c])
                return
            for next_r, next_c in [(r+1, c), (r-1, c), (r, c+1), (r, c-1)]:
                if next_r not in range(rows) or next_c not in range(cols) or (next_r, next_c) in visited or board[next_r][next_c] not in node.children:
                    continue
                visited.add((next_r, next_c))
                path.append(board[next_r][next_c])
                dfs(path, next_r, next_c, visited, node.children[board[next_r][next_c]], node)
                visited.remove((next_r, next_c))
                path.pop()

        for r in range(rows):
            for c in range(cols):
                if board[r][c] in trie.root.children:
                    dfs([board[r][c]], r, c, {(r, c)}, trie.root.children[board[r][c]], trie.root)
        return res
                
# time O(RC * 3**L), L is the longest word's length
# space O(nL), due to trie
# using dfs and backtracking and backtracking with constraints and trie and pruning
```


## 📄 [J]backtracking\[J]backtracking\216-combination-sum-iii.py

```py
class Solution:
    def combinationSum3(self, k: int, n: int) -> List[List[int]]:
        res = []

        def dfs(path, total, idx):
            if total > n:
                return
            if len(path) > k:
                return
            if total == n and len(path) == k:
                res.append(path[:])
                return
            if idx == 10:
                return
            
            for i in range(idx, 10):
                path.append(i)
                total += i
                dfs(path, total, i + 1)
                path.pop()
                total -= i
        
        dfs([], 0, 1)
        return res
    
# time O(9!/(9-k)!k! * k), 9!/(9-k)! is the number of combinations, and k is for copying path
# space O(k)
# using dfs and backtracking and combination
'''
1. type: combination
2. duplicate elements: no
3. selectable repeatedly: no
'''
```


## 📄 [J]backtracking\[J]backtracking\22-generate-parentheses.py

```py
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        res = []

        def dfs(path, left, right):
            if left == right == n:
                res.append(''.join(path))
                return
            if left < n:
                path.append('(')
                dfs(path, left + 1, right)
                path.pop()
            if right < left:
                path.append(')')
                dfs(path, left, right + 1)
                path.pop()

        dfs([], 0, 0)
        return res

# time catalan(n)
# space catalan(n), stack size is O(n)
# using dfs and backtracking and backtracking with constraints
```


## 📄 [J]backtracking\[J]backtracking\257-binary-tree-paths.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def binaryTreePaths(self, root: Optional[TreeNode]) -> List[str]:
        
        res = []

        def dfs(path, node):
            if not node.left and not node.right:
                res.append('->'.join(path))
                return
            for child in [node.left, node.right]:
                if child:
                    path.append(str(child.val))
                    dfs(path, child)
                    path.pop()
        
        if root:
            dfs([str(root.val)], root)
        return res
    
# time O(n**2)
# space O(n**2)
# using dfs and backtracking and backtracking with constraints
```


## 📄 [J]backtracking\[J]backtracking\267-palindrome-permutation-ii.py

```py
from collections import defaultdict
class Solution:
    def generatePalindromes(self, s: str) -> List[str]:
        char_freq = defaultdict(int)
        for c in s:
            char_freq[c] += 1
        odd_char = None
        chars = []
        for c, f in char_freq.items():
            if f % 2:
                if odd_char != None:
                    return []
                odd_char = c
                chars.extend([c for _ in range((f - 1) // 2)])
            else:
                chars.extend([c for _ in range(f // 2)])
                
        res = []
        def dfs(path, visited):
            if len(path) == len(chars):
                if odd_char != None:
                    res.append(''.join(path) + odd_char + ''.join(path[::- 1]))      
                else:
                    res.append(''.join(path) + ''.join(path[::- 1]))
                return
            for i, c in enumerate(chars):
                if i - 1 >= 0 and chars[i - 1] == chars[i] and i - 1 not in visited:
                    continue
                if i not in visited:
                    path.append(chars[i])
                    visited.add(i)
                    dfs(path, visited)
                    path.pop()
                    visited.remove(i)
        
        dfs([], set())
        return res

# time O((n/2)! * n)
# space O(n/2), not count output
# using dfs and backtracking and hashmap and permutation
'''
1. type: permutation
2. duplicate elements: yes
3. selectable repeatedly: no
'''
```


## 📄 [J]backtracking\[J]backtracking\37-sudoku-solver.py

```py
class Solution:
    def solveSudoku(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        rows, cols = len(board), len(board[0])

        def valid(row, col, digit):
            for r in range(rows):
                if board[r][col] == digit:
                    return False
            for c in range(cols):
                if board[row][c] == digit:
                    return False
            for r in range(row // 3 * 3, row // 3 * 3 + 3):
                for c in range(col // 3 * 3, col // 3 * 3 + 3):
                    if board[r][c] == digit:
                        return False
            return True

        def dfs(row, col):
            if row == rows:
                return True
            if col == cols:
                return dfs(row + 1, 0)
            if board[row][col] != '.':
                return dfs(row, col + 1)
            for i in range(1, 10):
                if valid(row, col, str(i)):
                    board[row][col] = str(i)
                    if dfs(row, col + 1):
                        return True
                    board[row][col] = '.'
            return False

        dfs(0, 0)
                    
# time O(9**(nm))
# space O(nm)
# using dfs and backtracking and backtracking with constraints
```


## 📄 [J]backtracking\[J]backtracking\39-combination-sum.java

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        dfs(res, candidates, target, new ArrayList<>(), 0, 0);
        return res;
    }

    public void dfs(List<List<Integer>> res, int[] candidates, int target, List<Integer> path, int total, int idx) {
        if (total == target) {
            res.add(new ArrayList<>(path));
            return;
        }
        if (total > target) {
            return;
        }
        for (int i = idx; i < candidates.length; i++) {
            path.add(candidates[i]);
            total += candidates[i];
            dfs(res, candidates, target, path, total, i);
            path.remove(path.size() - 1);
            total -= candidates[i];
        }
    }
}

// time O(n ** (T/S)), T is target number, and S is the min number in candidates
// space O(T/S), due to recursion stack
// using dfs and backtracking and subset
/*
1. type: subset
2. duplicate elements: no
3. selectable repeatedly: yes
*/
```


## 📄 [J]backtracking\[J]backtracking\39-combination-sum.py

```py
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        res = []

        def dfs(path, total, idx):
            if total > target:
                return
            if total == target:
                res.append(path[:])
                return
            for i in range(idx, len(candidates)):
                path.append(candidates[i])
                total += candidates[i]
                dfs(path, total, i)
                path.pop()
                total -= candidates[i]
        
        dfs([], 0, 0)
        return res
    
# time O(n ** (T/S)), T is target number, and S is the min number in candidates
# space O(T/S), due to recursion stack
# using dfs and backtracking and subset
'''
1. type: subset
2. duplicate elements: no
3. selectable repeatedly: yes
'''
```


## 📄 [J]backtracking\[J]backtracking\40-combination-sum-ii.py

```py
class Solution:
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        candidates.sort()
        res = []

        def dfs(path, total, visited, idx):
            if total > target:
                return

            if total == target:
                res.append(path[:])
                return

            if idx == len(candidates):
                return
            
            for i in range(idx, len(candidates)):
                if i - 1 >= 0 and candidates[i - 1] == candidates[i] and i - 1 not in visited:
                    continue
                path.append(candidates[i])
                total += candidates[i]
                visited.add(i)
                dfs(path, total, visited, i + 1)
                path.pop()
                total -= candidates[i]
                visited.remove(i)

        dfs([], 0, set(), 0)
        return res
    
# time O(2**n)
# space O(n), due to recursion stack's size and hashset, not counting output
# using dfs and backtracking and pruning and subset
'''
1. type: subset
2. duplicate elements: yes
3. selectable repeatedly: no
'''

class Solution:
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        candidates.sort()
        res = []

        def dfs(path, total, visited, idx):
            if total > target:
                return
            if total == target:
                res.append(path[:])
                return
            if idx == len(candidates):
                return
               
            dfs(path, total, visited, idx + 1)

            if idx - 1 >= 0 and candidates[idx - 1] == candidates[idx] and idx - 1 not in visited:
                return
            path.append(candidates[idx])
            visited.add(idx)
            dfs(path, total + candidates[idx], visited, idx + 1)
            visited.remove(idx)
            path.pop()


        dfs([], 0, set(), 0)
        return res

# time O(2**n)
# space O(n), due to recursion stack's size and hashset, not counting output
# using dfs and backtracking and pruning and subset
'''
1. type: subset
2. duplicate elements: yes
3. selectable repeatedly: no
'''
```


## 📄 [J]backtracking\[J]backtracking\437-path-sum-iii.py

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import defaultdict
class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> int:
        
        res = 0
        prefix_count = defaultdict(int)
        prefix_count[0] = 1

        def dfs(node, total):
            nonlocal res
            res += prefix_count[total - targetSum]
            prefix_count[total] += 1
            for child in [node.left, node.right]:
                if child:
                    dfs(child, total + child.val)
            prefix_count[total] -= 1
            
        if root:
            dfs(root, root.val)
        return res
    
# time O(n), due to dfs preorder traversal
# space O(n), due to prefix sum's hashamp
# using dfs and backtracking and prefix sum and backtracking with constraints
'''
1. the reason for backtracking prefix count is because we only care downward path
'''
```


## 📄 [J]backtracking\[J]backtracking\46-permutations.java

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        dfs(nums, new ArrayList<>(), new HashSet<>(), res);
        return res;
    }

    public void dfs(int[] nums, ArrayList<Integer> path, HashSet<Integer> visited, List<List<Integer>> res) {
        if (path.size() == nums.length) {
            res.add(new ArrayList<>(path));
            return;
        }
        for (int i = 0; i < nums.length; i++) {
            if (!visited.contains(i)) {
                path.add(nums[i]);
                visited.add(i);
                dfs(nums, path, visited, res);
                path.remove(path.size() - 1);
                visited.remove(i);
            }
        }
    }
}

// time O(n*n!), dfs will calls n! times and each non-leaf node traverse list costs O(n) and leaf node copy a list to answer costs O(n)
// space O(n*n!), because answer contains n! permutations and each permutaiton can cost O(n). Besides, memory stack size is O(n)
// using dfs and backtracking and permutation
/*
1. type: permutation
2. duplicate elements: no
3. selectable repeatedly: no
*/
```


## 📄 [J]backtracking\[J]backtracking\46-permutations.py

```py
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        res = []

        def dfs(path, visited):
            if len(path) == len(nums):
                res.append(path[:])
                return
            for i in range(len(nums)):
                if i not in visited:
                    visited.add(i)
                    path.append(nums[i])
                    dfs(path, visited)
                    visited.remove(i)
                    path.pop()
        
        dfs([], set())
        return res
        
# time O(n*n!), dfs will calls n! times and each non-leaf node traverse list costs O(n) and leaf node copy a list to answer costs O(n)
# space O(n*n!), because answer contains n! permutations and each permutaiton can cost O(n). Besides, memory stack size is O(n)
# using dfs and backtracking and permutation
'''
1. type: permutation
2. duplicate elements: no
3. selectable repeatedly: no
'''
```


## 📄 [J]backtracking\[J]backtracking\465-optimal-account-balancing.py

```py
from collections import defaultdict
class Solution:
    def minTransfers(self, transactions: List[List[int]]) -> int:
        people_balance = defaultdict(int)
        for p, q, w in transactions:
            people_balance[p] += w
            people_balance[q] -= w
        vals = []
        for p, b in people_balance.items():
            if b != 0:
                vals.append(b)
        
        res = float('inf')

        def dfs(count, idx):
            nonlocal res
            if idx == len(vals):
                res = min(res, count)
                return
            if vals[idx] == 0:
                dfs(count, idx + 1)
                return
            for i in range(idx, len(vals)):
                if i == idx:
                    continue
                if vals[idx] * vals[i] >= 0:
                    continue
                settle = vals[idx]
                vals[idx] -= settle
                vals[i] += settle
                count += 1
                dfs(count, idx + 1)
                vals[idx] += settle
                vals[i] -= settle
                count -= 1
        
        dfs(0, 0)
        return res
    
# time O(n!)
# space O(n), due to recursion stack
# using dfs and backtracking and hashmap and backtracking with constraints
'''
1. we are enumerating every possible way to end the debt for each one
'''
```


## 📄 [J]backtracking\[J]backtracking\47-permutations-ii.py

```py
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        res = []

        def dfs(path, visited):
            if len(path) == len(nums):
                res.append(path[:])
                return
            for i in range(len(nums)):
                if i - 1 >= 0 and nums[i - 1] == nums[i] and i - 1 not in visited:
                    continue
                if i not in visited:
                    path.append(nums[i])
                    visited.add(i)
                    dfs(path, visited)
                    path.pop()
                    visited.remove(i)
        
        dfs([], set())
        return res
    
# time O(n! * n)
# space O(n), not count output
# using dfs and backtracking and permutation and sort
'''
1. type: permutation
2. duplicate elements: yes
3. selectable repeatedly: no
'''
```


## 📄 [J]backtracking\[J]backtracking\51-n-queens.py

```py
class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        g = [['.' for _ in range(n)] for _ in range(n)]
        col_set = set()
        diag_set = set()
        antidiag_set = set()
        res = []

        def dfs(r):
            if r == n:
                puzzle = []
                for row in range(len(g)):
                    puzzle.append(''.join(g[row]))
                res.append(puzzle)
                return
            for c in range(n):
                if c in col_set or r - c in diag_set or r + c in antidiag_set:
                    continue
                col_set.add(c)
                diag_set.add(r - c)
                antidiag_set.add(r + c)
                g[r][c] = 'Q'
                dfs(r + 1)
                col_set.remove(c)
                diag_set.remove(r - c)
                antidiag_set.remove(r + c)
                g[r][c] = '.'
        
        dfs(0)
        return res
    
# time O(n!)
# space O(n**2), not counting output
# using dfs and backtracking and backtracking with constraints
```


## 📄 [J]backtracking\[J]backtracking\77-combinations.py

```py
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        res = []

        def dfs(path, idx):
            if len(path) == k:
                res.append(path[:])
                return
            for i in range(idx, n + 1):
                path.append(i)
                dfs(path, i + 1)
                path.pop()

        dfs([], 1)
        return res
    
# time O(n!/(n-k)!k! * k)
# space O(k), not count output
# using dfs and backtracking and combination
'''
1. type: combination
2. duplicate elements: no
3. selectable repeatedly: no
'''
```


## 📄 [J]backtracking\[J]backtracking\78-subsets.java

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        dfs(res, nums, new ArrayList<>(), 0);
        return res;
    }

    public void dfs(List<List<Integer>> res, int[] nums, List<Integer> path, int idx) {
        if (idx == nums.length) {
            res.add(new ArrayList<>(path));
            return;
        }

        dfs(res, nums, path, idx + 1);

        path.add(nums[idx]);
        dfs(res, nums, path, idx + 1);
        path.remove(path.size() - 1);
        return;
    }
}

// time O(n*(2**n)), due to each element can take or not take (2**n), and n for copy list
// space O(n), due to recursion stack, not counting output here
// using dfs and backtracking and subset
/*
1. type: subset
2. duplicate elements: no
3. selectable repeatedly: no
*/
/*
this approach focus on considering each element:
for cur element, 
we don't take, then goto next element
or we take, then goto next element
till no more element to be considered, we record path
*/
```


## 📄 [J]backtracking\[J]backtracking\78-subsets.py

```py
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        res = []

        def dfs(path, idx):
            if idx == len(nums):
                res.append(path[:])
                return
            dfs(path, idx + 1)

            path.append(nums[idx])
            dfs(path, idx + 1)
            path.pop()
        
        dfs([], 0)
        return res
    
# time O(n*(2**n)), due to each element can take or not take (2**n), and n for copy list
# space O(n), due to recursion stack, not counting output here
# using dfs and backtracking and subset
'''
1. type: subset
2. duplicate elements: no
3. selectable repeatedly: no
'''
'''
this approach focus on considering each element:
for cur element, 
we don't take, then goto next element
or we take, then goto next element
till no more element to be considered, we record path
'''

class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        res = []

        def dfs(path, idx):
            if idx == len(nums):
                res.append(path[:])
                return

            res.append(path[:])
            for i in range(idx, len(nums)):
                path.append(nums[i])
                dfs(path, i + 1)
                path.pop()
        
        dfs([], 0)
        return res
    
# time O(n*(2**n)), due to each element can take or not take (2**n), and n for copy list
# space O(n), due to recursion stack, not counting output here
# using dfs and backtracking and subset
'''
1. type: subset
2. duplicate elements: no
3. selectable repeatedly: no
'''
'''
this approach focus on constructing the path:
record cur path,
then choose a element to add in path

more specific:
we have chosen nothing, record, try to add first element
we have chosen one element, record, try to add another element
we have chosen two elements, record, try to add another element
we have chosen three elements, record, try to add another element
'''
```


## 📄 [J]backtracking\[J]backtracking\79-word-search.java

```java
class Solution {
    char[][] board;
    String word;
    int rows;
    int cols;

    public boolean exist(char[][] board, String word) {
        this.board = board;
        this.word = word;
        rows = board.length;
        cols = board[0].length;

        HashMap<Character, Integer> charToFreq = new HashMap<>();
        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {
                charToFreq.compute(board[r][c], (k, v) -> v == null ? 1 : v + 1);
            }
        }
        for (int i = 0; i < word.length(); i++) {
            Character c = word.charAt(i);
            if (!charToFreq.containsKey(c)) {
                return false;
            }
            charToFreq.put(c, charToFreq.get(c) - 1);
            if (Objects.equals(charToFreq.get(c), 0)) {
                charToFreq.remove(c);
            }
        }

        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {
                HashSet<Integer> visited = new HashSet<>();
                if (dfs(r, c, 0, visited) == true) {
                    return true;
                }
            }
        }
        return false;
    }

    public boolean dfs(int r, int c, int idx, HashSet<Integer> visited) {
        if (0 > r || r >= rows || 0 > c || c >= cols || visited.contains(r * cols + c) || board[r][c] != word.charAt(idx)) {
            return false;
        }
        if (idx == word.length() - 1) {
            return true;
        }
        visited.add(r * cols + c);
        for (int[] nextrc: new int[][]{{r+1, c}, {r-1, c}, {r, c+1}, {r, c-1}}) {
            if (dfs(nextrc[0], nextrc[1], idx + 1, visited) == true) {
                return true;
            }
        }
        visited.remove(r * cols + c);
        return false;

    }
}

// time O(RC * 3**L)
// space O(RC), due to hashset
// using dfs and backtracking and backtracking with constraints and pruning
```


## 📄 [J]backtracking\[J]backtracking\79-word-search.py

```py
from collections import defaultdict
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        rows, cols = len(board), len(board[0])

        schar_freq = defaultdict(int)
        for r in range(rows):
            for c in range(cols):
                schar_freq[board[r][c]] += 1
        tchar_freq = defaultdict(int)
        for c in word:
            tchar_freq[c] += 1
        for tc, freq in tchar_freq.items():
            if freq > schar_freq[tc]:
                return False
        
        def dfs(r, c, idx, visited):
            if idx == len(word):
                return True
            for next_r, next_c in [(r+1, c), (r-1, c), (r, c+1), (r, c-1)]:
                if next_r not in range(rows) or next_c not in range(cols) or (next_r, next_c) in visited or board[next_r][next_c] != word[idx]:
                    continue
                visited.add((next_r, next_c))
                if dfs(next_r, next_c, idx + 1, visited):
                    return True
                visited.remove((next_r, next_c))
            return False

        for r in range(rows):
            for c in range(cols):
                if board[r][c] == word[0]:
                    if dfs(r, c, 1, {(r, c)}):
                        return True
        return False
    
# time O(RC * 3**L)
# space O(RC), due to hashset
# using dfs and backtracking and backtracking with constraints and pruning
```


## 📄 [J]backtracking\[J]backtracking\90-subsets-ii.py

```py
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        
        nums.sort()
        res = []

        def dfs(path, visited, idx):
            if idx == len(nums):
                res.append(path[:])
                return

            dfs(path, visited, idx + 1)

            if idx - 1 >= 0 and nums[idx - 1] == nums[idx] and idx - 1 not in visited:
                return
            path.append(nums[idx])
            visited.add(idx)
            dfs(path, visited, idx + 1)
            path.pop()
            visited.remove(idx)

        dfs([], set(), 0)
        return res
    
# time O(2**n * n)
# space O(n)
# using dfs and backtracking and subset and sort
'''
1. type: subset
2. duplicate elements: yes
3. selectable repeatedly: no
'''

class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        
        nums.sort()
        res = []

        def dfs(path, visited, idx):
            if idx == len(nums):
                res.append(path[:])
                return
            
            res.append(path[:])
            for i in range(idx, len(nums)):
                if i - 1 >= 0 and nums[i - 1] == nums[i] and i - 1 not in visited:
                    continue
                path.append(nums[i])
                visited.add(i)
                dfs(path, visited, i + 1)
                path.pop()
                visited.remove(i)

        dfs([], set(), 0)
        return res

# time O(2**n * n)
# space O(n)
# using dfs and backtracking and subset and sort
'''
1. type: subset
2. duplicate elements: yes
3. selectable repeatedly: no
'''
```


## 📄 [J]backtracking\[J]backtracking\93-restore-ip-addresses.py

```py
class Solution:
    def restoreIpAddresses(self, s: str) -> List[str]:
        
        res = []

        def dfs(path, idx):
            if idx == len(s) or len(path) == 4:
                if idx == len(s) and len(path) == 4:
                    res.append('.'.join(path))
                return
            if 0 <= int(s[idx]) <= 9:
                path.append(s[idx])
                dfs(path, idx + 1)
                path.pop()
            if 10 <= int(s[idx:idx + 2]) <= 99:
                path.append(s[idx:idx + 2])
                dfs(path, idx + 2)
                path.pop()
            if 100 <= int(s[idx:idx + 3]) <= 255:
                path.append(s[idx:idx + 3])
                dfs(path, idx + 3)
                path.pop()

        dfs([], 0)
        return res

# time O(s * 3**4), s is the length of address (duplicate to output's cost)
# space O(4), due to recursion stack's size, not counting output
# using dfs and backtracking and backtracking with constraints
```


## 📄 [K]graph\[K]graph-bellman-ford\787-cheapest-flights-within-k-stops.py

```py
class Solution:
    def findCheapestPrice(self, n: int, flights: List[List[int]], src: int, dst: int, k: int) -> int:
        node_dist = [float('inf') for _ in range(n)]
        node_dist[src] = 0

        for i in range(k + 1):
            temp_node_dist = node_dist[:]
            for p, q, w in flights:
                if node_dist[p] != float('inf') and node_dist[p] + w < temp_node_dist[q]:
                    temp_node_dist[q] = node_dist[p] + w
            node_dist = temp_node_dist
        return node_dist[dst] if node_dist[dst] != float('inf') else - 1

# time O(kE), at most O(VE) for original bellman ford algo
# space O(V)
# using graph and bellman ford and shortest path

from heapq import *
class Solution:
    def findCheapestPrice(self, n: int, flights: List[List[int]], src: int, dst: int, k: int) -> int:
        graph = [[] for _ in range(n)]
        for p, q, w in flights:
            graph[p].append((q, w))
        step_total = k + 1
        step_node_dist = [[float('inf') for _ in range(n)] for _ in range(step_total + 1)]
        step_node_dist[0][src] = 0
        heap = [(0, 0, src)]
        heapify(heap)
        visited = set()
        while heap:
            prev, step, node = heappop(heap)
            if node == dst:
                break
            if step == step_total:
                continue
            if (step, node) in visited:
                continue
            visited.add((step, node))
            for neighbor, w in graph[node]:
                d = prev + w
                if d < step_node_dist[step + 1][neighbor]:
                    heappush(heap, (d, step + 1, neighbor))
                    step_node_dist[step + 1][neighbor] = d

        res = float('inf')
        for s in range(step_total + 1):
            res = min(res, step_node_dist[s][dst])
        return res if res != float('inf') else - 1

# time O(Eklog(Ek))
# space O(Vk)
# using graph and dijkstra and shortest path
```


## 📄 [K]graph\[K]graph-bfs\1091-shortest-path-in-binary-matrix.py

```py
from collections import deque
class Solution:
    def shortestPathBinaryMatrix(self, grid: List[List[int]]) -> int:
        rows, cols = len(grid), len(grid[0])
        visited = set()
        queue = deque([])
        if grid[0][0] == 0:
            queue.append((0, 0, 1))
            visited.add((0, 0))
        while queue:
            r, c, count = queue.popleft()
            if (r, c) == (rows - 1, cols - 1):
                return count
            for next_r, next_c in [(r+1, c), (r-1, c), (r, c+1), (r, c-1), (r+1, c+1), (r-1, c-1), (r+1, c-1), (r-1, c+1)]:
                if next_r not in range(rows) or next_c not in range(cols) or (next_r, next_c) in visited or grid[next_r][next_c] == 1:
                    continue
                queue.append((next_r, next_c, count + 1))
                visited.add((next_r, next_c))
        return - 1
    
# time O(RC)
# space O(RC)
# using graph and bfs with single source
```


## 📄 [K]graph\[K]graph-bfs\1197-minimum-knight-moves.py

```py
from collections import deque
class Solution:
    def minKnightMoves(self, x: int, y: int) -> int:
        target = (x, y)
        visited = {(0, 0)}
        queue = deque([(0, 0, 0)])
        while queue:
            x, y, step = queue.popleft()
            if (x, y) == target:
                break
            for offset_x, offset_y in [(2, 1), (1, 2), (-1, 2), (-2, 1), (-2, -1), (-1, -2), (1, -2), (2, - 1)]:
                next_x, next_y = x + offset_x, y + offset_y
                if (next_x, next_y) in visited:
                    continue
                if 3 < abs(x - target[0]) + abs(y - target[1]) < abs(next_x - target[0]) + abs(next_y - target[1]):
                    continue
                queue.append((next_x, next_y, step + 1))
                visited.add((next_x, next_y))
        return step

# time O(RC), due to the search's square
# space O(RC), due to set, the queue is O(max(R, C))
# using graph and bfs with single source and pruning
```


## 📄 [K]graph\[K]graph-bfs\126-word-ladder-ii.py

```py
from collections import defaultdict, deque
import string
class Solution:
    def findLadders(self, beginWord: str, endWord: str, wordList: List[str]) -> List[List[str]]:
        graph = defaultdict(list)
        wordset = set(wordList)
        queue = deque([beginWord])
        while queue:
            length = len(queue)
            next_queue = set()
            remove_wordset = set()
            found = False
            for _ in range(length):
                word = queue.popleft()
                if word == endWord:
                    found = True
                    break
                for replace_i in range(len(word)):
                    for c in string.ascii_lowercase:
                        new_word = word[: replace_i] + c + word[replace_i + 1:]
                        if new_word in wordset:
                            next_queue.add(new_word)
                            remove_wordset.add(new_word)
                            graph[new_word].append(word)
            if found:
                break
            wordset -= remove_wordset
            queue.extend(next_queue)

        res = []
        def dfs(path):
            if path[- 1] == beginWord:
                res.append(path[:: - 1])
                return
            for neighbor in graph[path[- 1]]:
                path.append(neighbor)
                dfs(path)
                path.pop()

        dfs([endWord])
        return res

# time O(n * L**2 + nL * 26**L), n * L**2 for bfs and building graph
# space O(nL), not couning output
# using graph and bfs with hashset as queue and hashset and dfs and backtracking
'''
1. bfs to build graph
2. dfs and backtracking to get all paths
'''
```


## 📄 [K]graph\[K]graph-bfs\127-word-ladder.py

```py
from collections import deque
import string
class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        wordset = set(wordList)
        queue = deque([(beginWord, 1)])
        while queue:
            word, count = queue.popleft()
            if word == endWord:
                return count
            for replace_i in range(len(word)):
                for c in string.ascii_lowercase:
                    new_word = word[: replace_i] + c + word[replace_i + 1:]
                    if new_word in wordset:
                        queue.append((new_word, count + 1))
                        wordset.remove(new_word)
        return 0
    
# time O(n * L**2)
# space O(nL), due to hashset
# using graph and bfs with single source
```


## 📄 [K]graph\[K]graph-bfs\130-surrounded-regions.py

```py
from collections import deque
class Solution:
    def solve(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        rows, cols = len(board), len(board[0])
        visited = set()
        queue = deque([])
        for r in range(rows):
            for c in range(cols):
                if board[r][c] == 'O' and (r in [0, rows - 1] or c in [0, cols - 1]):
                    queue.append((r, c))
                    visited.add((r, c))
        
        while queue:
            r, c = queue.popleft()
            for next_r, next_c in [(r+1, c), (r-1, c), (r, c+1), (r, c-1)]:
                if next_r not in range(rows) or next_c not in range(cols) or (next_r, next_c) in visited or board[next_r][next_c] == 'X':
                    continue
                queue.append((next_r, next_c))
                visited.add((next_r, next_c))
        
        for r in range(rows):
            for c in range(cols):
                if board[r][c] == 'O' and (r, c) not in visited:
                    board[r][c] = 'X'    

# time O(RC)
# space O(RC)
# using graph and bfs with multiple sources
```


## 📄 [K]graph\[K]graph-bfs\133-clone-graph.java

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> neighbors;
    public Node() {
        val = 0;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val) {
        val = _val;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val, ArrayList<Node> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
}
*/

class Solution {
    public Node cloneGraph(Node node) {
        HashMap<Node, Node> oldToNew = new HashMap<>();
        if (node == null) {
            return node;
        }
        oldToNew.put(node, new Node(node.val));
        ArrayDeque<Node> queue = new ArrayDeque<>();
        queue.offer(node);
        while (!queue.isEmpty()) {
            Node oldNode = queue.poll();
            Node newNode = oldToNew.get(oldNode);
            for (Node neighbor: oldNode.neighbors) {
                if (!oldToNew.containsKey(neighbor)) {
                    oldToNew.put(neighbor, new Node(neighbor.val));
                    queue.offer(neighbor);
                }
                Node newNeighbor = oldToNew.get(neighbor);
                newNode.neighbors.add(newNeighbor);
            }
        }
        return oldToNew.get(node);
    }
}

// time O(n)
// space O(n)
// using graph and bfs with single source and hashmap
```


## 📄 [K]graph\[K]graph-bfs\133-clone-graph.py

```py
"""
# Definition for a Node.
class Node:
    def __init__(self, val = 0, neighbors = None):
        self.val = val
        self.neighbors = neighbors if neighbors is not None else []
"""

from typing import Optional
from collections import deque
class Solution:
    def cloneGraph(self, node: Optional['Node']) -> Optional['Node']:
        if not node:
            return node
        old_new = {}
        queue = deque([])
        visited = set()
        queue.append(node)
        visited.add(node)
        while queue:
            old_node = queue.popleft()
            if old_node not in old_new:
                old_new[old_node] = Node(old_node.val)
            for neighbor in old_node.neighbors:
                if neighbor not in old_new:
                    old_new[neighbor] = Node(neighbor.val)
                old_new[old_node].neighbors.append(old_new[neighbor])
                if neighbor not in visited:
                    queue.append(neighbor)
                    visited.add(neighbor)
        return old_new[node]
    
# time O(n)
# space O(n)
# using graph and bfs with single source and hashmap
```


## 📄 [K]graph\[K]graph-bfs\1345-jump-game-iv.py

```py
from collections import defaultdict, deque
class Solution:
    def minJumps(self, arr: List[int]) -> int:
        val_indices = defaultdict(list)
        for i, val in enumerate(arr):
            val_indices[val].append(i)
        visited = {0}
        queue = deque([(0, 0)])
        while queue:
            i, step = queue.popleft()
            if i == len(arr) - 1:
                return step
            for next_idx in [i - 1, i + 1] + val_indices[arr[i]]:
                if next_idx not in range(len(arr)) or next_idx in visited:
                    continue
                queue.append((next_idx, step + 1))
                visited.add(next_idx)
            val_indices.pop(arr[i])
            
# time O(n)
# space O(n)
# using graph and bfs with single source and pruning
```


## 📄 [K]graph\[K]graph-bfs\1730-shortest-path-to-get-food.py

```py
from collections import deque
class Solution:
    def getFood(self, grid: List[List[str]]) -> int:
        rows, cols = len(grid), len(grid[0])
        visited = set()
        queue = deque([])
        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == '*':
                    queue.append((r, c, 0))
        while queue:
            r, c, step = queue.popleft()
            if grid[r][c] == '#':
                return step
            for next_r, next_c in [(r+1, c), (r-1, c), (r, c+1), (r, c-1)]:
                if next_r not in range(rows) or next_c not in range(cols) or (next_r, next_c) in visited or grid[next_r][next_c] == 'X':
                    continue
                queue.append((next_r, next_c, step + 1))
                visited.add((next_r, next_c))

        return - 1

# time O(RC)
# space O(RC)
# using graph and bfs with single source
```


## 📄 [K]graph\[K]graph-bfs\1905-count-sub-islands.py

```py
from collections import deque
class Solution:
    def countSubIslands(self, grid1: List[List[int]], grid2: List[List[int]]) -> int:
        rows, cols = len(grid1), len(grid1[0])
        visited = set()
        res = 0
        for r in range(rows):
            for c in range(cols):
                if (r, c) in visited or grid2[r][c] == 0:
                    continue
                queue = deque([(r, c)])
                visited.add((r, c))
                match = True
                while queue:
                    row, col = queue.popleft()
                    if grid1[row][col] == 0:
                        match = False
                    for next_r, next_c in [(row+1, col), (row-1, col), (row, col+1), (row, col-1)]:
                        if next_r not in range(rows) or next_c not in range(cols) or (next_r, next_c) in visited or grid2[next_r][next_c] == 0:
                            continue
                        queue.append((next_r, next_c))
                        visited.add((next_r, next_c))
                if match:
                    res += 1
        return res
    
# time O(RC)
# space O(RC)
# using graph and bfs with single source
```


## 📄 [K]graph\[K]graph-bfs\1992-find-all-groups-of-farmland.py

```py
from collections import deque
class Solution:
    def findFarmland(self, land: List[List[int]]) -> List[List[int]]:
        rows, cols = len(land), len(land[0])
        visited = set()
        res = []
        for r in range(rows):
            for c in range(cols):
                if (r, c) in visited or land[r][c] == 0:
                    continue
                queue = deque([(r, c)])
                visited.add((r, c))
                max_r, max_c = r, c
                while queue:
                    row, col = queue.popleft()
                    max_r, max_c = max(max_r, row), max(max_c, col)
                    for next_r, next_c in [(row+1, col), (row-1, col), (row, col+1), (row, col-1)]:
                        if next_r not in range(rows) or next_c not in range(cols) or (next_r, next_c) in visited or land[next_r][next_c] == 0:
                            continue
                        queue.append((next_r, next_c))
                        visited.add((next_r, next_c))
                res.append([r, c, max_r, max_c])
        return res
    
# time O(RC)
# space O(RC)
# using graph and bfs with single source
```


## 📄 [K]graph\[K]graph-bfs\200-number-of-islands.java

```java
class Solution {
    public int numIslands(char[][] grid) {
        int res = 0;
        int rows = grid.length;
        int cols = grid[0].length;
        HashSet<Integer> visited = new HashSet<>();
        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {
                if (visited.contains(r * cols + c) || grid[r][c] == '0') {
                    continue;
                }
                ArrayDeque<int[]> queue = new ArrayDeque<>();
                queue.offer(new int[]{r, c});
                visited.add(r * cols + c);
                res += 1;
                while (!queue.isEmpty()) {
                    int[] rc = queue.poll();
                    int cur_r = rc[0];
                    int cur_c = rc[1];
                    for (int[] nextrc: new int[][]{{cur_r+1, cur_c}, {cur_r-1, cur_c}, {cur_r, cur_c+1}, {cur_r, cur_c-1}}) {
                        int next_r = nextrc[0];
                        int next_c = nextrc[1];
                        if (0 <= next_r && next_r < rows && 0 <= next_c && next_c < cols && !visited.contains(next_r * cols + next_c) && grid[next_r][next_c] == '1') {
                            queue.offer(new int[]{next_r, next_c});
                            visited.add(next_r * cols + next_c);
                        }
                    }
                }
            }
        }
        return res;
    }
}

// time O(RC)
// space O(RC)
// using graph and bfs with single source
```


## 📄 [K]graph\[K]graph-bfs\200-number-of-islands.py

```py
from collections import deque
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        rows, cols = len(grid), len(grid[0])
        visited = set()
        res = 0
        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == "1" and (r, c) not in visited:
                    res += 1
                    visited.add((r, c))
                    queue = deque([(r, c)])
                    while queue:
                        row, col = queue.popleft()
                        for next_r, next_c in [(row+1, col), (row-1, col), (row, col+1), (row, col-1)]:
                            if next_r not in range(rows) or next_c not in range(cols) or (next_r, next_c) in visited or grid[next_r][next_c] == "0":
                                continue
                            queue.append((next_r, next_c))
                            visited.add((next_r, next_c))
        return res
    
# time O(RC)
# space O(RC)
# using graph and bfs with single source
```


## 📄 [K]graph\[K]graph-bfs\261-graph-valid-tree.py

```py
from collections import defaultdict, deque
class Solution:
    def validTree(self, n: int, edges: List[List[int]]) -> bool:
        graph = defaultdict(list)
        for p, q in edges:
            graph[p].append(q)
            graph[q].append(p)
        
        visited = {0}
        queue = deque([(0, - 1)])
        while queue:
            node, parent = queue.popleft()
            for neighbor in graph[node]:
                if neighbor == parent:
                    continue
                if neighbor in visited:
                    return False
                queue.append((neighbor, node))
                visited.add(neighbor)

        return len(visited) == n
    
# time O(V+E)
# space O(V+E)
# using graph and bfs with single source
'''
1. tree is a special graph with properties that
    - connected
    - acyclic
    - non-direction edges
    - one path between any two vertices/nodes
'''

class UnionFind:
    def __init__(self, n):
        self.parent = [i for i in range(n)]
        self.rank = [0 for _ in range(n)]
        self.count = n
    
    def find(self, p):
        while p != self.parent[p]:
            self.parent[p] = self.parent[self.parent[p]]
            p = self.parent[p]
        return p

    def union(self, p, q):
        root_p = self.find(p)
        root_q = self.find(q)
        if root_p == root_q:
            return
        if self.rank[root_p] > self.rank[root_q]:
            self.parent[root_q] = root_p
        elif self.rank[root_p] < self.rank[root_q]:
            self.parent[root_p] = root_q
        else:
            self.parent[root_p] = root_q
            self.rank[root_q] += 1
        self.count -= 1
    
    def is_connected(self, p, q):
        return self.find(p) == self.find(q)
    
    def get_count(self):
        return self.count

class Solution:
    def validTree(self, n: int, edges: List[List[int]]) -> bool:
        uf = UnionFind(n)
        for p, q in edges:
            if uf.is_connected(p, q):
                return False
            uf.union(p, q)
        return uf.get_count() == 1

# time O(V+E)
# space O(V)
# using graph and union find
'''
1. tree is a special graph with properties that
    - connected
    - acyclic
    - non-direction edges
    - one path between any two vertices/nodes
'''
```


## 📄 [K]graph\[K]graph-bfs\286-walls-and-gates.py

```py
from collections import deque
class Solution:
    def wallsAndGates(self, rooms: List[List[int]]) -> None:
        """
        Do not return anything, modify rooms in-place instead.
        """
        rows, cols = len(rooms), len(rooms[0])
        visited = set()
        queue = deque([])
        for r in range(rows):
            for c in range(cols):
                if rooms[r][c] == 0:
                    queue.append((r, c, 0))
                    visited.add((r, c))
        while queue:
            r, c, step = queue.popleft()
            rooms[r][c] = step
            for next_r, next_c in [(r+1, c), (r-1, c), (r, c+1), (r, c-1)]:
                if next_r not in range(rows) or next_c not in range(cols) or (next_r, next_c) in visited or rooms[next_r][next_c] == - 1:
                    continue
                queue.append((next_r, next_c, step + 1))
                visited.add((next_r, next_c))
                
# time O(RC)
# space O(RC)
# using graph and bfs with multiple sources
```


## 📄 [K]graph\[K]graph-bfs\301-remove-invalid-parentheses.py

```py
from collections import deque
class Solution:
    def removeInvalidParentheses(self, s: str) -> List[str]:
        
        def valid(s):
            balance = 0
            for c in s:
                if c == '(':
                    balance += 1
                elif c == ')':
                    balance -= 1
                    if balance < 0:
                        return False
            return balance == 0

        queue = deque([s])
        res = []
        while queue:
            length = len(queue)
            next_queue = set()
            for _ in range(length):
                string = queue.popleft()
                if valid(string):
                    res.append(string)
                    continue
                for i, c in enumerate(string):
                    if c in '()':
                        next_queue.add(string[: i] + string[i + 1:])
            if res:
                break
            queue.extend(next_queue)

        return res
        
# time O(n * 2**n)
# space O(n * C(2/n, n)), due to the max number of combinations in i round
# using graph and bfs with hashset as queue
```


## 📄 [K]graph\[K]graph-bfs\417-pacific-atlantic-water-flow.py

```py
from collections import deque
class Solution:
    def pacificAtlantic(self, heights: List[List[int]]) -> List[List[int]]:
        g = heights
        rows, cols = len(g), len(g[0])

        def bfs(queue, visited, temp):
            while queue:
                r, c = queue.popleft()
                temp[r][c] += 1
                for next_r, next_c in [(r+1, c), (r-1, c), (r, c+1), (r, c-1)]:
                    if next_r not in range(rows) or next_c not in range(cols) or (next_r, next_c) in visited or g[r][c] > g[next_r][next_c]:
                        continue
                    queue.append((next_r, next_c))
                    visited.add((next_r, next_c))
        
        temp = [[0 for _ in range(cols)] for _ in range(rows)]
        p_queue = deque([])
        p_visited = set()
        a_queue = deque([])
        a_visited = set()
        for r in range(rows):
            for c in range(cols):
                if r == 0 or c == 0:
                    p_queue.append((r, c))
                    p_visited.add((r, c))
                if r == rows - 1 or c == cols - 1:
                    a_queue.append((r, c))
                    a_visited.add((r, c))
        bfs(p_queue, p_visited, temp)
        bfs(a_queue, a_visited, temp)
        res = []
        for r in range(rows):
            for c in range(cols):
                if temp[r][c] == 2:
                    res.append([r, c])
        return res
    
# time O(RC)
# space O(RC)
# using graph and bfs with multiple sources
```


## 📄 [K]graph\[K]graph-bfs\542-01-matrix.java

```java
class Solution {
    public int[][] updateMatrix(int[][] mat) {
        int rows = mat.length;
        int cols = mat[0].length;
        int[][] res = new int[rows][cols];

        ArrayDeque<int[]> queue = new ArrayDeque<>();
        HashSet<Integer> visited = new HashSet<>();

        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {
                if (mat[r][c] == 0) {
                    queue.offer(new int[]{r, c, 0});
                    visited.add(r * cols + c);
                }
            }
        }
        
        while (!queue.isEmpty()) {
            int[] rcs = queue.poll();
            int r = rcs[0];
            int c = rcs[1];
            int s = rcs[2];
            res[r][c] = s;
            for (int[] nextrc: new int[][]{{r + 1, c}, {r - 1, c}, {r, c + 1}, {r, c - 1}}) {
                int nextr = nextrc[0];
                int nextc = nextrc[1];
                if (0 <= nextr && nextr < rows && 0 <= nextc && nextc < cols && !visited.contains(nextr * cols + nextc)) {
                    queue.offer(new int[]{nextr, nextc, s + 1});
                    visited.add(nextr * cols + nextc);
                }
            }
        }
        return res;
    }
}

// time O(RC)
// space O(RC)
// using graph and bfs with multiple sources
```


## 📄 [K]graph\[K]graph-bfs\542-01-matrix.py

```py
from collections import deque
class Solution:
    def updateMatrix(self, mat: List[List[int]]) -> List[List[int]]:
        rows, cols = len(mat), len(mat[0])
        res = [[0 for _ in range(cols)] for _ in range(rows)]

        visited = set()
        queue = deque([])
        for r in range(rows):
            for c in range(cols):
                if mat[r][c] == 0:
                    queue.append((r, c, 0))
                    visited.add((r, c))
        
        while queue:
            r, c, step = queue.popleft()
            res[r][c] = step
            for next_r, next_c in [(r+1, c), (r-1, c), (r, c+1), (r, c-1)]:
                if next_r not in range(rows) or next_c not in range(cols) or (next_r, next_c) in visited:
                    continue
                queue.append((next_r, next_c, step + 1))
                visited.add((next_r, next_c))
        return res
    
# time O(RC)
# space O(RC)
# using graph and bfs with multiple sources
```


## 📄 [K]graph\[K]graph-bfs\694-number-of-distinct-islands.py

```py
from collections import deque
class Solution:
    def numDistinctIslands(self, grid: List[List[int]]) -> int:
        rows, cols = len(grid), len(grid[0])
        visited = set()
        islands = set()
        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == 1 and (r, c) not in visited:
                    visited.add((r, c))
                    queue = deque([(r, c)])
                    path = []
                    while queue:
                        row, col = queue.popleft()
                        path.append((row - r, col - c))
                        for next_r, next_c in [(row+1, col), (row-1, col), (row, col+1), (row, col-1)]:
                            if next_r not in range(rows) or next_c not in range(cols) or (next_r, next_c) in visited or grid[next_r][next_c] == 0:
                                continue
                            queue.append((next_r, next_c))
                            visited.add((next_r, next_c))
                    islands.add(tuple(path))
        return len(islands)
    
# time O(RC)
# space O(RC)
# using graph and bfs with single source
```


## 📄 [K]graph\[K]graph-bfs\695-max-area-of-island.py

```py
from collections import deque
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        rows, cols = len(grid), len(grid[0])
        res = 0
        visited = set()
        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == 0 or (r, c) in visited:
                    continue
                area = 1
                queue = deque([(r, c)])
                visited.add((r, c))
                while queue:
                    row, col = queue.popleft()
                    for next_r, next_c in [(row+1, col), (row-1, col), (row, col+1), (row, col-1)]:
                        if next_r not in range(rows) or next_c not in range(cols) or (next_r, next_c) in visited or grid[next_r][next_c] == 0:
                            continue
                        queue.append((next_r, next_c))
                        visited.add((next_r, next_c))
                        area += 1
                res = max(res, area)
        return res
    
# time O(RC)
# space O(RC)
# using graph and bfs with single source
```


## 📄 [K]graph\[K]graph-bfs\733-flood-fill.java

```java
class Solution {
    public int[][] floodFill(int[][] image, int sr, int sc, int color) {
        int oldColor = image[sr][sc];
        if (oldColor == color) {
            return image;
        }
        int rows = image.length;
        int cols = image[0].length;
        ArrayDeque<int[]> queue = new ArrayDeque<>();
        HashSet<Integer> visited = new HashSet<>();
        queue.offer(new int[]{sr, sc});
        visited.add(sr * cols + sc);
        while (!queue.isEmpty()) {
            int[] rc = queue.poll();
            int r = rc[0];
            int c = rc[1];
            image[r][c] = color;
            for (int[] d: new int[][]{{1, 0}, {- 1, 0}, {0, 1}, {0, - 1}}) {
                int nextR = r + d[0];
                int nextC = c + d[1];
                if (0 <= nextR && nextR < rows && 0 <= nextC && nextC < cols && !visited.contains(nextR * cols + nextC) && image[nextR][nextC] == oldColor) {
                    queue.offer(new int[]{nextR, nextC});
                    visited.add(nextR * cols + nextC);
                }
            }
        }
        return image;
    }
}

// time O(RC)
// space O(RC)
// using graph and bfs with single source
```


## 📄 [K]graph\[K]graph-bfs\733-flood-fill.py

```py
from collections import deque
class Solution:
    def floodFill(self, image: List[List[int]], sr: int, sc: int, color: int) -> List[List[int]]:
        rows, cols = len(image), len(image[0])
        old_color = image[sr][sc]
        visited = set()
        queue = deque([(sr, sc)])
        visited.add((sr, sc))
        while queue:
            r, c = queue.popleft()
            image[r][c] = color
            for next_r, next_c in [(r+1, c), (r-1, c), (r, c+1), (r, c-1)]:
                if next_r not in range(rows) or next_c not in range(cols) or (next_r, next_c) in visited or image[next_r][next_c] != old_color:
                    continue
                queue.append((next_r, next_c)) 
                visited.add((next_r, next_c))
        return image

# time O(RC)
# space O(RC)
# using graph and bfs with single source
```


## 📄 [K]graph\[K]graph-bfs\749-contain-virus.py

```py
from collections import deque
class Solution:
    def containVirus(self, isInfected: List[List[int]]) -> int:
        g = isInfected
        rows, cols = len(g), len(g[0])
        
        def bfs(row, col):
            old_area = set()
            new_area = set()
            walls = 0
            queue = deque([(row, col)])
            old_area.add((row, col))
            while queue:
                r, c = queue.popleft()
                for next_r, next_c in [(r+1, c), (r-1, c), (r, c+1), (r, c-1)]:
                    if next_r not in range(rows) or next_c not in range(cols) or (next_r, next_c) in old_area:
                        continue
                    if g[next_r][next_c] == 0:
                        walls += 1
                        new_area.add((next_r, next_c))
                    elif g[next_r][next_c] == 1:
                        queue.append((next_r, next_c))
                        old_area.add((next_r, next_c))
            return walls, old_area, new_area
        
        res = 0
        while True:
            idx_info = {}
            visited = set()
            idx = 0
            for r in range(rows):
                for c in range(cols):
                    if g[r][c] != 1 or (r, c) in visited:
                        continue
                    walls, old_area, new_area = bfs(r, c)
                    idx_info[idx] = (walls, old_area, new_area)
                    for row, col in old_area:
                        visited.add((row, col))
                    idx += 1
            if not idx_info:
                break
            target = max(idx_info.keys(), key = lambda x: len(idx_info[x][2]))
            walls, old_area, new_area = idx_info[target]
            res += walls
            for row, col in old_area:
                g[row][col] = 2
            idx_info.pop(target)
            for walls, old_area, new_area in idx_info.values():
                for row, col in new_area:
                    g[row][col] = 1
        return res
    
# time O(RC * (R + C)), each day cost RC and (R+C) days at most
# space O(RC)
# using graph and bfs with single source and hashmap
```


## 📄 [K]graph\[K]graph-bfs\815-bus-routes.py

```py
from collections import defaultdict, deque
class Solution:
    def numBusesToDestination(self, routes: List[List[int]], source: int, target: int) -> int:
        stop_route = defaultdict(list)
        for i, r in enumerate(routes):
            for stop in r:
                stop_route[stop].append(i)
        
        visited = set()
        queue = deque([(source, 0)])
        while queue:
            stop, step = queue.popleft()
            if stop == target:
                return step
            for r in stop_route[stop]:
                if r in visited:
                    continue
                visited.add(r)
                for stop in routes[r]:
                    queue.append((stop, step + 1))
                    
        return - 1
        
# time (n*m)
# space O(n*m), due to building graph, n is the number of routes, m is the number of stops
# using graph and bfs with single source
'''
1. when building graph, using bus route instead of bus stop
'''
```


## 📄 [K]graph\[K]graph-bfs\909-snakes-and-ladders.py

```py
from collections import deque
class Solution:
    def snakesAndLadders(self, board: List[List[int]]) -> int:
        rows, cols = len(board), len(board[0])
        
        def get_rc(num):
            num -= 1
            r, c = divmod(num, cols)
            if r % 2:
                c = cols - 1 - c
            r = rows - 1 - r
            return (r, c)

        visited = set()
        queue = deque([(1, 0)])
        visited.add(1)
        while queue:
            num, step = queue.popleft()
            r, c = get_rc(num)
            if board[r][c] != - 1:
                num = board[r][c]
            if num == rows * cols:
                return step
            for offset in range(1, 7):
                next_num = num + offset
                if next_num in visited:
                    continue
                queue.append((next_num, step + 1))
                visited.add(next_num)

        return - 1
    
# time O(RC)
# space O(RC)
# using graph and bfs with single source
```


## 📄 [K]graph\[K]graph-bfs\994-rotting-oranges.java

```java
class Solution {
    public int orangesRotting(int[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;
        int fresh = 0;
        int rotten = 0;
        ArrayDeque<int[]> queue = new ArrayDeque<>();
        HashSet<Integer> visited = new HashSet<>();
        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {
                if (grid[r][c] == 1) {
                    fresh += 1;
                }
                else if (grid[r][c] == 2) {
                    rotten += 1;
                    queue.offer(new int[]{r, c, 0});
                    visited.add(r * cols + c);
                }
            }
        }
        if (fresh == 0) {
            return 0;
        }
        if (rotten == 0) {
            return - 1;
        }
        int res = 0;
        while (!queue.isEmpty()) {
            int[] rc = queue.poll();
            int r = rc[0];
            int c = rc[1];
            int step = rc[2];
            res = step;
            if (grid[r][c] == 1) {
                fresh -= 1;
            }
            for (int[] nextrc: new int[][]{{r+1, c}, {r-1, c}, {r, c+1}, {r, c-1}}) {
                int next_r = nextrc[0];
                int next_c = nextrc[1];
                if (0 <= next_r && next_r < rows && 0 <= next_c && next_c < cols && !visited.contains(next_r * cols + next_c) && grid[next_r][next_c] == 1) {
                    queue.offer(new int[]{next_r, next_c, step + 1});
                    visited.add(next_r * cols + next_c);
                }
            }
        }
        return fresh == 0 ? res : - 1;
    }
}

// time O(RC)
// space O(RC)
// using graph and bfs with multiple sources
```


## 📄 [K]graph\[K]graph-bfs\994-rotting-oranges.py

```py
from collections import deque
class Solution:
    def orangesRotting(self, grid: List[List[int]]) -> int:
        rows, cols = len(grid), len(grid[0])
        visited = set()
        queue = deque([])
        fresh = 0
        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == 1:
                    fresh += 1
                elif grid[r][c] == 2:
                    queue.append((r, c, 0))
                    visited.add((r, c))
        if fresh == 0:
            return 0

        while queue:
            r, c, minute = queue.popleft()
            if grid[r][c] == 1:
                fresh -= 1
                if fresh == 0:
                    return minute
            for next_r, next_c in [(r+1, c), (r-1, c), (r, c+1), (r, c-1)]:
                if next_r not in range(rows) or next_c not in range(cols) or (next_r, next_c) in visited or grid[next_r][next_c] != 1:
                    continue
                queue.append((next_r, next_c, minute + 1))
                visited.add((next_r, next_c))
            
        return - 1
    
# time O(RC)
# space O(RC)
# using graph and bfs with multiple sources
```


## 📄 [K]graph\[K]graph-dfs\1059-all-paths-from-source-lead-to-destination.py

```py
from collections import defaultdict
class Solution:
    def leadsToDestination(self, n: int, edges: List[List[int]], source: int, destination: int) -> bool:
        graph = defaultdict(set)
        for p, q in edges:
            graph[p].add(q)

        node_flag = defaultdict(int)
        cyclic = False
        invalid_dest = False
        
        def dfs(node):
            nonlocal cyclic, invalid_dest
            node_flag[node] = 1
            if not graph[node]:
                node_flag[node] = 2
                if node != destination:
                    invalid_dest = True
                return
            for neighbor in graph[node]:
                if node_flag[neighbor] == 0:
                    dfs(neighbor)
                elif node_flag[neighbor] == 1:
                    cyclic = True
            node_flag[node] = 2

        dfs(source)

        return not cyclic and not invalid_dest

# time O(V+E)
# space O(V+E)
# using graph and dfs and detecting cycles
'''
# 0 not visited
# 1 visiting
# 2 completed visited
'''
```


## 📄 [K]graph\[K]graph-dfs\329-longest-increasing-path-in-a-matrix.py

```py
class Solution:
    def longestIncreasingPath(self, matrix: List[List[int]]) -> int:
        rows, cols = len(matrix), len(matrix[0])
        cell_len = {}

        def dfs(r, c):
            total = 1
            new_total = total
            for next_r, next_c in [(r+1, c), (r-1, c), (r, c+1), (r, c-1)]:
                if next_r not in range(rows) or next_c not in range(cols) or matrix[r][c] >= matrix[next_r][next_c]:
                    continue
                if (next_r, next_c) in cell_len:
                    new_total = max(new_total, total + cell_len[(next_r, next_c)])
                else:
                    new_total = max(new_total, total + dfs(next_r, next_c))
            cell_len[(r, c)] = new_total
            return new_total

        for r in range(rows):
            for c in range(cols):
                dfs(r, c)
        return max(cell_len.values())
    
# time O(RC)
# space O(RC)
# using graph and dfs and memorizing res for long paths
```


## 📄 [K]graph\[K]graph-dijkstra\1514-path-with-maximum-probability.py

```py
from heapq import *
class Solution:
    def maxProbability(self, n: int, edges: List[List[int]], succProb: List[float], start_node: int, end_node: int) -> float:
        g = [[] for _ in range(n)]
        for i in range(len(edges)):
            p, q = edges[i]
            w = 1 / succProb[i]
            g[p].append((q, w))
            g[q].append((p, w))

        dist = [float('inf') for _ in range(n)]
        dist[start_node] = 1
        
        heap = [(1, start_node)]
        heapify(heap)

        visited = set()

        while heap:
            prev, node = heappop(heap)
            if node == end_node:
                return 1 / prev
            if node in visited:
                continue
            visited.add(node)
            for neighbor, w in g[node]:
                d = prev * w
                if d < dist[neighbor]:
                    heappush(heap, (d, neighbor))
                    dist[neighbor] = d
        return 0

# time O(V + E + ElogE)
# space O(V+E)
# using graph and dijkstra and shortest path
```


## 📄 [K]graph\[K]graph-dijkstra\2093-minimum-cost-to-reach-city-with-discounts.py

```py
from heapq import *
class Solution:
    def minimumCost(self, n: int, highways: List[List[int]], discounts: int) -> int:
        graph = [[] for _ in range(n)]
        for p, q, w in highways:
            graph[p].append((q, w))
            graph[q].append((p, w))
        dist = [[float('inf') for _ in range(discounts + 1)] for _ in range(n)]
        dist[0][discounts] = 0
        heap = [(0, discounts, 0)]
        heapify(heap)
        visited = set()
        while heap:
            prev, discount, node = heappop(heap)
            if node == n - 1:
                return prev
            if (node, discount) in visited:
                continue
            visited.add((node, discount))
            for neighbor, w in graph[node]:
                if neighbor == node:
                    continue
                d = prev + w
                if d < dist[neighbor][discount]:
                    heappush(heap, (d, discount, neighbor))
                    dist[neighbor][discount] = d
                if discount > 0:
                    d = prev + w // 2
                    new_discount = discount - 1
                    if d < dist[neighbor][new_discount]:
                        heappush(heap, (d, new_discount, neighbor))
                        dist[neighbor][new_discount] = d

        return - 1
    
# time O(V + E + Vk + Eklog(Ek))
# space O(V+E+Vk)
# using graph and dijkstra and shortest path
```


## 📄 [K]graph\[K]graph-dijkstra\505-the-maze-ii.py

```py
from heapq import *
class Solution:
    def shortestDistance(self, maze: List[List[int]], start: List[int], destination: List[int]) -> int:
        rows, cols = len(maze), len(maze[0])
        dist = [[float('inf') for _ in range(cols)] for _ in range(rows)]
        dist[start[0]][start[1]] = 0
        heap = [(0, start[0], start[1])]
        heapify(heap)
        visited = set()
        while heap:
            prev, r, c = heappop(heap)
            if (r, c) == (destination[0], destination[1]):
                return prev
            if (r, c) in visited:
                continue
            visited.add((r, c))
            for offset_r, offset_c in [(1, 0), (0, 1), (- 1, 0), (0, - 1)]:
                next_r, next_c = r, c
                w = 0
                while next_r + offset_r in range(rows) and next_c + offset_c in range(cols) and maze[next_r + offset_r][next_c + offset_c] != 1:
                    next_r += offset_r
                    next_c += offset_c
                    w += 1
                d = prev + w
                if d < dist[next_r][next_c]:
                    heappush(heap, (d, next_r, next_c))
                    dist[next_r][next_c] = d
        return - 1

# time O(V + ElogE), V is RC, E is 4RC
# space O(V+E)
# using graph and dijkstra and shortest path
```


## 📄 [K]graph\[K]graph-dijkstra\743-network-delay-time.py

```py
from collections import defaultdict
from heapq import *
class Solution:
    def networkDelayTime(self, times: List[List[int]], n: int, k: int) -> int:
        graph = defaultdict(list)
        for p, q, w in times:
            graph[p - 1].append((q - 1, w))
        start = k - 1
        dist = [float('inf') for _ in range(n)]
        dist[start] = 0
        heap = [(0, start)]
        heapify(heap)
        visited = set()
        while heap:
            prev, node = heappop(heap)
            if node in visited:
                continue
            visited.add(node)
            for neighbor, w in graph[node]:
                cur = prev + w
                if cur < dist[neighbor]:
                    heappush(heap, (cur, neighbor))
                    dist[neighbor] = cur
        return max(dist) if max(dist) != float('inf') else - 1

# time O(V + E + ElogE), ElogE -> Elog(V**2) -> ElogV
# space O(V+E)
# using graph and dijkstra and shortest path
```


## 📄 [K]graph\[K]graph-dijkstra\778-swim-in-rising-water.py

```py
from collections import defaultdict
from heapq import *
class Solution:
    def swimInWater(self, grid: List[List[int]]) -> int:
        rows, cols = len(grid), len(grid[0])
        node_dist = defaultdict(int)
        for r in range(rows):
            for c in range(cols):
                node_dist[(r, c)] = float('inf')
        node_dist[(0, 0)] = grid[0][0]
        heap = [(grid[0][0], 0, 0)]
        heapify(heap)
        visited = set()
        while heap:
            prev, r, c = heappop(heap)
            if (r, c) == (rows - 1, cols - 1):
                break
            if (r, c) in visited:
                continue
            visited.add((r, c))
            for next_r, next_c in [(r+1, c), (r-1, c), (r, c+1), (r, c-1)]:
                if next_r not in range(rows) or next_c not in range(cols):
                    continue
                d = max(prev, grid[next_r][next_c])
                if d < node_dist[(next_r, next_c)]:
                    heappush(heap, (d, next_r, next_c))
                    node_dist[(next_r, next_c)] = d

        return node_dist[(rows - 1, cols - 1)]

# time O(V + E + ElogE), V is RC, E is 4RC
# space O(V+E)
# using graph and dijkstra and shortest path
```


## 📄 [K]graph\[K]graph-floyd-warshall\1334-find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance.py

```py
class Solution:
    def findTheCity(self, n: int, edges: List[List[int]], distanceThreshold: int) -> int:
        dist = [[float('inf') for _ in range(n)] for _ in range(n)]
        for p, q, w in edges:
            dist[p][q] = w
            dist[q][p] = w
        for i in range(n):
            dist[i][i] = 0

        for mid in range(n):
            for start in range(n):
                for end in range(n):
                    if dist[start][mid] + dist[mid][end] < dist[start][end]:
                        dist[start][end] = dist[start][mid] + dist[mid][end]
        
        res = 0
        res_count = n
        for i in range(n):
            count = 0
            for j in range(n):
                if i == j:
                    continue
                if dist[i][j] <= distanceThreshold:
                    count += 1
            if count <= res_count:
                res_count = count
                res = i
        return res
    
# time O(V**3)
# space O(V**2)
# using graph and floyd warshall and shortest path
```


## 📄 [K]graph\[K]graph-hierholzer\332-reconstruct-itinerary.py

```py
from collections import defaultdict
class Solution:
    def findItinerary(self, tickets: List[List[str]]) -> List[str]:
        graph = defaultdict(list)
        for p, q in sorted(tickets, reverse=True):
            graph[p].append(q)

        stack = []
        def dfs(node):
            while graph[node]:
                neighbor = graph[node].pop()
                dfs(neighbor)
            stack.append(node)
        
        dfs("JFK")
        
        path = []
        while stack:
            path.append(stack.pop())
        return path

# time O(ElogE), due to sort
# space O(V + E)
# using graph and hierholzer and eulerian path
```


## 📄 [K]graph\[K]graph-hierholzer\753-cracking-the-safe.py

```py
from collections import defaultdict
class Solution:
    def crackSafe(self, n: int, k: int) -> str:
        if n == 1:
            res = [str(i) for i in range(k)]
            return ''.join(res)

        passwords = []
        def build(path):
            if len(path) == n:
                passwords.append(''.join(path))
                return
            for i in range(k):
                path.append(str(i))
                build(path)
                path.pop()
        build([])

        graph = defaultdict(list)
        for password in passwords:
            p = password[: - 1]
            q = password[1:]
            graph[p].append(q)

        stack = []
        def dfs(node):
            while graph[node]:
                neighbor = graph[node].pop()
                dfs(neighbor)
            stack.append(node)
        dfs('0' * (n - 1))
        
        res = ''
        while stack:
            if not res:
                res += stack.pop()
            else:
                res += stack.pop()[- 1]
        return res
    
# time O(k**n)
# space O(k**n)
# using graph and hierholzer and eulerian path
'''
1. build graph: if n == 3, then 010 can create node 01 and node 10 (and connect them)
'''
```


## 📄 [K]graph\[K]graph-kahn\1136-parallel-courses.py

```py
from collections import deque
class Solution:
    def minimumSemesters(self, n: int, relations: List[List[int]]) -> int:
        graph = [[] for _ in range(n)]
        indegrees = [0 for _ in range(n)]
        for p, q in relations:
            p -= 1
            q -= 1
            graph[p].append(q)
            indegrees[q] += 1
        
        queue = deque([])
        for i, indegree in enumerate(indegrees):
            if indegree == 0:
                queue.append((i, 1))

        res = []
        while queue:
            node, step = queue.popleft()
            res.append(node)
            if len(res) == n:
                return step
            for neighbor in graph[node]:
                indegrees[neighbor] -= 1
                if indegrees[neighbor] == 0:
                    queue.append((neighbor, step + 1))
            
        return - 1

# time O(V+E)
# space O(V+E)
# using graph and kahn and topological sort
```


## 📄 [K]graph\[K]graph-kahn\1203-sort-items-by-groups-respecting-dependencies.py

```py
from collections import deque
class Solution:
    def sortItems(self, n: int, m: int, group: List[int], beforeItems: List[List[int]]) -> List[int]:

        def topo(graph, indegrees):
            queue = deque([])
            for i, indegree in enumerate(indegrees):
                if indegree == 0:
                    queue.append(i)
            dag = []
            while queue:
                node = queue.popleft()
                dag.append(node)
                for neighbor in graph[node]:
                    indegrees[neighbor] -= 1
                    if indegrees[neighbor] == 0:
                        queue.append(neighbor)
            return dag

        group_id = m
        for i, g in enumerate(group):
            if g == - 1:
                group[i] = group_id
                group_id += 1
        
        group_graph = [[] for _ in range(group_id)]
        group_indegrees = [0 for _ in range(group_id)]
        item_graph = [[] for _ in range(n)]
        item_indegrees = [0 for _ in range(n)]

        for i in range(n):
            g = group[i]
            for before_item in beforeItems[i]:
                before_group = group[before_item]
                if before_group != g:
                    group_graph[before_group].append(g)
                    group_indegrees[g] += 1
                item_graph[before_item].append(i)
                item_indegrees[i] += 1
        
        group_dag = topo(group_graph, group_indegrees)
        if len(group_dag) != len(group_graph):
            return []
        item_dag = topo(item_graph, item_indegrees)
        if len(item_dag) != len(item_graph):
            return []
        
        group_items = [[] for _ in range(group_id)]
        for item in item_dag:
            g = group[item]
            group_items[g].append(item)
        res = []
        for g in group_dag:
            res.extend(group_items[g])
        return res
        
# time O(n**2 + E for groups + E for items)
# space O(n**2)
# using graph and kahn and topological sort

```


## 📄 [K]graph\[K]graph-kahn\2050-parallel-courses-iii.py

```py
from heapq import *
class Solution:
    def minimumTime(self, n: int, relations: List[List[int]], time: List[int]) -> int:
        graph = [[] for _ in range(n)]
        indegrees = [0 for _ in range(n)]
        for p, q in relations:
            p -= 1
            q -= 1
            graph[p].append(q)
            indegrees[q] += 1

        heap = []
        for i, indegree in enumerate(indegrees):
            if indegree == 0:
                heappush(heap, (time[i], i))
        
        while heap:
            prev, node = heappop(heap)
            for neighbor in graph[node]:
                indegrees[neighbor] -= 1
                if indegrees[neighbor] == 0:
                    heappush(heap, (prev + time[neighbor], neighbor))
        return prev

# time O(VlogV)
# space O(V+E)
# using graph and kahn and topological sort and heap

from collections import deque
class Solution:
    def minimumTime(self, n: int, relations: List[List[int]], time: List[int]) -> int:
        graph = [[] for _ in range(n)]
        indegrees = [0 for _ in range(n)]
        for p, q in relations:
            p -= 1
            q -= 1
            graph[p].append(q)
            indegrees[q] += 1

        costs = [0 for _ in range(n)]
        queue = deque([])
        for i, indegree in enumerate(indegrees):
            if indegree == 0:
                queue.append(i)
                costs[i] = time[i]
        
        while queue:
            node = queue.popleft()
            for neighbor in graph[node]:
                indegrees[neighbor] -= 1
                costs[neighbor] = max(costs[neighbor], costs[node] + time[neighbor])
                if indegrees[neighbor] == 0:
                    queue.append(neighbor)
                    
        return max(costs)
    
# time O(V+E)
# space O(V+E)
# using graph and kahn and topological sort and dp
```


## 📄 [K]graph\[K]graph-kahn\207-course-schedule.java

```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        HashMap<Integer, List<Integer>> graph = new HashMap<>();
        HashMap<Integer, Integer> indegrees = new HashMap<>();
        for (int i = 0; i < numCourses; i++) {
            graph.put(i, new ArrayList<>());
            indegrees.put(i, 0);
        }
        for (int[] prereq: prerequisites) {
            int q = prereq[0];
            int p = prereq[1];
            graph.get(p).add(q);
            indegrees.put(q, indegrees.get(q) + 1);
        }

        ArrayDeque<Integer> queue = new ArrayDeque<>();
        for (Integer node: indegrees.keySet()) {
            if (Objects.equals(indegrees.get(node), 0)) {
                queue.offer(node);
            }
        }
        ArrayList<Integer> res = new ArrayList<>();
        while (!queue.isEmpty()) {
            Integer node = queue.poll();
            res.add(node);
            for (Integer neighbor: graph.get(node)) {
                indegrees.put(neighbor, indegrees.get(neighbor) - 1);
                if (Objects.equals(indegrees.get(neighbor), 0)) {
                    queue.offer(neighbor);
                }
            }
        }
        return res.size() == numCourses;
    }
}

// time O(V+E)
// space O(V+E), due to building graph
// using graph and kahn and topological sort
```


## 📄 [K]graph\[K]graph-kahn\207-course-schedule.py

```py
from collections import deque
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        graph = [[] for _ in range(numCourses)]
        indegrees = [0 for _ in range(numCourses)]
        for q, p in prerequisites:
            graph[p].append(q)
            indegrees[q] += 1

        queue = deque([])
        for i, indegree in enumerate(indegrees):
            if indegree == 0:
                queue.append(i)

        res = []
        while queue:
            node = queue.popleft()
            res.append(node)
            for neighbor in graph[node]:
                indegrees[neighbor] -= 1
                if indegrees[neighbor] == 0:
                    queue.append(neighbor)

        return len(res) == numCourses
    
# time O(V+E)
# space O(V+E), due to building graph
# using graph and kahn and topological sort

class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        graph = [[] for _ in range(numCourses)]
        for q, p in prerequisites:
            graph[p].append(q)
        
        node_flag = [0 for _ in range(numCourses)]
        cyclic = False

        def dfs(node):
            nonlocal cyclic
            node_flag[node] = 1
            for neighbor in graph[node]:
                if node_flag[neighbor] == 0:
                    dfs(neighbor)
                elif node_flag[neighbor] == 1:
                    cyclic = True
            node_flag[node] = 2

        for node in range(numCourses):
            if node_flag[node] == 0:
                dfs(node)
                
        return not cyclic

# time O(V+E)
# space O(V+E)
# using graph and dfs and detecting cycles
'''
# 0 not visited
# 1 visiting
# 2 completed visited
'''
```


## 📄 [K]graph\[K]graph-kahn\210-course-schedule-ii.py

```py
from collections import deque
class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        graph = [[] for _ in range(numCourses)]
        indegrees = [0 for _ in range(numCourses)]
        for q, p in prerequisites:
            graph[p].append(q)
            indegrees[q] += 1

        queue = deque([])
        for i, indegree in enumerate(indegrees):
            if indegree == 0:
                queue.append(i)
        
        res = []
        while queue:
            node = queue.popleft()
            res.append(node)
            for neighbor in graph[node]:
                indegrees[neighbor] -= 1
                if indegrees[neighbor] == 0:
                    queue.append(neighbor)
                    
        return res if len(res) == numCourses else []

# time O(V+E)
# space O(V+E), due to building graph
# using graph and kahn and topological sort

class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        graph = [[] for _ in range(numCourses)]
        for q, p in prerequisites:
            graph[p].append(q)
        
        node_flag = [0 for _ in range(numCourses)]
        cyclic = False
        res = []

        def dfs(node):
            nonlocal cyclic
            node_flag[node] = 1
            for neighbor in graph[node]:
                if node_flag[neighbor] == 0:
                    dfs(neighbor)
                elif node_flag[neighbor] == 1:
                    cyclic = True
            node_flag[node] = 2
            res.append(node)

        for node in range(numCourses):
            if node_flag[node] == 0:
                dfs(node)
                
        return res[::- 1] if not cyclic else []
    
# time O(V+E)
# space O(V+E)
# using graph and dfs and detecting cycles
'''
# 0 not visited
# 1 visiting
# 2 completed visited
'''
```


## 📄 [K]graph\[K]graph-kahn\2115-find-all-possible-recipes-from-given-supplies.py

```py
from collections import defaultdict, deque
class Solution:
    def findAllRecipes(self, recipes: List[str], ingredients: List[List[str]], supplies: List[str]) -> List[str]:
        graph = defaultdict(list)
        indegrees = defaultdict(int)
        for i in range(len(recipes)):
            recipe = recipes[i]
            sources = ingredients[i]
            for s in sources:
                graph[s].append(recipe)
            indegrees[recipe] += len(sources)
            
        queue = deque([])
        for supply in supplies:
            queue.append(supply)
        
        res = []
        while queue:
            node = queue.popleft()
            if node in indegrees:
                res.append(node)
            for neighbor in graph[node]:
                indegrees[neighbor] -= 1
                if indegrees[neighbor] == 0:
                    queue.append(neighbor)
        return res

# time O(V+E)
# space O(V+E), due to building graph
# using graph and kahn and topological sort
```


## 📄 [K]graph\[K]graph-kahn\2192-all-ancestors-of-a-node-in-a-directed-acyclic-graph.py

```py
from collections import deque
class Solution:
    def getAncestors(self, n: int, edges: List[List[int]]) -> List[List[int]]:
        graph = [[] for _ in range(n)]
        indegrees = [0 for _ in range(n)]
        for p, q in edges:
            graph[p].append(q)
            indegrees[q] += 1
        queue = deque([])
        for i, indegree in enumerate(indegrees):
            if indegree == 0:
                queue.append(i)

        dag = []
        res = [set() for _ in range(n)]
        while queue:
            node = queue.popleft()
            for neighbor in graph[node]:
                indegrees[neighbor] -= 1
                if indegrees[neighbor] == 0:
                    queue.append(neighbor)
                res[neighbor].update(res[node])
                res[neighbor].add(node)

        return [sorted(list(ancestors)) for ancestors in res]

# time O(V + VE + V*VlogV)
# space O(V + E + V**2)
# using graph and kahn and topological sort and sort
```


## 📄 [K]graph\[K]graph-kahn\269-alien-dictionary.py

```py
from collections import deque
class Solution:
    def alienOrder(self, words: List[str]) -> str:
        graph = {}
        indegrees = {}
        for word in words:
            for c in word:
                graph[c] = set()
                indegrees[c] = 0

        for i in range(1, len(words)):
            w1 = words[i - 1]
            w2 = words[i]
            diff = False
            for j in range(min(len(w1), len(w2))):
                c1 = w1[j]
                c2 = w2[j]
                if c1 != c2:
                    if c2 not in graph[c1]:
                        graph[c1].add(c2)
                        indegrees[c2] += 1
                    diff = True
                    break
            if not diff and len(w1) > len(w2):
                return ''
        
        queue = deque([])
        for i, indegree in indegrees.items():
            if indegree == 0:
                queue.append(i)
        res = []
        while queue:
            node = queue.popleft()
            res.append(node)
            for neighbor in graph[node]:
                indegrees[neighbor] -= 1
                if indegrees[neighbor] == 0:
                    queue.append(neighbor)
        return ''.join(res) if len(res) == len(indegrees) else ''
    
# time O(nL)
# space O(nL), due to building graph
# using graph and kahn and topological sort
```


## 📄 [K]graph\[K]graph-kahn\310-minimum-height-trees.java

```java
class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {
        if (n == 1) {
            return new ArrayList<>(Arrays.asList(0));
        }
        HashMap<Integer, ArrayList<Integer>> graph = new HashMap<>();
        HashMap<Integer, Integer> indegrees = new HashMap<>();
        for (int i = 0; i < n; i++) {
            graph.put(i, new ArrayList<>());
            indegrees.put(i, 0);
        }
        for (int[] pq: edges) {
            int p = pq[0];
            int q = pq[1];
            graph.get(p).add(q);
            graph.get(q).add(p);
            indegrees.put(p, indegrees.get(p) + 1);
            indegrees.put(q, indegrees.get(q) + 1);
        }

        ArrayDeque<Integer> queue = new ArrayDeque<>();
        for (Integer p: indegrees.keySet()) {
            if (Objects.equals(indegrees.get(p), 1)) {
                queue.offer(p);
            }
        }
        List<Integer> res = new ArrayList<>();
        while (!queue.isEmpty()) {
            int levelCount = queue.size();
            res = new ArrayList<>();
            for (int i = 0; i < levelCount; i++) {
                Integer node = queue.poll();
                res.add(node);
                for (Integer neighbor: graph.get(node)) {
                    indegrees.put(neighbor, indegrees.get(neighbor) - 1);
                    if (Objects.equals(indegrees.get(neighbor), 1)) {
                        queue.offer(neighbor);
                    }
                }
            }
        }
        return res;
    }
}

// time O(V+E)
// space O(V+E), due to building graph
// using graph and kahn and topological sort
/*
1. we want the root node as center as possible
2. so start from removing all cur leaf nodes in each round
*/
```


## 📄 [K]graph\[K]graph-kahn\310-minimum-height-trees.py

```py
from collections import deque
class Solution:
    def findMinHeightTrees(self, n: int, edges: List[List[int]]) -> List[int]:
        if n == 1:
            return [0]
        graph = [[] for _ in range(n)]
        indegrees = [0 for _ in range(n)]
        for p, q in edges:
            graph[p].append(q)
            graph[q].append(p)
            indegrees[q] += 1
            indegrees[p] += 1

        queue = deque([])
        for i, indegree in enumerate(indegrees):
            if indegree == 1:
                queue.append(i)

        while queue:
            count = len(queue)
            level_nodes = []
            for _ in range(count):
                node = queue.popleft()
                level_nodes.append(node)
                for neighbor in graph[node]:
                    indegrees[neighbor] -= 1
                    if indegrees[neighbor] == 1:
                        queue.append(neighbor)
        return level_nodes
    
# time O(V+E)
# space O(V+E), due to building graph
# using graph and kahn and topological sort
'''
1. we want the root node as center as possible
2. so start from removing all cur leaf nodes in each round
'''
```


## 📄 [K]graph\[K]graph-kahn\802-find-eventual-safe-states.py

```py
from collections import deque
class Solution:
    def eventualSafeNodes(self, graph: List[List[int]]) -> List[int]:
        rev_g = [[] for _ in range(len(graph))]
        indegrees = [0 for _ in range(len(graph))]
        for node, neighbors in enumerate(graph):
            for neighbor in neighbors:
                rev_g[neighbor].append(node)
                indegrees[node] += 1

        queue = deque([])
        for i, indegree in enumerate(indegrees):
            if indegree == 0:
                queue.append(i)
        
        res = [False for _ in range(len(graph))]
        while queue:
            node = queue.popleft()
            res[node] = True
            for neighbor in rev_g[node]:
                indegrees[neighbor] -= 1
                if indegrees[neighbor] == 0:
                    queue.append(neighbor)
        return [i for i, flag in enumerate(res) if flag]

# time O(V+E)
# space O(V+E)
# using graph and kahn and topological sort
```


## 📄 [K]graph\[K]graph-kruskal\1135-connecting-cities-with-minimum-cost.py

```py
class UnionFind:
    def __init__(self, n):
        self.parent = [i for i in range(n)]
        self.rank = [0 for _ in range(n)]

    def find(self, p):
        while p != self.parent[p]:
            self.parent[p] = self.parent[self.parent[p]]
            p = self.parent[p]
        return p
    
    def union(self, p, q):
        root_p = self.find(p)
        root_q = self.find(q)
        if root_p == root_q:
            return
        if self.rank[root_p] > self.rank[root_q]:
            self.parent[root_q] = root_p
        elif self.rank[root_p] < self.rank[root_q]:
            self.parent[root_p] = root_q
        else:
            self.parent[root_p] = root_q
            self.rank[root_q] += 1
    
    def is_connected(self, p, q):
        return self.find(p) == self.find(q)

class Solution:
    def minimumCost(self, n: int, connections: List[List[int]]) -> int:
        connections.sort(key = lambda x: x[2])
        uf = UnionFind(n)
        mst = []
        res = 0
        for p, q, w in connections:
            p -= 1
            q -= 1
            if not uf.is_connected(p, q):
                uf.union(p, q)
                mst.append((p, q, w))
                res += w
        return res if len(mst) == n - 1 else - 1

# time O(ElogE)
# space O(E + V)
# using graph and kruskal and mst and union find
```


## 📄 [K]graph\[K]graph-kruskal\1168-optimize-water-distribution-in-a-village.py

```py
class UnionFind:
    def __init__(self, n):
        self.parent = [i for i in range(n)]
        self.rank = [0 for _ in range(n)]

    def find(self, p):
        while p != self.parent[p]:
            self.parent[p] = self.parent[self.parent[p]]
            p = self.parent[p]
        return p

    def union(self, p, q):
        root_p = self.find(p)
        root_q = self.find(q)
        if root_p == root_q:
            return
        if self.rank[root_p] > self.rank[root_q]:
            self.parent[root_q] = root_p
        elif self.rank[root_p] < self.rank[root_q]:
            self.parent[root_p] = root_q
        else:
            self.parent[root_p] = root_q
            self.rank[root_q] += 1

    def is_connected(self, p, q):
        return self.find(p) == self.find(q)

class Solution:
    def minCostToSupplyWater(self, n: int, wells: List[int], pipes: List[List[int]]) -> int:
        uf = UnionFind(n + 1)
        edges = []
        for i, w in enumerate(wells):
            edges.append((w, i, n))
        for p, q, w in pipes:
            edges.append((w, p - 1, q - 1))
        edges.sort()

        res = 0
        for w, p, q in edges:
            if not uf.is_connected(p, q):
                uf.union(p, q)
                res += w
        return res
    
# time O(ElogE)
# space O(V + E)
# using graph and kruskal and mst and union find
```


## 📄 [K]graph\[K]graph-kruskal\1489-find-critical-and-pseudo-critical-edges-in-minimum-spanning-tree.py

```py
class UnionFind:
    def __init__(self, n):
        self.parent = [i for i in range(n)]
        self.rank = [0 for _ in range(n)]
    
    def find(self, p):
        while p != self.parent[p]:
            self.parent[p] = self.parent[self.parent[p]]
            p = self.parent[p]
        return p
    
    def union(self, p, q):
        root_p = self.find(p)
        root_q = self.find(q)
        if root_p == root_q:
            return
        if self.rank[root_p] > self.rank[root_q]:
            self.parent[root_q] = root_p
        elif self.rank[root_p] < self.rank[root_q]:
            self.parent[root_p] = root_q
        else:
            self.parent[root_p] = root_q
            self.rank[root_q] += 1

    def is_connected(self, p, q):
        return self.find(p) == self.find(q)

class Solution:
    def findCriticalAndPseudoCriticalEdges(self, n: int, edges: List[List[int]]) -> List[List[int]]:
        sort_edges = []
        for i, (p, q, w) in enumerate(edges):
            sort_edges.append((w, p, q, i))
        sort_edges.sort()

        def mst(exclude=None, include=None):
            uf = UnionFind(n)
            res = []
            if include != None:
                p, q, w = edges[include]
                uf.union(p, q)
                res.append(w)
            for w, p, q, i in sort_edges:
                if i == exclude or i == include:
                    continue
                if not uf.is_connected(p, q):
                    uf.union(p, q)
                    res.append(w)
            return sum(res) if len(res) == n - 1 else float('inf')

        cost = mst()
        pseudo_criticals = set()
        for i in range(len(edges)):
            if cost == mst(include=i):
                pseudo_criticals.add(i)
        criticals = []
        for i in list(pseudo_criticals):
            if cost < mst(exclude=i):
                criticals.append(i)
                pseudo_criticals.remove(i)

        return [criticals, list(pseudo_criticals)]

# time O(E**2)
# space O(V + E)
# using graph and kruskal and mst and union find
```


## 📄 [K]graph\[K]graph-kruskal\1584-min-cost-to-connect-all-points.py

```py
class UnionFind:
    def __init__(self, n):
        self.parent = [i for i in range(n)]
        self.rank = [0 for _ in range(n)]

    def find(self, p):
        while p != self.parent[p]:
            self.parent[p] = self.parent[self.parent[p]]
            p = self.parent[p]
        return p
    
    def union(self, p, q):
        root_p = self.find(p)
        root_q = self.find(q)
        if root_p == root_q:
            return
        if self.rank[root_p] > self.rank[root_q]:
            self.parent[root_q] = root_p
        elif self.rank[root_p] < self.rank[root_q]:
            self.parent[root_p] = root_q
        else:
            self.parent[root_p] = root_q
            self.rank[root_q] += 1

    def is_connected(self, p, q):
        return self.find(p) == self.find(q)

class Solution:
    def minCostConnectPoints(self, points: List[List[int]]) -> int:
        edges = []
        for i in range(len(points)):
            for j in range(i + 1, len(points)):
                x1, y1 = points[i]
                x2, y2 = points[j]
                edges.append((abs(x1 - x2) + abs(y1 - y2), i, j))

        edges.sort()

        uf = UnionFind(len(points))
        res = 0
        for w, i, j in edges:
            if not uf.is_connected(i, j):
                uf.union(i, j)
                res += w
        return res
    
# time O(ElogE)
# space O(V + E)
# using graph and kruskal and mst and union find
```


## 📄 [K]graph\[K]graph-kruskal\1724-checking-existence-of-edge-length-limited-paths-ii.py

```py
class UnionFind:
    def __init__(self, n):
        self.parent = [i for i in range(n)]
        self.rank = [0 for _ in range(n)]

    def find(self, p):
        while p != self.parent[p]:
            self.parent[p] = self.parent[self.parent[p]]
            p = self.parent[p]
        return p

    def union(self, p, q):
        root_p = self.find(p)
        root_q = self.find(q)
        if root_p == root_q:
            return
        if self.rank[root_p] > self.rank[root_q]:
            self.parent[root_q] = root_p
        elif self.rank[root_p] < self.rank[root_q]:
            self.parent[root_p] = root_q
        else:
            self.parent[root_p] = root_q
            self.rank[root_q] += 1

    def is_connected(self, p, q):
        return self.find(p) == self.find(q)

from collections import defaultdict
class DistanceLimitedPathsExist:

    def __init__(self, n: int, edgeList: List[List[int]]):
        self.edges = sorted(edgeList, key = lambda x: x[2])
        self.limit_parent = defaultdict(list)
        self.uf = UnionFind(n)
        for u, v, w in self.edges:
            if w not in self.limit_parent:
                self.limit_parent[w] = self.uf.parent[:]
            if not self.uf.is_connected(u, v):
                self.uf.union(u, v)
        self.limit_parent[float('inf')] = self.uf.parent[:]
        self.limits = list(self.limit_parent.keys())

    def query(self, p: int, q: int, limit: int) -> bool:
        left, right, boundary = 0, len(self.limits) - 1, - 1
        while left <= right:
            m = (left + right) // 2
            if limit == self.limits[m]:
                boundary = m
                break
            elif limit > self.limits[m]:
                boundary = m + 1
                left = m + 2
            else:
                right = m - 1
        if boundary == - 1:
            return False
        self.uf.parent = self.limit_parent[self.limits[boundary]]
        return self.uf.is_connected(p, q)

# Your DistanceLimitedPathsExist object will be instantiated and called as such:
# obj = DistanceLimitedPathsExist(n, edgeList)
# param_1 = obj.query(p,q,limit)

# time O(ElogE + EV) for init, O(logE) for query()
# space O(EV) for init, O(1) for query()
# using graph and kruskal and mst and union find and binary search and hashmap
```


## 📄 [K]graph\[K]graph-matrix\1582-special-positions-in-a-binary-matrix.py

```py
class Solution:
    def numSpecial(self, mat: List[List[int]]) -> int:
        rows, cols = len(mat), len(mat[0])
        row = [0 for _ in range(rows)]
        col = [0 for _ in range(cols)]
        for r in range(rows):
            for c in range(cols):
                if mat[r][c] == 1:
                    row[r] += 1
                    col[c] += 1
        
        res = 0
        for r in range(rows):
            for c in range(cols):
                if mat[r][c] == 1 and row[r] == 1 and col[c] == 1:
                    res += 1
        return res
      
# time O(RC)
# space O(R+C)
# using graph and matrix
```


## 📄 [K]graph\[K]graph-matrix\348-design-tic-tac-toe.py

```py
class TicTacToe:

    def __init__(self, n: int):
        self.n = n
        self.row = [0 for _ in range(n)]
        self.col = [0 for _ in range(n)]
        self.diag = 0
        self.anti_diag = 0

    def move(self, row: int, col: int, player: int) -> int:
        weight = 1 if player == 1 else - 1
        self.row[row] += weight
        self.col[col] += weight
        if row == col:
            self.diag += weight
        if row + col == self.n - 1:
            self.anti_diag += weight
        if abs(self.row[row]) == self.n or abs(self.col[col]) == self.n or abs(self.diag) == self.n or abs(self.anti_diag) == self.n:
            return 1 if player == 1 else 2
        return 0

# Your TicTacToe object will be instantiated and called as such:
# obj = TicTacToe(n)
# param_1 = obj.move(row,col,player)

# time O(1)
# space O(n), due to lists
# using graph and matrix
```


## 📄 [K]graph\[K]graph-matrix\48-rotate-image.py

```py
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        rows, cols = len(matrix), len(matrix[0])

        for r in range(rows // 2):
            for c in range(cols):
                matrix[r][c], matrix[rows - 1 - r][c] = matrix[rows - 1 - r][c], matrix[r][c]
        
        for r in range(rows):
            for c in range(r):
                matrix[r][c], matrix[c][r] = matrix[c][r], matrix[r][c]

# time O(RC)
# space O(1)
# using graph and matrix
'''
1. flip by horizontal first, then flip by main diagonal
'''
```


## 📄 [K]graph\[K]graph-matrix\54-spiral-matrix.java

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        int rows = matrix.length;
        int cols = matrix[0].length;
        int d = 0;
        int r = 0;
        int c = 0;
        int[][] directions = new int[][]{{0, 1}, {1, 0}, {0, - 1}, {- 1, 0}};
        HashSet<Integer> visited = new HashSet<>();
        List<Integer> res = new ArrayList<>();
        while (res.size() < rows * cols) {
            res.add(matrix[r][c]);
            visited.add(r * cols + c);
            int nextR = r + directions[d][0];
            int nextC = c + directions[d][1];
            if (0 > nextR || nextR >= rows || 0 > nextC || nextC >= cols || visited.contains(nextR * cols + nextC)) {
                d = (d + 1) % directions.length;
                nextR = r + directions[d][0];
                nextC = c + directions[d][1];
            }
            r = nextR;
            c = nextC;
        }
        return res;
    }
}

// time O(RC)
// space O(RC)
// using graph and matrix and hashset
```


## 📄 [K]graph\[K]graph-matrix\54-spiral-matrix.py

```py
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        rows, cols = len(matrix), len(matrix[0])
        visited = set()
        directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]
        r, c, d = 0, 0, 0
        res = []
        while len(res) < rows * cols:
            res.append(matrix[r][c])
            visited.add((r, c))
            next_r, next_c = r + directions[d][0], c + directions[d][1]
            if next_r not in range(rows) or next_c not in range(cols) or (next_r, next_c) in visited:
                d += 1
                d %= len(directions)
                next_r, next_c = r + directions[d][0], c + directions[d][1]
            r, c = next_r, next_c
        return res
    
# time O(RC)
# space O(RC)
# using graph and matrix and hashset
```


## 📄 [K]graph\[K]graph-matrix\73-set-matrix-zeroes.py

```py
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        rows, cols = len(matrix), len(matrix[0])
        zero_in_first_row = False
        zero_in_first_col = False
        for r in range(rows):
            for c in range(cols):
                if matrix[r][c] == 0:
                    matrix[r][0] = 0
                    matrix[0][c] = 0
                    if r == 0:
                        zero_in_first_row = True
                    if c == 0:
                        zero_in_first_col = True
        for r in range(1, rows):
            for c in range(1, cols):
                if matrix[r][0] == 0 or matrix[0][c] == 0:
                    matrix[r][c] = 0
        if zero_in_first_row:
            for c in range(cols):
                matrix[0][c] = 0
        if zero_in_first_col:
            for r in range(rows):
                matrix[r][0] = 0
                
# time O(RC)
# space O(1)
# using graph and matrix
```


## 📄 [K]graph\[K]graph-tarjan\1192-critical-connections-in-a-network.py

```py
from collections import defaultdict
class Solution:
    def criticalConnections(self, n: int, connections: List[List[int]]) -> List[List[int]]:
        graph = defaultdict(list)
        for p, q in connections:
            graph[p].append(q)
            graph[q].append(p)
        V = n
        time = 0
        ids = [- 1 for _ in range(V)]
        low = [- 1 for _ in range(V)]
        on_stack = [False for _ in range(V)]
        stack = []
        used_edges = set()
        res = []

        def dfs(node):
            nonlocal time
            ids[node] = time
            low[node] = time
            time += 1
            on_stack[node] = True
            stack.append(node)

            for neighbor in graph[node]:
                if (node, neighbor) in used_edges or (neighbor, node) in used_edges:
                    continue
                used_edges.add((node, neighbor))
                used_edges.add((neighbor, node))

                if ids[neighbor] == - 1:
                    dfs(neighbor)
                    low[node] = min(low[node], low[neighbor])
                    if low[neighbor] > ids[node]:
                        res.append([node, neighbor])

                elif on_stack[neighbor]:
                    low[node] = min(low[node], ids[neighbor])

            if low[node] == ids[node]:
                component = []
                while stack:
                    stack_node = stack.pop()
                    on_stack[stack_node] = False
                    component.append(stack_node)
                    if stack_node == node:
                        break
    
        for i in range(V):
            if ids[i] == - 1:
                dfs(i)

        return res
    
# time O(V+E)
# space O(V+E)
# using graph and tarjan and scc
```


## 📄 [K]graph\[K]graph-union-find\1101-the-earliest-moment-when-everyone-become-friends.py

```py
class UnionFind:
    def __init__(self, n):
        self.parent = [i for i in range(n)]
        self.rank = [0 for _ in range(n)]
        self.count = n

    def find(self, p):
        while p != self.parent[p]:
            self.parent[p] = self.parent[self.parent[p]]
            p = self.parent[p]
        return p

    def union(self, p, q):
        root_p = self.find(p)
        root_q = self.find(q)
        if root_p == root_q:
            return
        if self.rank[root_p] > self.rank[root_q]:
            self.parent[root_q] = root_p
        elif self.rank[root_p] < self.rank[root_q]:
            self.parent[root_p] = root_q
        else:
            self.parent[root_p] = root_q
            self.rank[root_q] += 1
        self.count -= 1

    def get_count(self):
        return self.count

class Solution:
    def earliestAcq(self, logs: List[List[int]], n: int) -> int:
        uf = UnionFind(n)
        logs.sort()
        for t, p, q in logs:
            uf.union(p, q)
            if uf.get_count() == 1:
                return t
        return - 1
        
# time O(mlogm + n + m)
# space O(n), not count the built in sort's cost
# using graph and union find and sort
```


## 📄 [K]graph\[K]graph-union-find\1102-path-with-maximum-minimum-value.py

```py
class UnionFind:
    def __init__(self, n):
        self.parent = [i for i in range(n)]
        self.rank = [0 for _ in range(n)]

    def find(self, p):
        while p != self.parent[p]:
            self.parent[p] = self.parent[self.parent[p]]
            p = self.parent[p]
        return p
    
    def union(self, p, q):
        root_p = self.find(p)
        root_q = self.find(q)
        if root_p == root_q:
            return
        if self.rank[root_p] > self.rank[root_q]:
            self.parent[root_q] = root_p
        elif self.rank[root_p] < self.rank[root_q]:
            self.parent[root_p] = root_q
        else:
            self.parent[root_p] = root_q
            self.rank[root_q] += 1

    def is_connected(self, p, q):
        return self.find(p) == self.find(q)

class Solution:
    def maximumMinimumPath(self, grid: List[List[int]]) -> int:
        rows, cols = len(grid), len(grid[0])

        def get_id(r, c):
            return r * cols + c

        nodes = []
        for r in range(rows):
            for c in range(cols):
                nodes.append((- grid[r][c], get_id(r, c), r, c))
        nodes.sort()

        n = rows * cols
        uf = UnionFind(n)
        for neg_val, idx, r, c in nodes:
            for next_r, next_c in [(r+1, c), (r-1, c), (r, c+1), (r, c-1)]:
                if next_r not in range(rows) or next_c not in range(cols) or grid[next_r][next_c] < - neg_val:
                    continue
                uf.union(idx, get_id(next_r, next_c))
            if uf.is_connected(0, n - 1):
                return - neg_val
            
# time O(RC * logRC)
# space O(RC)
# using graph and union find and sort

from heapq import *
class Solution:
    def maximumMinimumPath(self, grid: List[List[int]]) -> int:
        rows, cols = len(grid), len(grid[0])
        heap = [(- grid[0][0], 0, 0)]
        heapify(heap)
        visited = set()
        visited.add((0, 0))
        res = float('inf')
        while heap:
            neg_val, r, c = heappop(heap)
            res = min(res, - neg_val)
            if (r, c) == (rows - 1, cols - 1):
                return res
            for next_r, next_c in [(r+1, c), (r-1, c), (r, c+1), (r, c-1)]:
                if next_r not in range(rows) or next_c not in range(cols) or (next_r, next_c) in visited:
                    continue
                heappush(heap, (- grid[next_r][next_c], next_r, next_c))
                visited.add((next_r, next_c))

# time O(RC * logRC)
# space O(RC)
# using graph and bfs with single source and heap
```


## 📄 [K]graph\[K]graph-union-find\2316-count-unreachable-pairs-of-nodes-in-an-undirected-graph.py

```py
class UnionFind:
    def __init__(self, n):
        self.parent = [i for i in range(n)]
        self.rank = [0 for _ in range(n)]
        self.weight = [1 for _ in range(n)]

    def find(self, p):
        while p != self.parent[p]:
            self.parent[p] = self.parent[self.parent[p]]
            p = self.parent[p]
        return p
    
    def union(self, p, q):
        root_p = self.find(p)
        root_q = self.find(q)
        if root_p == root_q:
            return
        if self.rank[root_p] > self.rank[root_q]:
            self.parent[root_q] = root_p
            self.weight[root_p] += self.weight[root_q]
            self.weight[root_q] = 0
        elif self.rank[root_p] < self.rank[root_q]:
            self.parent[root_p] = root_q
            self.weight[root_q] += self.weight[root_p]
            self.weight[root_p] = 0
        else:
            self.parent[root_p] = root_q
            self.rank[root_q] += 1
            self.weight[root_q] += self.weight[root_p]
            self.weight[root_p] = 0

    def get_weight(self, p):
        return self.weight[self.find(p)]

class Solution:
    def countPairs(self, n: int, edges: List[List[int]]) -> int:
        uf = UnionFind(n)
        for p, q in edges:
            uf.union(p, q)
        res = 0
        for i in range(n):
            res += n - uf.get_weight(i)
        return res // 2
    
# time O(V+E)
# space O(V)
# using graph and union find
```


## 📄 [K]graph\[K]graph-union-find\2421-number-of-good-paths.py

```py
class UnionFind:
    def __init__(self, n):
        self.parent = [i for i in range(n)]
        self.rank = [0 for _ in range(n)]

    def find(self, p):
        while p != self.parent[p]:
            self.parent[p] = self.parent[self.parent[p]]
            p = self.parent[p]
        return p

    def union(self, p, q):
        root_p = self.find(p)
        root_q = self.find(q)
        if root_p == root_q:
            return
        if self.rank[root_p] > self.rank[root_q]:
            self.parent[root_q] = root_p
        elif self.rank[root_p] < self.rank[root_q]:
            self.parent[root_p] = root_q
        else:
            self.parent[root_p] = root_q
            self.rank[root_q] += 1

from collections import defaultdict
class Solution:
    def numberOfGoodPaths(self, vals: List[int], edges: List[List[int]]) -> int:
        n = len(vals)
        uf = UnionFind(n)
        
        val_nodes = defaultdict(list)
        for i, val in enumerate(vals):
            val_nodes[val].append(i)
        val_edges = defaultdict(list)
        for p, q in edges:
            val_edges[vals[p]].append((p, q))
            val_edges[vals[q]].append((q, p))

        res = 0
        for val in sorted(set(vals)):
            for p, q in val_edges[val]:
                if vals[p] >= vals[q]:
                    uf.union(p, q)
            group_count = defaultdict(int)
            for node in val_nodes[val]:
                group = uf.find(node)
                group_count[group] += 1
                res += 1
            for group, count in group_count.items():
                res += (count * (count - 1)) // (2 * 1)
        return res
    
# time O(VlogV)
# space O(V+E)
# using graph and union find and sort and hashset
```


## 📄 [K]graph\[K]graph-union-find\305-number-of-islands-ii.py

```py
class UnionFind:
    def __init__(self, n):
        self.parent = [i for i in range(n)]
        self.rank = [0 for _ in range(n)]
    
    def find(self, p):
        while p != self.parent[p]:
            self.parent[p] = self.parent[self.parent[p]]
            p = self.parent[p]
        return p

    def union(self, p, q):
        root_p = self.find(p)
        root_q = self.find(q)
        if root_p == root_q:
            return
        if self.rank[root_p] > self.rank[root_q]:
            self.parent[root_q] = root_p
        elif self.rank[root_p] < self.rank[root_q]:
            self.parent[root_p] = root_q
        else:
            self.parent[root_p] = root_q
            self.rank[root_q] += 1

    def is_connected(self, p, q):
        return self.find(p) == self.find(q)

class Solution:
    def numIslands2(self, m: int, n: int, positions: List[List[int]]) -> List[int]:
        rows, cols = m, n
        n = m * n
        g = [[0 for _ in range(cols)] for _ in range(rows)]

        def get_idx(r, c):
            return r * cols + c

        uf = UnionFind(n)
        count = 0
        res = []
        for r, c in positions:
            if g[r][c] == 0:
                g[r][c] = 1
                count += 1
                for next_r, next_c in [(r+1, c), (r-1, c), (r, c+1), (r, c-1)]:
                    if next_r not in range(rows) or next_c not in range(cols) or g[next_r][next_c] == 0:
                        continue
                    if not uf.is_connected(get_idx(r, c), get_idx(next_r, next_c)):
                        uf.union(get_idx(r, c), get_idx(next_r, next_c))
                        count -= 1
            res.append(count)
        return res
    
# time O(RC + n)
# space O(RC), not counting output
# using graph and union find
```


## 📄 [K]graph\[K]graph-union-find\323-number-of-connected-components-in-an-undirected-graph.py

```py
class UnionFind:
    def __init__(self, n):
        self.parent = [i for i in range(n)]
        self.rank = [0 for _ in range(n)]
        self.count = n
    
    def find(self, p):
        while p != self.parent[p]:
            self.parent[p] = self.parent[self.parent[p]]
            p = self.parent[p]
        return p

    def union(self, p, q):
        root_p = self.find(p)
        root_q = self.find(q)
        if root_p == root_q:
            return
        if self.rank[root_p] > self.rank[root_q]:
            self.parent[root_q] = root_p
        elif self.rank[root_p] < self.rank[root_q]:
            self.parent[root_p] = root_q
        else:
            self.parent[root_p] = root_q
            self.rank[root_q] += 1
        self.count -= 1

    def get_count(self):
        return self.count

class Solution:
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        uf = UnionFind(n)
        for p, q in edges:
            uf.union(p, q)
        return uf.get_count()
    
# time O(V+E)
# space O(V)
# using graph and union find
```


## 📄 [K]graph\[K]graph-union-find\399-evaluate-division.py

```py
class UnionFind:
    def __init__(self, n):
        self.parent = [i for i in range(n)]
        self.rank = [0 for _ in range(n)]
        self.weight = [1.0 for _ in range(n)]

    def find(self, p):
        if p != self.parent[p]:
            original_parent = self.parent[p]
            self.parent[p] = self.find(self.parent[p])
            self.weight[p] = self.weight[p] * self.weight[original_parent]
            p = self.parent[p]
        return p
    
    def union(self, p, q, w):
        root_p = self.find(p)
        root_q = self.find(q)
        if root_p == root_q:
            return
        if self.rank[root_p] > self.rank[root_q]:
            self.parent[root_q] = root_p
            self.weight[root_q] = self.weight[p] * (1/w) / self.weight[q]
        elif self.rank[root_p] < self.rank[root_q]:
            self.parent[root_p] = root_q
            self.weight[root_p] = self.weight[q] * w / self.weight[p]
        else:
            self.parent[root_p] = root_q
            self.weight[root_p] = self.weight[q] * w / self.weight[p]
            self.rank[root_q] += 1
        
    def get_weight(self, p, q):
        root_p = self.find(p)
        root_q = self.find(q)
        if root_p == root_q:
            return self.weight[p] / self.weight[q]
        return - 1.0

class Solution:
    def calcEquation(self, equations: List[List[str]], values: List[float], queries: List[List[str]]) -> List[float]:
        s_idx = {}
        idx = 0
        for p, q in equations:
            if p not in s_idx:
                s_idx[p] = idx
                idx += 1
            if q not in s_idx:
                s_idx[q] = idx
                idx += 1
        uf = UnionFind(idx)
        for i in range(len(equations)):
            p, q = equations[i]
            w = values[i]
            uf.union(s_idx[p], s_idx[q], w)

        res = []
        for p, q in queries:
            if p not in s_idx or q not in s_idx:
                res.append(- 1.0)
            else:
                res.append(uf.get_weight(s_idx[p], s_idx[q]))
        
        return res
            
# time O((n+m)), n is the number of equations, m is the number of queries
# space O(n), due to union find
# using graph and union find
'''
1. if A/B = 2, we record weight of node A is 2, weight of node B is 1
2. in find method, 
   we use recursive version instead of iterative because this let leaf node updates final weight relative to root node correctly
3. in find method,
   we let node connect to grand parent node instead of parent node,
   so node weight become original node weight * parent node weight
4. in union method,
   we want p connect to q. 
   if q belong to high rank tree, then update weight for root_p (q * w / p)
   if p belong to high rank tree, we treat as we want q connect to p
'''
```


## 📄 [K]graph\[K]graph-union-find\547-number-of-provinces.py

```py
class UnionFind:
    def __init__(self, n):
        self.parent = [i for i in range(n)]
        self.rank = [0 for _ in range(n)]
        self.count = n

    def find(self, p):
        while p != self.parent[p]:
            self.parent[p] = self.parent[self.parent[p]]
            p = self.parent[p]
        return p

    def union(self, p, q):
        root_p = self.find(p)
        root_q = self.find(q)
        if root_p == root_q:
            return
        if self.rank[root_p] > self.rank[root_q]:
            self.parent[root_q] = root_p
        elif self.rank[root_p] < self.rank[root_q]:
            self.parent[root_p] = root_q
        else:
            self.parent[root_p] = root_q
            self.rank[root_q] += 1
        self.count -= 1

    def get_count(self):
        return self.count

class Solution:
    def findCircleNum(self, isConnected: List[List[int]]) -> int:
        n = len(isConnected)
        uf = UnionFind(n)
        for p in range(n):
            for q in range(n):
                if isConnected[p][q]:
                    uf.union(p, q)
        return uf.get_count()
    
# time O(n**2), using path compression and union by rank can reduce cost to near O(1)
# space O(n)
# using graph and union find
```


## 📄 [K]graph\[K]graph-union-find\721-accounts-merge.java

```java
class UnionFind {
    int[] parents;
    int[] rank;

    public UnionFind(Integer n) {
        parents = new int[n];
        rank = new int[n];
        for (int i = 0; i < n; i++) {
            parents[i] = i;
            rank[i] = 0;
        }
    }

    public Integer find(Integer p) {
        while (p != parents[p]) {
            parents[p] = parents[parents[p]];
            p = parents[p];
        }
        return p;
    }

    public void union(Integer p, Integer q) {
        Integer rootP = find(p);
        Integer rootQ = find(q);
        if (rootP == rootQ) {
            return;
        }
        if (rank[rootP] > rank[rootQ]) {
            parents[rootQ] = rootP;
        } else if (rank[rootP] < rank[rootQ]) {
            parents[rootP] = rootQ;
        } else {
            parents[rootP] = rootQ;
            rank[rootQ] += 1;
        }
    }
}

class Solution {
    public List<List<String>> accountsMerge(List<List<String>> accounts) {
        UnionFind uf = new UnionFind(accounts.size());
        HashMap<String, Integer> emailToId = new HashMap<>();
        for (int i = 0; i < accounts.size(); i++) {
            for (int j = 1; j < accounts.get(i).size(); j++) {
                String mail = accounts.get(i).get(j);
                if (emailToId.containsKey(mail)) {
                    uf.union(emailToId.get(mail), i);
                } else {
                    emailToId.put(mail, i);
                }
            }
        }

        HashMap<Integer, Set<String>> idToEmails = new HashMap<>();
        for (int i = 0; i < accounts.size(); i++) {
            for (int j = 1; j < accounts.get(i).size(); j++) {
                String mail = accounts.get(i).get(j);
                Integer id = uf.find(i);
                idToEmails.computeIfAbsent(id, k -> new HashSet<>()).add(mail);
            }
        }

        List<List<String>> res = new ArrayList<>();
        for (Map.Entry<Integer, Set<String>> entry: idToEmails.entrySet()) {
            Integer id = entry.getKey();
            Set<String> mails = entry.getValue();
            ArrayList<String> info = new ArrayList<>();
            info.addAll(mails);
            Collections.sort(info);
            info.add(0, accounts.get(id).get(0));
            res.add(info);
        }
        return res;
    }
}

// time O(mlogm + n + m), due to sort
// space O(m+n), due to hashmap, m is the number of mails, n is the number of accounts
// using graph and union find and sort
```


## 📄 [K]graph\[K]graph-union-find\721-accounts-merge.py

```py
class UnionFind:
    def __init__(self, n):
        self.parent = [i for i in range(n)]
        self.rank = [0 for _ in range(n)]

    def find(self, p):
        while p != self.parent[p]:
            self.parent[p] = self.parent[self.parent[p]]
            p = self.parent[p]
        return p
        
    def union(self, p, q):
        root_p = self.find(p)
        root_q = self.find(q)
        if root_p == root_q:
            return
        if self.rank[root_p] > self.rank[root_q]:
            self.parent[root_q] = root_p
        elif self.rank[root_p] < self.rank[root_q]:
            self.parent[root_p] = root_q
        else:
            self.parent[root_p] = root_q
            self.rank[root_q] += 1
        
from collections import defaultdict
class Solution:
    def accountsMerge(self, accounts: List[List[str]]) -> List[List[str]]:
        n = len(accounts)
        uf = UnionFind(n)
        email_id = {}
        for i, info in enumerate(accounts):
            for j in range(1, len(info)):
                if info[j] in email_id:
                    uf.union(i, email_id[info[j]])
                else:
                    email_id[info[j]] = i

        id_emails = defaultdict(set)
        for email, id in email_id.items():
            id_emails[uf.find(id)].add(email)
        
        res = []
        for id, emails in id_emails.items():
            info = [accounts[id][0]]
            info.extend(sorted(emails))
            res.append(info)
        return res
    
# time O(mlogm + n + m), due to sort
# space O(m+n), due to hashmap, m is the number of mails, n is the number of accounts
# using graph and union find and sort
```


## 📄 [K]graph\[K]graph-union-find\737-sentence-similarity-ii.py

```py
class UnionFind:
    def __init__(self, n):
        self.parent = [i for i in range(n)]
        self.rank = [0 for _ in range(n)]

    def find(self, p):
        while p != self.parent[p]:
            self.parent[p] = self.parent[self.parent[p]]
            p = self.parent[p]
        return p
    
    def union(self, p, q):
        root_p = self.find(p)
        root_q = self.find(q)
        if root_p == root_q:
            return
        if self.rank[root_p] > self.rank[root_q]:
            self.parent[root_q] = root_p
        elif self.rank[root_p] < self.rank[root_q]:
            self.parent[root_p] = root_q
        else:
            self.parent[root_p] = root_q
            self.rank[root_q] += 1

    def is_connected(self, p, q):
        return self.find(p) == self.find(q)

class Solution:
    def areSentencesSimilarTwo(self, sentence1: List[str], sentence2: List[str], similarPairs: List[List[str]]) -> bool:
        if len(sentence1) != len(sentence2):
            return False
        id = 0
        word_id = {}
        for w1, w2 in zip(sentence1, sentence2):
            if w1 not in word_id:
                word_id[w1] = id
                id += 1
            if w2 not in word_id:
                word_id[w2] = id
                id += 1
        for w1, w2 in similarPairs:
            if w1 not in word_id:
                word_id[w1] = id
                id += 1
            if w2 not in word_id:
                word_id[w2] = id
                id += 1
        uf = UnionFind(id)
        for w1, w2 in similarPairs:
            uf.union(word_id[w1], word_id[w2])
        for w1, w2 in zip(sentence1, sentence2):
            if not uf.is_connected(word_id[w1], word_id[w2]):
                return False
        return True
            
# time O(n + P)
# space O(n + P)
# using graph and union find and hashmap
```


## 📄 [L]bit-manipulation\[L]bit-manipulation\1356-sort-integers-by-the-number-of-1-bits.py

```py
class Solution:
    def sortByBits(self, arr: List[int]) -> List[int]:
        
        def get_count(n):
            res = 0
            for _ in range(32):
                if n & 1:
                    res += 1
                n >>= 1
            return res

        return sorted(arr, key = lambda x: (get_count(x), x))

# time O(nlogn)
# space O(1), not count built in sort's cost and output list
# using bit manipulation and shift
```


## 📄 [L]bit-manipulation\[L]bit-manipulation\136-single-number.java

```java
class Solution {
    public int singleNumber(int[] nums) {
        int res = 0;
        for (int num: nums) {
            res ^= num;
        }
        return res;
    }
}

// time O(n)
// space O(1)
// using bit manipulation and xor
```


## 📄 [L]bit-manipulation\[L]bit-manipulation\136-single-number.py

```py
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        res = 0
        for num in nums:
            res ^= num
        return res
    
# time O(n)
# space O(1)
# using bit manipulation and xor
```


## 📄 [L]bit-manipulation\[L]bit-manipulation\1542-find-longest-awesome-substring.py

```py
class Solution:
    def longestAwesome(self, s: str) -> int:
        mask_freq = {}
        mask_freq[0] = - 1
        mask = 0
        res = 0
        for i, c in enumerate(s):
            mask ^= 1 << (int(c))
            for j in range(10):
                if mask ^ (1 << j) in mask_freq:
                    res = max(res, i - mask_freq[mask ^ (1 << j)])
            if mask in mask_freq:
                res = max(res, i - mask_freq[mask])
            else:
                mask_freq[mask] = i
        return res
    
# time O(n)
# space O(min(n, 2**10))
# using bit manipulation and bitmasking and prefix sum and hashmap to validate the gap subarray
```


## 📄 [L]bit-manipulation\[L]bit-manipulation\190-reverse-bits.java

```java
public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
        int res = 0;
        for (int i = 0; i < 32; i++) {
            res = (res << 1) | (n & 1);
            n >>= 1;
        }
        return res;
    }
}

// time O(1)
// space O(1)
// using bit manipulation and shift
```


## 📄 [L]bit-manipulation\[L]bit-manipulation\190-reverse-bits.py

```py
class Solution:
    def reverseBits(self, n: int) -> int:
        res = 0
        for _ in range(32):
            res <<= 1
            res |= n & 1
            n >>= 1
        return res

# time O(1)
# space O(1)
# using bit manipulation and shift
```


## 📄 [L]bit-manipulation\[L]bit-manipulation\191-number-of-1-bits.java

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int res = 0;
        for (int i = 0; i < 32; i++) {
            res += n & 1;
            n >>= 1;
        }
        return res;
    }
}

// time O(1), due to 32 bit int
// space O(1)
// using bit manipulation and shift
```


## 📄 [L]bit-manipulation\[L]bit-manipulation\191-number-of-1-bits.py

```py
class Solution:
    def hammingWeight(self, n: int) -> int:
        res = 0
        for _ in range(32):
            if n & 1:
                res += 1
            n >>= 1
        return res
        
# time O(1), due to 32 bit int
# space O(1)
# using bit manipulation and shift
```


## 📄 [L]bit-manipulation\[L]bit-manipulation\1915-number-of-wonderful-substrings.py

```py
from collections import defaultdict
class Solution:
    def wonderfulSubstrings(self, word: str) -> int:
        mask_freq = defaultdict(int)
        mask_freq[0] = 1
        res = 0
        mask = 0
        for c in word:
            mask ^= 1 << (ord(c) - ord('a'))
            for i in range(10):
                res += mask_freq[mask ^ (1 << i)]
            res += mask_freq[mask]
            mask_freq[mask] += 1
        return res
        
# time O(n)
# space O(min(n, 2**10))
# using bit manipulation and bitmasking and prefix sum and hashmap to validate the gap subarray
```


## 📄 [L]bit-manipulation\[L]bit-manipulation\268-missing-number.java

```java
class Solution {
    public int missingNumber(int[] nums) {
        int res = 0;
        for (int i = 0; i < nums.length; i++) {
            res ^= i;
            res ^= nums[i];
        }
        res ^= nums.length;
        return res;
    }
}

// time O(n)
// space O(1)
// using bit manipulation and xor
```


## 📄 [L]bit-manipulation\[L]bit-manipulation\268-missing-number.py

```py
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        res = 0
        for i in range(0, len(nums) + 1):
            res ^= i
        for num in nums:
            res ^= num
        return res
    
# time O(n)
# space O(1)
# using bit manipulation and xor
```


## 📄 [L]bit-manipulation\[L]bit-manipulation\36-valid-sudoku.py

```py
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        rows, cols = len(board), len(board[0])
        
        def valid(start_r, end_r, start_c, end_c):
            val = 0
            for r in range(start_r, end_r + 1):
                for c in range(start_c, end_c + 1):
                    if board[r][c] == '.':
                        continue
                    if val & (1 << int(board[r][c])):
                        return False
                    val |= (1 << int(board[r][c]))
            return True
        
        for r in range(rows):
            if not valid(r, r, 0, cols - 1):
                return False
        for c in range(cols):
            if not valid(0, rows - 1, c, c):
                return False
        for r in range(0, rows, 3):
            for c in range(0, cols, 3):
                if not valid(r, r + 2, c, c + 2):
                    return False
        return True
    
# time O(1)
# space O(1)
# using bit manipulation and bitmasking
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\10-regular-expression-matching.py

```py
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        m, n = len(s), len(p)
        dp = [[False for _ in range(n + 1)] for _ in range(m + 1)]

        dp[0][0] = True
        for i in range(1, n + 1):
            if p[i - 1] == '*' and dp[0][i - 2]:
                dp[0][i] = True
        for j in range(1, m + 1):
            dp[j][0] = False
        
        for i in range(1, m + 1):
            for j in range(1, n + 1):
                if s[i - 1] == p[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1]
                elif p[j - 1] == '.':
                    dp[i][j] = dp[i - 1][j - 1]
                elif p[j - 1] == '*':
                    if p[j - 2] == '.':
                        dp[i][j] |= dp[i][j - 2]
                        dp[i][j] |= dp[i - 1][j - 2]
                        dp[i][j] |= dp[i - 1][j]
                    elif s[i - 1] == p[j - 2]:
                        dp[i][j] |= dp[i][j - 2]
                        dp[i][j] |= dp[i - 1][j - 2]
                        dp[i][j] |= dp[i - 1][j]
                    else:
                        dp[i][j] = dp[i][j - 2]
                else:
                    dp[i][j] = False

        return dp[m][n]
        
# time O(mn)
# space O(mn)
# using dynamic programming and double sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\1049-last-stone-weight-ii.py

```py
class Solution:
    def lastStoneWeightII(self, stones: List[int]) -> int:
        val = sum(stones) // 2
        dp = [0 for _ in range(val + 1)]

        for stone in stones:
            for total in range(val, stone - 1, - 1):
                dp[total] = max(dp[total], dp[total - stone] + stone)
        
        group_a = dp[val]
        group_b = sum(stones) - group_a
        return group_b - group_a

# time O(nV), V is half of sum of stones
# space O(V)
# using dynamic programming and knapsack (0-1 knapsack) 
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\1092-shortest-common-supersequence.py

```py
class Solution:
    def shortestCommonSupersequence(self, str1: str, str2: str) -> str:
        m, n = len(str1), len(str2)
        dp = [[0 for _ in range(n + 1)] for _ in range(m + 1)]
        char = [['' for _ in range(n + 1)] for _ in range(m + 1)]
        source = [[(- 1, - 1) for _ in range(n + 1)] for _ in range(m + 1)]
        for i in range(1, m + 1):
            dp[i][0] = i
            char[i][0] = str1[i - 1]
            source[i][0] = (i - 1, 0)
        for j in range(1, n + 1):
            dp[0][j] = j
            char[0][j] = str2[j - 1]
            source[0][j] = (0, j - 1)

        for i in range(1, m + 1):
            for j in range(1, n + 1):
                if str1[i - 1] == str2[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1] + 1
                    char[i][j] = str1[i - 1]
                    source[i][j] = (i - 1, j - 1)
                else:
                    if dp[i][j - 1] < dp[i - 1][j]:
                        dp[i][j] = dp[i][j - 1] + 1
                        char[i][j] = str2[j - 1]
                        source[i][j] = (i, j - 1)
                    else:
                        dp[i][j] = dp[i - 1][j] + 1
                        char[i][j] = str1[i - 1]
                        source[i][j] = (i - 1, j)
        
        res = ''
        i, j = m, n
        while (i, j) != (- 1, - 1):
            res = char[i][j] + res
            i, j = source[i][j]
        return res

# time O(mn)
# space O(mn)
# using dynamic programming and double sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\1105-filling-bookcase-shelves.py

```py
class Solution:
    def minHeightShelves(self, books: List[List[int]], shelfWidth: int) -> int:
        dp = [float('inf') for _ in range(len(books) + 1)]
        dp[0] = 0

        for i in range(1, len(books) + 1):
            cur_width, cur_height = 0, 0
            for j in range(i - 1, - 1, - 1):
                cur_width += books[j][0]
                cur_height = max(cur_height, books[j][1])
                if cur_width > shelfWidth:
                    break
                dp[i] = min(dp[i], cur_height + dp[j])
        
        return dp[len(books)]
    
# time O(n**2)
# space O(n)
# using dynamic programming and linear sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\1143-longest-common-subsequence.py

```py
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        m, n = len(text1), len(text2)
        dp = [[0 for _ in range(n + 1)] for _ in range(m + 1)]
        
        for i in range(1, m + 1):
            for j in range(1, n + 1):
                if text1[i - 1] == text2[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1] + 1
                else:
                    dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])
        
        return dp[m][n]

# time O(mn)
# space O(mn)
# using dynamic programming and double sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\115-distinct-subsequences.py

```py
class Solution:
    def numDistinct(self, s: str, t: str) -> int:
        m, n = len(s), len(t)
        dp = [[0 for _ in range(n + 1)] for _ in range(m + 1)]
        dp[0][0] = 1
        for i in range(1, m + 1):
            dp[i][0] = 1

        for i in range(1, m + 1):
            for j in range(1, n + 1):
                if s[i - 1] == t[j - 1]:
                    dp[i][j] = dp[i - 1][j] + dp[i - 1][j - 1]
                else:
                    dp[i][j] = dp[i - 1][j]

        return dp[m][n]

# time O(mn)
# space O(mn)
# using dynamic programming and double sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\123-best-time-to-buy-and-sell-stock-iii.py

```py
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        sell = [[0, float('-inf')] for _ in range(3)]

        for p in prices:
            first_buy = max(sell[0][1], - p)
            first_sell = max(sell[1][0], sell[0][1] + p)
            second_buy = max(sell[1][1], sell[1][0] - p)
            second_sell = max(sell[2][0], sell[1][1] + p)
            sell[0][1] = first_buy
            sell[1][0] = first_sell
            sell[1][1] = second_buy
            sell[2][0] = second_sell
        return max(sell[1][0], sell[2][0])
    
# time O(n)
# space O(1)
# using dynamic programming and linear sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\1278-palindrome-partitioning-iii.py

```py
class Solution:
    def palindromePartition(self, s: str, k: int) -> int:

        n = len(s)
        if n == k:
            return 0

        count = [[0 for _ in range(n)] for _ in range(n)]
        for length in range(2, n + 1):
            for start in range(n):
                end = start + length - 1
                if end >= n:
                    break
                if s[start] == s[end]:
                    count[start][end] = count[start + 1][end - 1] if start + 1 <= end - 1 else 0
                else:
                    count[start][end] = count[start + 1][end - 1] + 1 if start + 1 <= end - 1 else 1

        dp = [[float('inf') for _ in range(k + 1)] for _ in range(n)]
        for i in range(n):
            dp[i][1] = count[0][i]

        for end in range(n):
            for interval in range(2, k + 1):
                for cut in range(end, interval - 2, - 1):
                    dp[end][interval] = min(dp[end][interval], dp[cut - 1][interval - 1] + count[cut][end])

        return dp[n - 1][k]

# time O(n**2 + n**2 * k)
# space O(n**2 + nk)
# using dynamic programming and interval (start from one interval) and interval (start from short interval)
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\1335-minimum-difficulty-of-a-job-schedule.py

```py
class Solution:
    def minDifficulty(self, jobDifficulty: List[int], d: int) -> int:
        jobs = jobDifficulty
        n = len(jobs)
        if n < d:
            return - 1
        if n == d:
            return sum(jobs)

        dp = [[float('inf') for _ in range(d + 1)] for _ in range(n)]
        max_job = jobs[0]
        for i in range(n):
            if jobs[i] > max_job:
                max_job = jobs[i]
            dp[i][1] = max_job
        
        for end in range(n):
            for interval in range(2, d + 1):
                max_job = jobs[end]
                for cut in range(end, interval - 2, - 1):
                    max_job = max(max_job, jobs[cut])
                    dp[end][interval] = min(dp[end][interval], dp[cut - 1][interval - 1] + max_job)
        
        return dp[n - 1][d]
    
# time O(n**2 * k)
# space O(nk)
# using dynamic programming and interval (start from one interval)
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\139-word-break.java

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        HashSet<String> set = new HashSet<>(wordDict);
        boolean[] dp = new boolean[s.length() + 1];
        dp[0] = true;
        for (int start = 0; start < s.length(); start++) {
            for (int end = start; end < s.length(); end++) {
                if (set.contains(s.substring(start, end + 1))) {
                    dp[end + 1] |= dp[start];
                }
            }
        }
        return dp[s.length()];
    }
}

// time O(n**3), due to two nested lopp and slice string
// space O(n + m), due to dp list and hashset
// using dynamic programming and linear sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\139-word-break.py

```py
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        word_set = set(wordDict)
        dp = [False for _ in range(len(s) + 1)]
        dp[0] = True
        
        for i in range(1, len(s) + 1):
            for start_idx in range(i):
                if s[start_idx: i] in word_set:
                    dp[i] |= dp[start_idx]
                    
        return dp[len(s)]

# time O(n**3), due to two nested lopp and slice string
# space O(n + m), due to dp list and hashset
# using dynamic programming and linear sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\152-maximum-product-subarray.py

```py
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        min_p = nums[0]
        max_p = nums[0]
        res = nums[0]
        for i in range(1, len(nums)):
            min_p, max_p = min(nums[i], min_p * nums[i], max_p * nums[i]), max(nums[i], max_p * nums[i], min_p * nums[i])
            res = max(res, max_p)
        return res
    
# time O(n), due to traverse
# space O(1)
# using dynamic programming and linear sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\1547-minimum-cost-to-cut-a-stick.py

```py
class Solution:
    def minCost(self, n: int, cuts: List[int]) -> int:
        cuts = [0] + sorted(cuts) + [n]
        m = len(cuts)
        dp = [[float('inf') for _ in range(m)] for _ in range(m)]
        for i in range(m - 1):
            dp[i][i + 1] = 0
 
        for length in range(2, m):
            for start in range(m):
                end = start + length
                if end >= m:
                    break
                for cut in range(start + 1, end):
                    cost = cuts[end] - cuts[start]
                    dp[start][end] = min(dp[start][end], dp[start][cut] + cost + dp[cut][end])

        return dp[0][m - 1]

# time O(m**3)
# space O(m**2)
# using dynamic programming and interval (start from short interval)
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\1964-find-the-longest-valid-obstacle-course-at-each-position.py

```py
class Solution:
    def longestObstacleCourseAtEachPosition(self, obstacles: List[int]) -> List[int]:

        def find_first_larger(vals, num):
            left, right, boundary = 0, len(vals) - 1, - 1
            while left <= right:
                m = (left + right) // 2
                if num < vals[m]:
                    boundary = m
                    right = m - 1
                else:
                    left = m + 1
            return boundary

        o = obstacles
        res = [1 for _ in range(len(o))]
        dp = []
        for i, num in enumerate(o):
            if not dp or dp[- 1] <= num:
                dp.append(num)
                res[i] = len(dp)
            else:
                idx = find_first_larger(dp, num)
                dp[idx] = num
                res[i] = idx + 1
        return res

# time O(nlogn), due to binary search costs logn and traverse every num
# space O(n), due to dp list
# using dynamic programming and LIS and patience sort and greedy and binary search
'''
1. dp[i] means the smallest last num when subseq's length is i+1
2. this num should greedily find out the smallest one
3. when new num is greater or equal than last one means subsequence can grow
4. else have to find this num can help which length's subsequence improve
'''
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\198-house-robber.java

```java
class Solution {
    public int rob(int[] nums) {
        int n = nums.length;
        if (n == 1) {
            return nums[0];
        }
        if (n == 2) {
            return Math.max(nums[0], nums[1]);
        }
        int prevPrev = nums[0];
        int prev = Math.max(nums[0], nums[1]);
        for (int i = 2; i < n; i++) {
            int cur = Math.max(prevPrev + nums[i], prev);
            prevPrev = prev;
            prev = cur;
        }
        return prev;
    }
}

// time O(n), due to traverse
// space O(1)
// using dynamic programming and linear sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\198-house-robber.py

```py
class Solution:
    def rob(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return nums[0]
        if len(nums) == 2:
            return max(nums[0], nums[1])
        prev_prev = nums[0]
        prev = max(nums[0], nums[1])
        for i in range(2, len(nums)):
            cur = max(prev_prev + nums[i], prev)
            prev_prev, prev = prev, cur
        return cur
        
# time O(n), due to traverse
# space O(1)
# using dynamic programming and linear sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\213-house-robber-ii.py

```py
class Solution:
    def rob(self, nums: List[int]) -> int:
        
        def helper(left, right):
            n = right - left + 1
            if n == 1:
                return nums[left]
            if n == 2:
                return max(nums[left], nums[left + 1])
            prev_prev = nums[left]
            prev = max(nums[left], nums[left + 1])
            for i in range(left + 2, right + 1):
                cur = max(prev_prev + nums[i], prev)
                prev_prev, prev = prev, cur
            return cur

        if len(nums) == 1:
            return nums[0]
        return max(helper(0, len(nums) - 2), helper(1, len(nums) - 1))

# time O(n), due to traverse twice
# space O(1)
# using dynamic programming and linear sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\221-maximal-square.py

```py
class Solution:
    def maximalSquare(self, matrix: List[List[str]]) -> int:
        
        rows, cols = len(matrix), len(matrix[0])
        dp = [[0 for _ in range(cols)] for _ in range(rows)]

        res = 0
        for i in range(rows):
            for j in range(cols):
                if matrix[i][j] == "0":
                    continue
                if i == 0 or j == 0:
                    dp[i][j] = 1
                else:
                    dp[i][j] = min(dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]) + 1
                res = max(res, dp[i][j] ** 2)
        return res
    
# time O(nm), due to matrix' size
# space O(nm), due to list
# using dynamic programming and 2D
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\256-paint-house.py

```py
class Solution:
    def minCost(self, costs: List[List[int]]) -> int:
        red = 0
        blue = 0
        green = 0
        for r, b, g in costs:
            red, blue, green = min(blue + r, green + r), min(red + b, green + b), min(red + g, blue + g)
        return min(red, blue, green)
    
# time O(n)
# space O(1)
# using dynamic programming and linear sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\279-perfect-squares.py

```py
class Solution:
    def numSquares(self, n: int) -> int:
        nums = []
        for i in range(1, n + 1):
            if i ** 2 <= n:
                nums.append(i ** 2)
            else:
                break
        dp = [float('inf') for _ in range(n + 1)]
        dp[0] = 0

        for num in nums:
            for total in range(1, n + 1):
                if total >= num:
                    dp[total] = min(dp[total], dp[total - num] + 1)
        return dp[n]
    
# time O(n**0.5 * n)
# space O(n), due to dp table
# using dynamic programming and knapsack (complete knapsack) 
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\300-longest-increasing-subsequence.py

```py
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        dp = [1 for _ in range(len(nums))]
        for end in range(len(nums)):
            for start in range(end):
                if nums[start] < nums[end]:
                    dp[end] = max(dp[end], dp[start] + 1)
        return max(dp)

# time O(n**2), due to each num has run a loop to check the nums before it
# space O(n), due to dp list
# using dynamic programming and linear sequence
'''
1. dp[i] means the length of LIS which ends in i
'''

class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:

        def find_first_larger_or_equal(vals, num):
            left, right, boundary = 0, len(vals) - 1, - 1
            while left <= right:
                m = (left + right) // 2
                if num <= vals[m]:
                    boundary = m
                    right = m - 1
                else:
                    left = m + 1
            return boundary

        dp = []
        for i, num in enumerate(nums):
            if not dp or dp[- 1] < num:
                dp.append(num)
            else:
                idx = find_first_larger_or_equal(dp, num)
                dp[idx] = num
        return len(dp)

# time O(nlogn), due to binary search costs logn and traverse every num
# space O(n), due to dp list
# using dynamic programming and LIS and patience sort and greedy and binary search
'''
1. dp[i] means the smallest last num when subseq's length is i+1
2. this num should greedily find out the smallest one
3. when new num is greater than last one means subsequence can grow
4. else have to find this num can help which length's subsequence improve
'''
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\309-best-time-to-buy-and-sell-stock-with-cooldown.py

```py
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        not_hold = 0
        hold = float('-inf')
        cooldown = 0
        for p in prices:
            not_hold, hold, cooldown = max(not_hold, cooldown), max(hold, - p, not_hold - p), max(cooldown, hold + p)
        return max(not_hold, cooldown)

# time O(n)
# space O(1)
# using dynamic programming and linear sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\312-burst-balloons.py

```py
class Solution:
    def maxCoins(self, nums: List[int]) -> int:
        n = len(nums)
        dp = [[0 for _ in range(n)] for _ in range(n)]
        for i, num in enumerate(nums):
            cur = num
            if i - 1 >= 0:
                cur *= nums[i - 1]
            if i + 1 < n:
                cur *= nums[i + 1]
            dp[i][i] = cur
        
        for length in range(2, n + 1):
            for start in range(n):
                end = start + length - 1
                if end >= n:
                    break
                for cut in range(start, end + 1):
                    cur = nums[cut]
                    if start - 1 >= 0:
                        cur *= nums[start - 1]
                    if end + 1 < n:
                        cur *= nums[end + 1]
                    if cut - 1 >= start:
                        cur += dp[start][cut - 1]
                    if cut + 1 <= end:
                        cur += dp[cut + 1][end]
                    dp[start][end] = max(dp[start][end], cur)
        
        return dp[0][n - 1]
    
# time O(n**3), due to width and start pointer and balloon location's loops
# space O(n**2), due to dp table
# using dynamic programming and interval (start from short interval)
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\322-coin-change.java

```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] dp = new int[amount + 1];
        int max = Integer.MAX_VALUE;
        Arrays.fill(dp, max);
        dp[0] = 0;

        for (int i = 0; i < coins.length; i++) {
            for (int j = 1; j < amount + 1; j++) {
                if (coins[i] <= j) {
                    int cand = dp[j - coins[i]] == max ? max : dp[j - coins[i]] + 1;
                    dp[j] = Math.min(dp[j], cand);
                }
            }
        }
        return dp[amount] == max ? - 1 : dp[amount];
    }
}

// time O(m * n), m is the amount and n is the number of coins
// space O(m), due to the dp list's size
// using dynamic programming and knapsack (complete knapsack) 
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\322-coin-change.py

```py
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [float('inf') for _ in range(amount + 1)]
        dp[0] = 0

        for coin in coins:
            for total in range(1, amount + 1):
                if total >= coin:
                    dp[total] = min(dp[total], dp[total - coin] + 1)

        return dp[amount] if dp[amount] != float('inf') else - 1

# time O(m * n), m is the amount and n is the number of coins
# space O(m), due to the dp list's size
# using dynamic programming and knapsack (complete knapsack) 
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\354-russian-doll-envelopes.py

```py
class Solution:
    def maxEnvelopes(self, envelopes: List[List[int]]) -> int:

        def find_first_larger_or_equal(vals, num):
            left, right, boundary = 0, len(vals) - 1, - 1
            while left <= right:
                m = (left + right) // 2
                if num <= vals[m]:
                    boundary = m
                    right = m - 1
                else:
                    left = m + 1
            return boundary

        envelopes.sort(key = lambda x: (x[0], - x[1]))
        dp = []
        for w, h in envelopes:
            if not dp or dp[- 1] < h:
                dp.append(h)
            else:
                idx = find_first_larger_or_equal(dp, h)
                dp[idx] = h

        return len(dp)
    
# time O(nlogn)
# space O(n)
# using dynamic programming and LIS and patience sort and greedy and binary search and sort
'''
1. notice the condition of sorting
'''
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\368-largest-divisible-subset.py

```py
class Solution:
    def largestDivisibleSubset(self, nums: List[int]) -> List[int]:
        nums.sort()
        source = [- 1 for _ in range(len(nums))]
        length = [1 for _ in range(len(nums))]
        for i in range(len(nums)):
            for j in range(i - 1, - 1, - 1):
                if nums[i] % nums[j] == 0 and length[j] + 1 > length[i]:
                    length[i] = length[j] + 1
                    source[i] = j
        
        max_length = max(length)
        res = []
        for i, l in enumerate(length):
            if l == max_length:
                while len(res) < max_length:
                    res.append(nums[i])
                    i = source[i]
                break

        return res[:: - 1]
    
# time O(n**2), due to each num has run a loop to check the nums before it
# space O(n)
# using dynamic programming and linear sequence and sort
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\376-wiggle-subsequence.py

```py
class Solution:
    def wiggleMaxLength(self, nums: List[int]) -> int:
        last_small = 1
        last_large = 1
        for i in range(1, len(nums)):
            if nums[i - 1] < nums[i]:
                last_large = last_small + 1
            elif nums[i - 1] > nums[i]:
                last_small = last_large + 1
        return max(last_small, last_large)

# time O(n)
# space O(1)
# using dynamic programming and linear sequence
'''
1. if nums[i - 1] < nums[i], we can use seq with last_small and cur element to form new subseq
2. the last small subseq might use nums[i - 1] as last element, then add nums[i] to subseq is valid
3. the last small subseq might not use nums[i - 1] as last element, means its last element is smaller then nums[i - 1], then add nums[i] to subseq is also valid
'''
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\377-combination-sum-iv.py

```py
class Solution:
    def combinationSum4(self, nums: List[int], target: int) -> int:
        dp = [0 for _ in range(target + 1)]
        dp[0] = 1
        for total in range(1, target + 1):
            for num in nums:
                if total >= num:
                    dp[total] += dp[total - num]
        return dp[target]
        
# time O(m*n), m is the target and n is the number of nums
# space O(m), m is the target
# using dynamic programming and knapsack (permutation knapsack) 
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\410-split-array-largest-sum.py

```py
class Solution:
    def splitArray(self, nums: List[int], k: int) -> int:
        n = len(nums)
        prefix = [0 for _ in range(n + 1)]
        total = 0
        for i, num in enumerate(nums):
            total += num
            prefix[i + 1] = total
        
        dp = [[float('inf') for _ in range(k + 1)] for _ in range(n)]
        for end in range(n):
            dp[end][1] = prefix[end + 1] - prefix[0]

        for end in range(n):
            for interval in range(2, k + 1):
                for cut in range(end, interval - 2, - 1):
                    largest_sum = max(dp[cut - 1][interval - 1], prefix[end + 1] - prefix[cut])
                    dp[end][interval] = min(dp[end][interval], largest_sum)
        return dp[n - 1][k]

# time O(n**2 * k)
# space O(nk)
# using dynamic programming and interval (start from one interval)

class Solution:
    def splitArray(self, nums: List[int], k: int) -> int:

        def valid(bound):
            group = 1
            total = 0
            for num in nums:
                if num > bound:
                    return False
                if total + num > bound:
                    group += 1
                    total = num
                else:
                    total += num
            return group <= k

        left, right, boundary = 0, sum(nums), - 1
        while left <= right:
            m = (left + right) // 2
            if valid(m):
                boundary = m
                right = m - 1
            else:
                left = m + 1
        return boundary

# time O(nlogm), m is the total of nums
# space O(1)
# using binary search and search in sth’s range
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\416-partition-equal-subset-sum.java

```java
class Solution {
    public boolean canPartition(int[] nums) {
        int total = 0;
        for (int num: nums) {
            total += num;
        }
        if (total % 2 == 1) {
            return false;
        }
        int target = total / 2;
        boolean[] dp = new boolean[target + 1];
        dp[0] = true;
        for (int num: nums) {
            for (int t = target; t >= 0; t--) {
                if (t >= num) {
                    dp[t] |= dp[t - num];
                }
            }
        }
        return dp[target];
    }
}

// time O(nm), n is the number of nums
// space O(m), m is the sum of all elements in nums
// using dynamic programming and knapsack (0-1 knapsack) 
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\416-partition-equal-subset-sum.py

```py
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        total = sum(nums)
        if total % 2:
            return False
        target = total // 2

        dp = [False for _ in range(target + 1)]
        dp[0] = True
        for num in nums:
            for total in range(target, num - 1, - 1):
                dp[total] = dp[total] or dp[total - num]
        return dp[target]

# time O(nm), n is the number of nums
# space O(m), m is the sum of all elements in nums
# using dynamic programming and knapsack (0-1 knapsack) 
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\474-ones-and-zeroes.py

```py
class Solution:
    def findMaxForm(self, strs: List[str], m: int, n: int) -> int:
        dp = [[0 for _ in range(n + 1)] for _ in range(m + 1)]

        for s in strs:
            zero = s.count('0')
            one = s.count('1')
            for i in range(m, zero - 1, - 1):
                for j in range(n, one - 1, - 1):
                    dp[i][j] = max(dp[i][j], dp[i - zero][j - one] + 1)
        return dp[m][n]

# time O(n * (pq + L))
# space O(pq)
# using dynamic programming and knapsack (0-1 knapsack) 
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\487-max-consecutive-ones-ii.py

```py
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        res = 0
        flip = 0
        non_flip = 0
        for num in nums:
            if num == 1:
                flip += 1
                non_flip += 1
            else:
                flip = non_flip + 1
                non_flip = 0
            res = max(res, flip, non_flip)
        return res
    
# time O(n)
# space O(1)
# using dynamic programming and linear sequence

class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        res = 0
        left = 0
        flip = 0
        for right in range(len(nums)):
            if nums[right] != 1:
                flip += 1
            while flip > 1:
                if nums[left] == 0:
                    flip -= 1
                left += 1
            res = max(res, right - left + 1)
        return res

# time O(n)
# space O(1)
# using array and standard sliding window
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\494-target-sum.py

```py
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        if (sum(nums) + target) % 2:
            return 0
        val = (sum(nums) + target) // 2
        if val < 0:
            return 0
        dp = [0 for _ in range(val + 1)]
        dp[0] = 1

        for num in nums:
            for total in range(val, num - 1, - 1):
                dp[total] += dp[total - num]
        return dp[val]

# time O(nV)
# space O(V)
# using dynamic programming and knapsack (0-1 knapsack) 
'''
T = V - (sum - V)
(T + sum) // 2 = V
'''
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\516-longest-palindromic-subsequence.py

```py
class Solution:
    def longestPalindromeSubseq(self, s: str) -> int:
        n = len(s)
        dp = [[0 for _ in range(n)] for _ in range(n)]
        for i in range(n):
            dp[i][i] = 1

        for length in range(2, n + 1):
            for start in range(n):
                end = start + length - 1
                if end >= n:
                    break
                if s[start] == s[end]:
                    cur = 2
                    if start + 1 <= end - 1:
                        cur += dp[start + 1][end - 1]
                    dp[start][end] = cur
                else:
                    cur = 0
                    if start + 1 <= end - 1:
                        cur += max(dp[start][end - 1], dp[start + 1][end])
                    else:
                        cur += 1
                    dp[start][end] = cur
            
        return dp[0][n - 1]

# time O(n**2)
# space O(n**2)
# using dynamic programming and interval (start from short interval)
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\518-coin-change-ii.py

```py
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        dp = [0 for _ in range(amount + 1)]
        dp[0] = 1
        for coin in coins:
            for total in range(1, amount + 1):
                if total >= coin:
                    dp[total] += dp[total - coin]
        return dp[amount]
    
# time O(m*n), m is the amount and n is the number of coins
# space O(m), m is the amount
# using dynamic programming and knapsack (combination knapsack) 
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\55-jump-game.py

```py
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        far = 0
        for i, jump in enumerate(nums):
            if far < i:
                return False
            far = max(far, i + jump)
        return True

# time O(n)
# space O(1)
# using dynamic programming and linear sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\62-unique-paths.java

```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (i == 0 && j == 0) {
                    dp[i][j] = 1;
                } else if (i == 0) {
                    dp[i][j] = dp[i][j - 1];
                } else if (j == 0) {
                    dp[i][j] = dp[i - 1][j];
                } else {
                    dp[i][j] = dp[i][j - 1] + dp[i - 1][j];
                }
            }
        }
        return dp[m - 1][n - 1];
    }
}

// time O(nm), due to grids' size
// space O(nm), due to list
// using dynamic programming and 2D
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\62-unique-paths.py

```py
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        res = [[0 for _ in range(n)] for _ in range(m)]
        for i in range(m):
            res[i][0] = 1
        for i in range(n):
            res[0][i] = 1

        for i in range(1, m):
            for j in range(1, n):
                res[i][j] = res[i - 1][j] + res[i][j - 1]
                
        return res[m - 1][n - 1]
    
# time O(nm), due to grids' size
# space O(nm), due to list
# using dynamic programming and 2D
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\63-unique-paths-ii.py

```py
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        g = obstacleGrid
        rows, cols = len(g), len(g[0])
        dp = [[0 for _ in range(cols)] for _ in range(rows)]

        for i in range(rows):
            for j in range(cols):
                if g[i][j] == 1:
                    continue
                if i == 0 and j == 0:
                    dp[i][j] = 1
                elif i == 0:
                    dp[i][j] = dp[i][j - 1]
                elif j == 0:
                    dp[i][j] = dp[i - 1][j]
                else:
                    dp[i][j] = dp[i - 1][j] + dp[i][j - 1]

        return dp[rows-  1][cols - 1]

# time O(RC)
# space O(RC)
# using dynamic programming and 2D
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\64-minimum-path-sum.py

```py
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        rows, cols = len(grid), len(grid[0])
        dp = [[float('inf') for _ in range(cols)] for _ in range(rows)]

        for i in range(rows):
            for j in range(cols):
                if i == 0 and j == 0:
                    dp[i][j] = grid[i][j]
                elif i == 0:
                    dp[i][j] = dp[i][j - 1] + grid[i][j]
                elif j == 0:
                    dp[i][j] = dp[i - 1][j] + grid[i][j]
                else:
                    dp[i][j] = min(dp[i][j - 1], dp[i - 1][j]) + grid[i][j]
                    
        return dp[rows - 1][cols - 1]

# time O(RC)
# space O(RC)
# using dynamic programming and 2D
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\647-palindromic-substrings.py

```py
class Solution:
    def countSubstrings(self, s: str) -> int:
        n = len(s)
        dp = [[False for _ in range(n)] for _ in range(n)]
        res = 0
        for i in range(n):
            dp[i][i] = True
            res += 1
        
        for length in range(2, n + 1):
            for start in range(n):
                end = start + length - 1
                if end >= n:
                    break
                if s[start] == s[end]:
                    cur = True
                    if start + 1 <= end - 1:
                        cur = dp[start + 1][end - 1]
                    dp[start][end] = cur
                    if cur:
                        res += 1
        
        return res

# time O(n**2)
# space O(n**2)
# using dynamic programming and interval (start from short interval)
'''
1. notice that this solution is not the best choice for time complexity
'''

class Solution:
    def countSubstrings(self, s: str) -> int:
        n = len(s)
        res = 0

        def expand(left_center, right_center):
            nonlocal res
            while left_center >= 0 and right_center < n and s[left_center] == s[right_center]:
                res += 1
                left_center -= 1
                right_center += 1
        
        for i in range(n):
            expand(i, i)
            expand(i, i + 1)
        return res

# time O(n**2)
# space O(1)
# using array and two pointers opposite direction and expand type
'''
1. notice that this solution is not the best choice for time complexity
'''
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\688-knight-probability-in-chessboard.py

```py
class Solution:
    def knightProbability(self, n: int, k: int, row: int, column: int) -> float:
        dp = [[[0 for _ in range(k + 1)] for _ in range(n)] for _ in range(n)]
        dp[row][column][0] = 1

        for step in range(1, k + 1):
            for r in range(n):
                for c in range(n):
                    prob = 0
                    for offset_r, offset_c in [(2, 1), (1, 2), (-1, 2), (-2, 1), (-2, -1), (-1, -2), (1, -2), (2, -1)]:
                        if r + offset_r not in range(n) or c + offset_c not in range(n):
                            continue
                        prob += dp[r + offset_r][c + offset_c][step - 1]
                    prob /= 8
                    dp[r][c][step] = prob
                    
        res = 0
        for r in range(n):
            for c in range(n):
                res += dp[r][c][k]
        return res
    
# time O(RCK)
# space O(RCK)
# using dynamic programming and 2D
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\70-climbing-stairs.java

```java
class Solution {
    public int climbStairs(int n) {
        if (n == 1) {
            return 1;
        }
        if (n == 2) {
            return 2;
        }
        int prevPrev = 1;
        int prev = 2;
        for (int i = 3; i < n + 1; i++) {
            int cur = prevPrev + prev;
            int temp = prev;
            prev = cur;
            prevPrev = temp;
        }
        return prev;
    }
}

// time O(n)
// space O(1)
// using dynamic programming and linear sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\70-climbing-stairs.py

```py
class Solution:
    def climbStairs(self, n: int) -> int:
        if n == 1:
            return 1
        if n == 2:
            return 2
        two_step_before = 1
        one_step_before = 2
        for i in range(3, n + 1):
            cur = two_step_before + one_step_before
            two_step_before, one_step_before = one_step_before, cur
        return cur

# time O(n)
# space O(1)
# using dynamic programming and linear sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\72-edit-distance.py

```py
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        m, n = len(word1), len(word2)
        dp = [[float('inf') for _ in range(n + 1)] for _ in range(m + 1)]
        dp[0][0] = 0
        for i in range(1, m + 1):
            dp[i][0] = i
        for j in range(1, n + 1):
            dp[0][j] = j

        for i in range(1, m + 1):
            for j in range(1, n + 1):
                if word1[i - 1] == word2[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1]
                else:
                    dp[i][j] = min(dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1]) + 1
        
        return dp[m][n]
    
# time O(nm)
# space O(nm)
# using dynamic programming and double sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\91-decode-ways.py

```py
class Solution:
    def numDecodings(self, s: str) -> int:
        dp = [0 for _ in range(len(s) + 1)]
        if s[0] == '0':
            return 0
        dp[0] = 1
        dp[1] = 1
        for i in range(2, len(s) + 1):
            if s[i - 1] != '0':
                dp[i] += dp[i - 1]
            if 10 <= int(s[i - 2: i]) <= 26:
                dp[i] += dp[i - 2]

        return dp[len(s)]
    
# time O(n), n is the string's length
# space O(n)
# using dynamic programming and linear sequence

class Solution:
    def numDecodings(self, s: str) -> int:
        dp = [0 for _ in range(len(s) + 1)]
        if s[0] == '0':
            return 0
        dp[0] = 1
        dp[1] = 1
        for i in range(2, len(s) + 1):
            if s[i - 2] == '0':
                if s[i - 1] == '0':
                    return 0
                dp[i] = dp[i - 1]
            elif s[i - 2] == '1':
                if s[i - 1] == '0':
                    dp[i] = dp[i - 2]
                else:
                    dp[i] = dp[i - 1] + dp[i - 2]
            elif s[i - 2] == '2':
                if s[i - 1] == '0':
                    dp[i] = dp[i - 2]
                elif '1' <= s[i - 1] <= '6':
                    dp[i] = dp[i - 1] + dp[i - 2]
                else:
                    dp[i] = dp[i - 1]
            else:
                if s[i - 1] == '0':
                    return 0
                dp[i] = dp[i - 1]

        return dp[len(s)]

# time O(n), n is the string's length
# space O(n)
# using dynamic programming and linear sequence
```


## 📄 [M]dynamic-programming\[M]dynamic-programming\97-interleaving-string.py

```py
class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        m, n = len(s1), len(s2)
        if m + n != len(s3):
            return False
        dp = [[False for _ in range(n + 1)] for _ in range(m + 1)]
        dp[0][0] = True

        for i in range(1, m + 1):
            if s1[i - 1] == s3[i - 1]:
                dp[i][0] = True
            else:
                break
        
        for j in range(1, n + 1):
            if s2[j - 1] == s3[j - 1]:
                dp[0][j] = True
            else:
                break

        for i in range(1, m + 1):
            for j in range(1, n + 1):
                dp[i][j] = (s3[i + j - 1] == s1[i - 1] and dp[i - 1][j]) or (s3[i + j - 1] == s2[j - 1] and dp[i][j - 1])
        
        return dp[m][n]

# time O(mn)
# space O(mn)
# using dynamic programming and double sequence
```


## 📄 [N]greedy\[N]greedy\134-gas-station.java

```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int totalGas = 0;
        for (int g: gas) {
            totalGas += g;
        }
        int totalCost = 0;
        for (int c: cost) {
            totalCost += c;
        }
        if (totalGas < totalCost) {
            return - 1;
        }
        int res = 0;
        int cur = 0;
        for (int i = 0; i < gas.length; i++) {
            cur += gas[i];
            cur -= cost[i];
            if (cur < 0) {
                cur = 0;
                res = i + 1;
            }
        }
        return res;
    }
}

// time O(n)
// space O(1)
// using greedy
/*
1. check it is possible or not
2. traverse and rule out the impossible start stations
*/
```


## 📄 [N]greedy\[N]greedy\134-gas-station.py

```py
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        if sum(gas) < sum(cost):
            return - 1
        
        total = 0
        start = 0
        for i in range(len(gas)):
            total += gas[i]
            total -= cost[i]
            if total < 0:
                total = 0
                start = i + 1
        return start
    
# time O(n)
# space O(1)
# using greedy
'''
1. check it is possible or not
2. traverse and rule out the impossible start stations
'''
```


## 📄 [N]greedy\[N]greedy\135-candy.py

```py
class Solution:
    def candy(self, ratings: List[int]) -> int:
        n = len(ratings)
        res = [1 for _ in range(n)]

        for i in range(1, n):
            if ratings[i - 1] < ratings[i]:
                res[i] = max(res[i], res[i - 1] + 1)
        
        for i in range(n - 2, - 1, - 1):
            if ratings[i + 1] < ratings[i]:
                res[i] = max(res[i], res[i + 1] + 1)
        
        return sum(res)

# time O(n)
# space O(n)
# using greedy
'''
1. make sure to get more than left child if cur child have higher rating
2. make sure to get more than right child if cur child have higher rating
'''
```


## 📄 [N]greedy\[N]greedy\1567-maximum-length-of-subarray-with-positive-product.py

```py
class Solution:
    def getMaxLen(self, nums: List[int]) -> int:
        pos = 0
        neg = 0
        first_neg = None

        res = 0
        for i, num in enumerate(nums):
            if num > 0:
                pos += 1
            elif num < 0:
                neg += 1
                if first_neg == None:
                    first_neg = i
            else:
                pos = 0
                neg = 0
                first_neg = None

            if neg == 0:
                res = max(res, pos)
            elif neg % 2 == 0:
                res = max(res, pos + neg)
            else:
                res = max(res, i - first_neg)
        
        return res
    
# time O(n)
# space O(1)
# using greedy
```


## 📄 [N]greedy\[N]greedy\1864-minimum-number-of-swaps-to-make-the-binary-string-alternating.py

```py
from collections import defaultdict
import math
class Solution:
    def minSwaps(self, s: str) -> int:
        char_freq = defaultdict(int)
        for c in s:
            char_freq[c] += 1
        if abs(char_freq['0'] - char_freq['1']) > 1:
            return - 1
        
        one_first = 0
        zero_first = 0
        for i, c in enumerate(s):
            if i % 2 == 0:
                if c == '0':
                    one_first += 1
                else:
                    zero_first += 1
            else:
                if c == '0':
                    zero_first += 1
                else:
                    one_first += 1
                    
        if char_freq['0'] > char_freq['1']:
            return int(zero_first / 2)
        elif char_freq['0'] < char_freq['1']:
            return int(one_first / 2)
        else:
            return min(int(zero_first / 2), int(one_first / 2))
        
# time O(n)
# space O(1)
# using greedy and hashmap
'''
1. only two types of string's formation
'''
```


## 📄 [N]greedy\[N]greedy\2366-minimum-replacements-to-sort-the-array.py

```py
import math
class Solution:
    def minimumReplacement(self, nums: List[int]) -> int:
        
        res = 0
        prev = nums[- 1]
        for i in range(len(nums) - 2, - 1, - 1):
            if nums[i] > prev:
                count = math.ceil(nums[i] / prev)
                res += count - 1
                prev = math.floor(nums[i] / count)
            else:
                prev = nums[i]
        return res
      
# time O(n)
# space O(1)
# using greedy
```


## 📄 [N]greedy\[N]greedy\277-find-the-celebrity.py

```py
# The knows API is already defined for you.
# return a bool, whether a knows b
# def knows(a: int, b: int) -> bool:

class Solution:
    def findCelebrity(self, n: int) -> int:
        cand = 0
        for i in range(1, n):
            if knows(cand, i):
                cand = i
        for i in range(n):
            if i == cand:
                continue
            if not knows(i, cand) or knows(cand, i):
                return - 1
        return cand
        
# time O(n), due to traverse twice
# space O(1)
# using greedy
```


## 📄 [N]greedy\[N]greedy\2870-minimum-number-of-operations-to-make-array-empty.py

```py
from collections import defaultdict
import math
class Solution:
    def minOperations(self, nums: List[int]) -> int:
        num_freq = defaultdict(int)
        for num in nums:
            num_freq[num] += 1
        
        res = 0
        for num, freq in num_freq.items():
            if freq == 1:
                return - 1
            count = math.ceil(freq / 3)
            res += count
        return res

# time O(n)
# space O(n)
# using greedy and hashmap
```


## 📄 [N]greedy\[N]greedy\406-queue-reconstruction-by-height.py

```py
class Solution:
    def reconstructQueue(self, people: List[List[int]]) -> List[List[int]]:
        people.sort(key = lambda x: (- x[0], x[1]))
        res = []
        for p in people:
            res.insert(p[1], p)
        return res
        
# time O(n**2)
# space O(n)
# using greedy and sort
'''
1. sort
2. reconstruct by inserting
'''
```


## 📄 [N]greedy\[N]greedy\45-jump-game-ii.py

```py
class Solution:
    def jump(self, nums: List[int]) -> int:
        res = 0
        cur = 0
        reach = 0
        for i, num in enumerate(nums):
            reach = max(reach, i + num)
            if i == len(nums) - 1:
                return res
            if i == cur:
                res += 1
                cur = reach
        return res
                
# time O(n)
# space O(1)
# using greedy
```


## 📄 [N]greedy\[N]greedy\53-maximum-subarray.java

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int res = Integer.MIN_VALUE;
        int total = 0;
        for (int num: nums) {
            total += num;
            res = Math.max(res, total);
            if (total < 0) {
                total = 0;
            }
        }
        return res;
    }
}

// time O(n)
// space O(1)
// using greedy
```


## 📄 [N]greedy\[N]greedy\53-maximum-subarray.py

```py
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        res = float('-inf')
        total = 0
        for num in nums:
            total += num
            res = max(res, total)
            if total < 0:
                total = 0
        return res
        
# time O(n)
# space O(1)
# using greedy
```


## 📄 [N]greedy\[N]greedy\621-task-scheduler.java

```java
class Solution {
    public int leastInterval(char[] tasks, int n) {
        HashMap<Character, Integer> charToFreq = new HashMap<>();
        for (int i = 0; i < tasks.length; i++) {
            charToFreq.compute(tasks[i], (k, v) -> v == null ? 1 : v + 1);
        }
        int maxFreq = Collections.max(charToFreq.values());
        int maxFreqCount = 0;
        for (Character c: charToFreq.keySet()) {
            if (Objects.equals(charToFreq.get(c), maxFreq)) {
                maxFreqCount += 1;
            }
        }
        return Math.max(tasks.length, (maxFreq - 1) * (n + 1) + maxFreqCount);
    }
}

// time O(n)
// space O(1), due to task's category
// using greedy and hashmap
```


## 📄 [N]greedy\[N]greedy\621-task-scheduler.py

```py
from collections import defaultdict
class Solution:
    def leastInterval(self, tasks: List[str], n: int) -> int:
        task_freq = defaultdict(int)
        for t in tasks:
            task_freq[t] += 1
        max_freq = max(task_freq.values())
        tasks_with_max_freq = []
        for t, f in task_freq.items():
            if f == max_freq:
                tasks_with_max_freq.append(t)
        
        h = max_freq - 1
        w = n + 1
        res = h * w + len(tasks_with_max_freq)
        return res if res > len(tasks) else len(tasks)

# time O(n)
# space O(1), due to task's category
# using greedy and hashmap
```


## 📄 [N]greedy\[N]greedy\659-split-array-into-consecutive-subsequences.py

```py
from collections import defaultdict
class Solution:
    def isPossible(self, nums: List[int]) -> bool:
        num_freq = defaultdict(int)
        for num in nums:
            num_freq[num] += 1
        tail_freq = defaultdict(int)
        for num in nums:
            if num_freq[num] == 0:
                continue
            num_freq[num] -= 1
            if tail_freq[num - 1] > 0:
                tail_freq[num - 1] -= 1
                tail_freq[num] += 1
            elif num_freq[num + 1] and num_freq[num + 2]:
                num_freq[num + 1] -= 1
                num_freq[num + 2] -= 1
                tail_freq[num + 2] += 1
            else:
                return False
        return True
        
# time O(n)
# space O(n)
# using greedy and hashmap
```


## 📄 [N]greedy\[N]greedy\665-non-decreasing-array.py

```py
class Solution:
    def checkPossibility(self, nums: List[int]) -> bool:
        modify = False
        for i, num in enumerate(nums):
            if i + 1 < len(nums) and nums[i] > nums[i + 1]:
                if modify:
                    return False
                modify = True
                large, small = nums[i], nums[i + 1]
                if i - 1 < 0 or nums[i - 1] <= small:
                    nums[i] = small
                else:
                    nums[i + 1] = large
        return True

# time O(n)
# space O(1)
# using greedy
'''
1. [5, 8, 3, 9], [1, 3, 2, 2]
2. sometimes change to larger one, sometimes change to smaller one
'''
```


## 📄 [N]greedy\[N]greedy\763-partition-labels.py

```py
from collections import defaultdict
class Solution:
    def partitionLabels(self, s: str) -> List[int]:
        char_lastidx = defaultdict(int)
        for i, c in enumerate(s):
            char_lastidx[c] = i
        
        left = 0
        right = 0
        res = []
        for i in range(len(s)):
            right = max(right, char_lastidx[s[i]])
            if i == right:
                res.append(right - left + 1)
                left = i + 1
                right = i + 1
        return res
                
# time O(n), due to traverse
# space O(1), due to hashmap stores only english letters
# using greedy and hashmap
'''
1. record the last appear idx
'''
```


## 📄 [N]greedy\[N]greedy\926-flip-string-to-monotone-increasing.py

```py
from collections import defaultdict
class Solution:
    def minFlipsMonoIncr(self, s: str) -> int:
        char_freq = defaultdict(int)
        for c in s:
            char_freq[c] += 1
        
        res = min(len(s) - char_freq['0'], len(s) - char_freq['1'])
        curchar_freq = defaultdict(int)
        for c in s:
            curchar_freq[c] += 1
            res = min(res, curchar_freq['1'] + char_freq['0'] - curchar_freq['0'])
        return res
        
# time O(n)
# space O(1)
# using greedy and hashmap
```


## 📄 [O]math\[O]math\171-excel-sheet-column-number.py

```py
class Solution:
    def titleToNumber(self, columnTitle: str) -> int:
        res = 0
        for c in columnTitle:
            res = res * 26 + ord(c) - ord('A') + 1
        return res
        
# time O(n), due to traverse
# space O(1)
# using math
```


## 📄 [O]math\[O]math\204-count-primes.py

```py
class Solution:
    def countPrimes(self, n: int) -> int:
        if n <= 1:
            return 0
        primes = [True for _ in range(n)]
        primes[0] = False
        primes[1] = False
        for p in range(2, int(n ** 0.5) + 1):
            if primes[p]:
                for mul_p in range(p ** 2, n, p):
                    primes[mul_p] = False
        return sum(primes)
    
# time O(nloglogn)
# space O(n)
# using math and sieve of eratosthenes
```


## 📄 [O]math\[O]math\258-add-digits.py

```py
class Solution:
    def addDigits(self, num: int) -> int:
        return (num - 1) % 9 + 1 if num else 0

# time O(1)
# space O(1)
# using math
```


## 📄 [O]math\[O]math\263-ugly-number.py

```py
class Solution:
    def isUgly(self, n: int) -> bool:
        if n <= 0:
            return False
        if n == 1:
            return True
        while n > 1:
            if n % 2 == 0:
                n //= 2
            elif n % 3 == 0:
                n //= 3
            elif n % 5 == 0:
                n //= 5
            else:
                return False
        return True
    
# time O(logn)
# space O(1)
# using math
```


## 📄 [O]math\[O]math\338-counting-bits.java

```java
class Solution {
    public int[] countBits(int n) {
        int[] res = new int[n + 1];
        for (int i = 0; i < n + 1; i++) {
            if (i % 2 == 1) {
                res[i] = res[i / 2] + 1;
            } else {
                res[i] = res[i / 2];
            }
        }
        return res;
    }
}

// time O(n)
// space O(n)
// using math
```


## 📄 [O]math\[O]math\338-counting-bits.py

```py
class Solution:
    def countBits(self, n: int) -> List[int]:
        res = [0 for _ in range(n + 1)]
        for i in range(n + 1):
            if i % 2 == 0:
                res[i] = res[i // 2]
            else:
                res[i] = res[i // 2] + 1
        return res
    
# time O(n)
# space O(n)
# using math

```


## 📄 [O]math\[O]math\391-perfect-rectangle.py

```py
from collections import defaultdict
class Solution:
    def isRectangleCover(self, rectangles: List[List[int]]) -> bool:
        point_freq = defaultdict(int)
        area = 0
        for x, y, a, b in rectangles:
            point_freq[(x, y)] += 1
            point_freq[(a, b)] += 1
            point_freq[(a, y)] += 1
            point_freq[(x, b)] += 1
            area += (a - x) * (b - y)

        corners = []
        for p, f in point_freq.items():
            if f == 1:
                corners.append(p)
            elif f == 2:
                continue
            elif f == 4:
                continue
            else:
                return False
        if len(corners) != 4:
            return False
        
        x, y, a, b = float('inf'), float('inf'), float('-inf'), float('-inf')
        for p, q in corners:
            x = min(x, p)
            y = min(y, q)
            a = max(a, p)
            b = max(b, q)
        if (a - x) * (b - y) != area:
            return False
        return True
    
# time O(n)
# space O(n)
# using math and hashmap
```


## 📄 [O]math\[O]math\415-add-strings.py

```py
class Solution:
    def addStrings(self, num1: str, num2: str) -> str:
        res = ''
        carry = 0
        i = len(num1) - 1
        j = len(num2) - 1
        while carry or i >= 0 or j >= 0:
            if i >= 0:
                carry += ord(num1[i]) - ord('0')
                i -= 1
            if j >= 0:
                carry += ord(num2[j]) - ord('0')
                j -= 1
            carry, remainder = divmod(carry, 10)
            res = chr(remainder + ord('0')) + res
        return res
    
# time O(max(m, n))
# space O(max(m, n))
# using math
```


## 📄 [O]math\[O]math\470-implement-rand10-using-rand7.py

```py
# The rand7() API is already defined for you.
# def rand7():
# @return a random integer in the range 1 to 7

class Solution:
    def rand10(self):
        """
        :rtype: int
        """
        
        while True:
            num = (rand7() - 1) * 7 + rand7()
            if num <= 40:
                return num % 10 + 1
        
# time O(1) or O(inf)
# space O(1)
# using math and rejection sampling
'''
1. (rand7() - 1) * 7, generate 0,7,14,21,28,35,42
2. after + rand7(), will have random num between 1 - 49 with equal probability
3. then use rejection sampling, if num not in desired range then re-sample it
4. if num in desired range, and inside range every num has same probability, then choose it
'''
```


## 📄 [O]math\[O]math\50-powx-n.py

```py
class Solution:
    def myPow(self, x: float, n: int) -> float:
        
        def helper(x, n):
            if n < 0:
                return 1 / helper(x, - n)
            if n == 0:
                return 1.0
            if n == 1:
                return x
            half = helper(x, n // 2)
            if n % 2 == 1:
                return x * half * half
            return half * half
        
        return helper(x, n)

# time O(logn), each time divide to half
# space O(logn), due to recursion stack
# using math and exponentiation by squaring
```


## 📄 [O]math\[O]math\67-add-binary.java

```java
class Solution {
    public String addBinary(String a, String b) {
        int i = a.length() - 1;
        int j = b.length() - 1;
        int carry = 0;
        StringBuffer s = new StringBuffer();
        while (carry > 0 || i >= 0 || j >= 0) {
            if (i >= 0) {
                if (a.charAt(i) == '1') {
                    carry += 1;
                }
                i -= 1;
            }
            if (j >= 0) {
                if (b.charAt(j) == '1') {
                    carry += 1;
                }
                j -= 1;
            }
            int quo = carry / 2;
            int rem = carry % 2;
            if (rem == 1) {
                s.append('1');
            } else {
                s.append('0');
            }
            carry = quo;
        }
        return s.reverse().toString();
    }
}

// time O(max(m, n))
// space O(max(m, n))
// using math
```


## 📄 [O]math\[O]math\67-add-binary.py

```py
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        res = ''
        carry = 0
        i = len(a) - 1
        j = len(b) - 1
        while carry or i >= 0 or j >= 0:
            if i >= 0:
                if a[i] == '1':
                    carry += 1
                i -= 1
            if j >= 0:
                if b[j] == '1':
                    carry += 1
                j -= 1
            carry, remainder = divmod(carry, 2)
            if remainder == 1:
                res = '1' + res
            else:
                res = '0' + res
        return res    
            
# time O(max(m, n))
# space O(max(m, n))
# using math
```


## 📄 [O]math\[O]math\7-reverse-integer.py

```py
class Solution:
    def reverse(self, x: int) -> int:
        if x == 0:
            return 0
        pos = True if x > 0 else False
        if not pos:
            x = abs(x)
        upper_bound = 2**31 - 1
        lower_bound = - (2**31)

        res = 0
        while x:
            x, remainder = divmod(x, 10)
            if pos and (res > upper_bound // 10 or (res == upper_bound // 10 and remainder > upper_bound % 10)):
                return 0
            if not pos and (- res < int(lower_bound / 10) or (- res == int(lower_bound / 10) and remainder > 10 - lower_bound % 10)):
                return 0
            res = res * 10 + remainder
        
        return res if pos else - res
            
# time O(logn), base 10
# space O(1)
# using math
```


## 📄 [O]math\[O]math\869-reordered-power-of-2.py

```py
class Solution:
    def reorderedPowerOf2(self, n: int) -> bool:

        def check(num):
            res = [0 for _ in range(10)]
            while num:
                num, remainder = divmod(num, 10)
                res[remainder] += 1
            return res

        target = check(n)
        val = 1
        for i in range(31):
            if check(val) == target:
                return True
            val <<= 1
        return False
    
# time O(1)
# space O(1)
# using math
```


## 📄 [O]math\[O]math\9-palindrome-number.java

```java
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0) {
            return false;
        }
        if (x == 0) {
            return true;
        }
        if (x % 10 == 0) {
            return false;
        }
        int firstHalf = x;
        int secondHalf = 0;
        while (firstHalf > secondHalf) {
            int rem = firstHalf % 10;
            secondHalf = secondHalf * 10 + rem;
            firstHalf /= 10;
        }
        if (firstHalf < secondHalf) {
            secondHalf /= 10;
        }
        return firstHalf == secondHalf;
    }
}

// time O(logn), base 10
// space O(1)
// using math
```


## 📄 [O]math\[O]math\9-palindrome-number.py

```py
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if x < 0:
            return False
        if x == 0:
            return True
        if x % 10 == 0:
            return False
        
        first_half = x
        second_half = 0
        while first_half > second_half:
            first_half, remainder = divmod(first_half, 10)
            second_half = second_half * 10 + remainder
        if first_half < second_half:
            second_half //= 10
        return first_half == second_half

# time O(logn), base 10
# space O(1)
# using math
```


## 📄 [P]segment-tree\[P]segment-tree\2158-amount-of-new-area-painted-each-day.py

```py
class Node:
    def __init__(self, start, end):
        self.start = start
        self.end = end
        self.mid = (start + end) // 2
        self.left = None
        self.right = None
        self.val = 0
        self.lazy = - 1

class SegmentTree:
    def __init__(self, start, end):
        self.root = Node(start, end)

    def push_down(self, node):
        if not node.left:
            node.left = Node(node.start, node.mid)
        if not node.right:
            node.right = Node(node.mid + 1, node.end)
        if node.lazy == - 1:
            return
        node.left.val = node.lazy * (node.left.end - node.left.start + 1)
        node.right.val = node.lazy * (node.right.end - node.right.start + 1)
        node.left.lazy = node.lazy
        node.right.lazy = node.lazy
        node.lazy = - 1

    def push_up(self, node):
        node.val = node.left.val + node.right.val

    def update(self, node, start, end, val):
        if start <= node.start and node.end <= end:
            node.val = val * (node.end - node.start + 1)
            node.lazy = val
            return node.val
        self.push_down(node)
        res = 0
        if start <= node.mid:
            res += self.update(node.left, start, end, val)
        if end >= node.mid + 1:
            res += self.update(node.right, start, end, val)
        self.push_up(node)
        return res

    def query(self, node, start, end):
        if start <= node.start and node.end <= end:
            return node.val
        self.push_down(node)
        res = 0
        if start <= node.mid:
            res += self.query(node.left, start, end)
        if end >= node.mid + 1:
            res += self.query(node.right, start, end)
        return res

class Solution:
    def amountPainted(self, paint: List[List[int]]) -> List[int]:
        st = SegmentTree(0, 10**9)
        res = []
        for p, q in paint:
            s, e = p, q - 1
            old_paint = st.query(st.root, s, e)
            new_paint = st.update(st.root, s, e, 1)
            res.append(new_paint - old_paint)
        return res

# time O(nlogC)
# space O(n), due to segment tree
# using segment tree and count type segment tree
```


## 📄 [P]segment-tree\[P]segment-tree\218-the-skyline-problem.py

```py
class Node:
    def __init__(self, start, end):
        self.start = start
        self.end = end
        self.mid = (start + end) // 2
        self.left = None
        self.right = None
        self.val = 0
        self.lazy = 0

class SegmentTree:
    def __init__(self, start, end):
        self.root = Node(start, end)

    def push_down(self, node):
        if not node.left:
            node.left = Node(node.start, node.mid)
        if not node.right:
            node.right = Node(node.mid + 1, node.end)
        if node.lazy == 0:
            return
        node.left.val = max(node.left.val, node.lazy)
        node.right.val = max(node.right.val, node.lazy)
        node.left.lazy = max(node.left.lazy, node.lazy)
        node.right.lazy = max(node.right.lazy, node.lazy)
        node.lazy = 0

    def push_up(self, node):
        node.val = max(node.left.val, node.right.val)

    def update(self, node, start, end, val):
        if start <= node.start and node.end <= end:
            node.val = max(node.val, val)
            node.lazy = max(node.lazy, val)
            return
        self.push_down(node)
        if start <= node.mid:
            self.update(node.left, start, end, val)
        if end >= node.mid + 1:
            self.update(node.right, start, end, val)
        self.push_up(node)

    def query(self, node, start, end):
        if start <= node.start and node.end <= end:
            return node.val
        self.push_down(node)
        res = 0
        if start <= node.mid:
            res = max(res, self.query(node.left, start, end))
        if end >= node.mid + 1:
            res = max(res, self.query(node.right, start, end))
        return res

class Solution:
    def getSkyline(self, buildings: List[List[int]]) -> List[List[int]]:
        st = SegmentTree(0, 2**31-1)
        lines = []
        for p, q, h in buildings:
            lines.append(p)
            lines.append(q)
            st.update(st.root, p, q - 1, h)
        
        lines.sort()
        res = []
        for p in lines:
            h = st.query(st.root, p, p)
            if not res or res[- 1][1] != h:
                res.append([p, h])
        return res

# time O(nlogC + nlogn)
# space O(n), due to segment tree
# using segment tree and max type segment tree and line sweep
```


## 📄 [P]segment-tree\[P]segment-tree\2407-longest-increasing-subsequence-ii.py

```py
class Node:
    def __init__(self, start, end):
        self.start = start
        self.end = end
        self.mid = (start + end) // 2
        self.left = None
        self.right = None
        self.val = 0
        self.lazy = 0

class SegmentTree:
    def __init__(self, start, end):
        self.root = Node(start, end)

    def push_down(self, node):
        if not node.left:
            node.left = Node(node.start, node.mid)
        if not node.right:
            node.right = Node(node.mid + 1, node.end)
        if node.lazy == 0:
            return
        node.left.val = max(node.left.val, node.lazy)
        node.right.val = max(node.right.val, node.lazy)
        node.left.lazy = max(node.left.lazy, node.lazy)
        node.right.lazy = max(node.right.lazy, node.lazy)
        node.lazy = 0

    def push_up(self, node):
        node.val = max(node.left.val, node.right.val)

    def update(self, node, start, end, val):
        if start <= node.start and node.end <= end:
            node.val = max(node.val, val)
            node.lazy = max(node.lazy, val)
            return
        self.push_down(node)
        if start <= node.mid:
            self.update(node.left, start, end, val)
        if end >= node.mid + 1:
            self.update(node.right, start, end, val)
        self.push_up(node)

    def query(self, node, start, end):
        if start <= node.start and node.end <= end:
            return node.val
        self.push_down(node)
        res = 0
        if start <= node.mid:
            res = max(res, self.query(node.left, start, end))
        if end >= node.mid + 1:
            res = max(res, self.query(node.right, start, end))
        return res

class Solution:
    def lengthOfLIS(self, nums: List[int], k: int) -> int:
        st = SegmentTree(0, 10**9)
        res = 0
        for num in nums:
            prev_len = st.query(st.root, max(num - k, 0), num - 1)
            cur_len = prev_len + 1
            st.update(st.root, num, num, cur_len)
            res = max(res, cur_len)
        return res
            
# time O(nlogC)
# space O(n), due to segment tree
# using segment tree and max type segment tree
```


## 📄 [P]segment-tree\[P]segment-tree\307-range-sum-query-mutable.py

```py
class Node:
    def __init__(self, start, end):
        self.start = start
        self.end = end
        self.mid = (start + end) // 2
        self.left = None
        self.right = None
        self.val = 0

class NumArray:
    def __init__(self, nums: List[int]):
        def build(start, end):
            if start == end:
                node = Node(start, end)
                node.val = nums[start]
                return node
            node = Node(start, end)
            node.left = build(start, node.mid)
            node.right = build(node.mid + 1, end)
            node.val = node.left.val + node.right.val
            return node
        
        self.root = build(0, len(nums) - 1)
    
    def update(self, index: int, val: int) -> None:
        def helper(node, index, val):
            if node.start == node.end:
                node.val = val
                return
            if index <= node.mid:
                helper(node.left, index, val)
            else:
                helper(node.right, index, val)
            node.val = node.left.val + node.right.val
        
        helper(self.root, index, val)

    def sumRange(self, left: int, right: int) -> int:
        def helper(node, start, end):
            if start <= node.start and node.end <= end:
                return node.val
            res = 0
            if start <= node.mid:
                res += helper(node.left, start, end)
            if end >= node.mid + 1:
                res += helper(node.right, start, end)
            return res
            
        return helper(self.root, left, right)

# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# obj.update(index,val)
# param_2 = obj.sumRange(left,right)

# time O(n) for initialize and O(logn) for update() and sumRange()
# space O(n), due to segment tree
# using segment tree and sum type segment tree
```


## 📄 [P]segment-tree\[P]segment-tree\715-range-module.py

```py
class Node:
    def __init__(self, start, end):
        self.start = start
        self.end = end
        self.mid = (start + end) // 2
        self.left = None
        self.right = None
        self.val = 0
        self.lazy = - 1

class SegmentTree:
    def __init__(self, start, end):
        self.root = Node(start, end)

    def push_down(self, node):
        if not node.left:
            node.left = Node(node.start, node.mid)
        if not node.right:
            node.right = Node(node.mid + 1, node.end)
        if node.lazy == - 1:
            return
        node.left.val = node.lazy * (node.left.end - node.left.start + 1)
        node.right.val = node.lazy * (node.right.end - node.right.start + 1)
        node.left.lazy = node.lazy
        node.right.lazy = node.lazy
        node.lazy = - 1

    def push_up(self, node):
        node.val = node.left.val + node.right.val

    def update(self, node, start, end, val):
        if start <= node.start and node.end <= end:
            node.val = val * (node.end - node.start + 1)
            node.lazy = val
            return
        self.push_down(node)
        if start <= node.mid:
            self.update(node.left, start, end, val)
        if end >= node.mid + 1:
            self.update(node.right, start, end, val)
        self.push_up(node)

    def query(self, node, start, end):
        if start <= node.start and node.end <= end:
            return node.val == node.end - node.start + 1
        self.push_down(node)
        if start <= node.mid:
            if not self.query(node.left, start, end):
                return False
        if end >= node.mid + 1:
            if not self.query(node.right, start, end):
                return False
        return True

class RangeModule:

    def __init__(self):
        self.st = SegmentTree(0, 10**9)

    def addRange(self, left: int, right: int) -> None:
        self.st.update(self.st.root, left, right - 1, 1)

    def queryRange(self, left: int, right: int) -> bool:
        return self.st.query(self.st.root, left, right - 1)

    def removeRange(self, left: int, right: int) -> None:
        self.st.update(self.st.root, left, right - 1, 0)

# Your RangeModule object will be instantiated and called as such:
# obj = RangeModule()
# obj.addRange(left,right)
# param_2 = obj.queryRange(left,right)
# obj.removeRange(left,right)

# time O(1) for initialize and O(logC) for others
# space O(min(n, C)), due to segment tree
# using segment tree and count type segment tree
```


## 📄 [P]segment-tree\[P]segment-tree\729-my-calendar-i.py

```py
class Node:
    def __init__(self, start, end):
        self.start = start
        self.end = end
        self.mid = (start + end) // 2
        self.left = None
        self.right = None
        self.val = 0
        self.lazy = - 1

class SegmentTree:
    def __init__(self, start, end):
        self.root = Node(start, end)

    def push_down(self, node):
        if not node.left:
            node.left = Node(node.start, node.mid)
        if not node.right:
            node.right = Node(node.mid + 1, node.end)
        if node.lazy == - 1:
            return
        node.left.val = node.lazy * (node.left.end - node.left.start + 1)
        node.right.val = node.lazy * (node.right.end - node.right.start + 1)
        node.left.lazy = node.lazy
        node.right.lazy = node.lazy
        node.lazy = - 1

    def push_up(self, node):
        node.val = node.left.val + node.right.val

    def update(self, node, start, end, val):
        if start <= node.start and node.end <= end:
            node.val = val * (node.end - node.start + 1)
            node.lazy = val
            return
        self.push_down(node)
        if start <= node.mid:
            self.update(node.left, start, end, val)
        if end >= node.mid + 1:
            self.update(node.right, start, end, val)
        self.push_up(node)

    def query(self, node, start, end):
        if start <= node.start and node.end <= end:
            return node.val > 0
        self.push_down(node)
        if start <= node.mid:
            if self.query(node.left, start, end):
                return True
        if end >= node.mid + 1:
            if self.query(node.right, start, end):
                return True
        return False

class MyCalendar:

    def __init__(self):
        self.st = SegmentTree(0, 10**9)

    def book(self, start: int, end: int) -> bool:
        if self.st.query(self.st.root, start, end - 1):
            return False
        self.st.update(self.st.root, start, end - 1, 1)
        return True

# Your MyCalendar object will be instantiated and called as such:
# obj = MyCalendar()
# param_1 = obj.book(start,end)

# time O(1) for initialize and O(logC) for book and others
# space O(min(n, C)), due to segment tree
# using segment tree and count type segment tree
```


## 📄 [P]segment-tree\[P]segment-tree\731-my-calendar-ii.py

```py
class Node:
    def __init__(self, start, end):
        self.start = start
        self.end = end
        self.mid = (start + end) // 2
        self.left = None
        self.right = None
        self.val = 0
        self.lazy = 0

class SegmentTree:
    def __init__(self, start, end):
        self.root = Node(start, end)

    def push_down(self, node):
        if not node.left:
            node.left = Node(node.start, node.mid)
        if not node.right:
            node.right = Node(node.mid + 1, node.end)
        if node.lazy == 0:
            return
        node.left.val += node.lazy
        node.right.val += node.lazy
        node.left.lazy += node.lazy
        node.right.lazy += node.lazy
        node.lazy = 0

    def push_up(self, node):
        node.val = max(node.left.val, node.right.val)

    def update(self, node, start, end, val):
        if start <= node.start and node.end <= end:
            node.val += val
            node.lazy += val
            return
        self.push_down(node)
        if start <= node.mid:
            self.update(node.left, start, end, val)
        if end >= node.mid + 1:
            self.update(node.right, start, end, val)
        self.push_up(node)

    def query(self, node, start, end):
        if start <= node.start and node.end <= end:
            return node.val
        self.push_down(node)
        res = 0
        if start <= node.mid:
            res = max(res, self.query(node.left, start, end))
        if end >= node.mid + 1:
            res = max(res, self.query(node.right, start, end))
        return res

class MyCalendarTwo:

    def __init__(self):
        self.st = SegmentTree(0, 10**9)

    def book(self, start: int, end: int) -> bool:
        if self.st.query(self.st.root, start, end - 1) == 2:
            return False
        self.st.update(self.st.root, start, end - 1, 1)
        return True

# Your MyCalendarTwo object will be instantiated and called as such:
# obj = MyCalendarTwo()
# param_1 = obj.book(start,end)

# time O(1) for initialize and O(logC) for book and others
# space O(min(n, C)), due to segment tree
# using segment tree and max type segment tree
```
