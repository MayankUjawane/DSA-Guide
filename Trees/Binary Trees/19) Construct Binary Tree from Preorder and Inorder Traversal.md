# Construct Binary Tree from Preorder and Inorder Traversal
Try to solve the question [Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/) first with your own.     
> **`Logic`**   
> [Requirements needed to construct a Unique Binary Tree](https://www.youtube.com/watch?v=9GMECGQgWrQ&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=34)      
> Preorder -> Root, Left, Right    
> Inorder -> Left, Root, Right
```java
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if (preorder.length == 1) return new TreeNode(preorder[0]);
        
        HashMap<Integer, Integer> inorderMap = new HashMap();
        for(int i=0; i<inorder.length; i++) {
            inorderMap.put(inorder[i], i);
        }
        
        return buildTree(preorder, 0, inorderMap, 0, inorder.length-1);
    }    
    
    public TreeNode buildTree(int[] preorder, int preStart, Map<Integer,Integer> inorderMap, int start, int last) {
        if (start > last) return null;
        
        TreeNode root = new TreeNode(preorder[preStart]);
        int inorderRootIndex = inorderMap.get(root.val);
        
        root.left = buildTree(preorder, preStart+1, inorderMap, start, inorderRootIndex-1);
        
        int rightPreStart = preStart + (inorderRootIndex - start + 1); 
        root.right = buildTree(preorder, rightPreStart, inorderMap, inorderRootIndex+1, last);
        
        return root;
    }
}      
```
> `Time Complexity` : **O(N)**    
> `Space Complexity` : **O(N)**    
---
Video Explanations -> [Construct Binary Tree from Preorder and Inorder Traversal](https://www.youtube.com/watch?v=aZNaLrVebKQ&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=35)  
<hr>
