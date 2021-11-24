# 01 Matrix
Question -> [01 Matrix](https://leetcode.com/problems/01-matrix/)    

### Implementation
```java
class Solution {
    private class Coordinates {
        int x;
        int y;
        Coordinates(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }
    public int[][] updateMatrix(int[][] mat) {
        int[][] matrix = mat;
        Queue<Coordinates> q = new LinkedList<>();
        // convert all 1 to -1 so that we can use -1 as unvisited and add all 0 to the list so that  
        // we can apply multisource BFS from all 0.
        for(int i=0; i<matrix.length; i++) {
            for(int j=0; j<matrix[0].length; j++) {
                if(matrix[i][j] == 0) {
                    q.offer(new Coordinates(i, j));
                } else {
                    matrix[i][j] = -1;
                }
            }
        }
        
        int[][] directions = {{1,0}, {-1,0}, {0,1}, {0,-1}};
        // Applying Multisource BFS form all 0 
        while(!q.isEmpty()) {
            Coordinates rem = q.poll();
            for(int i=0; i<directions.length; i++) {
                int x = directions[i][0] + rem.x;
                int y = directions[i][1] + rem.y;
                
                if(x>=0 && y>=0 && x<matrix.length && y<matrix[0].length && matrix[x][y] == -1) {
                    matrix[x][y] = matrix[rem.x][rem.y] + 1;
                    // now add this node to the queue
                    q.offer(new Coordinates(x,y));
                }
            }
        }
        
        return matrix;
    }
}     
```
> `Time Complexity` : **O(N)**, where N = row * column      
> `Space Complexity` : **O(N)**, where N = row * column, this space is required to maintain the queue. 
> The space used to store the output (matrix) does not count towards the space complexity.  
---
Video Explanations -> [01 Matrix](https://www.youtube.com/watch?v=BJbaUH9dN24&list=WL&index=25)  
<hr>
