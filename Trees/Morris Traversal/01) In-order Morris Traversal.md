# In-order Morris Traversal
Try to solve the question [In-order Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/submissions/) using Morris Traversal.     
> **`Logic`**          
> * In-order -> Left, Root, Right
> * If at any time current node does not have left child then add the node to the list (In-order -> Left, Root, Right) and move to the right child.
> * Connect the right most node of the current nodes left subtree to the current node.
> * If the right most node of left subtree is already connected to the current node that means the thread is present and you are visiting the current node again after 
> traversing its left subtree, so this time add the current node to the list (In-order -> Left, Root, Right) and remove the thread (tree should not be modified if you 
> create thread then you should remove it also).
> * Since you traversed the left subtree so now move to right node.
```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList();
        TreeNode curr = root;
        
        while (curr != null) {
            if (curr.left == null) {
                list.add(curr.val);
                curr = curr.right;
            } else {
                TreeNode rightMost = getRightMostNode(curr, curr.left);
                
                if (rightMost.right == null) {
                    // Create Thread
                    rightMost.right = curr;
                    curr = curr.left;
                } else {
                    // Delete Thread
                    rightMost.right = null;
                    list.add(curr.val);
                    curr = curr.right;
                }
            }
        }
        return list;
    }    
    
    public TreeNode getRightMostNode(TreeNode curr, TreeNode node) {
        while (node.right != null && node.right != curr) {
            node = node.right;
        }
        return node;
    }
}      
```
> `Time Complexity` : **O(3N)**    
> `Space Complexity` : **O(1)**    
---
Video Explanations -> [Threaded Binary Tree](https://www.youtube.com/watch?v=viegWtuH0uI&list=WL&index=9), 
                      1) [In-order Morris Traversal](https://www.youtube.com/watch?v=oz17ihxBxgU&list=WL&index=9), 
                      2) [In-order Morris Traversal](https://www.youtube.com/watch?v=80Zug6D1_r4&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=38)
<hr>
