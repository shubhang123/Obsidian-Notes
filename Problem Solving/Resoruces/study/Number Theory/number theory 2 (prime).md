# Prime Numbers and Related Concepts

The concept of prime numbers is a very important concept in math. This article discusses the concept of prime numbers and related properties.

## What are Prime Numbers and Composite Numbers?

**Prime numbers** are those numbers that are greater than 1 and have only two factors: 1 and itself.

**Composite numbers** are also numbers that are greater than 1, but they have at least one more divisor other than 1 and itself.

For example:

- 5 is a prime number because it is divisible only by 1 and 5.
- 6 is a composite number as it is divisible by 1, 2, 3, and 6.

---

## Naive Approach

Traverse all the numbers from 1 to `N` and count the number of divisors. If the number of divisors is equal to 2, then the given number is prime, else it is not.

```cpp
void checkprime(int N){
    int count = 0;
    for(int i = 1; i <= N; ++i)
        if(N % i == 0)
            count++;
    if(count == 2)
        cout << N << " is a prime number." << endl;
    else
        cout << N << " is not a prime number." << endl;
}
```

**Time Complexity:**
```math
O(N)
```

---

## Better Approach

If you have two positive numbers `a` and `b`, such that `a` is divisible by `b`, and:

```math
b < \sqrt{a} \Rightarrow \frac{a}{b} > \sqrt{a}
```

So, if a divisor of `N` exists that is less than `\sqrt{N}`, there will also be a divisor greater than `\sqrt{N}`. So we only need to traverse till `\sqrt{N}`.

### Example:
```math
N = 50,\quad \sqrt{50} \approx 7
```

The divisors of 50 are:
```math
\{1, 2, 5, 10, 25, 50\}
```

So it is not prime.

```cpp
void checkprime(int N) {
    int count = 0;
    for(int i = 1; i * i <= N; ++i) {
        if(N % i == 0) {
            if(i * i == N)
                count++;
            else
                count += 2;
        }
    }
    if(count == 2)
        cout << N << " is a prime number." << endl;
    else
        cout << N << " is not a prime number." << endl;
}
```

**Time Complexity:**
```math
O(\sqrt{N})
```

---

## Sieve of Eratosthenes

Use the Sieve of Eratosthenes to find all prime numbers ≤ `N`.

### Idea:
- Mark all numbers as prime initially (except 0 and 1).
- For each number `i` starting from 2 up to `\sqrt{N}`:
  - If `i` is still marked prime, mark all its multiples as composite.

```cpp
void sieve(int N) {
    bool isPrime[N+1];
    for(int i = 0; i <= N; ++i)
        isPrime[i] = true;
    isPrime[0] = false;
    isPrime[1] = false;

    for(int i = 2; i * i <= N; ++i) {
        if(isPrime[i]) {
            for(int j = i * i; j <= N; j += i)
                isPrime[j] = false;
        }
    }
}
```

### Example for \( N = 10 \):
The prime numbers are:
```math
\{2, 3, 5, 7\}
```

### Time Complexity:
```math
N \left(\frac{1}{2} + \frac{1}{3} + \frac{1}{5} + \dots \right) = O(N \log \log N)
```

---

## Fast Prime Factorization

Basic method:

```cpp
vector<int> factorize(int n) {
    vector<int> res;
    for (int i = 2; i * i <= n; ++i) {
        while (n % i == 0) {
            res.push_back(i);
            n /= i;
        }
    }
    if (n != 1)
        res.push_back(n);
    return res;
}
```

---

### Optimized with Modified Sieve:

Precompute:
```cpp
int minPrime[n + 1];
for (int i = 2; i * i <= n; ++i) {
    if (minPrime[i] == 0) {
        for (int j = i * i; j <= n; j += i) {
            if (minPrime[j] == 0)
                minPrime[j] = i;
        }
    }
}
for (int i = 2; i <= n; ++i) {
    if (minPrime[i] == 0)
        minPrime[i] = i;
}
```

Fast factorization in `O(log N)`:

```cpp
vector<int> factorize(int n) {
    vector<int> res;
    while (n != 1) {
        res.push_back(minPrime[n]);
        n /= minPrime[n];
    }
    return res;
}
```

---

## Divisor Count Formula

If:
```math
N = p_1^{a_1} \cdot p_2^{a_2} \cdots p_k^{a_k}
```

Then number of divisors:
```math
(a_1 + 1)(a_2 + 1) \cdots (a_k + 1)
```

---

## Segmented Sieve of Eratosthenes

Used to find all primes in range `[l, r]`, where `r` is large:

```cpp
bool isPrime[r - l + 1];
fill(isPrime, isPrime + (r - l + 1), true);

for (long long i = 2; i * i <= r; ++i) {
    for (long long j = max(i * i, (l + i - 1) / i * i); j <= r; j += i) {
        isPrime[j - l] = false;
    }
}

for (long long i = max(l, 2LL); i <= r; ++i) {
    if (isPrime[i - l]) {
        // i is prime
    }
}
```

**Time Complexity:**
```math
O(\sqrt{R})
```

---

## Efficient Primality Test (Recommended)

Use for single number checks:

```cpp
bool isPrime(int n) {
    if (n < 2) return false;
    for (int i = 2; i * i <= n; ++i) {
        if (n % i == 0)
            return false;
    }
    return true;
}
```
