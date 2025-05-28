#dp 
```cpp



#include <bits/stdc++.h>
using namespace std;

const int mod = 1e9 + 7;
const int MAXN = 1e6 + 5;

int dp[MAXN];
//we are going over the remaining value of amount everytimne we recursively call this function
//we will check it for all the coins and then we will find the way
//if it is 0 exactly then we found a way thats why we add 1
//if it goes -ve that means it cant be made with that
//that is why it is 0
//we will keep adding the ways.
int rec(int amount,vector<int>& coins){
    if(amount == 0) return 1;
    if(amount < 0) return 0;

    if(dp[amount] != -1) return dp[amount];
    int ways = 0;
    for(int coin : coins){
        ways = (ways + rec(amount - coin,coins)) % mod;
    }
    return dp[amount] = ways;
}
//in our recusrive function we are bascially taking the entire amounnt
//and then keep decreasing the amount to get to the answer
//we will do the opposite here we will declare the base condition inside the dp
//in a way in recusrive function we are looping over the amounts, here we are doing it in a seperatre loop 
//instead of recursion , and the rest of the process is the same
int solve(int amount,vector<int>& coins){
    dp[0] = 1;

    for(int i =1; i <= amount; i++){
        for(int coin : coins){
            if(i - coin >= 0){
                dp[i] = (dp[i]+dp[i-coin]) % mod ;
            }
        }
    }
    return dp[amount];
}

int main(){
    int n,amount;
    cin>>n>>amount;

    vector<int> coins(n);
    for(int i =0; i <n ;i++){
        cin>>coins[i];
    }

    //memset(dp,0,sizeof(dp));  //for iterative 
    memset(dp,0,sizeof(dp)); // for recursive
    int ans = solve(amount,coins);
    cout<< ans;
    return 0;
}

```