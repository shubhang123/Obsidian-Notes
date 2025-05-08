Here's the formatted markdown table with LeetCode problems:

| Difficulty | Title | Frequency | Acceptance Rate | Link | Topics |
|------------|-------|-----------|-----------------|------|--------|
| MEDIUM | [Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer) | 100.0 | 59.50% | Hash Table, Linked List |
| MEDIUM | [Rotting Oranges](https://leetcode.com/problems/rotting-oranges) | 94.8 | 55.97% | Array, Breadth-First Search, Matrix |
| MEDIUM | [Merge Intervals](https://leetcode.com/problems/merge-intervals) | 94.8 | 48.81% | Array, Sorting |
| MEDIUM | [Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree) | 88.5 | 67.45% | Hash Table, String, Design, Trie |
| MEDIUM | [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters) | 88.5 | 36.33% | Hash Table, String, Sliding Window |
| MEDIUM | [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self) | 88.5 | 67.38% | Array, Prefix Sum |
| MEDIUM | [Design Authentication Manager](https://leetcode.com/problems/design-authentication-manager) | 80.3 | 58.13% | Hash Table, Linked List, Design, Doubly-Linked List |
| HARD | [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream) | 80.3 | 52.97% | Two Pointers, Design, Sorting, Heap (Priority Queue), Data Stream |
| MEDIUM | [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements) | 80.3 | 64.08% | Array, Hash Table, Divide and Conquer, Sorting, Heap (Priority Queue), Bucket Sort, Counting, Quickselect |
| HARD | [Reaching Points](https://leetcode.com/problems/reaching-points) | 80.3 | 33.55% | Math |
| EASY | [Excel Sheet Column Number](https://leetcode.com/problems/excel-sheet-column-number) | 80.3 | 65.32% | Math, String |
| MEDIUM | [Sort Colors](https://leetcode.com/problems/sort-colors) | 80.3 | 66.36% | Array, Two Pointers, Sorting |
| EASY | [Valid Parentheses](https://leetcode.com/problems/valid-parentheses) | 80.3 | 41.85% | String, Stack |
| MEDIUM | [3Sum](https://leetcode.com/problems/3sum) | 80.3 | 36.42% | Array, Two Pointers, Sorting |
| MEDIUM | [Reorder Routes to Make All Paths Lead to the City Zero](https://leetcode.com/problems/reorder-routes-to-make-all-paths-lead-to-the-city-zero) | 68.9 | 64.79% | Depth-First Search, Breadth-First Search, Graph |
| MEDIUM | [Course Schedule](https://leetcode.com/problems/course-schedule) | 68.9 | 48.48% | Depth-First Search, Breadth-First Search, Graph, Topological Sort |
| MEDIUM | [Insert Delete GetRandom O(1)](https://leetcode.com/problems/insert-delete-getrandom-o1) | 68.9 | 54.91% | Array, Hash Table, Math, Design, Randomized |
| MEDIUM | [Shortest Bridge](https://leetcode.com/problems/shortest-bridge) | 68.9 | 58.34% | Array, Depth-First Search, Breadth-First Search, Matrix |
| MEDIUM | [Peak Index in a Mountain Array](https://leetcode.com/problems/peak-index-in-a-mountain-array) | 68.9 | 67.77% | Array, Binary Search |
| MEDIUM | [Inorder Successor in BST](https://leetcode.com/problems/inorder-successor-in-bst) | 68.9 | 50.49% | Tree, Depth-First Search, Binary Search Tree, Binary Tree |
| MEDIUM | [Count Good Nodes in Binary Tree](https://leetcode.com/problems/count-good-nodes-in-binary-tree) | 68.9 | 73.32% | Tree, Depth-First Search, Breadth-First Search, Binary Tree |
| EASY | [Two Sum](https://leetcode.com/problems/two-sum) | 68.9 | 55.07% | Array, Hash Table |
| MEDIUM | [Optimal Partition of String](https://leetcode.com/problems/optimal-partition-of-string) | 68.9 | 78.10% | Hash Table, String, Greedy |
| MEDIUM | [LRU Cache](https://leetcode.com/problems/lru-cache) | 68.9 | 44.43% | Hash Table, Linked List, Design, Doubly-Linked List |
| EASY | [Palindrome Permutation](https://leetcode.com/problems/palindrome-permutation) | 68.9 | 68.08% | Hash Table, String, Bit Manipulation |
| MEDIUM | [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal) | 68.9 | 69.82% | Tree, Breadth-First Search, Binary Tree |
| HARD | [IPO](https://leetcode.com/problems/ipo) | 68.9 | 53.00% | Array, Greedy, Sorting, Heap (Priority Queue) |
| MEDIUM | [Boats to Save People](https://leetcode.com/problems/boats-to-save-people) | 68.9 | 59.94% | Array, Two Pointers, Greedy, Sorting |
| MEDIUM | [Clone Graph](https://leetcode.com/problems/clone-graph) | 68.9 | 61.19% | Hash Table, Depth-First Search, Breadth-First Search, Graph |
| MEDIUM | [Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal) | 68.9 | 61.01% | Tree, Breadth-First Search, Binary Tree |
| MEDIUM | [Minesweeper](https://leetcode.com/problems/minesweeper) | 68.9 | 67.75% | Array, Depth-First Search, Breadth-First Search, Matrix |
| MEDIUM | [Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure) | 68.9 | 46.70% | String, Depth-First Search, Design, Trie |
Awesome, Shashank! Let's go full throttle 🚀  
Here are **C++ solutions for all 33 problems** one by one, fully written and optimized.

---

### ✅ **1. [Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer)**

```cpp
class Solution {
public:
    Node* copyRandomList(Node* head) {
        if (!head) return nullptr;

        unordered_map<Node*, Node*> map;
        Node* curr = head;
        while (curr) {
            map[curr] = new Node(curr->val);
            curr = curr->next;
        }

        curr = head;
        while (curr) {
            map[curr]->next = map[curr->next];
            map[curr]->random = map[curr->random];
            curr = curr->next;
        }

        return map[head];
    }
};
```

---

### ✅ **2. [Rotting Oranges](https://leetcode.com/problems/rotting-oranges)**

```cpp
class Solution {
public:
    typedef pair<int, int> P;
    vector<vector<int>> directions{{-1, 0}, {1, 0}, {0, -1}, {0, 1}};

    int orangesRotting(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();

        queue<P> que;
        int freshCount = 0;

        for(int i = 0; i < m; i++) {
            for(int j = 0; j < n; j++) {
                if(grid[i][j] == 2) {
                    que.push({i, j}); //Storing all possible sources at once in the queue
                }
                else if(grid[i][j] == 1) {
                    freshCount++;
                }
            }
        }
        
        if(freshCount == 0)
            return 0;
        
        auto isSafe = [&](int x, int y) {
            return x >= 0 && x < grid.size() && y >= 0 && y<grid[x].size() && grid[x][y] == 1;
        };
        
        //Applying Multi-Source BFS
        int time = 0;
        while(!que.empty()) {
            int n = que.size();
            //because we want to cover all neighbours of a node
            //at once which are affected in a particular time frame
            while(n--) {
                P curr = que.front();
                que.pop();
                int i = curr.first;
                int j = curr.second;
                
                for(auto &dir : directions) {
                    int new_i = i + dir[0];
                    int new_j = j + dir[1];
                    
                    if(isSafe(new_i, new_j)) {
                        grid[new_i][new_j] = 2;
                        que.push({new_i, new_j});
                        freshCount--;
                    }
                }
            }
            time++;
        }
        
        return (freshCount==0) ? time-1 : -1;
    }
};
```

---

### ✅ **3. [Merge Intervals](https://leetcode.com/problems/merge-intervals)**

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> merged;

        for (auto& interval : intervals) {
            if (merged.empty() || merged.back()[1] < interval[0])
                merged.push_back(interval);
            else
                merged.back()[1] = max(merged.back()[1], interval[1]);
        }

        return merged;
    }
};
```

---

### ✅ **4. [Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree)**

```cpp
class TrieNode {
public:
    TrieNode* children[26] = {};
    bool isEnd = false;
};

class Trie {
private:
    TrieNode* root;

public:
    Trie() { root = new TrieNode(); }

    void insert(string word) {
        TrieNode* node = root;
        for (char ch : word) {
            if (!node->children[ch - 'a']) node->children[ch - 'a'] = new TrieNode();
            node = node->children[ch - 'a'];
        }
        node->isEnd = true;
    }

    bool search(string word) {
        TrieNode* node = root;
        for (char ch : word) {
            if (!node->children[ch - 'a']) return false;
            node = node->children[ch - 'a'];
        }
        return node->isEnd;
    }

    bool startsWith(string prefix) {
        TrieNode* node = root;
        for (char ch : prefix) {
            if (!node->children[ch - 'a']) return false;
            node = node->children[ch - 'a'];
        }
        return true;
    }
};
```

---

### ✅ **5. [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters)**

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char, int> map;
        int left = 0, maxLen = 0;
        for (int right = 0; right < s.size(); ++right) {
            if (map.find(s[right]) != map.end())
                left = max(left, map[s[right]] + 1);
            map[s[right]] = right;
            maxLen = max(maxLen, right - left + 1);
        }
        return maxLen;
    }
};
```

---

I'll continue with the next batch (6 to 10) in the following message to keep it clean and readable.

Shall I proceed with **Product of Array Except Self** next?

Awesome! Here's the **next batch (6 to 10)** of C++ solutions:

---

### ✅ **6. [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self)**

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> res(n, 1);

        int left = 1;
        for (int i = 0; i < n; i++) {
            res[i] = left;
            left *= nums[i];
        }

        int right = 1;
        for (int i = n - 1; i >= 0; i--) {
            res[i] *= right;
            right *= nums[i];
        }

        return res;
    }
};
```

---

### ✅ **7. [Design Authentication Manager](https://leetcode.com/problems/design-authentication-manager)**

```cpp
class AuthenticationManager {
    int ttl;
    unordered_map<string, int> tokens;

public:
    AuthenticationManager(int timeToLive) {
        ttl = timeToLive;
    }

    void generate(string tokenId, int currentTime) {
        tokens[tokenId] = currentTime + ttl;
    }

    void renew(string tokenId, int currentTime) {
        if (tokens.count(tokenId) && tokens[tokenId] > currentTime) {
            tokens[tokenId] = currentTime + ttl;
        }
    }

    int countUnexpiredTokens(int currentTime) {
        int count = 0;
        for (auto& [_, expTime] : tokens) {
            if (expTime > currentTime) count++;
        }
        return count;
    }
};
```

---

### ✅ **8. [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream)**

```cpp
class MedianFinder {
    priority_queue<int> maxHeap; // lower half
    priority_queue<int, vector<int>, greater<int>> minHeap; // upper half

public:
    void addNum(int num) {
        maxHeap.push(num);
        minHeap.push(maxHeap.top());
        maxHeap.pop();

        if (minHeap.size() > maxHeap.size()) {
            maxHeap.push(minHeap.top());
            minHeap.pop();
        }
    }

    double findMedian() {
        if (maxHeap.size() > minHeap.size())
            return maxHeap.top();
        return (maxHeap.top() + minHeap.top()) / 2.0;
    }
};
```

---

### ✅ **9. [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements)**

```cpp
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> freq;
        for (int num : nums) freq[num]++;

        priority_queue<pair<int, int>> pq;
        for (auto& [num, count] : freq)
            pq.push({count, num});

        vector<int> res;
        while (k--) {
            res.push_back(pq.top().second);
            pq.pop();
        }

        return res;
    }
};
```

---

### ✅ **10. [Reaching Points](https://leetcode.com/problems/reaching-points)**

```cpp
class Solution {
public:
    bool reachingPoints(int sx, int sy, int tx, int ty) {
        while (tx >= sx && ty >= sy) {
            if (tx == sx && ty == sy) return true;
            if (tx > ty)
                tx %= ty;
            else
                ty %= tx;
        }
        return false;
    }
};
```

---

Let me know if you'd like the **next batch (11 to 15)** — it's ready to go!

Great! Here's the next batch — **C++ solutions for problems 11 to 15**:

---

### ✅ **11. [Excel Sheet Column Number](https://leetcode.com/problems/excel-sheet-column-number)**

```cpp
class Solution {
public:
    int titleToNumber(string columnTitle) {
        int result = 0;
        for (char c : columnTitle) {
            result = result * 26 + (c - 'A' + 1);
        }
        return result;
    }
};
```

---

### ✅ **12. [Sort Colors](https://leetcode.com/problems/sort-colors)**

(Dutch National Flag Algorithm)

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int low = 0, mid = 0, high = nums.size() - 1;

        while (mid <= high) {
            if (nums[mid] == 0)
                swap(nums[low++], nums[mid++]);
            else if (nums[mid] == 1)
                mid++;
            else
                swap(nums[mid], nums[high--]);
        }
    }
};
```

---

### ✅ **13. [Valid Parentheses](https://leetcode.com/problems/valid-parentheses)**

```cpp
class Solution {
public:
    bool isValid(string s) {
        stack<char> stk;
        for (char c : s) {
            if (c == '(' || c == '{' || c == '[')
                stk.push(c);
            else {
                if (stk.empty()) return false;
                char top = stk.top();
                if ((c == ')' && top != '(') ||
                    (c == '}' && top != '{') ||
                    (c == ']' && top != '[')) return false;
                stk.pop();
            }
        }
        return stk.empty();
    }
};
```

---

### ✅ **14. [3Sum](https://leetcode.com/problems/3sum)**

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        vector<vector<int>> res;

        for (int i = 0; i < nums.size(); ++i) {
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            int target = -nums[i], left = i + 1, right = nums.size() - 1;

            while (left < right) {
                int sum = nums[left] + nums[right];
                if (sum == target) {
                    res.push_back({nums[i], nums[left++], nums[right--]});
                    while (left < right && nums[left] == nums[left - 1]) left++;
                    while (left < right && nums[right] == nums[right + 1]) right--;
                } else if (sum < target)
                    left++;
                else
                    right--;
            }
        }

        return res;
    }
};
```

---

### ✅ **15. [Reorder Routes to Make All Paths Lead to the City Zero](https://leetcode.com/problems/reorder-routes-to-make-all-paths-lead-to-the-city-zero)**

```cpp
class Solution {
public:
    int minReorder(int n, vector<vector<int>>& connections) {
        vector<vector<pair<int, int>>> graph(n);
        for (auto& conn : connections) {
            graph[conn[0]].push_back({conn[1], 1}); // needs reordering
            graph[conn[1]].push_back({conn[0], 0}); // already fine
        }

        int count = 0;
        vector<bool> visited(n);
        function<void(int)> dfs = [&](int node) {
            visited[node] = true;
            for (auto& [nei, change] : graph[node]) {
                if (!visited[nei]) {
                    count += change;
                    dfs(nei);
                }
            }
        };

        dfs(0);
        return count;
    }
};
```

---

Next up are problems **16 to 20**, including **Course Schedule** and **Shortest Bridge**.  
Ready to roll?

Let’s keep going! Here's the **C++ solutions for problems 16 to 20** from your list:

---

### ✅ **16. [Course Schedule](https://leetcode.com/problems/course-schedule)**

(Topological Sort – Kahn's Algorithm)

```cpp
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> adj(numCourses);
        vector<int> indegree(numCourses, 0);

        for (auto& pre : prerequisites) {
            adj[pre[1]].push_back(pre[0]);
            indegree[pre[0]]++;
        }

        queue<int> q;
        for (int i = 0; i < numCourses; ++i)
            if (indegree[i] == 0) q.push(i);

        int count = 0;
        while (!q.empty()) {
            int node = q.front(); q.pop();
            count++;
            for (int next : adj[node]) {
                if (--indegree[next] == 0)
                    q.push(next);
            }
        }

        return count == numCourses;
    }
};
```

---

### ✅ **17. [Insert Delete GetRandom O(1)](https://leetcode.com/problems/insert-delete-getrandom-o1)**

```cpp
class RandomizedSet {
private:
    unordered_map<int, int> valToIndex;
    vector<int> values;

public:
    bool insert(int val) {
        if (valToIndex.count(val)) return false;
        values.push_back(val);
        valToIndex[val] = values.size() - 1;
        return true;
    }

    bool remove(int val) {
        if (!valToIndex.count(val)) return false;

        int last = values.back();
        int idx = valToIndex[val];

        values[idx] = last;
        valToIndex[last] = idx;

        values.pop_back();
        valToIndex.erase(val);

        return true;
    }

    int getRandom() {
        return values[rand() % values.size()];
    }
};
```

---

### ✅ **18. [Shortest Bridge](https://leetcode.com/problems/shortest-bridge)**

```cpp
class Solution {
    int n;
    queue<pair<int, int>> q;

    void dfs(vector<vector<int>>& grid, int x, int y) {
        if (x < 0 || y < 0 || x >= n || y >= n || grid[x][y] != 1) return;
        grid[x][y] = 2;
        q.push({x, y});
        dfs(grid, x+1, y);
        dfs(grid, x-1, y);
        dfs(grid, x, y+1);
        dfs(grid, x, y-1);
    }

public:
    int shortestBridge(vector<vector<int>>& grid) {
        n = grid.size();
        bool found = false;

        for (int i = 0; i < n && !found; ++i) {
            for (int j = 0; j < n && !found; ++j) {
                if (grid[i][j] == 1) {
                    dfs(grid, i, j);
                    found = true;
                }
            }
        }

        int steps = 0;
        vector<int> dir = {-1, 0, 1, 0, -1};
        while (!q.empty()) {
            int sz = q.size();
            while (sz--) {
                auto [x, y] = q.front(); q.pop();
                for (int d = 0; d < 4; ++d) {
                    int nx = x + dir[d], ny = y + dir[d+1];
                    if (nx >= 0 && ny >= 0 && nx < n && ny < n) {
                        if (grid[nx][ny] == 1) return steps;
                        if (grid[nx][ny] == 0) {
                            grid[nx][ny] = 2;
                            q.push({nx, ny});
                        }
                    }
                }
            }
            steps++;
        }
        return -1;
    }
};
```

---

### ✅ **19. [Peak Index in a Mountain Array](https://leetcode.com/problems/peak-index-in-a-mountain-array)**

```cpp
class Solution {
public:
    int peakIndexInMountainArray(vector<int>& arr) {
        int left = 0, right = arr.size() - 1;
        while (left < right) {
            int mid = (left + right) / 2;
            if (arr[mid] < arr[mid + 1])
                left = mid + 1;
            else
                right = mid;
        }
        return left;
    }
};
```

---

### ✅ **20. [Inorder Successor in BST](https://leetcode.com/problems/inorder-successor-in-bst)**

```cpp
class Solution {
public:
    TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
        TreeNode* succ = nullptr;
        while (root) {
            if (p->val < root->val) {
                succ = root;
                root = root->left;
            } else {
                root = root->right;
            }
        }
        return succ;
    }
};
```

---

Next up: **Count Good Nodes in Binary Tree → Design Add and Search Words Data Structure (21 to 25)**.  
Let me know if I should keep it coming!


Let's finish strong! Here's the **C++ solutions for problems 21 to 25**:

---

### ✅ **21. [Count Good Nodes in Binary Tree](https://leetcode.com/problems/count-good-nodes-in-binary-tree)**

```cpp
class Solution {
public:
    int goodNodes(TreeNode* root, int maxSoFar = INT_MIN) {
        if (!root) return 0;
        int count = root->val >= maxSoFar ? 1 : 0;
        maxSoFar = max(maxSoFar, root->val);
        return count + goodNodes(root->left, maxSoFar) + goodNodes(root->right, maxSoFar);
    }
};
```

---

### ✅ **22. [Two Sum](https://leetcode.com/problems/two-sum)**

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> map;
        for (int i = 0; i < nums.size(); i++) {
            int complement = target - nums[i];
            if (map.count(complement)) return {map[complement], i};
            map[nums[i]] = i;
        }
        return {};
    }
};
```

---

### ✅ **23. [Optimal Partition of String](https://leetcode.com/problems/optimal-partition-of-string)**

```cpp
class Solution {
public:
    int partitionString(string s) {
        unordered_set<char> seen;
        int count = 1;

        for (char c : s) {
            if (seen.count(c)) {
                count++;
                seen.clear();
            }
            seen.insert(c);
        }

        return count;
    }
};
```

---

### ✅ **24. [LRU Cache](https://leetcode.com/problems/lru-cache)**

```cpp
class LRUCache {
    int capacity;
    list<pair<int, int>> dll;
    unordered_map<int, list<pair<int, int>>::iterator> cache;

public:
    LRUCache(int cap) { capacity = cap; }

    int get(int key) {
        if (cache.find(key) == cache.end()) return -1;
        auto it = cache[key];
        int value = it->second;
        dll.erase(it);
        dll.push_front({key, value});
        cache[key] = dll.begin();
        return value;
    }

    void put(int key, int value) {
        if (cache.find(key) != cache.end())
            dll.erase(cache[key]);

        dll.push_front({key, value});
        cache[key] = dll.begin();

        if (dll.size() > capacity) {
            int k = dll.back().first;
            cache.erase(k);
            dll.pop_back();
        }
    }
};
```

---

### ✅ **25. [Palindrome Permutation](https://leetcode.com/problems/palindrome-permutation)**

```cpp
class Solution {
public:
    bool canPermutePalindrome(string s) {
        unordered_set<char> st;
        for (char c : s) {
            if (st.count(c)) st.erase(c);
            else st.insert(c);
        }
        return st.size() <= 1;
    }
};
```

---

Next up: **problems 26–33** — final lap!  
Shall I go ahead and wrap them all up in the next message?
You're crushing it, Shashank! 💪  
Here comes the **final batch (problems 26 to 33)** of clean, optimized **C++ solutions**.

---

### ✅ **26. [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal)**

```cpp
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if (!root) return res;

        queue<TreeNode*> q;
        q.push(root);

        while (!q.empty()) {
            int sz = q.size();
            vector<int> level;
            for (int i = 0; i < sz; ++i) {
                TreeNode* node = q.front(); q.pop();
                level.push_back(node->val);
                if (node->left) q.push(node->left);
                if (node->right) q.push(node->right);
            }
            res.push_back(level);
        }

        return res;
    }
};
```

---

### ✅ **27. [IPO](https://leetcode.com/problems/ipo)**

```cpp
class Solution {
public:
    int findMaximizedCapital(int k, int w, vector<int>& profits, vector<int>& capital) {
        priority_queue<int> maxProfit;
        vector<pair<int, int>> projects;
        int n = profits.size();

        for (int i = 0; i < n; ++i)
            projects.push_back({capital[i], profits[i]});

        sort(projects.begin(), projects.end());

        int i = 0;
        while (k--) {
            while (i < n && projects[i].first <= w)
                maxProfit.push(projects[i++].second);

            if (maxProfit.empty()) break;
            w += maxProfit.top(); maxProfit.pop();
        }

        return w;
    }
};
```

---

### ✅ **28. [Boats to Save People](https://leetcode.com/problems/boats-to-save-people)**

```cpp
class Solution {
public:
    int numRescueBoats(vector<int>& people, int limit) {
        sort(people.begin(), people.end());
        int i = 0, j = people.size() - 1, boats = 0;

        while (i <= j) {
            if (people[i] + people[j] <= limit) i++;
            j--;
            boats++;
        }

        return boats;
    }
};
```

---

### ✅ **29. [Clone Graph](https://leetcode.com/problems/clone-graph)**

```cpp
class Solution {
    unordered_map<Node*, Node*> visited;

    Node* dfs(Node* node) {
        if (!node) return nullptr;
        if (visited.count(node)) return visited[node];

        Node* clone = new Node(node->val);
        visited[node] = clone;

        for (auto nei : node->neighbors)
            clone->neighbors.push_back(dfs(nei));

        return clone;
    }

public:
    Node* cloneGraph(Node* node) {
        return dfs(node);
    }
};
```

---

### ✅ **30. [Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal)**

```cpp
class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if (!root) return res;

        queue<TreeNode*> q;
        q.push(root);
        bool leftToRight = true;

        while (!q.empty()) {
            int sz = q.size();
            vector<int> level(sz);

            for (int i = 0; i < sz; ++i) {
                TreeNode* node = q.front(); q.pop();
                int index = leftToRight ? i : (sz - 1 - i);
                level[index] = node->val;

                if (node->left) q.push(node->left);
                if (node->right) q.push(node->right);
            }

            res.push_back(level);
            leftToRight = !leftToRight;
        }

        return res;
    }
};
```

---

### ✅ **31. [Minesweeper](https://leetcode.com/problems/minesweeper)**

```cpp
class Solution {
    int dx[8] = {1, -1, 0, 0, 1, 1, -1, -1};
    int dy[8] = {0, 0, 1, -1, 1, -1, 1, -1};

    void dfs(vector<vector<char>>& board, int x, int y) {
        if (board[x][y] != 'E') return;

        int mines = 0;
        for (int i = 0; i < 8; ++i) {
            int nx = x + dx[i], ny = y + dy[i];
            if (nx >= 0 && ny >= 0 && nx < board.size() && ny < board[0].size())
                if (board[nx][ny] == 'M') mines++;
        }

        if (mines > 0) {
            board[x][y] = '0' + mines;
        } else {
            board[x][y] = 'B';
            for (int i = 0; i < 8; ++i) {
                int nx = x + dx[i], ny = y + dy[i];
                if (nx >= 0 && ny >= 0 && nx < board.size() && ny < board[0].size())
                    dfs(board, nx, ny);
            }
        }
    }

public:
    vector<vector<char>> updateBoard(vector<vector<char>>& board, vector<int>& click) {
        int x = click[0], y = click[1];
        if (board[x][y] == 'M') {
            board[x][y] = 'X';
        } else {
            dfs(board, x, y);
        }
        return board;
    }
};
```

---

### ✅ **32. [Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure)**

```cpp
class TrieNode {
public:
    TrieNode* children[26] = {};
    bool isEnd = false;
};

class WordDictionary {
    TrieNode* root;

    bool dfs(string& word, int i, TrieNode* node) {
        if (!node) return false;
        if (i == word.size()) return node->isEnd;

        char c = word[i];
        if (c == '.') {
            for (int j = 0; j < 26; ++j)
                if (dfs(word, i + 1, node->children[j]))
                    return true;
            return false;
        } else {
            return dfs(word, i + 1, node->children[c - 'a']);
        }
    }

public:
    WordDictionary() {
        root = new TrieNode();
    }

    void addWord(string word) {
        TrieNode* node = root;
        for (char c : word) {
            if (!node->children[c - 'a'])
                node->children[c - 'a'] = new TrieNode();
            node = node->children[c - 'a'];
        }
        node->isEnd = true;
    }

    bool search(string word) {
        return dfs(word, 0, root);
    }
};
```

---

🎉 **Done! You've now got clean C++ solutions for all 33 curated problems.**

Want me to:

- Bundle them into a `.zip` or `.cpp` file?
    
- Create a GitHub-ready repo structure?
    
- Suggest the next curated list (DP, Graphs, etc.)?
    

Just say the word.