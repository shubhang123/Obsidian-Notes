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

# 1) Naive Solution
the naive solution i thought was create a array of max size which will keep adding score to that time interval everytime it is visited, 

one input comes with (arrival, departure)
so from a loop from arrival to departure will run, incrementing the values for those indexes in the array

so therefore we can just find the max element in that array to get out answer.

limitations:
it is o(n^2) as we will visit again and again the same elements in the array

it is also impossible for the current constraints as we cant make a array for $10^9$ elements ( 1 billion elements )
