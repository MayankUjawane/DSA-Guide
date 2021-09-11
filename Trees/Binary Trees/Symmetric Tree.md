#  Symmetric Tree
Try to solve the question first [Symmetric Tree](https://leetcode.com/problems/symmetric-tree/) with your own.
 
```java
class Solution {
    
    public boolean isSymmetric(TreeNode root) {
        return root==null || isSymmetric(root.left, root.right);
    }    
    public boolean isSymmetric(TreeNode node1, TreeNode node2) {
        if (node1 == null || node2 == null) return node1 == node2;
        
        if (node1.val != node2.val) return false;
        
        return (isSymmetric(node1.left, node2.right) && isSymmetric(node1.right, node2.left));
    }
}
```
> `Time Complexity` : **O(N)**   
> `Space Complexity` : **O(N)**   
---
Video Explanations -> [Symmetric Tree](https://www.youtube.com/watch?v=nKggNAiEpBE&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=26)
<hr>
