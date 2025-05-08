## Understanding the Knuth-Morris-Pratt (KMP) Algorithm

The Knuth-Morris-Pratt (KMP) algorithm is a highly efficient string-searching method that finds all occurrences of a pattern within a larger text. Unlike the naive string matching approach, which can take O(n * m) time in the worst case (where n is the text length and m is the pattern length), KMP operates in O(n + m) time. This efficiency stems from its use of the **Longest Prefix Suffix (LPS) array**, which helps the algorithm skip unnecessary comparisons by leveraging the pattern’s internal structure. In this explanation, we’ll dive into the intuition behind the KMP algorithm, explore how the LPS array is built and used, perform dry runs to illustrate the process, and then provide a C++ implementation.

---

### What is the KMP Algorithm?

The KMP algorithm, developed in 1977 by Donald Knuth, Vaughan Pratt, and James Morris, is designed to locate a pattern (substring) within a text efficiently. The key idea is to avoid backtracking in the text when a mismatch occurs, which is a major inefficiency in naive string matching. Instead, KMP uses information from previous matches to determine where to resume the comparison, making it faster and more practical for applications like text editors, search engines, and DNA sequence analysis.

The algorithm operates in two phases:
1. **Preprocessing the pattern**: Build the LPS array.
2. **Searching the text**: Use the LPS array to guide the matching process.

---

### Intuition Behind the KMP Algorithm

Imagine you’re searching for the pattern "ABABC" in the text "ABABDABABC". In naive matching, if a mismatch occurs after matching "ABAB", you’d slide the pattern back to the start and recheck characters in the text, even those you’ve already matched. This is wasteful because the text doesn’t change, and the pattern’s structure contains clues about where to resume matching.

The KMP algorithm avoids this by asking: *“When a mismatch happens, what part of the pattern can I reuse based on what I’ve already matched?”* The LPS array answers this question by telling us, for each position in the pattern, the longest portion of the pattern’s beginning (prefix) that also appears at the end (suffix) up to that point. This allows KMP to skip ahead intelligently, reducing redundant comparisons.

---

### The Role of the LPS Array

The **Longest Prefix Suffix (LPS) array** is the heart of KMP. For each position in the pattern, it stores the length of the longest proper prefix (a prefix that isn’t the entire string) that is also a suffix up to that position. This information helps the algorithm decide how far to shift the pattern forward after a mismatch, ensuring no backtracking in the text.

#### Intuition Behind Building the LPS Array

Building the LPS array is about recognizing self-similarity within the pattern. For example, in the pattern "ABABC":
- If I’ve matched "ABAB" and the next character mismatches, can I reuse part of "ABAB" to avoid starting over?
- The LPS array tells me that "AB" (a prefix) matches "AB" (a suffix) at that point, so I can skip rechecking the first "AB" and continue from there.

The construction process compares characters within the pattern, tracking the longest prefix that matches a suffix as we move forward. When a mismatch occurs, we use previously computed LPS values to "fall back" to an earlier prefix that might still match.

#### How LPS Helps in Searching

During the search:
- When characters match, we proceed as usual.
- When a mismatch occurs after some matches, the LPS array tells us where to reposition the pattern pointer, skipping characters that don’t need rechecking.
- This ensures the text pointer only moves forward, achieving linear time complexity.

---

### Dry Run: Building the LPS Array

Let’s build the LPS array for the pattern "ABABCABAB" step-by-step to see how it works.

- **Pattern**: "ABABCABAB"
- **LPS Array**: We’ll fill it position by position.

| Position | Character | Prefixes         | Suffixes         | Longest Match | LPS Value |
|----------|-----------|------------------|------------------|---------------|-----------|
| 0        | A         | None             | None             | None          | 0         |
| 1        | B         | A                | B                | None          | 0         |
| 2        | A         | A, AB            | A, BA            | A             | 1         |
| 3        | B         | A, AB, ABA       | B, AB, BAB       | AB            | 2         |
| 4        | C         | A, AB, ABA, ABAB| C, BC, ABC, BABC | None          | 0         |
| 5        | A         | ..., ABABC       | A, CA, BCA, ...  | A             | 1         |
| 6        | B         | ..., ABABCA      | B, AB, CAB, ...  | AB            | 2         |
| 7        | A         | ..., ABABCAB     | A, BA, ABA, ...  | ABA           | 3         |
| 8        | B         | ..., ABABCABA    | B, AB, BAB, ...  | ABAB          | 4         |

**Resulting LPS Array**: [0, 0, 1, 2, 0, 1, 2, 3, 4]

**Explanation**:
- **Position 0**: No proper prefix or suffix, so LPS[0] = 0.
- **Position 1**: "A" ≠ "B", no match, LPS[1] = 0.
- **Position 2**: "A" matches "A", LPS[2] = 1.
- **Position 3**: "AB" matches "AB", LPS[3] = 2.
- **Position 4**: No prefix matches "C", reset to LPS[4] = 0.
- **Position 5**: "A" matches again, LPS[5] = 1.
- **Position 6**: "AB" matches, LPS[6] = 2.
- **Position 7**: "ABA" matches, LPS[7] = 3.
- **Position 8**: "ABAB" matches, LPS[8] = 4.

This array captures the pattern’s structure, showing how much we can reuse after a mismatch.

---

### Dry Run: Searching with KMP

Now, let’s search for "ABABCABAB" in the text "ABABDABACDABABCABAB" using the LPS array [0, 0, 1, 2, 0, 1, 2, 3, 4].

- **Text**: "ABABDABACDABABCABAB"
- **Pattern**: "ABABCABAB"
- **i**: Text index, **j**: Pattern index

