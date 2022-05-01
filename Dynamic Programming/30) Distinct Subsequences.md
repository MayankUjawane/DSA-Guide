# Distinct Subsequences
Question -> [Distinct Subsequences](https://leetcode.com/problems/distinct-subsequences/)    

### Recursion
```java
class Solution {
    public int numDistinct(String s, String t) {
        int m = s.length();
        int n = t.length();
        return numDistinct(m-1, s, n-1, t);
    }
    private int numDistinct(int i, String s, int j, String t) {
        if(j < 0) return 1;
        if(i < 0) return 0;
        
        int take = 0;
        if(s.charAt(i) == t.charAt(j)) take = numDistinct(i-1, s, j-1, t);
        int notTake = numDistinct(i-1, s, j, t);
        return take+notTake;
    }
}
```           
> `Time Complexity` : **O(2<sup>M</sup>\*2<sup>N</sup>)**, where M = Length of string1 and N = Length of string2          
> `Space Complexity` : **O(M+N)**    
---
### Memoization
```java
class Solution {
    public int numDistinct(String s, String t) {
        int m = s.length();
        int n = t.length();
        int[][] dp = new int[m][n];
        for(int[] arr : dp) Arrays.fill(arr, -1);
        return numDistinct(m-1, s, n-1, t, dp);
    }
    private int numDistinct(int i, String s, int j, String t, int[][] dp) {
        if(j < 0) return 1;
        if(i < 0) return 0;
        
        if(dp[i][j] != -1) return dp[i][j];
        int take = 0;
        if(s.charAt(i) == t.charAt(j)) take = numDistinct(i-1, s, j-1, t, dp);
        int notTake = numDistinct(i-1, s, j, t, dp);
        return dp[i][j] = take+notTake;
    }
}
```
> `Time Complexity` : **O(M\*N)**           
> `Space Complexity` : **O(M+N)+O(M\*N)**, for Recursion Stack and dp array
---
### Memoization with Index Shifting
```java
class Solution {
    public int numDistinct(String s, String t) {
        int m = s.length();
        int n = t.length();
        int[][] dp = new int[m+1][n+1];
        for(int[] arr : dp) Arrays.fill(arr, -1);
        return numDistinct(m, s, n, t, dp);
    }
    private int numDistinct(int i, String s, int j, String t, int[][] dp) {
        if(j == 0) return 1;
        if(i == 0) return 0;
        
        if(dp[i][j] != -1) return dp[i][j];
        int take = 0;
        if(s.charAt(i-1) == t.charAt(j-1)) take = numDistinct(i-1, s, j-1, t, dp);
        int notTake = numDistinct(i-1, s, j, t, dp);
        return dp[i][j] = take+notTake;
    }
}
```
> `Time Complexity` : **O(M\*N)**            
> `Space Complexity` : **O(M+N)+O(M\*N)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Solution {
    public int numDistinct(String s, String t) {
        int m = s.length();
        int n = t.length();
        int[][] dp = new int[m+1][n+1];
        //base case
        for(int i=0; i<=m; i++) dp[i][0] = 1;
        for(int j=1; j<=n; j++) dp[0][j] = 0;
        
        for(int i=1; i<=m; i++) {
            for(int j=1; j<=n; j++) {
                int take = 0;
                if(s.charAt(i-1) == t.charAt(j-1)) take = dp[i-1][j-1];
                int notTake = dp[i-1][j];
                dp[i][j] = take + notTake;
            }
        }
        return dp[m][n];
    }
}
```
> `Time Complexity` : **O(M\*N)**             
> `Space Complexity` : **O(M\*N)** 
---
### Tabulation with Space Optimization
```java
class Solution {
    public int numDistinct(String s, String t) {
        int m = s.length();
        int n = t.length();
        int[] prev = new int[n+1];
        //base case
        for(int j=1; j<=n; j++) prev[j] = 0;
        prev[0] = 1;
        
        for(int i=1; i<=m; i++) {
            int[] curr = new int[n+1];
            curr[0] = 1;
            for(int j=1; j<=n; j++) {
                int take = 0;
                if(s.charAt(i-1) == t.charAt(j-1)) take = prev[j-1];
                int notTake = prev[j];
                curr[j] = take + notTake;
            }
            prev = curr;
        }
        
        return prev[n];
    }
}
```
> `Time Complexity` : **O(M\*N)**           
> `Space Complexity` : **O(N)+O(N)**, for prev and curr arrays.
---
### Tabulation using Single Array
```java
class Solution {
    public int numDistinct(String s, String t) {
        int m = s.length();
        int n = t.length();
        int[] dp = new int[n+1];
        //base case
        for(int j=1; j<=n; j++) dp[j] = 0;
        dp[0] = 1;
        
        for(int i=1; i<=m; i++) {
            for(int j=n; j>=1; j--) {
                int take = 0;
                if(s.charAt(i-1) == t.charAt(j-1)) take = dp[j-1];
                int notTake = dp[j];
                dp[j] = take + notTake;
            }
        }
        
        return dp[n];
    }
}
```
> `Time Complexity` : **O(M\*N)**           
> `Space Complexity` : **O(N)**, for dp arrays.
---
Video Explanations -> [Distinct Subsequences](https://youtu.be/nVG7eTiD2bY?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
