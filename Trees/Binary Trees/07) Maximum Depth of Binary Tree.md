# Maximum Depth of Binary Tree   
Attempt the question first [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/), if you are not able to get the logic then see the hint.    

> **`Hint`**   
> Use **Recursion**

> **`Logic`**   
> We will traverse to the whole tree and will find maximum depth present in Tree with the help of Recursion.

> ### `Maximum Depth of Binary Tree`
```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        
        int leftDepth = maxDepth(root.left);
        int rightDepth = maxDepth(root.right);
        
        return Math.max(leftDepth, rightDepth) + 1;
    }
}
```
> `Time Complexity` **O(N)**   
> `Space Complexity` **O(N)**   
---
     
[Video Explanation](https://www.youtube.com/watch?v=eD3tmO66aBA&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=15)
