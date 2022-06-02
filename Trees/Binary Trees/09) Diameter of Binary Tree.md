#  Diameter of Binary Tree
Attempt the question first [Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/), if you are not able to get the logic then see the hint.    

> **`Hint`**   
> Use the concept of **Height of Binary Tree**

> **`Logic`**   
> We will return the maximum height of left sub-tree and right sub-tree for every node and for every node will set the diameter.

```java 
class Solution {
    
    public int diameterOfBinaryTree(TreeNode root) {
        //since variables can not be passed as reference in Java that's why we are using Array
        int[] diameter = new int[1];
        height(root, diameter);
        return diameter[0];
    }
    
    public int height(TreeNode root, int[] diameter) {
        if (root == null) return 0;
        
        int left = height(root.left, diameter);
        int right = height(root.right, diameter);
        
        diameter[0] = Math.max(left+right, diameter[0]);
            
        return Math.max(left, right) + 1;    
    }
}
```

> `Time Complexity` **O(N)**   
> `Space Complexity` **O(N)**   
---
     
[Video Explanation](https://www.youtube.com/watch?v=Rezetez59Nk&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=17)
