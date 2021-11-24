# Number of Islands
Question -> [Number of Islands](https://leetcode.com/problems/number-of-islands/)    

### Implementation
```java
class Solution {
    public int numIslands(char[][] grid) {
        char[][] nGrid = grid;
        int row = grid.length;
        int col = grid[0].length;
        int numberOfIslands = 0;
        for(int i=0; i<row; i++) {
            for(int j=0; j<col; j++) {
                if(nGrid[i][j] == '1') {
                    dfs(nGrid, i, j);
                    numberOfIslands++;
                }
            }
        }
        return numberOfIslands;
    }
    
    int[][] directions = {{0,1},{0,-1},{1,0},{-1,0}};
    
    public void dfs(char[][] grid, int row, int col) {
        grid[row][col] = '0';
        
        for(int i=0; i<4; i++) {
            int nRow = row + directions[i][0];
            int nCol = col + directions[i][1];
            if(isSafe(grid, nRow, nCol)) {
                dfs(grid, nRow, nCol);
            }
        }
    }
    
    private boolean isSafe(char grid[][], int row, int col) {
        return (row>=0 && col>=0 && row<grid.length && col<grid[0].length && grid[row][col]=='1');
    }
}
```
> `Time Complexity` : **O(N)**, where N = row * column      
> `Space Complexity` : **O(N) + O(N)**, where N = row * column, this space is required for the recursion stack and the for visited array (nGrid). 
---
Video Explanations -> [Number of Islands](https://www.youtube.com/watch?v=ErPZFxugYkI)   
<hr>
