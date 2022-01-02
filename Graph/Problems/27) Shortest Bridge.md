# Shortest Bridge
Question -> [Shortest Bridge](https://leetcode.com/problems/shortest-bridge/)    

### Implementation
```java
class Solution {
    private class Coordinate {
        int row;
        int col;
        Coordinate(int row, int col) {
            this.row = row;
            this.col = col;
        }
    }
    public int shortestBridge(int[][] grid) {
        Queue<Coordinate> q = new LinkedList<>();
        int r = grid.length;
        int c = grid[0].length;
        boolean flag = false;
        for(int i=0; i<r && !flag; i++) {
            for(int j=0; j<c && !flag; j++) {
                if(grid[i][j] == 1) {
                    dfs(q, grid, i, j);
                    flag = true;
                }
            }
        }
        int[][] direction = {{0,1},{0,-1},{1,0},{-1,0}};
        int count = 0;
        while(!q.isEmpty()) {
            flag = false;
            int size = q.size();
            for(int i=0; i<size; i++) {
                Coordinate node = q.poll();
                for(int j=0; j<4; j++) {
                    int newRow = node.row + direction[j][0];
                    int newCol = node.col + direction[j][1];
                    if(newRow>=0 && newCol>=0 && newRow<r && newCol<c && grid[newRow][newCol] != 2) {
                        if(grid[newRow][newCol] == 1) return count;
                        grid[newRow][newCol] = 2;
                        q.offer(new Coordinate(newRow, newCol));
                        flag = true;
                    }    
                }
            }
            if(flag) count++;
        }
        return count;
    }
    public void dfs(Queue<Coordinate> q, int[][] grid, int row, int col) {
        if(row>=0 && col>=0 && row<grid.length && col<grid[0].length && grid[row][col] == 1) {
            grid[row][col] = -1;
            q.offer(new Coordinate(row, col));
            dfs(q, grid, row, col+1);
            dfs(q, grid, row, col-1);
            dfs(q, grid, row+1, col);
            dfs(q, grid, row-1, col);
        }
    }
}
```
> `Time Complexity` : **O(N)**, where N = row * column      
> `Space Complexity` : **O(N)**, where N = row * column, this space is required to maintain the queue.  
---
Video Explanations -> [Shortest Bridge](https://youtu.be/VuNzLtd8PBg)  
<hr>
