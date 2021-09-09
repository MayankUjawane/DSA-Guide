#  Vertical Order Traversal of a Binary Tree
Try to solve the question first [Vertical Order Traversal of a Binary Tree](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/) with your own.
 
> **`Hint`**   
> Use **PriorityQueue**

### Method 1 (Using Two Priority Queue)
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
> `Time Complexity` : **O(NlogN)**   
> `Space Complexity` : **O(N)**   
---
Video Explanations -> [Vertical Order Traversal of a Binary Tree](https://www.youtube.com/watch?v=8o-0CxZHNdQ&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=16), [Time Complexity](https://www.youtube.com/watch?v=KU2aFq6AsFA&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=17), [Lambda Expression In PriorityQueue](https://www.youtube.com/watch?v=2kNeNVIdrQY&list=PL-Jc9J83PIiE_OazJYjhsaMXyWCf1DFCD&index=7) 
<hr>

### Method 2 (Using TreeMap and PriorityQueue)
```java
class Solution {
    private class Pair {
        TreeNode node;
        int row;
        int column;
        Pair(TreeNode _node, int _row, int _column) {
            node = _node;
            row = _row;
            column = _column;
        }
    }
    
    public List<List<Integer>> verticalTraversal(TreeNode root) {
        List<List<Integer>> list = new ArrayList();
        if(root == null) return list;
        
        Queue<Pair> queue = new LinkedList();
        
        //TreeMap<Column, TreeMap<Row, PriorityQueue<Node Value>>>
        TreeMap<Integer, TreeMap<Integer, PriorityQueue<Integer>>> map = new TreeMap();
        
        queue.offer(new Pair(root, 0, 0));
        
        while(queue.size() > 0) {
            int size = queue.size();
            while (size-- > 0) {
                Pair top = queue.poll();
                TreeNode node = top.node;
                int column = top.column;
                int row = top.row;
                
                if (map.get(column) == null) {
                   // map.put(column, new TreeMap<>(){{put(row, new PriorityQueue<>());}});
                    map.put(column, new TreeMap<>());
                }
                
                if (map.get(column).get(row) == null) {
                    map.get(column).put(row, new PriorityQueue<>());
                }
                
                map.get(column).get(row).offer(node.val);
                
                if (node.left != null) queue.offer(new Pair(node.left, row+1, column-1));
                if (node.right != null) queue.offer(new Pair(node.right, row+1, column+1));
            }
        }
        
        //Iterating for every column and we will get column in increasing order because of TreeMap
        for(TreeMap<Integer, PriorityQueue<Integer>> columnTreeMap : map.values()) {
            list.add(new ArrayList());
            //Iterating for every row of the column
            for(PriorityQueue<Integer> pq : columnTreeMap.values()) {
                //In pq we will get the overlaped nodes and because of the property of PriorityQueue will get them in sorted form.
                while (pq.size() > 0) {
                    //We are iterating column in increasing order that's why we have to add the elements in the last arraylist.
                    list.get(list.size()-1).add(pq.poll());
                }
            }
        }
        
        return list;
    }
}
```
> `Time Complexity` : **O(NlogN)**   
> `Space Complexity` : **O(N)** 
----
Video Explanation -> [Vertical Order Traversal of a Binary Tree](https://www.youtube.com/watch?v=q_a6lpbKJdw&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=22) Method 2
<HR>
