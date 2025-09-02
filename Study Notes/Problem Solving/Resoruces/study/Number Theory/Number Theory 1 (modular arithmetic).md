# Math for Competitive Programming

This article discusses topics that are frequently used to solve programming problems based on math. It includes the following topics:

- Modular arithmetic
- Modular exponentiation
- Greatest Common Divisor (GCD)
- Extended Euclidean algorithm
- Modular multiplicative inverse

---

## 1. Modular Arithmetic

When one number is divided by another, the modulo operation finds the remainder. It is denoted by the `%` symbol.

### Example

Let `a = 5` and `b = 2`. Then `5 % 2 = 1`.

### Properties

1. `(a + b) % c = ((a % c) + (b % c)) % c`
2. `(a - b) % c = ((a % c) - (b % c) + c) % c`
3. `(a * b) % c = ((a % c) * (b % c)) % c`
4. `(a / b) % c = (a * b⁻¹) % c`, where `b⁻¹` is the modular inverse of `b` modulo `c`.

### Why are these properties useful?

When `a` and `b` are very large, `a * b` might exceed integer limits. Using modular arithmetic avoids overflow.

---

## 2. Modular Exponentiation

Exponentiation is computing `x^n`, i.e., multiplying `x` by itself `n` times.

### Basic Recursive Method

```cpp
int recursivePower(int x, int n) {
    if(n == 0) return 1;
    return x * recursivePower(x, n - 1);
}
```

### Basic Iterative Method

```cpp
int iterativePower(int x, int n) {
    int result = 1;
    while(n > 0) {
        result = result * x;
        n--;
    }
    return result;
}
```

### Time Complexity

- Both are O(n), not suitable for large `n`.

### Optimized (Binary Exponentiation)

#### Recursive

```cpp
int binaryExponentiation(int x, int n) {
    if(n == 0) return 1;
    else if(n % 2 == 0)
        return binaryExponentiation(x * x, n / 2);
    else
        return x * binaryExponentiation(x * x, (n - 1) / 2);
}
```

#### Iterative

```cpp
int binaryExponentiation(int x, int n) {
    int result = 1;
    while(n > 0) {
        if(n % 2 == 1)
            result = result * x;
        x = x * x;
        n = n / 2;
    }
    return result;
}
```

### Modular Version

#### Recursive

```cpp
int modularExponentiation(int x, int n, int M) {
    if(n == 0) return 1;
    else if(n % 2 == 0)
        return modularExponentiation((x * x) % M, n / 2, M);
    else
        return (x * modularExponentiation((x * x) % M, (n - 1) / 2, M)) % M;
}
```

#### Iterative

```cpp
int modularExponentiation(int x, int n, int M) {
    int result = 1;
    while(n > 0) {
        if(n % 2 == 1)
            result = (result * x) % M;
        x = (x * x) % M;
        n = n / 2;
    }
    return result;
}
```

### Complexity

- Time: O(log N)
- Space: O(log N) (recursive), O(1) (iterative)

---

## 3. Greatest Common Divisor (GCD)

### Naive Method

```cpp
int GCD(int A, int B) {
    int m = min(A, B), gcd;
    for(int i = m; i > 0; --i)
        if(A % i == 0 && B % i == 0)
            return i;
}
```

- Time: O(min(A, B))

### Euclid’s Algorithm

```cpp
int GCD(int A, int B) {
    if(B == 0) return A;
    return GCD(B, A % B);
}
```

- Time: O(log(max(A, B)))

---

## 4. Extended Euclidean Algorithm

### Goal

Find `x` and `y` such that:  
`A * x + B * y = GCD(A, B)`

### Implementation

```cpp
#include <iostream>
using namespace std;

int d, x, y;

void extendedEuclid(int A, int B) {
    if(B == 0) {
        d = A;
        x = 1;
        y = 0;
    } else {
        extendedEuclid(B, A % B);
        int temp = x;
        x = y;
        y = temp - (A / B) * y;
    }
}

int main() {
    extendedEuclid(16, 10);
    cout << "GCD: " << d << "\n";
    cout << "x: " << x << ", y: " << y << "\n";
    return 0;
}
```

- Output:
  ```
  GCD: 2
  x: 2, y: -3
  ```

- Time: O(log(max(A, B)))

---

## 5. Modular Multiplicative Inverse

### Definition

Given `A` and `M`, find `B` such that:  
`(A * B) % M = 1`

Only exists if `GCD(A, M) = 1`.

---

### Approach 1: Naive (Brute Force)

```cpp
int modInverse(int A, int M) {
    A = A % M;
    for(int B = 1; B < M; B++)
        if((A * B) % M == 1)
            return B;
}
```

- Time: O(M)

---

### Approach 2: Extended Euclidean Algorithm

```cpp
int d, x, y;

int modInverse(int A, int M) {
    extendedEuclid(A, M);
    return (x % M + M) % M; // ensure positive result
}
```

- Time: O(log(max(A, M)))

---

### Approach 3: Fermat’s Little Theorem (when M is prime)

Fermat’s theorem:  
`A^(M-1) ≡ 1 (mod M)`  
⇒ `A^(M-2) ≡ A⁻¹ (mod M)`

```cpp
int modInverse(int A, int M) {
    return modularExponentiation(A, M - 2, M);
}
```

- Time: O(log M)

---

### When is modular inverse used?

To compute division in modular arithmetic:  
`(A / B) % M = (A * B⁻¹) % M`
