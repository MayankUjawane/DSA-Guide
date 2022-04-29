# Rod Cutting Problem
Question -> [Rod Cutting Problem](https://www.codingninjas.com/codestudio/problems/rod-cutting-problem_800284)    

### Recursion
```java
public class Solution {
    public static int cutRod(int price[], int n) {
        return cutRod(n-1, n, price);
    }
    public static int cutRod(int index, int remainingLength, int[] price) {
        if(index == 0) {
            // price at index 0 representing the price of length 1
            // so if length = 5, then we can divide it into 5 pieces of length 1
            return remainingLength*price[0];
        }
        int notTake = cutRod(index-1, remainingLength, price);
        int take = 0;
        // every index represents the price of length = (index+1)
        int rodLength = index+1;
        if(rodLength <= remainingLength) take = price[index] + cutRod(index, remainingLength-rodLength, price);
        return Math.max(take,notTake);
    }
}
```             
> `Time Complexity` : **Exponential**          
> `Space Complexity` : **O(N)**, N = Length of Rod    
---
### Memoization
```java
import java.util.*;
public class Solution {
    public static int cutRod(int price[], int n) {
        int[][] dp = new int[n][n+1];
        for(int[] arr : dp) Arrays.fill(arr,-1);
        return cutRod(n-1, n, price, dp);
    }
    public static int cutRod(int index, int remainingLength, int[] price, int[][] dp) {
        if(index == 0) {
            // price at index 0 representing the price of length 1
            // so if length = 5, then we can divide it into 5 pieces of length 1
            return remainingLength*price[0];
        }
        if(dp[index][remainingLength] != -1) return dp[index][remainingLength];
        int notTake = cutRod(index-1, remainingLength, price, dp);
        int take = 0;
        // every index represents the price of length = (index+1)
        int rodLength = index+1;
        if(rodLength <= remainingLength) take = price[index] + cutRod(index, remainingLength-rodLength, price, dp);
        return dp[index][remainingLength] = Math.max(take,notTake);
    }
}
```
> `Time Complexity` : **O(N\*N)**, N = Length of Rod          
> `Space Complexity` : **O(N)+O(N\*N)**, for Recursion Stack and dp array
---
### Tabulation
```java
public class Solution {
    public static int cutRod(int price[], int n) {
        int[][] dp = new int[n][n+1];
        // base case
        for(int length=0; length<=n; length++) {
            dp[0][length] = length*price[0];
        }
        for(int index=1; index<n; index++) {
            for(int length=0; length<=n; length++) {
                int notTake = dp[index-1][length];
                int take = 0;
                int rodLength = index+1;
                if(length >= rodLength) take = price[index] + dp[index][length-rodLength];
                dp[index][length] = Math.max(take,notTake);
            }
        }
        return dp[n-1][n];
    }
}
```
> `Time Complexity` : **O(N\*N)**             
> `Space Complexity` : **O(N\*N)**
---
### Tabulation using Two Arrays
```java
public class Solution {
    public static int cutRod(int price[], int n) {
        int[] prev = new int[n+1];
        // base case
        for(int length=0; length<=n; length++) {
            prev[length] = length*price[0];
        }
        for(int index=1; index<n; index++) {
            int[] curr = new int[n+1];
            for(int length=0; length<=n; length++) {
                int notTake = prev[length];
                int take = 0;
                int rodLength = index+1;
                if(length >= rodLength) take = price[index] + curr[length-rodLength];
                curr[length] = Math.max(take,notTake);
            }
            prev = curr;
        }
        return prev[n];
    }
}
```
> `Time Complexity` : **O(N\*N)**            
> `Space Complexity` : **O(N)+O(N)**, for prev and curr arrays.
---
### Tabulation using One Array
```java
public class Solution {
    public static int cutRod(int price[], int n) {
        int[] dp = new int[n+1];
        // base case
        for(int length=0; length<=n; length++) {
            dp[length] = length*price[0];
        }
        for(int index=1; index<n; index++) {
            for(int length=0; length<=n; length++) {
                int notTake = dp[length];
                int take = 0;
                int rodLength = index+1;
                if(length >= rodLength) take = price[index] + dp[length-rodLength];
                dp[length] = Math.max(take,notTake);
            }
        }
        return dp[n];
    }
}
```
> `Time Complexity` : **O(N\*N)**,            
> `Space Complexity` : **O(N)**
---
Video Explanations -> [Rod Cutting Problem](https://youtu.be/mO8XpGoJwuo?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
