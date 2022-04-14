# Unique Paths
Question -> [Unique Paths](https://leetcode.com/problems/unique-paths/)    

### Recursion
```java
class Solution {
    public int uniquePaths(int m, int n) {
        return paths(m-1, n-1);
    }
    public int paths(int row, int col) {
        if(row<0 || col<0) return 0;
        if(row==0 && col==0) return 1;
        
        int upPaths = paths(row-1, col);
        int leftPaths = paths(row, col-1);
        return (upPaths+leftPaths);
    }
}
```         
> `Time Complexity` : **O(2<sup>(M*N)</sup>)**          
> `Space Complexity` : **O(Path Length)**, maximun path length can be (m-1)+(n-1)
---
### Memoization
```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];
        return paths(m-1, n-1, dp);
    }
    public int paths(int row, int col, int[][] dp) {
        if(row<0 || col<0) return 0;
        
        if(dp[row][col] != 0) return dp[row][col];
        if(row==0 && col==0) {
            return dp[row][col] = 1;
        }
        
        int upPaths = paths(row-1, col, dp);
        int leftPaths = paths(row, col-1, dp);
        return dp[row][col] = (upPaths+leftPaths);
    }
}
```
> `Time Complexity` : **O(M\*N)**          
> `Space Complexity` : **O(Path Length)+O(M\*N)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];
        for(int row=0; row<m; row++) {
            for(int col=0; col<n; col++) {
                if(row==0 && col==0) {
                    dp[row][col] = 1;
                    continue;
                }
                int up=0, left=0;
                if(row-1 >= 0) up = dp[row-1][col];
                if(col-1 >= 0) left = dp[row][col-1];
                dp[row][col] = up+left;
            }
        }
        return dp[m-1][n-1];
    }
}
```
> `Time Complexity` : **O(M\*N)**          
> `Space Complexity` : **O(M\*N)**
---
### Tabulation with Space Optimization
```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[] prev = new int[n];
        for(int row=0; row<m; row++) {
            int[] curr = new int[n];
            for(int col=0; col<n; col++) {
                if(row==0 && col==0) {
                    curr[col] = 1;
                    continue;
                }
                int up=0, left=0;
                if(row-1 >= 0) up = prev[col];
                if(col-1 >= 0) left = curr[col-1];
                curr[col] = up+left;
            }
            prev = curr;
        }
        return prev[n-1];
    }
}
```
> `Time Complexity` : **O(M\*N)**          
> `Space Complexity` : **O(N)+O(N)**, for prev and curr arrays.
---
### Tabulation with One Array
```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[] dp = new int[n];
        for(int row=0; row<m; row++) {
            for(int col=0; col<n; col++) {
                if(row==0 && col==0) {
                    dp[col] = 1;
                    continue;
                }
                int up=0, left=0;
                if(row-1 >= 0) up = dp[col];
                if(col-1 >= 0) left = dp[col-1];
                dp[col] = up+left;
            }
        }
        return dp[n-1];
    }
}
```
> `Time Complexity` : **O(M\*N)**          
> `Space Complexity` : **O(N)**, for dp array.
---
Video Explanations -> [Unique Paths](https://youtu.be/sdE0A2Oxofw?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
