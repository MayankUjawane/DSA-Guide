# Best Time to Buy and Sell Stock III
Question -> [Best Time to Buy and Sell Stock III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)    

### Recursion
```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        return maxProfit(0, 1, prices, n, 0);
    }
    private int maxProfit(int index, int isBuyPossible, int[] prices, int n, int transaction) {
        if(index == n || transaction == 2) return 0;
        
        if(isBuyPossible == 1) {
            int buy = -prices[index] + maxProfit(index+1, 0, prices, n, transaction);
            int notBuy = 0 + maxProfit(index+1, 1, prices, n, transaction);
            return Math.max(buy, notBuy);
        } else {
            int sell = prices[index] + maxProfit(index+1, 1, prices, n, transaction+1);
            int notSell = 0 + maxProfit(index+1, 0, prices, n, transaction);
            return Math.max(sell, notSell);
        }
    }
}
```           
> `Time Complexity` : **O(2<sup>N</sup>)**, where N = prices.length          
> `Space Complexity` : **O(N)**    
---
### Memoization
```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        int[][][] dp = new int[n][2][2];
        for(int[][] arr : dp) {
            for(int[] row : arr) Arrays.fill(row,-1);
        }
        return maxProfit(0, 1, prices, n, 0, dp);
    }
    private int maxProfit(int index, int isBuyPossible, int[] prices, int n, int transaction, int[][][] dp) {
        if(index == n || transaction == 2) return 0;
        
        if(dp[index][isBuyPossible][transaction] != -1) return dp[index][isBuyPossible][transaction];
        
        if(isBuyPossible == 1) {
            int buy = -prices[index] + maxProfit(index+1, 0, prices, n, transaction, dp);
            int notBuy = 0 + maxProfit(index+1, 1, prices, n, transaction, dp);
            return dp[index][isBuyPossible][transaction] = Math.max(buy, notBuy);
        } else {
            int sell = prices[index] + maxProfit(index+1, 1, prices, n, transaction+1, dp);
            int notSell = 0 + maxProfit(index+1, 0, prices, n, transaction, dp);
            return dp[index][isBuyPossible][transaction] = Math.max(sell, notSell);
        }
    }
}
```
> `Time Complexity` : **O(N\*2\*2)**           
> `Space Complexity` : **O(N)+O(N\*2\*2)**, for Recursion Stack and dp array
---
### Memoization with 2D Array
```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        int[][] dp = new int[n][4];
        for(int[] arr : dp) Arrays.fill(arr,-1);
        return maxProfit(0, 0, prices, n, dp);
    }
    private int maxProfit(int index, int state, int[] prices, int n, int[][] dp) {
        if(index == n || state == 4) return 0;
        
        if(dp[index][state] != -1) return dp[index][state];
        
        if(state%2 == 0) {
            int buy = -prices[index] + maxProfit(index+1, state+1, prices, n, dp);
            int notBuy = 0 + maxProfit(index+1, state, prices, n, dp);
            return dp[index][state] = Math.max(buy, notBuy);
        } else {
            int sell = prices[index] + maxProfit(index+1, state+1, prices, n, dp);
            int notSell = 0 + maxProfit(index+1, state, prices, n, dp);
            return dp[index][state] = Math.max(sell, notSell);
        }
    }
}
```
> `Time Complexity` : **O(N\*4)**           
> `Space Complexity` : **O(N)+O(N\*4)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        int[][][] dp = new int[n+1][2][3];
        // base case
        for(int index=0; index<=n; index++) {
            for(int buy=0; buy<=1; buy++) {
                dp[index][buy][2] = 0;
            }
        }
        for(int buy=0; buy<=1; buy++) {
            for(int transaction=0; transaction<=1; transaction++) {
                dp[n][buy][transaction] = 0;
            }
        }
        
        for(int index=n-1; index>=0; index--) {
            for(int b=0; b<=1; b++) {
                for(int transaction=0; transaction<=1; transaction++) {
                    if(b == 1) {
                        int buy = -prices[index] + dp[index+1][0][transaction];
                        int notBuy = 0 + dp[index+1][1][transaction];
                        dp[index][b][transaction] = Math.max(buy, notBuy);
                    } else {
                        int sell = prices[index] + dp[index+1][1][transaction+1];
                        int notSell = 0 + dp[index+1][0][transaction];
                        dp[index][b][transaction] = Math.max(sell, notSell);
                    }
                }
            }
        }
        return dp[0][1][0];
    }
}
```
> `Time Complexity` : **O(N\*2\*3)**             
> `Space Complexity` : **O(N\*2\*3)** 
---
### Tabulation with Space Optimization
```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        int[][] front = new int[2][3];
        // base case
        for(int buy=0; buy<=1; buy++) {
            for(int transaction=0; transaction<=1; transaction++) {
                front[buy][transaction] = 0;
            }
        }
        
        for(int index=n-1; index>=0; index--) {
            int[][] curr = new int[2][3];
            for(int b=0; b<=1; b++) {
                for(int transaction=0; transaction<=1; transaction++) {
                    if(b == 1) {
                        int buy = -prices[index] + front[0][transaction];
                        int notBuy = 0 + front[1][transaction];
                        curr[b][transaction] = Math.max(buy, notBuy);
                    } else {
                        int sell = prices[index] + front[1][transaction+1];
                        int notSell = 0 + front[0][transaction];
                        curr[b][transaction] = Math.max(sell, notSell);
                    }
                }
            }
            front = curr;
        }
        return front[1][0];
    }
}
```
> `Time Complexity` : **O(N\*2\*3)**           
> `Space Complexity` : **O(2\*3)+O(2\*3)**, for front and curr arrays.
---
### Tabulation with 2D Array
```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        int[][] dp = new int[n+1][5];
        // base case
        for(int index=0; index<=n; index++) {
            dp[index][4] = 0;
        }
        for(int state=0; state<4; state++) {
            dp[n][state] = 0;
        }
        
        for(int index=n-1; index>=0; index--) {
            for(int state=0; state<4; state++) {
                if(state%2 == 0) {
                    int buy = -prices[index] + dp[index+1][state+1];
                    int notBuy = 0 + dp[index+1][state];
                    dp[index][state] = Math.max(buy, notBuy);
                } else {
                    int sell = prices[index] + dp[index+1][state+1];
                    int notSell = 0 + dp[index+1][state];
                    dp[index][state] = Math.max(sell, notSell);
                }
            }
        }
        return dp[0][0];
    }
}
```
> `Time Complexity` : **O(N\*4)**             
> `Space Complexity` : **O(N\*5)** 
---
### Tabulation with Space Optimization(2D Array)
```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        int[] front = new int[5];
        // base case
        for(int state=0; state<4; state++) {
            front[state] = 0;
        }
        
        for(int index=n-1; index>=0; index--) {
            int[] curr = new int[5];
            for(int state=0; state<4; state++) {
                if(state%2 == 0) {
                    int buy = -prices[index] + front[state+1];
                    int notBuy = 0 + front[state];
                    curr[state] = Math.max(buy, notBuy);
                } else {
                    int sell = prices[index] + front[state+1];
                    int notSell = 0 + front[state];
                    curr[state] = Math.max(sell, notSell);
                }
            }
            front = curr;
        }
        return front[0];
    }
}
```
> `Time Complexity` : **O(N\*4)**           
> `Space Complexity` : **O(5)+O(5)**, for front and curr arrays.
---
Video Explanations -> [Best Time to Buy and Sell Stock III](https://youtu.be/-uQGzhYj8BQ?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