| Step | i | j | Text[i] | Pattern[j] | Action                          | Notes                              |
|------|---|---|---------|------------|---------------------------------|------------------------------------|
| 1    | 0 | 0 | A       | A          | Match, i++, j++                | i=1, j=1                          |
| 2    | 1 | 1 | B       | B          | Match, i++, j++                | i=2, j=2                          |
| 3    | 2 | 2 | A       | A          | Match, i++, j++                | i=3, j=3                          |
| 4    | 3 | 3 | B       | B          | Match, i++, j++                | i=4, j=4                          |
| 5    | 4 | 4 | D       | C          | Mismatch, use LPS[j-1]         | LPS[3]=2, j=2, i stays at 4       |
| 6    | 4 | 2 | D       | A          | Mismatch, use LPS[j-1]         | LPS[1]=0, j=0, i stays at 4       |
| 7    | 4 | 0 | D       | A          | Mismatch, i++, j stays         | i=5, j=0                          |
| 8    | 5 | 0 | A       | A          | Match, i++, j++                | i=6, j=1                          |
| ...  | ... | ... | ...     | ...        | (Continue matching)            | Fast-forward to key moment        |
| 9    | 10| 0 | A       | A          | Match, i++, j++                | i=11, j=1                         |
| 10   | 11| 1 | B       | B          | Match, i++, j++                | i=12, j=2                         |
| 11   | 12| 2 | A       | A          | Match, i++, j++                | i=13, j=3                         |
| 12   | 13| 3 | B       | B          | Match, i++, j++                | i=14, j=4                         |
| 13   | 14| 4 | C       | C          | Match, i++, j++                | i=15, j=5                         |
| 14   | 15| 5 | A       | A          | Match, i++, j++                | i=16, j=6                         |
| 15   | 16| 6 | B       | B          | Match, i++, j++                | i=17, j=7                         |
| 16   | 17| 7 | A       | A          | Match, i++, j++                | i=18, j=8                         |
| 17   | 18| 8 | B       | B          | Match, i++, j++                | j=9 (pattern length), full match  |

**Result**: Pattern found at index 10 (i - j = 19 - 9 = 10).

**Key Insight**:
- At step 5, the mismatch at "D" vs. "C" uses LPS[3] = 2 to jump j back to 2, avoiding rechecking "AB" in the text.
- The LPS array ensures we skip ahead efficiently, resuming where the pattern’s structure allows.

---

### Intuition Behind LPS Array Building and Search

#### LPS Building Intuition
- **Why it works**: The LPS array is like a "memory" of the pattern’s repetition. It builds incrementally by comparing the current character with the prefix we’re tracking. If they match, the prefix length grows; if not, we fall back using earlier LPS values.
- **Example**: For "ABAB", at position 3, "AB" matches "AB", so LPS[3] = 2. This tells us we can reuse "AB" after a mismatch.

#### Search Intuition
- **Why it’s efficient**: The LPS array lets us slide the pattern by the maximum amount possible after a mismatch, based on what we’ve already matched. This eliminates backtracking, as the text pointer (i) only moves forward.
- **Example**: In "ABABD" vs. "ABABC", after matching "ABAB" and mismatching at "D" vs. "C", LPS[3] = 2 lets us skip to compare "A" again, leveraging the matched "AB".

---

### C++ Implementation

Here’s a complete C++ implementation of the KMP algorithm, incorporating the LPS array construction and search:

```cpp
#include <iostream>
#include <vector>
using namespace std;

// Function to compute the LPS array
vector<int> computeLPS(const string& pattern) {
    int m = pattern.length();
    vector<int> lps(m, 0); // Initialize LPS array with zeros
    int length = 0;        // Length of the previous longest prefix suffix
    int i = 1;             // Start from second character
    while (i < m) {
        if (pattern[i] == pattern[length]) {
            length++;
            lps[i] = length;
            i++;
        } else {
            if (length != 0) {
                length = lps[length - 1]; // Fall back to previous prefix
            } else {
                lps[i] = 0;
                i++;
            }
        }
    }
    return lps;
}

// KMP search function
void KMPSearch(const string& text, const string& pattern) {
    int n = text.length();
    int m = pattern.length();
    vector<int> lps = computeLPS(pattern);
    int i = 0; // Index for text
    int j = 0; // Index for pattern
    while (i < n) {
        if (pattern[j] == text[i]) {
            j++;
            i++;
        }
        if (j == m) {
            cout << "Pattern found at index " << i - j << endl;
            j = lps[j - 1]; // Move to next possible match
        } else if (i < n && pattern[j] != text[i]) {
            if (j != 0) {
                j = lps[j - 1]; // Use LPS to skip
            } else {
                i++; // No match at start, move text pointer
            }
        }
    }
}

int main() {
    string text = "ABABDABACDABABCABAB";
    string pattern = "ABABCABAB";
    KMPSearch(text, pattern);
    return 0;
}
```

**Output**:
```
Pattern found at index 10
```

**Explanation**:
- `computeLPS`: Builds the LPS array in O(m) time by iterating through the pattern and comparing characters.
- `KMPSearch`: Uses the LPS array to search in O(n) time, printing the index where the pattern starts.

---

### Conclusion

The KMP algorithm’s brilliance lies in its use of the LPS array to eliminate redundant comparisons, achieving O(n + m) time complexity. The LPS array captures the pattern’s self-similarity, guiding both its construction and the search process. Through dry runs, we’ve seen how it skips ahead intelligently, and the code provides a practical way to implement it. This makes KMP a powerful tool for efficient string matching in real-world applications.