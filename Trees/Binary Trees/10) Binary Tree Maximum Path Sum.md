#  Binary Tree Maximum Path Sum
Attempt the question first [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/), if you are not able to get the logic then see the logic.

> **`Logic`**   
> First we will create maximumPathSum and initialise it with minimum value. For every node we are going to compare the maximumPathSum with the nodes maximum path sum possible 
> and if found samller then will update maximumPathSum, then return the maximum path sum possible of that node for its parent node, so that for the parent node we can compare 
> the maximumPathSum with the maximum path sum possible of the parent node. 
```java 
class Solution {
    public int maxPathSum(TreeNode root) {
        int[] maximumPathSum = new int[1];
        maximumPathSum[0] = Integer.MIN_VALUE;
        maxPathSumHelper(root, maximumPathSum);
        return maximumPathSum[0];
    }
    
    public int maxPathSumHelper(TreeNode root, int[] maximumPathSum) {
        if (root == null) return 0;
        
        int leftSum = maxPathSumHelper(root.left, maximumPathSum);
        if (leftSum < 0) leftSum = 0;
        int rightSum = maxPathSumHelper(root.right, maximumPathSum);
        if (rightSum < 0) rightSum = 0;
        
        maximumPathSum[0] = Math.max(maximumPathSum[0], leftSum + rightSum + root.val);
        
        return Math.max(leftSum , rightSum) + root.val;
    }
}
```

> `Time Complexity` **O(N)**   
> `Space Complexity` **O(N)**   
---
     
[Video Explanation](https://www.youtube.com/watch?v=WszrfSwMz58&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=18)
