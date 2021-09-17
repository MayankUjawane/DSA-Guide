# Construct Binary Tree from Inorder and Postorder Traversal
Try to solve the question [Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/) first with your own.     
> **`Logic`**   
> [Requirements needed to construct a Unique Binary Tree](https://www.youtube.com/watch?v=9GMECGQgWrQ&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=34)      
> Postorder -> Left, Right, Root       
> Inorder -> Left, Root, Right
```java
class Solution {
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        if (inorder.length == 1) return new TreeNode(inorder[0]);
        
        HashMap<Integer, Integer> inMap = new HashMap();
        for(int i=0; i < inorder.length; i++) {
            inMap.put(inorder[i], i);
        }
        
        return buildTree(postorder, postorder.length-1, inMap, 0, inorder.length-1);
    }   
    
    public TreeNode buildTree(int[] postorder, int postEnd, 
                             Map<Integer,Integer> inMap, int inStart, 
                             int inEnd) {
        if (inStart > inEnd) return null;
        
        TreeNode root = new TreeNode(postorder[postEnd]);
        
        int inorderRootIndex = inMap.get(root.val);
        int postLeftEnd = postEnd - (inEnd - inorderRootIndex + 1);
        
        root.left = buildTree(postorder, postLeftEnd, inMap, inStart, inorderRootIndex-1);
        root.right = buildTree(postorder, postEnd-1, inMap, inorderRootIndex+1, inEnd);
        
        return root;
    }
}      
```
> `Time Complexity` : **O(N)**    
> `Space Complexity` : **O(N)**    
---
Video Explanations -> [Construct Binary Tree from Inorder and Postorder Traversal](https://www.youtube.com/watch?v=LgLRTaEMRVc&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=36)  
<hr>
