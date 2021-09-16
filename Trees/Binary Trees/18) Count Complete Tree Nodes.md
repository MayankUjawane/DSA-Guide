# Count Complete Tree Nodes
Try to solve the question [Count Complete Tree Nodes](https://leetcode.com/problems/count-complete-tree-nodes/) first with your own.

> **`Logic`**   
> A Perfect Binary Tree of height h (where the height of the binary tree is the longest path from the root node to any 
> leaf node in the tree, height of root node is 1) has ***`2h – 1`*** nodes. 
```java
class Solution {
    public int countNodes(TreeNode root) {
        if (root == null) return 0;
        
        int leftHeight = leftHeight(root);
        int rightHeight = rightHeight(root);
        
        //A perfect binary tree contains 2^h – 1 nodes.
        if (leftHeight == rightHeight) return ((int)Math.pow(2, leftHeight) - 1);
        
        return (1 + countNodes(root.left) + countNodes(root.right));
    }
    
    public int leftHeight(TreeNode root) {
        int leftHeight = 0;
        while (root != null) {
            leftHeight++;
            root = root.left;
        }
        return leftHeight;
    }
    
    public int rightHeight(TreeNode root) {
        int rightHeight = 0;
        while (root != null) {
            rightHeight++;
            root = root.right;
        }
        return rightHeight;
    }
}      
```
> `Time Complexity` : **O((logN)<sup>2</sup>)**    
> `Space Complexity` : **O(logN)** (since we have complete binary tree that's why height = logN)   
---
Video Explanations -> [Count Complete Tree Nodes](https://www.youtube.com/watch?v=u-yWemKGWO0&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=33)  
<hr>
