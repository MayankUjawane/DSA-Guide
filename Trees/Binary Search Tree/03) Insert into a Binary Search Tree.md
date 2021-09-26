# Insert into a Binary Search Tree
Try to solve the question [Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/) first with your own.     

### Using Iteration
```java
class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) return new TreeNode(val);
        TreeNode node = root;
        while (true) {
            if (node.val < val) {
                if (node.right == null) {
                    node.right = new TreeNode(val);
                    break;
                }
                node = node.right;
            } else {
                if (node.left == null) {
                    node.left = new TreeNode(val);
                    break;
                }
                node = node.left;
            }
        }
        return root;
    }
}      
```
> `Time Complexity` : **O(1)** 'h' is the height of BST       
> `Space Complexity` : **O(1)**    
---
Video Explanations -> [Insert into a Binary Search Tree](https://www.youtube.com/watch?v=FiFiNvM29ps&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=44)  
<hr>

### Using Recursion
```java
class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) {
            return new TreeNode(val);
        }
        if (root.val > val) {
            root.left = insertIntoBST(root.left, val);
        } else {
            root.right = insertIntoBST(root.right, val);
        } 
        return root;
    }
}      
```
> `Time Complexity` : **O(h)** 'h' is the height of BST       
> `Space Complexity` : **O(1)**    
---
