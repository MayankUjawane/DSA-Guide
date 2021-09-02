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
      public class Pair {
          TreeNode node;
          int state;
          Pair(TreeNode node, int state) {
              this.node = node;
              this.state = state;
          }
      }
    
      public List<Integer> postorderTraversal(TreeNode root) {
          List<Integer> list = new ArrayList();
          Stack<Pair> st = new Stack();
          if (root == null) return list;
          Pair rootPair = new Pair(root, 1);
          st.push(rootPair);

          while (st.size() > 0) {
              Pair top = st.peek();
              if (top.state == 1) {
                  //state=1 means we are in Pre-state (do state++ and move towards left child)
                  top.state++;
                  if (top.node.left != null) {
                      Pair leftNode = new Pair(top.node.left, 1);
                      st.push(leftNode);
                  }
              } else if (top.state == 2) {
                  //state=2 means we are in In-state (do state++ and move towards right child)
                  top.state++;
                  if (top.node.right != null) {
                      Pair rightNode = new Pair(top.node.right, 1);
                      st.push(rightNode);
                  }
              } else {
                  //state=3 means we are in Post-state (pop the node from the stack)
                  list.add(top.node.val);
                  st.pop();
              }
          }    
          
          return list;
      }
  }
```
> `Time Complexity` **O(3N)** -> Because we are iterating each node for three times.     
> `Space Complexity` **O(N)**    
----

LeetCode [Post-order Question](https://leetcode.com/problems/binary-tree-postorder-traversal/)     
YouTube video [Recursive](https://www.youtube.com/watch?v=COQOU6klsBg&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=8)   [Iterative](https://www.youtube.com/watch?v=12aMTS0L6WI&list=PL-Jc9J83PIiHYxUk8dSu2_G7MR1PaGXN4&index=13)
