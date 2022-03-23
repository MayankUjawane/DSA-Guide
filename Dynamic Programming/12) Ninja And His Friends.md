# Ninja And His Friends
Question -> [Ninja And His Friends](https://www.codingninjas.com/codestudio/problems/ninja-and-his-friends_3125885)    

### Recursion
```java
public class Solution {
    public static int maximumChocolates(int r, int c, int[][] grid) {
        return maximumChocolates(0, 0, c-1, grid, r, c);
    }
    public static int maximumChocolates(int row, int aliceCol, int bobCol, int[][] grid, int m, int n) {
        if(aliceCol < 0 || bobCol < 0 || aliceCol >= n || bobCol >= n) return Integer.MIN_VALUE;
        if(row == m-1) {
            if(aliceCol == bobCol) return grid[row][aliceCol];
            return grid[row][aliceCol]+grid[row][bobCol];
        }
        
        int max = Integer.MIN_VALUE;
        for(int i=-1; i<=1; i++) {
            for(int j=-1; j<=1; j++) {
                max = Math.max(max,maximumChocolates(row+1, aliceCol+i, bobCol+j, grid, m, n));
            }
        }
        
        if(aliceCol == bobCol) {
            max += grid[row][aliceCol];
        } else {
            max += grid[row][aliceCol] + grid[row][bobCol];
        }
        return max;
    }
}
```         
> `Time Complexity` : **O(3<sup>N</sup>\*3<sup>N</sup>)**          
> `Space Complexity` : **O(N)**    
---
### Memorization
```java
import java.util.*;
public class Solution {
    public static int maximumChocolates(int r, int c, int[][] grid) {
        int[][][] dp = new int[r][c][c];
        for(int[][] array : dp) {
            for(int[] arr : array) Arrays.fill(arr,-1);
        }
        return maximumChocolates(0, 0, c-1, grid, r, c, dp);
    }
    public static int maximumChocolates(int row, int aliceCol, int bobCol, int[][] grid, int m, int n, int[][][] dp) {
        if(aliceCol < 0 || bobCol < 0 || aliceCol >= n || bobCol >= n) return Integer.MIN_VALUE;
        if(row == m-1) {
            if(aliceCol == bobCol) return grid[row][aliceCol];
            return grid[row][aliceCol]+grid[row][bobCol];
        }
        
        if(dp[row][aliceCol][bobCol] != -1) return dp[row][aliceCol][bobCol];
        int max = Integer.MIN_VALUE;
        for(int i=-1; i<=1; i++) {
            for(int j=-1; j<=1; j++) {
                max = Math.max(max,maximumChocolates(row+1, aliceCol+i, bobCol+j, grid, m, n, dp));
            }
        }
        
        if(aliceCol == bobCol) {
            max += grid[row][aliceCol];
        } else {
            max += grid[row][aliceCol] + grid[row][bobCol];
        }
        return dp[row][aliceCol][bobCol] = max;
    }
}
```
> `Time Complexity` : **O(M\*N\*N)\*9**, M = Number of Rows, N = Number of Columns          
> `Space Complexity` : **O(N)+O(M\*N\*N)**, for Recursion Stack and dp array
---
### Tabulation
```java

```
> `Time Complexity` : **O(N\*N)**          
> `Space Complexity` : **O(N\*N)**
---
### Tabulation with Space Optimization
```java

```
> `Time Complexity` : **O(N\*N)**          
> `Space Complexity` : **O(N)+O(N)**, for prev and curr arrays.
---
Video Explanations -> [Ninja And His Friends](https://youtu.be/QGfn7JeXK54?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
