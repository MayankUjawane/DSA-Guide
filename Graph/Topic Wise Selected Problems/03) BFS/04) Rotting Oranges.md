# Rotting Oranges
Question -> [Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)    

### Implementation
```java
class Solution {
    private class Coordinates {
        int row;
        int col;
        Coordinates(int row, int col) {
            this.row = row;
            this.col = col;
        }
    }
    public int orangesRotting(int[][] grid) {
        Queue<Coordinates> q = new LinkedList<>();
        
        int rows = grid.length;
        int cols = grid[0].length;
        //Put the position of all rotten oranges in queue
        //count the number of fresh oranges
        int freshOranges = 0;
        for(int i=0; i<rows; i++) {
            for(int j=0; j<cols; j++) {
                if(grid[i][j] == 1) {
                   freshOranges++; 
                } else if(grid[i][j] == 2) {
                    q.offer(new Coordinates(i,j));
                }
            }
        }
        if(freshOranges == 0) return 0;
        
        int[][] nGrid = grid;
        int[][] directions = {{-1,0},{1,0},{0,-1},{0,1}}; 
        // applying BFS from initially rotten oranges simultaneously (Multi-source BFS)
        int time = 0;
        boolean flag;
        while(!q.isEmpty()) {
            flag = false;
            // for all the oranges added in the queue at the same level will rot their neighbour fresh
            // fruits at the same time
            int size = q.size();
            for(int i=0; i<size; i++) {
                Coordinates rem = q.poll();
                for(int j=0; j<4; j++) {
                    int nRow = rem.row + directions[j][0];
                    int nCol = rem.col + directions[j][1];
                    if(nRow>=0 && nCol>=0 && nRow<rows && nCol<cols && nGrid[nRow][nCol]==1) {
                        //mark the orange as rotten
                        nGrid[nRow][nCol] = 2;
                        //decrease the count of fresh oranges by 1
                        freshOranges--;
                        //put the new rotten orange in queue
                        q.offer(new Coordinates(nRow, nCol));
                        
                        flag = true;
                    }
                } 
            }
            if(flag == true) time++;
        }
        
        if(freshOranges != 0) return -1;
        return time;
    }
}
```
> `Time Complexity` : **O(N)**, where N = row * column      
> `Space Complexity` : **O(N)**, where N = row * column, this space is required to maintain the queue. 
---
