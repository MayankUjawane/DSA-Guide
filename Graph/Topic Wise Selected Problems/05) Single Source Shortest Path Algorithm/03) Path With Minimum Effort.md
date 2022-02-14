# Path With Minimum Effort
Question -> [Path With Minimum Effort](https://leetcode.com/problems/path-with-minimum-effort/)    

### Implementation
```java
class Solution {
    public int minimumEffortPath(int[][] heights) {
        int r = heights.length, c = heights[0].length;
        if(r == 1 && c == 1) return 0;
        
        boolean[][] visited = new boolean[r][c];
        
        PriorityQueue<Node> pq = new PriorityQueue<>((x,y) -> x.diff - y.diff);
        pq.offer(new Node(0, 0, 0));
        
        int[][] directions = {{0,1},{1,0},{0,-1},{-1,0}};
        
        while(!pq.isEmpty()) {
            Node top = pq.poll();
            if(top.row == r-1 && top.col == c-1) return top.diff;
            
            if(visited[top.row][top.col] == true) continue;
            visited[top.row][top.col] = true;
            
            for(int[] direction: directions) {
                int nRow = top.row + direction[0];
                int nCol = top.col + direction[1];
                if(nRow>=0 && nRow<r && nCol>=0 && nCol<c && !visited[nRow][nCol]) {
                    int difference = Math.abs(heights[top.row][top.col] - heights[nRow][nCol]);
                    int maxDifference = Math.max(top.diff, difference);
                    
                    pq.offer(new Node(nRow, nCol, maxDifference));
                }
            }
        }
        return -1;
    }
    private class Node {
        int row;
        int col;
        int diff;
        Node(int r, int c, int d) {
            row = r;
            col = c;
            diff = d;
        }
    }
}
``` 
> `Time Complexity` : **O(NlogN)**, where N = Row\*Column     
> `Space Complexity` : **O(N)**, where N = Row\*Column   
---
