# Edit Distance
Question -> [Edit Distance](https://leetcode.com/problems/edit-distance/)    

### Recursion
```java
class Solution {
    public int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        return minDistance(m-1, word1, n-1, word2);
    }
    private int minDistance(int i, String word1, int j, String word2) {
        if(i < 0) return j+1; // for inserting the j+1 characters of word2 in word1
        if(j < 0) return i+1; // for deleting the remaining i+1 characters of word1
        
        if(word1.charAt(i) == word2.charAt(j)) return minDistance(i-1, word1, j-1, word2);
        
        // inserting the jth index charater of word2 in word1 at i+1 index
        int insert = 1 + minDistance(i, word1, j-1, word2); 
        // deleting the ith index charater of word1
        int delete = 1 + minDistance(i-1, word1, j, word2);
        // replacing the ith index charater of word1 with jth index charater of word2
        int replace = 1 + minDistance(i-1, word1, j-1, word2);
        
        return Math.min(insert, Math.min(delete,replace));
    }
}
```           
> `Time Complexity` : **O(3<sup>M</sup>\*3<sup>N</sup>)**, where M = Length of string1 and N = Length of string2          
> `Space Complexity` : **O(M+N)**    
---
### Memoization
```java
class Solution {
    public int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        int[][] dp = new int[m][n];
        for(int[] arr : dp) Arrays.fill(arr, -1);
        return minDistance(m-1, word1, n-1, word2, dp);
    }
    private int minDistance(int i, String word1, int j, String word2, int[][] dp) {
        if(i < 0) return j+1; // for inserting the j+1 characters of word2 in word1
        if(j < 0) return i+1; // for deleting the remaining i+1 characters of word1
        
        if(dp[i][j] != -1) return dp[i][j];
        
        if(word1.charAt(i) == word2.charAt(j)) return dp[i][j] = minDistance(i-1, word1, j-1, word2, dp);
        
        int insert = 1 + minDistance(i, word1, j-1, word2, dp); 
        int delete = 1 + minDistance(i-1, word1, j, word2, dp);
        int replace = 1 + minDistance(i-1, word1, j-1, word2, dp);
        
        return dp[i][j] = Math.min(insert, Math.min(delete,replace));
    }
}
```
> `Time Complexity` : **O(M\*N)**           
> `Space Complexity` : **O(M+N)+O(M\*N)**, for Recursion Stack and dp array
---
### Memoization with Index Shifting
```java
class Solution {
    public int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        int[][] dp = new int[m+1][n+1];
        for(int[] arr : dp) Arrays.fill(arr, -1);
        return minDistance(m, word1, n, word2, dp);
    }
    private int minDistance(int i, String word1, int j, String word2, int[][] dp) {
        if(i == 0) return j; // for inserting the j+1 characters of word2 in word1
        if(j == 0) return i; // for deleting the remaining i+1 characters of word1
        
        if(dp[i][j] != -1) return dp[i][j];
        
        if(word1.charAt(i-1) == word2.charAt(j-1)) return dp[i][j] = minDistance(i-1, word1, j-1, word2, dp);
        
        int insert = 1 + minDistance(i, word1, j-1, word2, dp); 
        int delete = 1 + minDistance(i-1, word1, j, word2, dp);
        int replace = 1 + minDistance(i-1, word1, j-1, word2, dp);
        
        return dp[i][j] = Math.min(insert, Math.min(delete,replace));
    }
}
```
> `Time Complexity` : **O(M\*N)**            
> `Space Complexity` : **O(M+N)+O(M\*N)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Solution {
    public int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        int[][] dp = new int[m+1][n+1];
        // base case
        for(int i=0; i<=m; i++) dp[i][0] = i;
        for(int j=0; j<=n; j++) dp[0][j] = j;
        
        for(int i=1; i<=m; i++) {
            for(int j=1; j<=n; j++) {
                if(word1.charAt(i-1) == word2.charAt(j-1)) {
                    dp[i][j] = dp[i-1][j-1];
                } else {
                    int insert = 1 + dp[i][j-1];
                    int delete = 1 + dp[i-1][j];
                    int replace = 1 + dp[i-1][j-1];
                    dp[i][j] = Math.min(insert,Math.min(delete,replace));
                }
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
    public int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();
        int[] prev = new int[n+1];
        // base case
        for(int j=0; j<=n; j++) prev[j] = j;
        
        for(int i=1; i<=m; i++) {
            int[] curr = new int[n+1];
            curr[0] = i;
            for(int j=1; j<=n; j++) {
                if(word1.charAt(i-1) == word2.charAt(j-1)) {
                    curr[j] = prev[j-1];
                } else {
                    int insert = 1 + curr[j-1];
                    int delete = 1 + prev[j];
                    int replace = 1 + prev[j-1];
                    curr[j] = Math.min(insert,Math.min(delete,replace));
                }
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
Video Explanations -> [Edit Distance](https://youtu.be/fJaKO8FbDdo?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
