# Minimum Path Sum
Question -> [Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/)    

### Recursion
```java
class Solution {
    public int minPathSum(int[][] grid) {
        int row = grid.length;
        int col = grid[0].length;
        return minPathSum(grid, row-1, col-1);
    }
    public int minPathSum(int[][] grid, int row, int col) {
        if(row<0 || col<0) return Integer.MAX_VALUE;
        if(row == 0 && col == 0) return grid[0][0];
        
        int up = minPathSum(grid, row-1, col);
        int left = minPathSum(grid, row, col-1);
        int sum = Math.min(up,left);
        sum += grid[row][col];
        return sum;
    }
}
```         
> `Time Complexity` : **O(2<sup>(M*N)</sup>)**          
> `Space Complexity` : **O(Path Length)**, maximun path length can be **(m-1)+(n-1)**, so S.C.-> **O((M-1)+(N-1))**
---
### Memorization
```java
class Solution {
    public int minPathSum(int[][] grid) {
        int row = grid.length;
        int col = grid[0].length;
        int[][] dp = new int[row][col];
        for(int[] arr : dp) Arrays.fill(arr,-1);
        return minPathSum(grid, row-1, col-1, dp);
    }
    public int minPathSum(int[][] grid, int row, int col, int[][] dp) {
        if(row<0 || col<0) return Integer.MAX_VALUE;
        if(row == 0 && col == 0) return dp[0][0] = grid[0][0];
        
        if(dp[row][col] != -1) return dp[row][col];
        int up = minPathSum(grid, row-1, col, dp);
        int left = minPathSum(grid, row, col-1, dp);
        int sum = Math.min(up,left);
        sum += grid[row][col];
        return dp[row][col] = sum;
    }
}
```
> `Time Complexity` : **O(M\*N)**          
> `Space Complexity` : **O(Path Length)+O(M\*N)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Solution {
    public int minPathSum(int[][] grid) {
        int row = grid.length;
        int col = grid[0].length;
        int[][] dp = new int[row][col];
        for(int r=0; r<row; r++) {
            for(int c=0; c<col; c++) {
                if(r==0 && c==0) {
                    dp[0][0] = grid[0][0];
                    continue;
                }
                int up=Integer.MAX_VALUE, left=Integer.MAX_VALUE; 
                if(r-1 >= 0) up = grid[r][c] + dp[r-1][c];
                if(c-1 >= 0) left = grid[r][c] + dp[r][c-1];
                dp[r][c] = Math.min(up,left);
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
    public int minPathSum(int[][] grid) {
        int row = grid.length;
        int col = grid[0].length;
        int[] prev = new int[col];
        
        for(int r=0; r<row; r++) {
            int[] curr = new int[col];
            for(int c=0; c<col; c++) {
                if(r==0 && c==0) {
                    curr[0] = grid[0][0];
                    continue;
                }
                int up=Integer.MAX_VALUE, left=Integer.MAX_VALUE; 
                if(r-1 >= 0) up = grid[r][c] + prev[c];
                if(c-1 >= 0) left = grid[r][c] + curr[c-1];
                curr[c] = Math.min(up,left);
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
Video Explanations -> [Minimum Path Sum](https://youtu.be/_rgTlyky1uQ?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
