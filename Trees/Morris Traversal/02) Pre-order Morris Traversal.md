# Pre-order Morris Traversal
Try to solve the question [Pre-order Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/submissions/) using Morris Traversal.     
> **`Logic`**          
> * Add the current node to the list (Pre-order -> Root, Left, Right).
> * If current node does not have left child then move to the right child.
> * Connect the right most node of the current nodes left subtree to the current node.
> * If the right most node of left subtree is connected to the current node that means the thread is already present and you have traversed the entire left subtree, 
> so remove the thread since the purpose of the thread is served (tree should not be modified, if you create thread then you should remove it also).
> * Since you traversed the left sub-tree so now move to right side.
```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList();
        TreeNode curr = root;
        
        while (curr != null) {
            if (curr.left == null) {
                list.add(curr.val);
                curr = curr.right;
            } else {
                TreeNode rightMost = getRightMostNode(curr, curr.left);
                if (rightMost.right == null) {
                    list.add(curr.val);
                    // Create Thread
                    rightMost.right = curr;
                    curr = curr.left;
                } else {
                    // Delete Thread
                    rightMost.right = null;
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
                      1) [Pre-order Morris Traversal](https://www.youtube.com/watch?v=8rwHi5CXwqY&list=WL&index=9), 
                      2) [Pre-order Morris Traversal](https://www.youtube.com/watch?v=80Zug6D1_r4&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=38)
<hr>
