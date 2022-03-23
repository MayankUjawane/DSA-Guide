# Unique Paths II
Question -> [Unique Paths II](https://leetcode.com/problems/unique-paths-ii/)    

### Recursion
```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int row = obstacleGrid.length;
        int col = obstacleGrid[0].length;
        return uniquePaths(obstacleGrid, row-1, col-1);
    }
    public int uniquePaths(int[][] obstacleGrid, int row, int col) {
        if(row<0 || col<0) return 0;
        if(obstacleGrid[row][col] == 1) return 0;
        if(row == 0 && col == 0) return 1;
        
        int up = uniquePaths(obstacleGrid, row-1, col);
        int left = uniquePaths(obstacleGrid, row, col-1);
        return (up+left);
    }
}
```         
> `Time Complexity` : **O(2<sup>(M*N)</sup>)**          
> `Space Complexity` : **O(Path Length)**, maximun path length can be (m-1)+(n-1)
---
### Memorization
```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int row = obstacleGrid.length;
        int col = obstacleGrid[0].length;
        int[][] dp = new int[row][col];
        for(int[] arr : dp) Arrays.fill(arr,-1);
        return uniquePaths(obstacleGrid, row-1, col-1, dp);
    }
    public int uniquePaths(int[][] obstacleGrid, int row, int col, int[][] dp) {
        if(row<0 || col<0) return 0;
        if(obstacleGrid[row][col] == 1) return dp[row][col] = 0;
        if(row == 0 && col == 0) return 1;
        
        if(dp[row][col] != -1) return dp[row][col];
        int up = uniquePaths(obstacleGrid, row-1, col, dp);
        int left = uniquePaths(obstacleGrid, row, col-1, dp);
        return dp[row][col] = (up+left);
    }
}
```
> `Time Complexity` : **O(M\*N)**          
> `Space Complexity` : **O(Path Length)+O(M\*N)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int row = obstacleGrid.length;
        int col = obstacleGrid[0].length;
        int[][] dp = new int[row][col];
        for(int r=0; r<row; r++) {
            for(int c=0; c<col; c++) {
                if(obstacleGrid[r][c] == 1) {
                    dp[r][c] = 0;
                    continue;
                }
                if(r==0 && c==0) {
                    dp[r][c] = 1;
                    continue;
                }
                int up = 0, left=0;
                if(r-1 >= 0) up = dp[r-1][c];
                if(c-1 >= 0) left = dp[r][c-1];
                dp[r][c] = up+left;
            }
        }
        return dp[row-1][col-1];
    }
}
```
> `Time Complexity` : **O(M\*N)**          
> `Space Complexity` : **O(M\*N)**
---
### Tabulation with Space Optimization
```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int row = obstacleGrid.length;
        int col = obstacleGrid[0].length;
        int[] prev = new int[col];
        
        for(int r=0; r<row; r++) {
            int[] curr = new int[col];
            for(int c=0; c<col; c++) {
                if(obstacleGrid[r][c] == 1) {
                    curr[c] = 0;
                    continue;
                }
                if(r==0 && c==0) {
                    curr[c] = 1;
                    continue;
                }
                int up = 0, left=0;
                if(r-1 >= 0) up = prev[c];
                if(c-1 >= 0) left = curr[c-1];
                curr[c] = up+left;
            }
            prev = curr;
        }
        return prev[col-1];
    }
}
```
> `Time Complexity` : **O(M\*N)**          
> `Space Complexity` : **O(N)+O(N)**, for prev and curr arrays.
---
Video Explanations -> [Unique Paths II](https://youtu.be/TmhpgXScLyY?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
