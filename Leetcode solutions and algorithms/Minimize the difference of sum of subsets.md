
We want to **minimize** the difference between the sums of two equal-sized subsets.

Let’s say:

- `subset1` and `subset2` are the two subsets (both of size n)
- `totalSum` = sum of all elements in the array
- `sum1` = sum of elements in subset1
- `sum2` = sum of elements in subset2

---

### ✅ Key Observations:

Since all elements are split between the two subsets:

$$
\text{sum1} + \text{sum2} = \text{totalSum}
$$

So:

$$
\text{sum2} = \text{totalSum} - \text{sum1}
$$

---

### 🔍 What we want to minimize:

We want:

$$
\left| \text{sum1} - \text{sum2} \right|
$$

Now plug in the expression for `sum2`:

$$
\left| \text{sum1} - (\text{totalSum} - \text{sum1}) \right|
$$

$$
= \left| 2 \cdot \text{sum1} - \text{totalSum} \right|
$$

Or equivalently:

$$
= \left| \text{totalSum} - 2 \cdot \text{sum1} \right|
$$

---

### ✅ Final Result:

To minimize the difference between the two equal-sized subsets,
we need to find a subset of size `n` such that:

$$
\boxed{\left| \text{totalSum} - 2 \cdot \text{subsetSum} \right|}
$$

is minimized.

---

### 💡 Intuition:

If `subsetSum` is **close to half** of `totalSum`, then both subsets will have similar sums, and their difference will be small — that’s exactly what we want.

# 1st Approach(TLE)

We are given an array `nums` of even length (say `n`).
Our task is to split it into two subsets of equal size (`n/2` each) such that the **absolute difference between their sums is minimized**.

---

### **Step 1: Calculate the total sum**

We first calculate the sum of all elements in the array and store it as `totalSum`.

This will help us later when we need to compute the sum of the *other* subset without looping over it (since `subset2 = totalSum - subset1`).

---

### **Step 2: Generate all possible subsets**

We use bitmasking to represent all possible subsets of the array.

Each bitmask of length `n` represents a subset where:

- If the `i-th` bit is set (`1`), it means `nums[i]` is included in the subset.
- If it’s `0`, then it is not included.

This gives us `2^n` total subsets.

---

### **Step 3: Filter subsets of size `n/2`**

Out of all `2^n` subsets, we are only interested in those which contain **exactly `n/2` elements**.

This is because we want both subsets to be of equal length.
We check this using `popcount` (number of 1s in the bitmask).

---

### **Step 4: For each valid subset, calculate its sum**

For every bitmask that represents a valid subset (i.e., has exactly `n/2` set bits), we:

- Traverse through all `n` bits
- If the bit is set, we add the corresponding element from `nums` to `subsetSum`.

This gives us the total of the current subset.

---

### **Step 5: Calculate the sum of the other subset**

Since we know the total sum of the array, the sum of the other subset is simply:

$$
\text{otherSubsetSum} = \text{totalSum} - \text{subsetSum}
$$

---

### **Step 6: Compute the difference**

We want the absolute difference between the two subsets:

$$
\text{diff} = |\text{subsetSum} - \text{otherSubsetSum}|
$$

Using the formula above:

$$
\text{diff} = |\text{subsetSum} - (totalSum - subsetSum)|
= |2 \cdot subsetSum - totalSum|
= |totalSum - 2 \cdot subsetSum|
$$

This is the key formula that helps us avoid recomputing the other subset’s sum.

---

### **Step 7: Track the minimum difference**

We keep updating a variable `best` with the minimum difference found so far.

---

### **Step 8: Return the result**

After checking all valid subsets, we return the smallest difference stored in `best`.

---

### ✅ Summary

- We check all possible ways to split the array into two equal halves.
- For each way, we compute how balanced their sums are.
- The formula `abs(totalSum - 2 * subsetSum)` gives us the difference.
- We return the minimum such value.

This approach fails for n over 13 which needs us to get a better approach by