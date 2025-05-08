
## 1) **Single Hashing Method:-**
		worse case time O(mn)

```cpp
#include <iostream>
#include <string>

#define size 26
#define prime 101

bool rabinKarp(std::string pat, std::string txt) {
    int m = pat.length();
    int n = txt.length();
    int pHash = 0, tHash = 0;
    int p = 1;

    // Calculate p value (size^(m-1)) % prime
    for (int i = 0; i < m - 1; i++) {
        p = (p * size) % prime;
    }

    // Calculate initial hash values for pattern and text
    for (int i = 0; i < m; i++) {
        pHash = (size * pHash + (pat[i] - 'a')) % prime;
        tHash = (size * tHash + (txt[i] - 'a')) % prime;
    }

    // Slide over text to find matching hash
    for (int i = 0; i <= n - m; i++) { // Fix loop condition here
        // Check for hash match
        if (pHash == tHash) {
            // Check actual substring to avoid hash collision
            if (txt.substr(i, m) == pat) {
                return true;
            }
        }

        // Calculate hash for next window
        if (i < n - m) {
            tHash = (size * (tHash - (txt[i] - 'a') * p) + (txt[i + m] - 'a')) % prime;

            // Ensure tHash is non-negative
            if (tHash < 0)
                tHash += prime;
        }
    }

    return false;
}


```

## 2) **Double Hashing Method**
```cpp
#include <iostream>
#include <string>
#include <vector>

#define SIZE 256 // Size of character set
#define PRIME1 101 // First prime number for hashing
#define PRIME2 103 // Second prime number for hashing

// Function to calculate the first hash value
long long computeHash(const std::string& str, int length, long long prime) {
    long long hashValue = 0;
    for (int i = 0; i < length; i++) {
        hashValue = (hashValue * SIZE + str[i]) % prime;
    }
    return hashValue;
}

// Double hashing function
bool doubleHashingRabinKarp(const std::string& text, const std::string& pattern) {
    int n = text.length();
    int m = pattern.length();

    if (m > n) return false;

    long long pHash1 = computeHash(pattern, m, PRIME1);
    long long pHash2 = computeHash(pattern, m, PRIME2);
    
    long long tHash1 = computeHash(text, m, PRIME1);
    long long tHash2 = computeHash(text, m, PRIME2);

    for (int i = 0; i <= n - m; i++) {
        // Check if hashes match
        if (pHash1 == tHash1 && pHash2 == tHash2) {
            // Verify by comparing actual strings to avoid false positives
            if (text.substr(i, m) == pattern) {
                return true; // Match found
            }
        }

        // Update hashes for next substring
        if (i < n - m) {
            tHash1 = (tHash1 * SIZE - text[i] * pow(SIZE, m) + text[i + m]) % PRIME1;
            tHash2 = (tHash2 * SIZE - text[i] * pow(SIZE, m) + text[i + m]) % PRIME2;

            // Ensure hashes are non-negative
            if (tHash1 < 0) tHash1 += PRIME1;
            if (tHash2 < 0) tHash2 += PRIME2;
        }
    }

    return false; // No match found
}

int main() {
    std::string text = "abcdeabcde";
    std::string pattern = "cde";

    if (doubleHashingRabinKarp(text, pattern)) {
        std::cout << "Pattern found!" << std::endl;
    } else {
        std::cout << "Pattern not found." << std::endl;
    }

    return 0;
}
```