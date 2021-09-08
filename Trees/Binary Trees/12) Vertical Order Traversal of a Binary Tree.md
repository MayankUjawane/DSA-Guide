#  Vertical Order Traversal of a Binary Tree
Try to solve the question first [Vertical Order Traversal of a Binary Tree](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/) with your own.
 
> **`Hint`**   
> Use **PriorityQueue**
```java 
class Solution {
    private class Pair {
        TreeNode node;
        int level;
        Pair(TreeNode node, int level) {
            this.node = node;
            this.level = level;
        }
    }
    
    public List<List<Integer>> verticalTraversal(TreeNode root) {
        List<List<Integer>> list = new ArrayList();
        if (root == null) return list;
        
        PriorityQueue<Pair> main = new PriorityQueue<>((a,b)->{
            return a.node.val - b.node.val;
        });
        PriorityQueue<Pair> child = new PriorityQueue<>((a,b)->{
            return a.node.val - b.node.val;
        });
        
        int[] minMax = {0,0};
        width(root, minMax, 0);
        int widthOfTree = minMax[1] - minMax[0] + 1;
        for (int i=0; i<widthOfTree; i++) {
            list.add(new ArrayList());
        }
        
        main.add(new Pair(root, Math.abs(minMax[0])));
        
        while(main.size() > 0) {
            int size = main.size();
            while (size-- > 0) {
                Pair top = main.remove();
                list.get(top.level).add(top.node.val);

                if(top.node.left != null) child.add(new Pair(top.node.left, top.level-1));
                if(top.node.right != null) child.add(new Pair(top.node.right, top.level+1));
            }
            PriorityQueue<Pair> temp = main;
            main = child;
            child = temp;
        }
        
        return list;
    }
    
    public void width(TreeNode root, int[] minMax, int level) {
        if (root == null) return;
        
        minMax[0] = Math.min(minMax[0], level);
        minMax[1] = Math.max(minMax[1], level);
        width(root.left, minMax, level-1);
        width(root.right, minMax, level+1);
    }
}
```

> `Time Complexity` **O(NlogN)**   
> `Space Complexity` **O(N)**   
---
     
Video Explanations -> [Vertical Order Traversal of a Binary Tree](https://www.youtube.com/watch?v=8o-0CxZHNdQ&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=16), [Time Complexity](https://www.youtube.com/watch?v=KU2aFq6AsFA&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=17), [Lambda Expression In PriorityQueue](https://www.youtube.com/watch?v=2kNeNVIdrQY&list=PL-Jc9J83PIiE_OazJYjhsaMXyWCf1DFCD&index=7) 
