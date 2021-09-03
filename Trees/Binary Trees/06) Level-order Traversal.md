#  Level-order Traversal
Get the better understanding of Level-order Traversal [click here](https://leetcode.com/explore/learn/card/data-structure-tree/134/traverse-a-tree/990/)    
Attempt the question first [Leve-order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/), if you are not able to get the logic then see the hint.    

> **`Hint`**   
> Use **Queue**

> **`Logic`**   
> Queue is a `First In First Out` Data Structure. We are going to declare a queue and two Lists, one will contain Lists of each level and other List will be used to store each 
> level nodes. We will run a loop for every level and will add the nodes value in the Level List and their childrens (if present, first left then right child) in the Queue. After 
> the loop ends we will add this Level List to the Main List. 

> ### `Level-order Traversal`
```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> resultList = new ArrayList();
        if (root == null) return resultList;
        
        Queue<TreeNode> queue = new LinkedList();
        queue.add(root);
        
        while (!queue.isEmpty()) {
            List<Integer> levelList = new ArrayList();
            int levelSize = queue.size();
            for (int i=0; i<levelSize; i++) {
                TreeNode frontNode = queue.remove();
                levelList.add(frontNode.val);
                if (frontNode.left != null) queue.add(frontNode.left);
                if (frontNode.right != null) queue.add(frontNode.right);              
            }  
            resultList.add(levelList);
        }  
        
        return resultList;
    }
}
```
> `Time Complexity` **O(N)**   
> `Space Complexity` **O(N)**   
---
     
[Video Explanation](https://www.youtube.com/watch?v=EoAsWbO7sqg&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=9)
