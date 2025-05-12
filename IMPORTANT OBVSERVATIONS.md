wherever we want all permutations we will keep the thing we want combination of inside the first loop like in case of this

```cpp
for (int i = 1; i <= amount; i++) {
    for (int coin : coins) {
        if (i - coin >= 0)
            dp[i] += dp[i - coin];
    }
}

```

here we are only getting all the permutations of coins that can lead to the amount, which also has repeated like 
1 + 2 + 3
also 
3+2+1

if there exists any case./


Whilee...

if you want unique combinations of something we have to keep that in the outer / upper loop so that it will generate unique combinations only.

ile in this case
```cpp
for (int coin : coins) {
    for (int i = coin; i <= amount; i++) {
        dp[i] += dp[i - coin];
    }
}

```

here only unique combinations will be added

| Approach                     | Loop Order                  | Result        |     |
| ---------------------------- | --------------------------- | ------------- | --- |
| Permutations (Order matters) | Outer: amount, Inner: coins | Overcounts    |     |
| Combinations (Order doesn't) | Outer: coins, Inner: amount | Correct count |     |

---

### ✅ CORRECT VERSION (Combinations – coins outer):

```cpp
for (int coin : coins)
    for (int i = coin; i <= amount; i++)
        dp[i] += dp[i - coin];
```

Initial `dp = [1, 0, 0, 0, 0, 0]`  
(`dp[0] = 1` because there's one way to make amount 0)

---

#### 🔹 coin = 1:

- `dp[1] += dp[0] → 1`
    
- `dp[2] += dp[1] → 1`
    
- `dp[3] += dp[2] → 1`
    
- `dp[4] += dp[3] → 1`
    
- `dp[5] += dp[4] → 1`
    

`dp = [1, 1, 1, 1, 1, 1]` → 1 way to make each amount using only 1s

---

#### 🔹 coin = 2:

- `dp[2] += dp[0] → 2` (`[2]`)
    
- `dp[3] += dp[1] → 2` (`[1,2]`)
    
- `dp[4] += dp[2] → 3` (`[2,2]`)
    
- `dp[5] += dp[3] → 3` (`[1,2,2]`)
    

`dp = [1, 1, 2, 2, 3, 3]`

---

#### 🔹 coin = 5:

- `dp[5] += dp[0] → 4` (`[5]`)
    

`dp = [1, 1, 2, 2, 3, 4]`  
✅ Final answer: `4` (Correct)

---

### ❌ WRONG VERSION (Permutations – amount outer):

```cpp
for (int i = 1; i <= amount; i++)
    for (int coin : coins)
        if (i - coin >= 0)
            dp[i] += dp[i - coin];
```

Initial `dp = [1, 0, 0, 0, 0, 0]`

---

#### 🔹 i = 1:

- `coin=1 → dp[1] += dp[0] = 1`  
    `dp = [1, 1, 0, 0, 0, 0]`
    

#### 🔹 i = 2:

- `coin=1 → dp[2] += dp[1] = 1`
    
- `coin=2 → dp[2] += dp[0] = 1`  
    `dp[2] = 2` (ways: `[1,1], [2]`)
    

---

#### 🔹 i = 3:

- `coin=1 → dp[3] += dp[2] = 2`
    
- `coin=2 → dp[3] += dp[1] = 1`  
    `dp[3] = 3` (ways: `[1,1,1], [1,2], [2,1]`)
    

---

#### 🔹 i = 4:

- `coin=1 → dp[4] += dp[3] = 3`
    
- `coin=2 → dp[4] += dp[2] = 2`  
    `dp[4] = 5` (ways: `[1,1,1,1], [1,1,2], [1,2,1], [2,1,1], [2,2]`)
    

---

#### 🔹 i = 5:

- `coin=1 → dp[5] += dp[4] = 5`
    
- `coin=2 → dp[5] += dp[3] = 3`
    
- `coin=5 → dp[5] += dp[0] = 1`  
    `dp[5] = 9` (includes permutations)
    

✅ Final answer: `9` (❌ Overcounted)

---

### 🔁 Summary

|Approach|Final `dp[5]`|Reason|
|---|---|---|
|✅ Combinations|4|Only unique combinations|
|❌ Permutations|9|Counts different orders too|

Would you like me to draw a tree diagram for these paths to visualize all combinations vs permutations?