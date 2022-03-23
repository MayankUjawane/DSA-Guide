# Triangle
Question -> [Triangle](https://leetcode.com/problems/triangle/)    

### Recursion
```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        return minimumTotal(triangle, 0, 0, triangle.size());    
    }
    public int minimumTotal(List<List<Integer>> triangle, int row, int col, int n) {
        if(row == n-1) return triangle.get(row).get(col);
        
        int down = triangle.get(row).get(col) + minimumTotal(triangle, row+1, col, n);
        int diagonal = triangle.get(row).get(col) + minimumTotal(triangle, row+1, col+1, n);
        
        return Math.min(down,diagonal);
    }
}
```         
> `Time Complexity` : **O(2<sup>(N*N)</sup>)**, where N = Length of last row          
> `Space Complexity` : **O(N)**, where N = Height of Triangle
---
### Memorization
```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int r = triangle.size();
        int c = triangle.get(r-1).size();
        int[][] dp = new int[r][c];
        for(int[] arr : dp) Arrays.fill(arr,Integer.MIN_VALUE);
        return minimumTotal(triangle, 0, 0, r, dp);    
    }
    public int minimumTotal(List<List<Integer>> triangle, int row, int col, int n, int[][] dp) {
        if(row == n-1) return triangle.get(row).get(col);
        
        if(dp[row][col] != Integer.MIN_VALUE) return dp[row][col];
        int down = triangle.get(row).get(col) + minimumTotal(triangle, row+1, col, n, dp);
        int diagonal = triangle.get(row).get(col) + minimumTotal(triangle, row+1, col+1, n, dp);
        return dp[row][col] = Math.min(down,diagonal);
    }
}
```
> `Time Complexity` : **O(N\*N)**, where N = Length of Last Row      
> At max, there will be (half of, due to triangle) N\*N calls of recursion.    
> `Space Complexity` : **O(N)+O(N\*N)**, for Recursion Stack and dp array
---
### Tabulation
```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int r = triangle.size();
        int c = triangle.get(r-1).size();
        int[][] dp = new int[r][c];
        // base case
        for(int col=0; col<c; col++) {
            dp[r-1][col] = triangle.get(r-1).get(col);
        }
        for(int row=r-2; row>=0; row--) {
            for(int col=row; col>=0; col--) {
                int up = triangle.get(row).get(col) + dp[row+1][col];
                int diagonal = triangle.get(row).get(col) + dp[row+1][col+1];
                dp[row][col] = Math.min(up,diagonal);
            }
        }
        return dp[0][0];
    }
}
```
> `Time Complexity` : **O(N\*N)**          
> `Space Complexity` : **O(N\*N)**
---
### Tabulation with Space Optimization
```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int r = triangle.size();
        int c = triangle.get(r-1).size();
        int[] prev = new int[c];
        // base case
        for(int col=0; col<c; col++) {
            prev[col] = triangle.get(r-1).get(col);
        }
        for(int row=r-2; row>=0; row--) {
            int[] curr = new int[row+1];
            for(int col=row; col>=0; col--) {
                int up = triangle.get(row).get(col) + prev[col];
                int diagonal = triangle.get(row).get(col) + prev[col+1];
                curr[col] = Math.min(up,diagonal);
            }
            prev = curr;
        }
        return prev[0];
    }
}
```
> `Time Complexity` : **O(N\*N)**          
> `Space Complexity` : **O(N)+O(N)**, for prev and curr arrays.
---
Video Explanations -> [Triangle](https://youtu.be/SrP-PiLSYC0?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
