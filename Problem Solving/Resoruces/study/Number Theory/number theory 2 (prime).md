## Basic Number Theory-2: Prime Numbers and Related Concepts

### What are Prime and Composite Numbers?

- **Prime Numbers**: Numbers greater than 1 with only two factors: 1 and itself.
    
- **Composite Numbers**: Numbers greater than 1 with at least one additional divisor other than 1 and itself.
    

**Example:**

- 5 is prime (divisors: 1, 5)
    
- 6 is composite (divisors: 1, 2, 3, 6)
    

---

### Naive Approach to Check Primality

```cpp
void checkprime(int N){
    int count = 0;
    for( int i = 1; i <= N;++i )
        if( N % i == 0 )
            count++;
    if(count == 2)
        cout << N << " is a prime number." << endl;
    else
        cout << N << " is not a prime number." << endl;
}
```

**Time Complexity:** $O(N)$

---

### Better Approach (up to $\sqrt{N}$)

If a number has a divisor less than $\sqrt{N}$, it must have a corresponding divisor greater than $\sqrt{N}$.

```cpp
void checkprime(int N) {
    int count = 0;
    for( int i = 1;i * i <=N;++i ) {
         if( N % i == 0) {
             if( i * i == N )
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

**Time Complexity:** $O(\sqrt{N})$

---

### Sieve of Eratosthenes

Used to find all prime numbers $\leq N$.

```cpp
void sieve(int N) {
    bool isPrime[N+1];
    for(int i = 0; i <= N;++i) {
        isPrime[i] = true;
    }
    isPrime[0] = false;
    isPrime[1] = false;
    for(int i = 2; i * i <= N; ++i) {
         if(isPrime[i] == true) {
             for(int j = i * i; j <= N ;j += i)
                 isPrime[j] = false;
        }
    }
}
```

**Time Complexity:** $O(N \log \log N)$

![[Pasted image 20250530200750.png]]

---

### Fast Factorization using Modified Sieve

```cpp
vector<int> factorize(int n) {
    vector<int> res;
    for (int i = 2; i * i <= n; ++i) {
        while (n % i == 0) {
            res.push_back(i);
            n /= i;
        }
    }
    if (n != 1) {
        res.push_back(n);
    }
    return res;
}
```

Use precomputed smallest prime factor:

```cpp
int minPrime[n + 1];
for (int i = 2; i * i <= n; ++i) {
    if (minPrime[i] == 0) {
        for (int j = i * i; j <= n; j += i) {
            if (minPrime[j] == 0) {
                minPrime[j] = i;
            }
        }
    }
}
for (int i = 2; i <= n; ++i) {
    if (minPrime[i] == 0) {
        minPrime[i] = i;
    }
}

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

### Divisors Count from Prime Factorization

If $N = p_1^{e_1} \cdot p_2^{e_2} \cdot \ldots \cdot p_k^{e_k}$,  
then number of divisors = $(e_1+1) \cdot (e_2+1) \cdot \ldots \cdot (e_k+1)$

---

### Segmented Sieve for Range $[L, R]$

```cpp
bool isPrime[r - l + 1]; //filled by true
for (long long i = 2; i * i <= r; ++i) {
    for (long long j = max(i * i, (l + (i - 1)) / i  * i); j <= r; j += i) {
        isPrime[j - l] = false;
    }
}
for (long long i = max(l, 2); i <= r; ++i) {
    if (isPrime[i - l]) {
        // then i is prime
    }
}
```

**Time Complexity:** $O(\sqrt{R})$

---

### Recommended Prime Check for Single Number

```cpp
bool isPrime(int n) {
    for (int i = 2; i * i <= n; ++i) {
        if (n % i == 0) {
            return false;
        }
    }
    return true;
}
```

---

### Practice Problem: Number of Primes $\leq N$

**Input:** A number $N$  
**Output:** Number of primes $\leq N$

**Sample Input:**

```
10
```

**Sample Output:**

```
4
```

```c
#include <stdio.h>

int main(){
    int num;
    scanf("%d", &num);
    printf("Input number is %d.\n", num);
}
```

---

