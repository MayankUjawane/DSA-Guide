# Number of Distinct Islands
Question -> [Number of Distinct Islands](https://www.geeksforgeeks.org/find-the-number-of-distinct-islands-in-a-2d-matrix/)    

### Implementation
```java
class Solution {
    public int numDistinctIslands(char[][] grid) {
        HashSet<String> distinctIslands = new HashSet<>();
        char[][] nGrid = grid;
        int row = grid.length;
        int col = grid[0].length;
        
        for(int i=0; i<row; i++) {
            for(int j=0; j<col; j++) {
                if(nGrid[i][j] == '1') {
                    StringBuilder island = new StringBuilder();
                    dfs(nGrid, i, j, island);
                    distinctIslands.add(island.toString());
                }
            }
        }
        return distinctIslands.size();
    }
    
    public void dfs(char[][] grid, int row, int col, StringBuilder island) {
        grid[row][col] = '0';
        
        //down
        if(isSafe(grid, row, col+1)) {
            island.append('d');
            dfs(grid, row, col+1, island);
            // b -> backtrack
            island.append('b'); 
        }
        //up
        if(isSafe(grid, row, col-1)) {
            island.append('u');
            dfs(grid, row, col-1, island);
            island.append('b');
        }
        //right
        if(isSafe(grid, row+1, col)) {
            island.append('r');
            dfs(grid, row+1, col, island);
            island.append('b');
        }
        //left
        if(isSafe(grid, row-1, col)) {
            island.append('l');
            dfs(grid, row-1, col, island);
            island.append('b');
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
Video Explanations -> [Number of Distinct Islands](https://www.youtube.com/watch?v=4vY_ZPi9jTs)   
<hr>
