# Longest Common Subsequence
Question -> [Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)    

### Recursion
```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length();
        int n = text2.length();
        return lcs(m-1, text1, n-1, text2);
    }
    public int lcs(int index1, String text1, int index2, String text2) {
        if(index1<0 || index2<0) return 0;
        // when both strings have same characters at particular indexes then move to the next indexes of both strings
        if(text1.charAt(index1) == text2.charAt(index2)) return (1 + lcs(index1-1, text1, index2-1, text2));
        // when strings have different characters then give chance to both the strings to match with next indexes
        return Math.max(lcs(index1-1, text1, index2, text2),lcs(index1, text1, index2-1, text2));
    }
}
```           
> `Time Complexity` : **O(2<sup>M</sup>\*2<sup>N</sup>)**, where M = Length of string1 and N = Length of string2          
> `Space Complexity` : **O(M+N)**    
---
### Memoization
```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length();
        int n = text2.length();
        int[][] dp = new int[m][n];
        for(int[] arr : dp) Arrays.fill(arr,-1);
        return lcs(m-1, text1, n-1, text2, dp);
    }
    public int lcs(int index1, String text1, int index2, String text2, int[][] dp) {
        if(index1<0 || index2<0) return 0;
        
        if(dp[index1][index2] != -1) return dp[index1][index2];
        // when both strings have same characters at particular indexes then move to the next idexes
        if(text1.charAt(index1) == text2.charAt(index2)) return dp[index1][index2] = (1 + lcs(index1-1, text1, index2-1, text2, dp));
        // when strings have different characters then give chance to both the strings to match with next indexes
        return dp[index1][index2] = Math.max(lcs(index1-1, text1, index2, text2, dp),lcs(index1, text1, index2-1, text2, dp));
    }
}
```
> `Time Complexity` : **O(M\*N)**           
> `Space Complexity` : **O(M+N)+O(M\*N)**, for Recursion Stack and dp array
---
### Memoization with Index Shifting
```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length();
        int n = text2.length();
        int[][] dp = new int[m+1][n+1];
        for(int[] arr : dp) Arrays.fill(arr,-1);
        return lcs(m, text1, n, text2, dp);
    }
    public int lcs(int index1, String text1, int index2, String text2, int[][] dp) {
        // now index==0 will represent the case index==-1
        if(index1==0 || index2==0) return 0;
        
        if(dp[index1][index2] != -1) return dp[index1][index2];
        // when both strings have same characters at particular indexes then move to the next idexes
        if(text1.charAt(index1-1) == text2.charAt(index2-1)) return dp[index1][index2] = (1 + lcs(index1-1, text1, index2-1, text2, dp));
        // when strings have different characters then give chance to both the strings to match with next indexes
        return dp[index1][index2] = Math.max(lcs(index1-1, text1, index2, text2, dp),lcs(index1, text1, index2-1, text2, dp));
    }
}
```
> `Time Complexity` : **O(M\*N)**            
> `Space Complexity` : **O(M+N)+O(M\*N)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length();
        int n = text2.length();
        int[][] dp = new int[m+1][n+1];
        // base case
        int length = Math.max(m,n);
        for(int index=0; index<=length; index++) {
            if(index<=m) dp[index][0] = 0;
            if(index<=n) dp[0][index] = 0;
        }
        
        for(int i=1; i<=m; i++) {
            for(int j=1; j<=n; j++) {
                if(text1.charAt(i-1) == text2.charAt(j-1)) dp[i][j] = 1 + dp[i-1][j-1];
                else dp[i][j] = Math.max(dp[i-1][j],dp[i][j-1]);
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
    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length();
        int n = text2.length();
        int[] prev = new int[n+1];
        // base case
        for(int index=0; index<=n; index++) {
            prev[index] = 0;
        }
        
        for(int i=1; i<=m; i++) {
            int[] curr = new int[n+1];
            curr[0] = 0;
            for(int j=1; j<=n; j++) {
                if(text1.charAt(i-1) == text2.charAt(j-1)) curr[j] = 1 + prev[j-1];
                else curr[j] = Math.max(prev[j],curr[j-1]);
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
Video Explanations -> [Longest Common Subsequence](https://youtu.be/NPZn9jBrX8U?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
