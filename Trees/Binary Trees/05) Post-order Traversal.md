#  Post-order Traversal
Post-order traversal is to traverse the left subtree first. Then traverse the right subtree. Finally, visit the root.

> ### `Post-order Traversal using Recursion`
```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> postorder = new ArrayList<Integer>(); 
        dfs(root, postorder);
        return postorder; 
    }
    private void dfs(TreeNode node, List<Integer> postorder) {
        if(node == null) return; 
       
        dfs(node.left, postorder);
        dfs(node.right, postorder); 
        postorder.add(node.val); 
    }
}
```
> `Time Complexity` **O(N)**   
> `Space Complexity` **O(N)**   
---

> ### `Post-order Traversal Iteratively`
```java
 class Solution {
    private class Pair {
        TreeNode node;
        int state;
        Pair(TreeNode node, int state) {
            this.node = node;
            this.state = state;
        }
    }
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList();
        if (root == null) return list;
        
        Stack<Pair> st = new Stack();
        st.push(new Pair(root, 1));
        
        while (st.size() > 0) {
            Pair top = st.peek();
            TreeNode node = top.node;
            
            if ((node.right == null && node.left == null) || top.state == 2) {
                list.add(st.pop().node.val);
                continue;
            }
            
            if (node.right != null && top.state == 1) st.push(new Pair(node.right, 1));
            if (node.left != null && top.state == 1) st.push(new Pair(node.left, 1));
            
            top.state = 2;
        }
        return list;
    }
  }
```
> `Time Complexity` **O(N)**     
> `Space Complexity` **O(N)**    
----

LeetCode [Post-order Question](https://leetcode.com/problems/binary-tree-postorder-traversal/)     
YouTube video [Recursive](https://www.youtube.com/watch?v=COQOU6klsBg&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=8)   [Iterative](https://www.youtube.com/watch?v=12aMTS0L6WI&list=PL-Jc9J83PIiHYxUk8dSu2_G7MR1PaGXN4&index=13)
