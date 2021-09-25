# Search in a Binary Search Tree
Try to solve the question [Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/) first with your own.     

```java
class Solution {
    public TreeNode searchBST(TreeNode root, int val) {
        while (root != null && root.val != val) {
            root = (root.val < val) ? root.right : root.left;
        }
        return root;
    }
}      
```
> `Time Complexity` : **O(h)** ('h' is the height of BST)   
> `Space Complexity` : **O(1)**    
---
Video Explanations -> [Search in a Binary Search Tree](https://www.youtube.com/watch?v=KcNt6v_56cc&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=41)  
<hr>
