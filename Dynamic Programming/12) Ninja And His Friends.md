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
> `Time Complexity` : **O(3<sup>N</sup>\*3<sup>N</sup>)**, N = number of rows          
> `Space Complexity` : **O(N)**    
---
### Memoization
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
import java.util.*;
public class Solution {
	public static int maximumChocolates(int r, int c, int[][] grid) {
        int[][][] dp = new int[r][c][c];
        //base cases
        for(int aliceCol=0; aliceCol<c; aliceCol++) {
            for(int bobCol=0; bobCol<c; bobCol++) {
                if(aliceCol==bobCol) {
                    dp[r-1][aliceCol][bobCol] = grid[r-1][aliceCol];
                } else {
                    // add cells of both alice and bob
                    dp[r-1][aliceCol][bobCol] = grid[r-1][aliceCol] + grid[r-1][bobCol];
                }
            }
        }
        
        for(int row=r-2; row>=0; row--) {
            for(int aliceCol=0; aliceCol<c; aliceCol++) {
                for(int bobCol=0; bobCol<c; bobCol++) {
                    int max = Integer.MIN_VALUE;
                    for(int i=-1; i<=1; i++) {
                        for(int j=-1; j<=1; j++) {
                            int aliceNewCol = aliceCol+i;
                            int bobNewCol = bobCol+j;
                            if(aliceNewCol<0 || aliceNewCol>=c || bobNewCol<0 || bobNewCol>=c) continue;
                            max = Math.max(max, dp[row+1][aliceNewCol][bobNewCol]);
                        }
                    }
                    if(aliceCol == bobCol) {
                        max += grid[row][bobCol];
                    } else {
                        max += grid[row][aliceCol] + grid[row][bobCol];
                    }
                    dp[row][aliceCol][bobCol] = max;
                }
            }
        }
        return dp[0][0][c-1];
    }
}
```
> `Time Complexity` : **O(M\*N\*N)\*9**, M = Number of Rows, N = Number of Columns          
> `Space Complexity` : **O(M\*N\*N)**, for dp array
---
### Tabulation with Space Optimization
```java
import java.util.*;
public class Solution {
	public static int maximumChocolates(int r, int c, int[][] grid) {
        int[][] prev = new int[c][c];
        //base cases
        for(int aliceCol=0; aliceCol<c; aliceCol++) {
            for(int bobCol=0; bobCol<c; bobCol++) {
                if(aliceCol==bobCol) {
                    prev[aliceCol][bobCol] = grid[r-1][aliceCol];
                } else {
                    // add cells of both alice and bob
                    prev[aliceCol][bobCol] = grid[r-1][aliceCol] + grid[r-1][bobCol];
                }
            }
        }
        
        for(int row=r-2; row>=0; row--) {
            int[][] curr = new int[c][c];
            for(int aliceCol=0; aliceCol<c; aliceCol++) {
                for(int bobCol=0; bobCol<c; bobCol++) {
                    int max = Integer.MIN_VALUE;
                    for(int i=-1; i<=1; i++) {
                        for(int j=-1; j<=1; j++) {
                            int aliceNewCol = aliceCol+i;
                            int bobNewCol = bobCol+j;
                            if(aliceNewCol<0 || aliceNewCol>=c || bobNewCol<0 || bobNewCol>=c) continue;
                            max = Math.max(max, prev[aliceNewCol][bobNewCol]);
                        }
                    }
                    if(aliceCol == bobCol) {
                        max += grid[row][bobCol];
                    } else {
                        max += grid[row][aliceCol] + grid[row][bobCol];
                    }
                    curr[aliceCol][bobCol] = max;
                }
            }
            prev = curr;
        }
        return prev[0][c-1];
    }
}
```
> `Time Complexity` : **O(M\*N\*N)\*9**, M = Number of Rows, N = Number of Columns          
> `Space Complexity` : **O(N\*N) + O(N\*N)**, for prev and curr arrays.
---
Video Explanations -> [Ninja And His Friends](https://youtu.be/QGfn7JeXK54?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY)   
<hr>
