```cpp
#include <bits/stdc++.h>
using namespace std;

const int mod = 1e9 + 7;
const int MAXN = 1e6 + 5;

int dp[MAXN];

int rec(int i,vector<int>&coins,int amount){
    
}

//if you want unique combinations of something we have to keep that in the outer 
/// upper loop so that it will generate unique combinations only.
int solve(int amount, vector<int>& coins) {
        dp[0] = 1;
        for (int coin : coins) {
            for (int i = coin; i <= amount; i++) {
                dp[i] =(dp[i] + dp[i - coin])%mod;  
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
    memset(dp,0,sizeof(dp)); 
    int ans = solve(amount,coins);
    cout<< ans;
    return 0;
}```

#leetcode