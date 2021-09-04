#  Balanced Binary Tree
Attempt the question first [Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/), if you are not able to get the logic then see the hint.    

> **`Hint`**   
> Use the concept of **Maximum Depth of Binary Tree**

> **`Logic`**   
> We will check the difference of height of left sub-tree and right sub-tree, if at any point it is greater than 1 then we will return false.

```java 
class Solution {
    public boolean isBalanced(TreeNode root) {
        if (root == null) return true;
        
        return isBalancedHelper(root) != -1;
    }
    
    public int isBalancedHelper(TreeNode root) {
        if (root == null) return 0;
        
        int leftHeight = isBalancedHelper(root.left);
        if (leftHeight == -1) return -1;
        int rightHeight = isBalancedHelper(root.right);
        if (rightHeight == -1) return -1;
        
        if (Math.abs(leftHeight - rightHeight) > 1) return -1;
        
        return Math.max(leftHeight, rightHeight) + 1;
    }
}
```

> `Time Complexity` **O(N)**   
> `Space Complexity` **O(N)**   
---
     
[Video Explanation](https://www.youtube.com/watch?v=Yt50Jfbd8Po&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=16)
