# Sliding Puzzle
Question -> [Sliding Puzzle](https://leetcode.com/problems/sliding-puzzle/)    

### Implementation
```java
class Solution {
    public int slidingPuzzle(int[][] board) {
        String target = "123450";
        //possible indexes to swap for every ith index
        int[][] possibleSwapIndex = {{1,3},{0,2,4},{1,5},{0,4},{1,3,5},{2,4}}; 
        
        //Convert 2D board in String so that we can compare easily
        StringBuilder sb = new StringBuilder();
        for(int i=0; i<board.length; i++) {
            for(int j=0; j<board[0].length; j++) {
                sb.append(board[i][j]);
            }
        }
        String original = sb.toString();
        if(original.equals(target)) {
            return 0;
        }
        HashSet<String> vis = new HashSet<>();
        Queue<String> q = new LinkedList<>();
        q.offer(original);
        vis.add(original);
        
        int swaps = 1;
        while(!q.isEmpty()) {
            int size = q.size();
            while(size-- > 0) {
                String rem = q.poll();
                //find the index of 0 in removed string
                int ind = -1;
                for(int i=0; i<rem.length(); i++) {
                    if(rem.charAt(i) == '0') {
                        ind = i;
                        break;
                    }
                }

                int[] possibleSwaps = possibleSwapIndex[ind];
                for(int swapingIndex: possibleSwaps) {
                    String swapedString = swapZero(rem, ind, swapingIndex);
                    if(!vis.contains(swapedString)) {
                        if(target.equals(swapedString)) {
                            return swaps;
                        }
                        q.offer(swapedString);
                        vis.add(swapedString);
                    }
                }
            }
            swaps++;
        }
        return -1;
    }
    public String swapZero(String st, int i, int j) {
        StringBuilder sb = new StringBuilder(st);
        sb.setCharAt(i, st.charAt(j));
        sb.setCharAt(j, st.charAt(i));
        return sb.toString();
    }
}
```
---
Video Explanations -> [Sliding Puzzle](https://youtu.be/-7zxQzs3D2A)   
<hr>
