#  In-order Traversal
In-order traversal is to traverse the left subtree first. Then visit the root. Finally, traverse the right subtree.

> ### `In-order Traversal using Recursion`
```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> inorder = new ArrayList<Integer>(); 
        dfs(root, inorder);
        return inorder; 
    }
    private void dfs(TreeNode node, List<Integer> inorder) {
        if(node == null) return; 
         
        dfs(node.left, inorder);
        inorder.add(node.val);
        dfs(node.right, inorder); 
    }
}
```
> `Time Complexity` **O(N)**   
> `Space Complexity` **O(N)**   
---

> ### `In-order Traversal Iteratively`

> **Logic**   
> We are going to move to the left children and add the node to the Stack until the root becomes null, when root becomes null that means we have reached to the left extreme so now       
> we will move to right children. We will do this process untill the Stack is not empty.    

> **Why this logic work ?**   
> In-order Traversal means `Left Child` then `Node` then `Right Child`. We are just simulating the recursion. In recursion we move to left until the root becomes null then we add
> value of node to the list then move to the right and repeat the same process, we did the same in iteration using Stack. 
               
```java
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> inorder = new ArrayList();
        Stack<TreeNode> stack = new Stack();
        
        while (true) {
            if (root != null) {
                stack.push(root);
                root = root.left;
            } else {
                if (stack.isEmpty()) {
                    break;
                }
                root = stack.pop();
                inorder.add(root.val);
                root = root.right;
            }
        }
        
        return inorder;
    }
```
> `Time Complexity` **O(N)**    
> `Space Complexity` **O(N)**    
----

LeetCode [In-order Question](https://leetcode.com/problems/binary-tree-inorder-traversal/)     
YouTube video [Recursive](https://www.youtube.com/watch?v=Z_NEgBgbRVI&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=7)   [Iterative](https://www.youtube.com/watch?v=lxTGsVXjwvM&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=11)
