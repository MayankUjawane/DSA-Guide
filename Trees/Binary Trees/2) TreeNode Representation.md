For the **implementation**, we'll use a **TreeNode class** that will store int value, and keep a reference to each child:

### Definition for a Binary Tree Node.
```java
 public class TreeNode {
     int val;
     TreeNode left;
     TreeNode right;
     TreeNode() {}
     TreeNode(int val) { this.val = val; }
     TreeNode(int val, TreeNode left, TreeNode right) {
         this.val = val;
         this.left = left;
         this.right = right;
     }
 }
 ```
