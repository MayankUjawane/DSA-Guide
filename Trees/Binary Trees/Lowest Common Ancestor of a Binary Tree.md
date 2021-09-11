#  Lowest Common Ancestor of a Binary Tree
Try to solve the question [Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) first with your own.

### Method 1
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        List<TreeNode> pathOfP = new ArrayList();
        List<TreeNode> pathOfQ = new ArrayList();
        
        getPath(root, p, pathOfP);
        getPath(root, q, pathOfQ);
        
        int count = 0;
        while (count < pathOfP.size() && count < pathOfQ.size()) {
            if (pathOfP.get(count) != pathOfQ.get(count)) {
                return pathOfP.get(count-1);
            }
            count++;
        }
        
        return pathOfP.get(count-1);
    }
    
    public boolean getPath(TreeNode root, TreeNode nodeToFind, List<TreeNode> path) {
        if (root == null) return false;
        if (nodeToFind == root) {
            path.add(root);
            return true;
        }
        path.add(root); 
        
        if (getPath(root.left, nodeToFind, path)) {
            return true;
        }
        if (getPath(root.right, nodeToFind, path)) {
            return true;
        }
        
        path.remove(path.size()-1);
        return false;
    } 
}
```
> `Time Complexity` : **O(N)**   
> `Space Complexity` : **O(N)**   
---
Video Explanations -> [Get Path](https://www.youtube.com/watch?v=fmflMqVOC7k&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=27), [Lowest Common Ancestor of a Binary Tree](https://www.youtube.com/watch?v=_-QHfMDde90&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=28)
<hr>

### Method 2
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) return null;
        
        if (root == p || root == q) return root;
        
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        
        if (left != null && right != null) return root;
        if (left != null) return left;
        return right;
    }
}
```
> `Time Complexity` : **O(N)**   
> `Space Complexity` : **O(N)**   
---
Video Explanations -> [Lowest Common Ancestor of a Binary Tree](https://www.youtube.com/watch?v=3MmWkR04n_8)
<hr>
