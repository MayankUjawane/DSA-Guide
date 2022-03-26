# Coin Change 2
Question -> [Coin Change 2](https://leetcode.com/problems/coin-change-2/)    

### Recursion
```java
class Solution {
    public int change(int amount, int[] coins) {
        int n = coins.length;
        return change(n-1, amount, coins);
    }
    public int change(int index, int amount, int[] coins) {
        if(index == 0) {
            if(amount%coins[0] == 0) return 1;
            return 0;
        }
        int notTake = change(index-1, amount, coins);
        int take = 0;
        if(amount >= coins[index]) take = change(index, amount-coins[index], coins);
        return take+notTake;
    }
}
```           
> `Time Complexity` : **Exponential**          
> `Space Complexity` : **O(Amount)**    
---
### Memorization
```java
class Solution {
    public int change(int amount, int[] coins) {
        int n = coins.length;
        int[][] dp = new int[n][amount+1];
        for(int[] arr : dp) Arrays.fill(arr,-1);
        return change(n-1, amount, coins, dp);
    }
    public int change(int index, int amount, int[] coins, int[][] dp) {
        if(index == 0) {
            if(amount%coins[0] == 0) return 1;
            return 0;
        }
        if(dp[index][amount] != -1) return dp[index][amount];
        int notTake = change(index-1, amount, coins, dp);
        int take = 0;
        if(amount >= coins[index]) take = change(index, amount-coins[index], coins, dp);
        return dp[index][amount] = take+notTake;
    }
}
```
> `Time Complexity` : **O(N\*T)**, T = amount          
> `Space Complexity` : **O(T)+O(N\*T)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Solution {
    public int change(int amount, int[] coins) {
        int n = coins.length;
        int[][] dp = new int[n][amount+1];
        // base case
        for(int target=0; target<=amount; target++) {
            if(target%coins[0] == 0) dp[0][target] = 1;
        }
        
        for(int index=1; index<n; index++) {
            for(int target=0; target<=amount; target++) {
                int notTake = dp[index-1][target];
                int take = 0;
                if(target >= coins[index]) take = dp[index][target-coins[index]];
                dp[index][target] = take + notTake;
            }
        }
        return dp[n-1][amount];
    }
}
```
> `Time Complexity` : **O(N\*T)**, T = amount           
> `Space Complexity` : **O(N\*T)**
---
### Tabulation with Space Optimization
```java
class Solution {
    public int change(int amount, int[] coins) {
        int n = coins.length;
        int[] prev = new int[amount+1];
        // base case
        for(int target=0; target<=amount; target++) {
            if(target%coins[0] == 0) prev[target] = 1;
        }
        
        for(int index=1; index<n; index++) {
            int[] curr = new int[amount+1];
            for(int target=0; target<=amount; target++) {
                int notTake = prev[target];
                int take = 0;
                if(target >= coins[index]) take = curr[target-coins[index]];
                curr[target] = take + notTake;
            }
            prev = curr;
        }
        return prev[amount];
    }
}
```
> `Time Complexity` : **O(N\*T)**, T = amount           
> `Space Complexity` : **O(T)+O(T)**, for prev and curr arrays.
---
Video Explanations -> [Coin Change 2](https://youtu.be/HgyouUi11zk?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
