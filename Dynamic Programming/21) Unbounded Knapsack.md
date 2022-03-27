# Unbounded Knapsack
Question -> [Unbounded Knapsack](https://www.codingninjas.com/codestudio/problems/unbounded-knapsack_1215029)    

### Recursion
```java
public class Solution {
    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
        return knapsack(n-1, w, profit, weight);
    }
    public static int knapsack(int index, int w, int[] profit, int[] weight) {
        if(w == 0) return 0;
        if(index == 0) {
            if(w >= weight[0]) return w/weight[0]*profit[0];
            return 0;
        }
        int notTake = knapsack(index-1, w, profit, weight);
        int take = 0;
        if(w >= weight[index]) take = profit[index] + knapsack(index, w-weight[index], profit, weight);
        return Math.max(take,notTake);
    }
}
```             
> `Time Complexity` : **Exponential**          
> `Space Complexity` : **O(W)**    
---
### Memorization
```java
import java.util.*;
public class Solution {
    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
        int[][] dp = new int[n][w+1];
        for(int[] arr : dp) Arrays.fill(arr,-1);
        return knapsack(n-1, w, profit, weight, dp);
    }
    public static int knapsack(int index, int w, int[] profit, int[] weight, int[][] dp) {
        if(w == 0) return 0;
        if(index == 0) {
            if(w >= weight[0]) return w/weight[0]*profit[0];
            return 0;
        }
        if(dp[index][w] != -1) return dp[index][w];
        int notTake = knapsack(index-1, w, profit, weight, dp);
        int take = 0;
        if(w >= weight[index]) take = profit[index] + knapsack(index, w-weight[index], profit, weight, dp);
        return dp[index][w] = Math.max(take,notTake);
    }
}
```
> `Time Complexity` : **O(N\*W)**, W = Weight Capacity          
> `Space Complexity` : **O(N)+O(N\*W)**, for Recursion Stack and dp array
---
### Tabulation
```java
public class Solution {
    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
        int[][] dp = new int[n][w+1];
        // base case
        for(int index=0; index<n; index++) dp[index][0] = 0;
        for(int wt=weight[0]; wt<=w; wt++) {
            dp[0][wt] = wt/weight[0]*profit[0];
        }
        for(int index=1; index<n; index++) {
            for(int wt=1; wt<=w; wt++) {
                int notTake = dp[index-1][wt];
                int take = 0;
                if(wt >= weight[index]) take = profit[index] + dp[index][wt-weight[index]];
                dp[index][wt] = Math.max(take,notTake);
            }
        }
        return dp[n-1][w];
    }
}
```
> `Time Complexity` : **O(N\*W)**,             
> `Space Complexity` : **O(N\*W)**
---
### Tabulation using Two Arrays
```java
public class Solution {
    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
        int[] prev = new int[w+1];
        // base case
        for(int wt=weight[0]; wt<=w; wt++) {
            prev[wt] = wt/weight[0]*profit[0];
        }
        for(int index=1; index<n; index++) {
            int[] curr = new int[w+1];
            for(int wt=0; wt<=w; wt++) {
                int notTake = prev[wt];
                int take = 0;
                if(wt >= weight[index]) take = profit[index] + curr[wt-weight[index]];
                curr[wt] = Math.max(take,notTake);
            }
            prev = curr;
        }
        return prev[w];
    }
}
```
> `Time Complexity` : **O(N\*W)**,            
> `Space Complexity` : **O(W)+O(W)**, for prev and curr arrays.
---
### Tabulation using One Array
```java
public class Solution {
    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
        int[] dp = new int[w+1];
        // base case
        for(int wt=weight[0]; wt<=w; wt++) {
            dp[wt] = wt/weight[0]*profit[0];
        }
        for(int index=1; index<n; index++) {
            for(int wt=0; wt<=w; wt++) {
                int notTake = dp[wt];
                int take = 0;
                if(wt >= weight[index]) take = profit[index] + dp[wt-weight[index]];
                dp[wt] = Math.max(take,notTake);
            }
        }
        return dp[w];
    }
}
```
> `Time Complexity` : **O(N\*W)**,            
> `Space Complexity` : **O(W)**
---
Video Explanations -> [Unbounded Knapsack](https://youtu.be/OgvOZ6OrJoY?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
