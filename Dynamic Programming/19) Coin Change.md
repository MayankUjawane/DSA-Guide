# Coin Change
Question -> [Coin Change](https://leetcode.com/problems/coin-change/)    

### Recursion
```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int n = coins.length;
        int ans = coinChange(n-1, coins, amount);
        return (ans == Integer.MAX_VALUE) ? -1 : ans;
    }
    public int coinChange(int index, int[] coins, int amount) {
        if(amount == 0) return 0;
        
        if(index == 0) {
            if(amount%coins[0] == 0) return amount/coins[0];
            return Integer.MAX_VALUE;
        }
        
        int notTake = coinChange(index-1, coins, amount);
        
        int take = Integer.MAX_VALUE;
        if(amount >= coins[index]) take = coinChange(index, coins, amount-coins[index]);
        if(take != Integer.MAX_VALUE) take += 1;

        return Math.min(take,notTake);
    }
}
```           
> `Time Complexity` : **Exponential**          
> `Space Complexity` : **O(Amount)**    
---
### Memoization
```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int n = coins.length;
        int[][] dp = new int[n][amount+1];
        for(int[] arr : dp) Arrays.fill(arr,-1);
        
        int ans = coinChange(n-1, coins, amount, dp);
        return (ans == Integer.MAX_VALUE) ? -1 : ans;
    }
    public int coinChange(int index, int[] coins, int amount, int[][] dp) {
        if(amount == 0) return 0;
        
        if(index == 0) {
            if(amount%coins[0] == 0) return amount/coins[0];
            return Integer.MAX_VALUE;
        }
        
        if(dp[index][amount] != -1) return dp[index][amount];
        
        int notTake = coinChange(index-1, coins, amount, dp);
        
        int take = Integer.MAX_VALUE;
        if(amount >= coins[index]) take = coinChange(index, coins, amount-coins[index], dp);
        if(take != Integer.MAX_VALUE) take += 1;

        return dp[index][amount] = Math.min(take,notTake);
    }
}
```
> `Time Complexity` : **O(N\*T)**, T = amount          
> `Space Complexity` : **O(T)+O(N\*T)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int n = coins.length;
        int[][] dp = new int[n][amount+1];
        // base case
        for(int a=0; a<=amount; a++) {
            if(a%coins[0] == 0) dp[0][a] = a/coins[0];
            else dp[0][a] = Integer.MAX_VALUE;
        }
        for(int index=1; index<n; index++) {
            for(int a=0; a<=amount; a++) {
                int notTake = dp[index-1][a];
                int take = Integer.MAX_VALUE;
                if(a >= coins[index]) take = dp[index][a - coins[index]];
                if(take != Integer.MAX_VALUE) take += 1;
                dp[index][a] = Math.min(take,notTake);
            }
        }
        return (dp[n-1][amount] == Integer.MAX_VALUE) ? -1 : dp[n-1][amount];
    }
}
```
> `Time Complexity` : **O(N\*T)**, T = target           
> `Space Complexity` : **O(N\*T)**
---
### Tabulation with Space Optimization
```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int n = coins.length;
        int[] prev = new int[amount+1];
        // base case
        for(int a=0; a<=amount; a++) {
            if(a % coins[0] == 0) prev[a] = a/coins[0];
            else prev[a] = Integer.MAX_VALUE;
        }
        for(int index=1; index<n; index++) {
            int[] curr = new int[amount+1];
            for(int a=0; a<=amount; a++) {
                int notTake = prev[a];
                int take = Integer.MAX_VALUE;
                if(a >= coins[index]) take = curr[a-coins[index]];
                if(take != Integer.MAX_VALUE) take += 1;
                
                curr[a] = Math.min(take,notTake);
            }
            prev = curr;
        }
        return (prev[amount] == Integer.MAX_VALUE) ? -1 : prev[amount];
    }
}
```
> `Time Complexity` : **O(N\*T)**, T = target           
> `Space Complexity` : **O(T)+O(T)**, for prev and curr arrays.
---
Video Explanations -> [Coin Change](https://youtu.be/myPeWb3Y68A?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
