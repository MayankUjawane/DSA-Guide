#  Diameter of Binary Tree
Try to solve the question first [Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)    

> **`Hint`**   
> Use the concept of **Level-order Traversal**

**Using Two Stack**
```java 
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        Stack<TreeNode> stack = new Stack();
        
        List<List<Integer>> mainList = new ArrayList();
        if (root == null) return mainList;
        stack.push(root);
        boolean oddLevel = true;
        
        while(stack.size() > 0) {
            List<Integer> levelList = new ArrayList();
            int size = stack.size();
            Stack tempStack = new Stack();
            
            if (oddLevel) {
                //oddLevel=true means left to right
                for (int i=0; i<size; i++) {
                    TreeNode topNode = stack.pop();
                    levelList.add(topNode.val);
                    if (topNode.left != null) tempStack.push(topNode.left);
                    if (topNode.right != null) tempStack.push(topNode.right);
                }
            } else {
                //oddLevel=false means right to left
                for (int i=0; i<size; i++) {
                    TreeNode topNode = stack.pop();
                    levelList.add(topNode.val);
                    if (topNode.right != null) tempStack.push(topNode.right);
                    if (topNode.left != null) tempStack.push(topNode.left);
                }
            }
            stack = tempStack;
            mainList.add(levelList);
            //switching the value of level
            oddLevel = !oddLevel;
        }
        
        return mainList;
    }
}
```
> `Time Complexity` **O(N)**   
> `Space Complexity` **O(2N)**  
---

**Using Single Queue**
```java 
class Solution {
     public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList();
        
        List<List<Integer>> mainList = new ArrayList();
        if (root == null) return mainList;
        queue.add(root);
        boolean oddLevel = true;
        
        while(queue.size() > 0) {
            int size = queue.size();
            List<Integer> levelList = new ArrayList();
            
            for (int i=1; i<=size; i++) {
                TreeNode topNode = queue.remove();
                if (topNode.left != null) queue.add(topNode.left);
                if (topNode.right != null) queue.add(topNode.right);
                
                //oddLevel=true means left to right
                if (oddLevel) {
                    levelList.add(topNode.val);
                } else {
                    levelList.add(0, topNode.val);
                }
            }
            oddLevel = !oddLevel;
            mainList.add(levelList);
        }
        
        return mainList;
    }
}
```
> `Time Complexity` **O(N)**   
> `Space Complexity` **O(N)**   
---

Video Explanation [Using Two Stack](https://www.youtube.com/watch?v=eDdPZ05y4Os&list=PL-Jc9J83PIiEmjuIVDrwR9h5i9TT2CEU_&index=17), [Single Queue](https://www.youtube.com/watch?v=3OXWEdlIGl4&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=20)
