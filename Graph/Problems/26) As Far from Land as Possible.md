# As Far from Land as Possible
Question -> [As Far from Land as Possible](https://leetcode.com/problems/as-far-from-land-as-possible/)    

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
    
    public int maxDistance(int[][] grid) {
        Queue<Coordinate> q = new LinkedList<>();
        int r = grid.length;
        int c = grid[0].length;
        
        for(int i=0; i<r; i++) {
            for(int j=0; j<c; j++) {
                if(grid[i][j] == 1) {
                    q.offer(new Coordinate(i,j));
                }    
            }
        }
        
        //q.size()==0 means no land is present
        //q.size()==grid.length*grid[0].length means no water is present
        if(q.size()==0 || q.size()==(grid.length*grid[0].length)) return -1;
        
        int[][] directions = {{0,1},{0,-1},{-1,0},{1,0}};
        int ans = -1;
        while(!q.isEmpty()) {
            ans++;
            int size = q.size();
            for(int i=0; i<size; i++) {
                Coordinate node = q.poll();
                for(int j=0; j<4; j++) {
                    int newRow = node.row + directions[j][0];
                    int newCol = node.col + directions[j][1];
                    if(newRow>=0 && newCol>=0 && newRow<r && newCol<c && grid[newRow][newCol]==0) {
                        grid[newRow][newCol] = 1;
                        q.offer(new Coordinate(newRow, newCol));
                    }
                }   
            }
        }
        return ans;
    }
}
```
> `Time Complexity` : **O(N)**, where N = row * column      
> `Space Complexity` : **O(N)**, where N = row * column, for Queue. 
---
Video Explanations -> [As Far from Land as Possible](https://youtu.be/yV-b0amHNVM)   
<hr>
