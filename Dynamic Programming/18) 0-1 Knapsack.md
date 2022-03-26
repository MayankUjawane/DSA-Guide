# 0/1 Knapsack
Question -> [0/1 Knapsack](https://www.codingninjas.com/codestudio/problems/0-1-knapsack_920542)    

### Recursion
```java
public class Solution{
    static int knapsack(int[] weight, int[] value, int n, int maxWeight) {
        return knapsack(n-1, weight, value, maxWeight);
    }
    public static int knapsack(int index, int[] weight, int[] value, int maxWeight) {
        // if the weight array contains weight 0 also then we cannot apply this check, then we have to move till index=0
        if(maxWeight == 0) {
            return 0;
        }
        if(index == 0) {
            if(maxWeight >= weight[0]) return value[0];
            return 0;
        }
        int notTake = knapsack(index-1, weight, value, maxWeight);
        int take = 0;
        if(maxWeight >= weight[index]) take = value[index] + knapsack(index-1, weight, value, maxWeight-weight[index]);
        return Math.max(take,notTake);
    }
}
```         
> `Recurrence Realtion` : **T(N) = 2(T(N-1))+C**     
> `Time Complexity` : **O(2<sup>(N)</sup>)**          
> `Space Complexity` : **O(N)**    
---
### Memorization
```java
import java.util.*;
public class Solution{
    static int knapsack(int[] weight, int[] value, int n, int maxWeight) {
        int[][] dp = new int[n][maxWeight+1];
        for(int[] arr : dp) Arrays.fill(arr,-1);
        return knapsack(n-1, weight, value, maxWeight, dp);
    }
    public static int knapsack(int index, int[] weight, int[] value, int maxWeight, int[][] dp) {
        if(maxWeight == 0) {
            return 0;
        }
        if(index == 0) {
            if(maxWeight >= weight[0]) return value[0];
            return 0;
        }
        if(dp[index][maxWeight] != -1) return dp[index][maxWeight];
        int notTake = knapsack(index-1, weight, value, maxWeight, dp);
        int take = Integer.MIN_VALUE;
        if(maxWeight >= weight[index]) take = value[index] + knapsack(index-1, weight, value, maxWeight-weight[index], dp);
        return dp[index][maxWeight] = Math.max(take,notTake);
    }
}
```
> `Time Complexity` : **O(N\*W)**, W = Max Weight          
> `Space Complexity` : **O(N)+O(N\*W)**, for Recursion Stack and dp array
---
### Tabulation
```java
public class Solution{
    static int knapsack(int[] weight, int[] value, int n, int maxWeight) {
        int[][] dp = new int[n][maxWeight+1];
        // base case
        for(int w=0; w<=maxWeight; w++) {
            if(w >= weight[0]) dp[0][w] = value[0];
            else dp[0][w] = 0;
        }
        for(int index=1; index<n; index++) {
            for(int w=0; w<=maxWeight; w++) {
                int notTake = dp[index-1][w];
                int take = Integer.MIN_VALUE;
                if(w >= weight[index]) take = value[index] + dp[index-1][w-weight[index]];
                dp[index][w] = Math.max(take,notTake);
            }
        }
        return dp[n-1][maxWeight];
    }
}
```
> `Time Complexity` : **O(N\*W)**,             
> `Space Complexity` : **O(N\*W)**
---
### Tabulation using Two Arrays
```java
public class Solution{
    static int knapsack(int[] weight, int[] value, int n, int maxWeight) {
        int[] prev = new int[maxWeight+1];
        // base case
        for(int w=0; w<=maxWeight; w++) {
            if(w >= weight[0]) prev[w] = value[0];
            else prev[w] = 0;
        }
        for(int index=1; index<n; index++) {
            int[] curr = new int[maxWeight+1];
            for(int w=0; w<=maxWeight; w++) {
                int notTake = prev[w];
                int take = Integer.MIN_VALUE;
                if(w >= weight[index]) take = value[index] + prev[w - weight[index]];
                curr[w] = Math.max(take,notTake);
            }
            prev = curr;
        }
        return prev[maxWeight];
    }
}
```
> `Time Complexity` : **O(N\*W)**,            
> `Space Complexity` : **O(W)+O(W)**, for prev and curr arrays.
---
### Tabulation using One Array
```java
public class Solution{
    static int knapsack(int[] weight, int[] value, int n, int maxWeight) {
        int[] dp = new int[maxWeight+1];
        // base case
        for(int w=weight[0]; w<=maxWeight; w++) {
            dp[w] = value[0];
        }
        for(int index=1; index<n; index++) {
            for(int w=maxWeight; w>=0; w--) {
                int notTake = dp[w];
                int take = Integer.MIN_VALUE;
                if(w >= weight[index]) take = value[index] + dp[w - weight[index]];
                dp[w] = Math.max(take,notTake);
            }
        }
        return dp[maxWeight];
    }
}
```
> `Time Complexity` : **O(N\*W)**,            
> `Space Complexity` : **O(W)**
---
Video Explanations -> [0/1 Knapsack](https://youtu.be/GqOmJHQZivw?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
