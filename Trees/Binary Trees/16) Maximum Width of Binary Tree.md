#  Maximum Width of Binary Tree
Try to solve the question [Maximum Width of Binary Tree](https://leetcode.com/problems/maximum-width-of-binary-tree/) first with your own.

> **`Logic`**   
> If the index of a node is i (assume root begins with index 1), the indices of its two children are (2*i) and (2*i + 1).      
> If the root begins with index 0 in the array, and the index of a node is i, then the indices of its two children are (2*i + 1) and (2*i + 2).

### Level Traversal (BFS)
```java
class Solution {
   private class Pair {
        TreeNode node;
        int index;
        Pair(TreeNode node, int index) {
            this.node = node;
            this.index = index;
        }
    }
    
    public int widthOfBinaryTree(TreeNode root) {
        if (root == null) return 0;
        
        int maxWidth = 0;
        Queue<Pair> queue = new LinkedList();
        queue.offer(new Pair(root, 0));
        
        while(!queue.isEmpty()) {
            int size = queue.size();
            int first = 0, last = 0;
            int minIndex = queue.peek().index;
            for(int i=0; i<size; i++) {
                Pair top = queue.poll();
                int index = top.index - minIndex;
                
                if(i == 0) first = index;
                if(i == size-1) last = index;
                
                // the root begins with index 1, so for the node having index i, the indices of its two children are 2*i + 1 and 2*i + 2.
                if(top.node.left != null) queue.offer(new Pair(top.node.left, 2*index+1));
                if(top.node.right != null) queue.offer(new Pair(top.node.right, 2*index+2));
            }
            int width = last-first+1;
            maxWidth = Math.max(maxWidth, width);
        }
        return maxWidth;
    } 
}
```
> `Time Complexity` : **O(N)**   
> `Space Complexity` : **O(N)**   
---
Video Explanations -> [Maximum Width of Binary Tree](https://www.youtube.com/watch?v=ZbybYvcVLks&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=29)
<hr>

### DFS
```java
class Solution {

	public int widthOfBinaryTree1(TreeNode root) {
    int[] maxWidth = new int[1];
		List<Integer> levelHeads = new ArrayList<>(); // first nodes at each level;
		dfs(root, 1, 0, levelHeads, maxWidth);
		return maxWidth[0];
	}

	private void dfs(TreeNode node, int index, int level, List<Integer> levelHeads, int[] maxWidth) {
		if (level == levelHeads.size()) levelHeads.add(index);   // add first node
		maxWidth[0] = Math.max(maxWidth[0], index - levelHeads.get(depth) + 1);

    // the root begins with index 0, so for the node having index i, the indices of its two children are 2*i and 2*i + 1.
		if (node.left != null)
			dfs(node.left, index * 2, level + 1, levelHeads, maxWidth);
		if (node.right != null)
			dfs(node.right, index * 2 + 1, level + 1, levelHeads, maxWidth);
	}
}
```
> `Time Complexity` : **O(N)**   
> `Space Complexity` : **O(N)**   
---
Video Explanations -> [Maximum Width of Binary Tree](https://www.youtube.com/watch?v=YP_wb6pX0lk)
<hr>
