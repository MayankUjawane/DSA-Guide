#  Binary Tree Right Side View
Try to solve the question first [Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/) with your own.
 
> **`Hint`**   
> Use **Reverse Pre Order -> Root, Right, Left**

### Binary Tree Right Side View Using Recursion
```java
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> list = new ArrayList();
        rightSideView(root, list, 0);
        return list;
    }
    
    public void rightSideView(TreeNode root, List<Integer> list, int row) {
        if (root == null) return;
        
        if (row == list.size()) {
            list.add(root.val);
        }
        //we are traversing node, then right, then left since we want to view right side first
        rightSideView(root.right, list, row+1);
        rightSideView(root.left, list, row+1);
    }
}
```
> `Time Complexity` : **O(N)**   
> `Space Complexity` : **O(N)**   
---
Video Explanations -> [Binary Tree Right Side View](https://www.youtube.com/watch?v=KV4mRzTjlAk&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=25)
<hr>

### Binary Tree Right Side View Using Iteration      

> **`Hint`**   
> Use **Level Order Traversal**
```java
class Solution {
    private class Pair {
        TreeNode node;
        int row;
        Pair (TreeNode node, int row) {
            this.node = node;
            this.row = row;
        }
    }
    
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> list = new ArrayList();
        if (root == null) return list;
        
        //since we are doing level order traversal that's why we will move level in increasing order (level 0 to end level) 
        //so we can use LinkedHashMap because it stores the order in which we added.
        Map<Integer, Integer> map = new LinkedHashMap();
        Queue<Pair> queue = new LinkedList();
        queue.offer(new Pair(root, 0));
        
        while(!queue.isEmpty()) {
            int size = queue.size();
            while (size-- > 0) {
                Pair top = queue.poll();
                map.put(top.row, top.node.val);
                if (top.node.left != null) queue.offer(new Pair(top.node.left, top.row+1));
                if (top.node.right != null) queue.offer(new Pair(top.node.right, top.row+1));
            }
        }
        
        for(int data : map.values()) {
            list.add(data);
        }
        
        return list;
    }
}
```
> `Time Complexity` : **O(N)**    
> `Space Complexity` : **O(N)**    
----
