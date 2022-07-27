# Search a 2D Matrix II
> Question -> [Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/)    

### Implementation
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length;
        int n = matrix[0].length;
        
        int r=0, c=n-1;
        while(c>=0 && r<m) {
            int val = matrix[r][c];
            if(val == target) {
                return true;
            } else if(val > target) {
                c--;
            } else {
                r++;
            }
        }
        
        return false;
    }
}
```
> `Time Complexity` : **O(row + column)**, because we are traversing every row & column only once                   
> `Space Complexity` : **O(1)**
---
