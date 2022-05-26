# Matrix Chain Multiplication
Question -> [Matrix Chain Multiplication](https://www.codingninjas.com/codestudio/problems/matrix-chain-multiplication_975344)    

### Recursion
```java
public class Solution {
    public static int matrixMultiplication(int[] arr , int N) {
        return func(1, N-1, arr);
    }
    private static int func(int i, int j, int[] arr) {
        if(i==j) return 0;
        int min = Integer.MAX_VALUE;
        for(int k=i; k<j; k++) {
            int value = (arr[i-1]*arr[k]*arr[j]) + func(i,k,arr) + func(k+1,j,arr);
            if(value<min) min = value;
        }
        return min;
    }
}
```           
> `Time Complexity` : **Exponential**    
> `Space Complexity` : **O(N)** 
---
### Memoization
```java
import java.util.*;
public class Solution {
    public static int matrixMultiplication(int[] arr , int N) {
        int[][] dp = new int[N][N];
        for(int[] row : dp) Arrays.fill(row,-1);
        return func(1, N-1, arr, dp);
    }
    private static int func(int i, int j, int[] arr, int[][] dp) {
        if(i==j) return 0;
        if(dp[i][j] != -1) return dp[i][j];
        int min = Integer.MAX_VALUE;
        for(int k=i; k<j; k++) {
            int value = (arr[i-1]*arr[k]*arr[j]) + func(i,k,arr,dp) + func(k+1,j,arr,dp);
            if(value<min) min = value;
        }
        return dp[i][j] = min;
    }
}
```
> `Time Complexity` : **O(N<sup>3</sup>)**           
> `Space Complexity` : **O(N)+O(N\*N)**, for Recursion Stack and dp array
---
### Tabulation
```java
public class Solution {
    public static int matrixMultiplication(int[] arr , int N) {
        int[][] dp = new int[N][N];
        //base case
        for(int i=1; i<N; i++) dp[i][i] = 0;
        for(int i=N-1; i>=1; i--) {
            for(int j=i+1; j<N; j++) {
                int min = Integer.MAX_VALUE;
                for(int k=i; k<j; k++) {
                    int value = (arr[i-1]*arr[k]*arr[j]) + dp[i][k] + dp[k+1][j];
                    if(value<min) min = value;
                }
                dp[i][j] = min;
            }
        }
        return dp[1][N-1];
    }
}
```
> `Time Complexity` : **O(N<sup>3</sup>)**             
> `Space Complexity` : **O(N\*N)** 
---
Video Explanations -> [Memoization](https://youtu.be/vRVfmbCFW7Y?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY), [Tabulation](https://youtu.be/pDCXsbAw5Cg?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
