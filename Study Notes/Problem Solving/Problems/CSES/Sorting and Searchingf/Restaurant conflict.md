Of course! Here is a rewritten and expanded explanation of the solutions for finding the maximum number of customers in a restaurant. This version focuses on building intuition with clearer analogies and more detailed theory for each approach.

***

## Problem: Maximum Customers

You are given the arrival and departure times for `n` customers. The goal is to find the maximum number of customers that were present in the restaurant at the same time.

**Constraints:**
*   $1 \le n \le 2 \cdot 10^5$
*   $1 \le \text{arrival\_time} < \text{departure\_time} \le 10^9$
*   All arrival and departure times are distinct.
* 
![[Pasted image 20250617182112.png]]
### The Naive Approach and Why It Fails

A simple first thought might be to simulate time itself. We could create a massive array, where each index represents a moment in time. For each customer `(a, b)`, we would iterate from time `a` to `b` and increment a counter at each of these indices.

```cpp
// Pseudocode for the naive approach
// DO NOT USE - THIS WILL NOT WORK
int timeline[1000000001]; // Array of 1 billion integers
for each customer (a, b):
  for time t from a to b-1:
    timeline[t]++;

int max_customers = 0;
for time t from 1 to 1000000000:
  max_customers = max(max_customers, timeline[t]);
```

This approach has two critical flaws given the problem's constraints:

1.  **Memory Limit:** The maximum time can be $10^9$. An array of one billion integers would require approximately 4 GB of memory, which is far beyond the typical memory limit of a programming contest (e.g., 256-512 MB).
2.  **Time Limit:** For each of the `n` customers, we might iterate up to $10^9$ times. This would be incredibly slow, leading to a "Time Limit Exceeded" error.

The key insight to solve this problem efficiently is that the number of customers **only changes at an arrival or a departure**. We don't need to check every single nanosecond; we only need to examine these specific "event" times. All the following solutions are built on this principle.

---

### Solution 1: Event-List Sweep Line

This is the most direct and intuitive application of the "event-based" insight.

#### Theory
Imagine the timeline laid out before you. An arrival is a "+1" event, and a departure is a "-1" event. If we place all these events on the timeline and then "sweep" a line from the beginning to the end, we can keep a running count of the customers.

1.  **Represent Events:** We transform each customer `(a, b)` into two distinct events:
    *   An arrival event at time `a`, which increases the customer count: `(a, +1)`.
    *   A departure event at time `b`, which decreases the customer count: `(b, -1)`.

2.  **Process Chronologically:** To correctly simulate time, we must process these events in the order they occur. Sorting all `2n` events by their time achieves this.

3.  **Sweep and Count:** We iterate through the sorted list of events. We maintain a `current_customers` counter. When we process an `(a, +1)` event, we increment the counter. When we process a `(b, -1)` event, we decrement it. After each event, the counter reflects the number of customers in the restaurant, so we compare it with our `max_customers` variable and update it if needed.

**Why it works:** Sorting the events ensures we are simulating the passage of time perfectly. By processing each change in the customer count in chronological order, our running counter will accurately reflect the number of people inside at any given moment an event occurs.

