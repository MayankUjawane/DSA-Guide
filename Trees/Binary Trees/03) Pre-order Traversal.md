#  Pre-order Traversal
Pre-order traversal is to visit the root first. Then traverse the left subtree. Finally, traverse the right subtree.

> ### `Pre-order Traversal using Recursion`
```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> preorder = new ArrayList<Integer>(); 
        dfs(root, preorder);
        return preorder; 
    }
    private void dfs(TreeNode node, List<Integer> preorder) {
        if(node == null) return; 
        
        preorder.add(node.val); 
        dfs(node.left, preorder);
        dfs(node.right, preorder); 
    }
}
```
> `Time Complexity` **O(N)**   
> `Space Complexity` **O(N)**   
---

> ### `Pre-order Traversal Iteratively`

> **`Logic`**   
> We are going to print the value of node then we will add the right child and then left child of the node in the stack and then will move to its left child. We will repeat this
> until the stack is not empty.   
> 
> **Why this logic work ?**   
> Pre-order Traversal means `Node` then `Left Child` then `Right Child`. So we are printing the value of node then adding the right child and then left child because Stack is a 
> Last in First out Data Structure.
               

```java
   public List<Integer> preorderTraversal(TreeNode root) {

      Stack<TreeNode> preStack = new Stack();
      List<Integer> preorder = new ArrayList<Integer>(); 
      if (root == null) return preorder;
      preStack.add(root);

      while (!preStack.isEmpty()) {
          root = preStack.pop();

          preorder.add(root.val);

          if (root.right != null) {
              preStack.push(root.right);
          }

          if (root.left != null) {
              preStack.push(root.left);
          }
      }

      return preorder; 
  }
```
> `Time Complexity` **O(N)**    
> `Space Complexity` **O(N)**    
----

LeetCode [Pre-order Question](https://leetcode.com/problems/binary-tree-preorder-traversal/)     
YouTube video [Recursive](https://www.youtube.com/watch?v=RlUu72JrOCQ&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=6)   [Iterative](https://www.youtube.com/watch?v=Bfqd8BsPVuw&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=10)
