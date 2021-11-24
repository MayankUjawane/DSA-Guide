# Number of Enclaves
Question -> [Number of Enclaves](https://leetcode.com/problems/number-of-enclaves/)    

### Implementation
```java
class Solution {
    public int numEnclaves(int[][] grid) {
        //convert all the boundary 1's into 0's
        int[][] nGrid = grid;
        int row = nGrid.length;
        int col = nGrid[0].length;
        //traversing first and last columns
        for(int i=0; i<row; i++) {
            if(nGrid[i][0] == 1){
               dfs(i, 0, nGrid); 
            }
            if(nGrid[i][col-1] == 1) {
                dfs(i, col-1, nGrid);
            }
        }
        //traversing first and last row
        for(int i=0; i<col; i++) {
            if(nGrid[0][i] == 1){
               dfs(0, i, nGrid); 
            }
            if(nGrid[row-1][i] == 1) {
                dfs(row-1, i, nGrid);
            }
        }
        
        int count = 0;
        for(int i=0; i<row; i++) {
            for(int j=0; j<col; j++) {
                if(nGrid[i][j] == 1){
                   count++; 
                } 
            }
        }
        return count;
    }
    
    private int[][] directions = {{0,1},{0,-1},{1,0},{-1,0}};
    
    public void dfs(int row, int col, int[][] grid) {
        grid[row][col] = 0;
        //marking the boundary land cells as 0
        for(int i=0; i<4; i++) {
            int nRow = row + directions[i][0];
            int nCol = col + directions[i][1];
            if(nRow >= 0 && nCol >= 0 && nRow < grid.length && nCol < grid[0].length 
               && grid[nRow][nCol] == 1) {
                dfs(nRow, nCol, grid);
            }
        }
    }
}
```
> `Time Complexity` : **O(N)**, where N = row * column      
> `Space Complexity` : **O(N)**, where N = row * column, this space is required for the recursion stack. 
---
Video Explanations -> [Number of Enclaves](https://www.youtube.com/watch?v=TXyKxUmj5XU&list=WL&index=23)  
<hr>
