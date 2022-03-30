# Search In A Sorted 2D Array
Question -> [Search In A Sorted 2D Array](https://leetcode.com/problems/search-a-2d-matrix/)    

### Implementation
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int row = matrix.length;
        int col = matrix[0].length; 
        for(int r=0; r<row; r++) {
            if(matrix[r][col-1] >= target) {
                for(int c=col-1; c>=0; c--) {
                    if(matrix[r][c] == target) return true;
                }
                break;
            }
        }
        return false;
    }
}
```
---
Video Explanations -> [Search In A Sorted 2D Array](https://youtu.be/5vP0-g94xEA?list=PL-Jc9J83PIiFkOETg2Ybq-FMuJjkZSGeH)   
<hr>
