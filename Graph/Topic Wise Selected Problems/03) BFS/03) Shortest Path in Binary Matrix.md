# Shortest Path in Binary Matrix
Question -> [Shortest Path in Binary Matrix](https://leetcode.com/problems/shortest-path-in-binary-matrix/)    

### Implementation
```java
class Solution {
    public int shortestPathBinaryMatrix(int[][] grid) {
        int n = grid.length;
        if(grid[0][0] == 1 || grid[n-1][n-1] == 1) return -1;
        if(grid.length == 1) return 1; 
        
        int[][] directions = {{0,1},{1,0},{0,-1},{-1,0},{1,1},{1,-1},{-1,1},{-1,-1}};
        
        Queue<Coordinates> q = new LinkedList();
        q.add(new Coordinates(0,0,1));
        grid[0][0] = 1;
         
        while(q.size() > 0) {
            Coordinates top = q.poll();
            for(int[] direction: directions) {
                int nRow = top.row + direction[0];
                int nCol = top.col + direction[1];
                if(nRow >= 0 && nRow < n && nCol>=0 && nCol<n && grid[nRow][nCol] == 0) {
                    if(nRow == n-1 && nCol == n-1) return top.move+1;
                    q.add(new Coordinates(nRow,nCol,top.move+1));
                    grid[nRow][nCol] = 1;
                }
            }
        }
        return -1;
    }
    private class Coordinates {
        int row;
        int col;
        int move;
        Coordinates(int row, int col, int move) {
            this.row = row;
            this.col = col;
            this.move = move;
        }
    }
}
```
> `Time Complexity` : **O(N)**, where N = row * column         
> `Space Complexity` : **O(N)**, where N = row * column, this space is required to maintain the queue. 
---
