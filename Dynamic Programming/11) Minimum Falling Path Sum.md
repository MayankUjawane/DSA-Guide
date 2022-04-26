# Minimum Falling Path Sum
Question -> [Minimum Falling Path Sum](https://leetcode.com/problems/minimum-falling-path-sum/)    

### Recursion
```java
class Solution {
    public int minFallingPathSum(int[][] matrix) {
        int n = matrix.length;
        int pathSum = Integer.MAX_VALUE;
        for(int col=0; col<n; col++) {
            pathSum = Math.min(pathSum, minFallingPathSum(matrix, n-1, col, n));
        }
        return pathSum;
    }
    public int minFallingPathSum(int[][] matrix, int row, int col, int n) {
        if(col<0 || col==n) return Integer.MAX_VALUE;
        if(row == 0) return matrix[0][col];
        
        int up = minFallingPathSum(matrix, row-1, col, n);
        int leftDiagonal = minFallingPathSum(matrix, row-1, col-1, n);
        int rightDiagonal = minFallingPathSum(matrix, row-1, col+1, n);
      
        int pathSum = Math.min(up, Math.min(leftDiagonal,rightDiagonal));
        pathSum += matrix[row][col];
        return pathSum;
    }
}
```         
> `Recurrence Realtion` : **T(N) = 3(T(N-1))+C**     
> `Time Complexity` : **O(N\*3<sup>(N)</sup>)**          
> `Space Complexity` : **O(N)**    
---
### Memoization
```java
class Solution {
    public int minFallingPathSum(int[][] matrix) {
        int n = matrix.length;
        int[][] dp = new int[n][n];
        for(int[] arr : dp) Arrays.fill(arr,Integer.MAX_VALUE);
        
        int pathSum = Integer.MAX_VALUE;
        for(int col=0; col<n; col++) {
            pathSum = Math.min(pathSum, minFallingPathSum(matrix, n-1, col, n, dp));
        }
        return pathSum;
    }
    public int minFallingPathSum(int[][] matrix, int row, int col, int n, int[][] dp) {
        if(col<0 || col==n) return Integer.MAX_VALUE;
        if(row == 0) return matrix[0][col];
        
        if(dp[row][col] != Integer.MAX_VALUE) return dp[row][col];
        int up = minFallingPathSum(matrix, row-1, col, n, dp);
        int leftDiagonal = minFallingPathSum(matrix, row-1, col-1, n, dp);
        int rightDiagonal = minFallingPathSum(matrix, row-1, col+1, n, dp);
        
        int pathSum = Math.min(up, Math.min(leftDiagonal,rightDiagonal));
        pathSum += matrix[row][col];
        return dp[row][col] = pathSum;
    }
}
```
> `Time Complexity` : **O(N\*N)**          
> `Space Complexity` : **O(N)+O(N\*N)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Solution {
    public int minFallingPathSum(int[][] matrix) {
        int n = matrix.length;
        int[][] dp = new int[n][n];
      
        for(int row=0; row<n; row++) {
            for(int col=0; col<n; col++) {
                if(row==0) {
                    dp[row][col] = matrix[0][col];
                    continue;
                }
                int up=Integer.MAX_VALUE, leftDiagonal=Integer.MAX_VALUE, rightDiagonal=Integer.MAX_VALUE;
                
                up = matrix[row][col] + dp[row-1][col];
                if(col-1 >= 0) leftDiagonal = matrix[row][col] + dp[row-1][col-1];
                if(col+1 < n) rightDiagonal = matrix[row][col] + dp[row-1][col+1];

                dp[row][col] = Math.min(up, Math.min(leftDiagonal,rightDiagonal));
            }
        }
        int minPath = dp[n-1][0];
        for(int col=1; col<n; col++) {
            minPath = Math.min(minPath, dp[n-1][col]);
        }
        return minPath;
    }
}
```
> `Time Complexity` : **O(N\*N)**          
> `Space Complexity` : **O(N\*N)**
---
### Tabulation with Space Optimization
```java
class Solution {
    public int minFallingPathSum(int[][] matrix) {
        int n = matrix.length;
        int[] prev = new int[n];
        
        for(int row=0; row<n; row++) {
            int[] curr = new int[n];
            for(int col=0; col<n; col++) {
                if(row==0) {
                    curr[col] = matrix[0][col];
                    continue;
                }
                
                int up=Integer.MAX_VALUE, leftDiagonal=Integer.MAX_VALUE, rightDiagonal=Integer.MAX_VALUE;
                up = matrix[row][col] + prev[col];
                if(col-1 >= 0) leftDiagonal = matrix[row][col] + prev[col-1];
                if(col+1 < n) rightDiagonal = matrix[row][col] + prev[col+1];

                curr[col] = Math.min(up, Math.min(leftDiagonal,rightDiagonal));
            }
            prev = curr;
        }
        int minPath = prev[0];
        for(int col=1; col<n; col++) {
            minPath = Math.min(minPath, prev[col]);
        }
        return minPath;
    }
}
```
> `Time Complexity` : **O(N\*N)**          
> `Space Complexity` : **O(N)+O(N)**, for prev and curr arrays.
---
Video Explanations -> [Minimum Falling Path Sum](https://youtu.be/N_aJ5qQbYA0?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
