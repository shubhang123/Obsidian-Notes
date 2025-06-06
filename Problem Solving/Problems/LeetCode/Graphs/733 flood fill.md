Here are well-structured notes for your DFS-based **Flood Fill** implementation in C++:

---

## 🧠 Problem: Flood Fill

You're given a 2D image (grid of integers) and a starting cell `(sr, sc)`.  
You need to **change the color** of this cell and all **4-directionally connected** cells that have the **same original color** to a new given color.

---

## ✅ Key Concepts Used

- **Depth-First Search (DFS)** to recursively explore neighboring pixels.
    
- **Boundary checks** to ensure valid traversal.
    
- **Color matching** to control where the fill spreads.
    
- **In-place modification** of the image grid.


```cpp
class Solution {
   public:
    int m, n;

    void dfs(int i, int j, vector<vector<int>>& image, int oldColor, int newColor) {
        if (i < 0 || j < 0 || i >= m || j >= n)

            return;

        if (image[i][j] != oldColor)

            return;

        image[i][j] = newColor;

        dfs(i + 1, j, image, oldColor, newColor);  // down

        dfs(i - 1, j, image, oldColor, newColor);  // up

        dfs(i, j - 1, image, oldColor, newColor);  // left

        dfs(i, j + 1, image, oldColor, newColor);  // right
    }

    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int color) {
        m = image.size();

        n = image[0].size();

        if (image[sr][sc] != color)

            dfs(sr, sc, image, image[sr][sc], color);

        return image;
    }
};
```

---

## 🔧 Code Structure Explanation

### 🔹 Global Variables

```cpp
int m, n;
```

Stores the number of **rows (`m`)** and **columns (`n`)** in the image grid for easier access during DFS.

---

### 🔹 DFS Function: `dfs(i, j, image, oldColor, newColor)`

#### ✅ Base Conditions:

```cpp
if (i < 0 || j < 0 || i >= m || j >= n)
    return;  // out-of-bounds

if (image[i][j] != oldColor)
    return;  // not the target color
```

#### ✅ Color Replacement & Recursive Expansion:

```cpp
image[i][j] = newColor;  // fill this pixel

// recursive DFS calls in 4 directions
dfs(i + 1, j, ...);  // down
dfs(i - 1, j, ...);  // up
dfs(i, j - 1, ...);  // left
dfs(i, j + 1, ...);  // right
```

---

### 🔹 Main Function: `floodFill()`

#### 🔸 Setup:

```cpp
m = image.size();          // total rows
n = image[0].size();       // total columns
```

#### 🔸 Edge Case:

```cpp
if (image[sr][sc] != color)
    dfs(sr, sc, image, image[sr][sc], color);
```

Avoids unnecessary recursion if the start pixel already has the new color — this prevents infinite loops in DFS.

#### 🔸 Return:

```cpp
return image;  // return the modified image grid
```

---

## 📈 Time and Space Complexity

|Complexity|Value|
|---|---|
|**Time**|O(m × n) — in worst case, we visit every cell once|
|**Space**|O(m × n) — due to recursive stack (implicit visited tracking)|

---

## 📌 Summary

- You correctly implemented **DFS-based flood fill**.
    
- The logic avoids infinite loops and revisits by changing the color in-place.
    
- All checks are in the **right order**: boundary → color match → replace → recurse.
    
- Can be easily adapted to BFS if needed.
    

Let me know if you'd like a BFS version or visual representation explanation.