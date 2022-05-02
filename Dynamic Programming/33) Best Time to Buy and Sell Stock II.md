# Best Time to Buy and Sell Stock II
Question -> [Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)    

### Recursion
```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        return maxProfit(0, 1, prices, n);
    }
    private int maxProfit(int index, int isBuyPossible, int[] prices, int n) {
        if(index == n) return 0;
        
        if(isBuyPossible == 1) {
            int buy = -prices[index] + maxProfit(index+1, 0, prices, n);
            int notBuy = 0 + maxProfit(index+1, 1, prices, n);
            return Math.max(buy, notBuy);
        } else {
            int sell = prices[index] + maxProfit(index+1, 1, prices, n);
            int notSell = 0 + maxProfit(index+1, 0, prices, n);
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
        int[][] dp = new int[n][2];
        for(int[] arr : dp) Arrays.fill(arr, -1);
        return maxProfit(0, 1, prices, n, dp);
    }
    private int maxProfit(int index, int isBuyPossible, int[] prices, int n, int[][] dp) {
        if(index == n) return 0;
        
        if(dp[index][isBuyPossible] != -1) return dp[index][isBuyPossible];
        
        if(isBuyPossible == 1) {
            int buy = -prices[index] + maxProfit(index+1, 0, prices, n, dp);
            int notBuy = 0 + maxProfit(index+1, 1, prices, n, dp);
            return dp[index][isBuyPossible] = Math.max(buy, notBuy);
        } else {
            int sell = prices[index] + maxProfit(index+1, 1, prices, n, dp);
            int notSell = 0 + maxProfit(index+1, 0, prices, n, dp);
            return dp[index][isBuyPossible] = Math.max(sell, notSell);
        }
    }
}
```
> `Time Complexity` : **O(N\*2)**           
> `Space Complexity` : **O(N)+O(N\*2)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        int[][] dp = new int[n+1][2];
        // base case
        dp[n][0] = dp[n][1] = 0;
        
        for(int index=n-1; index>=0; index--) {
            for(int j=0; j<=1; j++) {
                if(j == 1) {
                    int buy = -prices[index] + dp[index+1][0];
                    int notBuy = dp[index+1][1];
                    dp[index][j] = Math.max(buy,notBuy);
                } else {
                    int sell = prices[index] + dp[index+1][1];
                    int notSell = dp[index+1][0];
                    dp[index][j] = Math.max(sell, notSell);
                }
            }
        }
        return dp[0][1];
    }
}
```
> `Time Complexity` : **O(2\*N)**             
> `Space Complexity` : **O(2\*N)** 
---
### Tabulation using Two Arrays
```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        int[] front = new int[2];
        // base case
        front[0] = front[1] = 0;
        
        for(int index=n-1; index>=0; index--) {
            int[] curr = new int[2];
            for(int j=0; j<=1; j++) {
                if(j == 1) {
                    int buy = -prices[index] + front[0];
                    int notBuy = front[1];
                    curr[j] = Math.max(buy,notBuy);
                } else {
                    int sell = prices[index] + front[1];
                    int notSell = front[0];
                    curr[j] = Math.max(sell, notSell);
                }
            }
            front = curr;
        }
        return front[1];
    }
}
```
> `Time Complexity` : **O(2\*N)**           
> `Space Complexity` : **O(2)+O(2)**, for front and curr arrays.
---
### Tabulation using Four Variables
```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        int frontBuy, frontSell, currBuy, currSell;
        // base case
        frontBuy = frontSell = 0;
        
        for(int index=n-1; index>=0; index--) {
            int buy = -prices[index] + frontSell;
            int notBuy = frontBuy;
            currBuy = Math.max(buy,notBuy);

            int sell = prices[index] + frontBuy;
            int notSell = frontSell;
            currSell = Math.max(sell, notSell);
            
            frontBuy = currBuy;
            frontSell = currSell;
        }
        return frontBuy;
    }
}
```
> `Time Complexity` : **O(N)**           
> `Space Complexity` : **O(1)**
---
Video Explanations -> [Best Time to Buy and Sell Stock II](https://youtu.be/nGJmxkUJQGs?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