_Complexity:_
*   **Time:** `O(n log n)`. Dominated by sorting the `2n` events. The final sweep is a single `O(n)` pass.
*   **Space:** `O(n)`. We need to store `2n` events in our list.

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    // A list of events: pair of (time, type)
    // type = +1 for arrival, -1 for departure
    vector<pair<int, int>> events;
    for (int i = 0; i < n; ++i) {
        int arrival, departure;
        cin >> arrival >> departure;
        events.push_back({arrival, +1});
        events.push_back({departure, -1});
    }

    // Sort events chronologically
    sort(events.begin(), events.end());

    long long current_customers = 0;
    long long max_customers = 0;

    // Sweep through the events
    for (const auto& event : events) {
        current_customers += event.second;
        max_customers = max(max_customers, current_customers);
    }

    cout << max_customers << '\n';
}
```
> **Tie-breaking Note:** The problem statement guarantees distinct timestamps. If ties were possible (e.g., a customer arrives at the exact moment another leaves), you would need to decide the order. Typically, you process arrivals *before* departures at the same timestamp. This can be achieved by sorting pairs `(time, type)` where `type` for arrivals (`+1`) is greater than for departures (`-1`). Sorting in descending order of `type` would handle this correctly.

---

### Solution 2: Two-Pointer Method

This is a clever variation that avoids creating a combined event list, sometimes leading to slightly simpler code.

#### Theory
Instead of mixing arrivals and departures into one list, we can keep them in two separate, sorted lists. The "next event" in time will always be either the next unprocessed arrival or the next unprocessed departure. We can use two pointers, one for each list, to find out which event comes first.

1.  **Separate and Sort:** Create an array `A` for all arrival times and an array `D` for all departure times. Sort both arrays independently.
2.  **Two Pointers:** Initialize a pointer `i` to the start of the arrivals array `A` and a pointer `j` to the start of the departures array `D`.
3.  **Compare and Process:** In a loop, compare `A[i]` and `D[j]`:
    *   If `A[i] < D[j]`: The next event is an arrival. Increment the customer count and advance the arrival pointer (`i++`).
    *   If `D[j] < A[i]`: The next event is a departure. Decrement the customer count and advance the departure pointer (`j++`).
4.  **Track Maximum:** After each event is processed, update the `max_customers` variable. The loop continues until all arrivals have been handled.

**Why it works:** By always comparing the next available arrival with the next available departure, we are correctly identifying the next chronological event across both sets. This effectively simulates the sweep-line without merging the lists.

_Complexity:_
*   **Time:** `O(n log n)`. Dominated by the two initial sorts of size `n`.
*   **Space:** `O(n)`. We need to store the `n` arrival and `n` departure times.

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    vector<int> arrivals(n), departures(n);
    for (int i = 0; i < n; ++i) {
        cin >> arrivals[i] >> departures[i];
    }

    sort(arrivals.begin(), arrivals.end());
    sort(departures.begin(), departures.end());

    long long current_customers = 0;
    long long max_customers = 0;
    int i = 0; // Pointer for arrivals
    int j = 0; // Pointer for departures

    // We only need to process up to the last arrival
    while (i < n) {
        // If the next event is an arrival
        if (arrivals[i] < departures[j]) {
            current_customers++;
            i++;
        } else { // Otherwise, it's a departure
            current_customers--;
            j++;
        }
        max_customers = max(max_customers, current_customers);
    }

    cout << max_customers << '\n';
}
```

---

### Solution 3: Min-Heap of Departures

This approach processes customers in order of arrival and uses a min-heap (priority queue) to efficiently manage the customers currently inside.

#### Theory
Think of yourself as a manager at the door. You have a list of customers sorted by their arrival time. As each new customer arrives, you first need to check if anyone who was already inside has left. A min-heap is the perfect tool to instantly find the customer who will be the *next to leave*.

1.  **Sort by Arrival:** First, sort all customers based on their arrival time.
2.  **Min-Heap for Departures:** We'll use a min-heap to store the departure times of all customers who are currently in the restaurant. The top of the min-heap will always give us the earliest departure time among all customers currently inside.
3.  **Process Customers:** Iterate through the customers, sorted by arrival time `(a, b)`:
    a. **Remove departed customers:** Look at the top of the heap. While the heap is not empty and its earliest departure time is before the current customer's arrival (`heap.top() < a`), it means that customer has already left. Pop them from the heap.
    b. **Add the new customer:** The new customer `(a, b)` is now inside. Push their departure time `b` onto the heap.
    c. **Update maximum:** The current number of customers is simply the number of elements in the heap (`heap.size()`). Update `max_customers` with this value.

**Why it works:** This method correctly maintains the set of active customers at each arrival event. The min-heap provides an efficient `O(log k)` way to find and remove the earliest departures (`k` being the number of current customers), ensuring the count is accurate when a new customer arrives.

