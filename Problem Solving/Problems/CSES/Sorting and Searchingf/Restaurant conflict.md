You are given the arrival and leaving times of nnn customers in a restaurant.

What was the maximum number of customers in the restaurant at any time?

# Problem Description
# Input

The first input line has an integer n: the number of customers. After this, there are n lines that describe the customers. Each line has two integers a and b: the arrival and leaving times of a customer. You may assume that all arrival and leaving times are distinct.

# Output

Print one integer: the maximum number of customers.

# Constraints

- $1≤n≤2.10^5$
- $1≤a<b≤10^9$

# Example

```cpp
Input:

3
5 8
2 4
3 9

Output:

2
```

# Solutions

![[Pasted image 20250617182112.png]]

# 1) Naive Solution
the naive solution i thought was create a array of max size which will keep adding score to that time interval everytime it is visited, 

one input comes with (arrival, departure)
so from a loop from arrival to departure will run, incrementing the values for those indexes in the array

so therefore we can just find the max element in that array to get out answer.

limitations:
it is o(n^2) as we will visit again and again the same elements in the array

it is also impossible for the current constraints as we cant make a array for $10^9$ elements ( 1 billion elements )

## 1. Event-list sweep line

### Theory

- Treat every “moment of interest” as an **event**.
    
    - **Arrival** → `+1` customer.
        
    - **Departure** → `–1` customer.
        
- Sort the `2 n` events by time.
    
- Walk through the array once, maintaining a running counter `cur` and its maximum `ans`.
    

Because the list is sorted, we know that all changes that happen at a smaller time are processed before larger ones, which faithfully simulates real time.

_Complexity_ `O(n log n)` for the sort, `O(n)` extra memory (`2 n` pairs).

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;  cin >> n;
    vector<pair<int,int>> ev;          // (time, delta)

    for (int i = 0; i < n; ++i) {
        int a, b;  cin >> a >> b;
        ev.push_back({a, +1});         // arrival
        ev.push_back({b, -1});         // departure
    }
    sort(ev.begin(), ev.end());        // O(2n log 2n)

    long long cur = 0, ans = 0;
    for (size_t i = 0; i < ev.size(); ++i) {
        cur += ev[i].second;
        ans  = max(ans, cur);
    }
    cout << ans << '\n';
}
```

> **Tie-breaking note**  
> The statement guarantees every timestamp is unique, so we don’t need “arrivals before departures” logic. If ties **were** possible, store the delta as `(time, ±1)` but sort by `time` then by `delta` descending so `+1` is processed before `–1`.

---

## 2. Two-pointer method on two sorted arrays

### Theory

Instead of one list with tags, keep **two** arrays:

- `A[]` – arrivals
    
- `D[]` – departures
    

Sort both.  
Maintain two indices `i` (next arrival) and `j` (next departure):

|Case|Condition|Action|
|---|---|---|
|Arrival happens first|`A[i] < D[j]`|`++cur`, `++i`|
|First departure is earlier|otherwise|`--cur`, `++j`|

Because times are distinct, `==` can’t occur.  
Track the maximum at each step.

_Complexity_ `O(n log n)` for two sorts, `O(n)` memory.

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;  cin >> n;
    vector<int> A(n), D(n);
    for (int i = 0; i < n; ++i) cin >> A[i] >> D[i];

    sort(A.begin(), A.end());
    sort(D.begin(), D.end());

    int i = 0, j = 0;
    long long cur = 0, ans = 0;
    while (i < n) {                    // we stop when all arrivals handled
        if (A[i] < D[j]) {             // arrival
            ++cur; ++i;
        } else {                       // earliest departure
            --cur; ++j;
        }
        ans = max(ans, cur);
    }
    cout << ans << '\n';
}
```

---

## 3. Min-heap of current departures

### Theory

Process the customers **in order of arrival only** (one sort):

1. Sort pairs by `arrival`.
    
2. Keep a **min-heap** with all departure times of customers who are currently inside.
    
3. For each arrival `(a, b)`
    
    - Pop from the heap while `heap.top() < a` → those customers have left.
        
    - Push the new customer’s `b`.
        
    - Heap size =`cur`. Update maximum.
        

_When useful_ Streaming / online scenario: you can feed customers one by one and still keep `O(log k)` time per event (`k` = current customers).

_Complexity_ `O(n log n)` (heap push/pop in total), `O(n)` memory (heap ≤ `n`).

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;  cin >> n;
    vector<pair<int,int>> cust(n);
    for (int i = 0; i < n; ++i) cin >> cust[i].first >> cust[i].second;

    sort(cust.begin(), cust.end());      // by arrival

    priority_queue<
        int, vector<int>, greater<int>
    > pq;                                // min-heap of departures

    long long ans = 0;
    for (auto &c : cust) {
        int a = c.first, b = c.second;
        while (!pq.empty() && pq.top() < a) pq.pop();
        pq.push(b);
        ans = max<long long>(ans, pq.size());
    }
    cout << ans << '\n';
}
```

---

## 4. Difference map (ordered map of deltas)

### Theory

A `std::map<int,int>` automatically keeps keys ordered.  
For every interval:

- `diff[a] += 1`
    
- `diff[b] -= 1`
    

Then a single pass (in key order) accumulates the running total.

_Advantages_

- No large arrays even if times are sparse.
    
- Handles streaming input: each insertion is `O(log current size)`.
    

_Complexity_ `O(n log n)` insertions, `O(n)` map nodes.

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;  cin >> n;
    map<int,int> diff;                   // time → delta

    for (int i = 0; i < n; ++i) {
        int a, b;  cin >> a >> b;
        diff[a] += 1;
        diff[b] -= 1;
    }

    long long cur = 0, ans = 0;
    for (map<int,int>::iterator it = diff.begin(); it != diff.end(); ++it) {
        cur += it->second;
        ans  = max(ans, cur);
    }
    cout << ans << '\n';
}
```

---

### Summary

|Method|Sorts?|Extra DS|Time|Space|Best when…|
|---|---|---|---|---|---|
|Event list|1 (2 n events)|none|`O(n log n)`|`O(n)`|Simple, most common|
|Two-pointer|2 (A & D)|none|`O(n log n)`|`O(n)`|Slightly less memory inc.|
|Min-heap|1 (arrivals)|min-heap|`O(n log n)`|`O(n)`|Online / streaming|
|Diff-map|log-insert|ordered map|`O(n log n)`|`O(n)`|Sparse times, incremental feed|

Pick whichever matches the constraints and coding style you prefer.