_Complexity:_
*   **Time:** `O(n log n)`. Sorting takes `O(n log n)`. Each of the `n` customers is pushed onto the heap once and popped once, with each heap operation taking `O(log n)` time.
*   **Space:** `O(n)`. For sorting the customers and for the heap, which can hold up to `n` departure times in the worst case.

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    vector<pair<int, int>> customers(n);
    for (int i = 0; i < n; ++i) {
        cin >> customers[i].first >> customers[i].second;
    }

    // Sort customers by arrival time
    sort(customers.begin(), customers.end());

    // Min-heap to store departure times of current customers
    priority_queue<int, vector<int>, greater<int>> departure_times;
    long long max_customers = 0;

    for (const auto& customer : customers) {
        int arrival = customer.first;
        int departure = customer.second;

        // Remove customers who have already left
        while (!departure_times.empty() && departure_times.top() < arrival) {
            departure_times.pop();
        }

        // Add the new customer
        departure_times.push(departure);

        // The size of the heap is the current number of customers
        max_customers = max(max_customers, (long long)departure_times.size());
    }

    cout << max_customers << '\n';
}
```
---

### Solution 4: Difference Map

This approach is conceptually very similar to the sweep-line method but uses an ordered map data structure to automatically handle sorting and aggregating events.

#### Theory
Instead of a list of events, we can use a map where the key is the `time` and the value is the `change` in the number of customers at that time. A `std::map` in C++ automatically keeps its keys sorted.

1.  **Populate the Map:** Create a map `time_to_delta`. For each customer `(a, b)`:
    *   `time_to_delta[a] += 1` (one person arrived)
    *   `time_to_delta[b] -= 1` (one person left)
    The map automatically handles cases where multiple events happen at the same time by summing the deltas.

2.  **Iterate and Accumulate:** Traverse the map. Since the map is ordered by key (time), this is equivalent to sweeping a line through the sorted events. Maintain a `current_customers` count, add the delta from each map entry, and update the `max_customers` after each step.

**Why it works:** An ordered map naturally stores the event points in chronological order and aggregates all changes (+1s and -1s) at a single point in time. Iterating through the map is therefore a clean way to implement the sweep-line logic.

_Complexity:_
*   **Time:** `O(n log n)`. Each of the `2n` insertions/updates into the map takes `O(log k)` time, where `k` is the current number of unique timestamps in the map (`k` ≤ `2n`).
*   **Space:** `O(n)`. The map will store at most `2n` distinct timestamps as keys.

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    // Map from time to the change in customer count
    map<int, int> time_to_delta;
    for (int i = 0; i < n; ++i) {
        int arrival, departure;
        cin >> arrival >> departure;
        time_to_delta[arrival]++;
        time_to_delta[departure]--;
    }

    long long current_customers = 0;
    long long max_customers = 0;

    // Iterate through the map (which is sorted by time)
    for (auto const& [time, delta] : time_to_delta) {
        current_customers += delta;
        max_customers = max(max_customers, current_customers);
    }

    cout << max_customers << '\n';
}
```
---

### Summary of Solutions

| Method | Core Idea | Time Complexity | Space Complexity | Best Use Case |
| :--- | :--- | :--- | :--- | :--- |
| **1. Event List** | Convert `(a, b)` to `(a, +1)` and `(b, -1)`, sort, and sweep. | `O(n log n)` | `O(n)` | General purpose, easy to understand. The most common approach. |
| **2. Two Pointers** | Sort arrivals and departures separately. Use two pointers to find the next chronological event. | `O(n log n)` | `O(n)` | Clean implementation, avoids pairs. Good alternative to Event List. |
| **3. Min-Heap** | Sort by arrival. Use a min-heap to track active departures. | `O(n log n)` | `O(n)` | Excellent for "online" scenarios where customers are revealed one by one. |
| **4. Difference Map** | Use an ordered map `time -> delta`. Let the map handle sorting and aggregation. | `O(n log n)` | `O(n)` | Elegant code, handles sparse time values naturally. |

For most competitive programming contexts, the **Event List** and **Two-Pointer** methods are the most straightforward and reliable choices.