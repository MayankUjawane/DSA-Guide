# All Nodes Distance K in Binary Tree
Try to solve the question [All Nodes Distance K in Binary Tree](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/) first with your own.

### Method 1
```java
class Solution {
    public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
        List<Integer> answer = new ArrayList();
        if (root == null) return answer;
        
        Map<TreeNode, TreeNode> parentMap = new HashMap();
        connectParentAndChild(root, parentMap);
        
        Map<TreeNode, Boolean> visitedNodes = new HashMap();
        Queue<TreeNode> queue = new LinkedList();
        queue.offer(target);
        int level = 0;
        
        while (!queue.isEmpty()) {
            if (level == k) break;
          
            int size = queue.size();
            for (int i=0; i<size; i++) {
                TreeNode top = queue.poll();
                visitedNodes.put(top, true);
                if (top.left != null && !visitedNodes.containsKey(top.left)) queue.offer(top.left);
                if (top.right != null && !visitedNodes.containsKey(top.right)) queue.offer(top.right);
                if (parentMap.get(top) != null && !visitedNodes.containsKey(parentMap.get(top))) queue.offer(parentMap.get(top));
            }
            level++;
        }
                    
        while (!queue.isEmpty()) {
            answer.add(queue.poll().val);
        }
        
        return answer;
    }
    
    public void connectParentAndChild(TreeNode root, Map<TreeNode, TreeNode> parentMap) {
        if (root == null) return;
        
        // connecting childs with parent
        if (root.left != null) parentMap.put(root.left, root);
        if (root.right != null) parentMap.put(root.right, root);
        
        connectParentAndChild(root.left, parentMap);
        connectParentAndChild(root.right, parentMap);
    }
}
```
> `Time Complexity` : **O(N)**   
> `Space Complexity` : **O(N)**   
---
Video Explanations -> 1) [All Nodes Distance K in Binary Tree](https://www.youtube.com/watch?v=i9ORlEy6EsI&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=31)  2) [All Nodes Distance K in Binary Tree](https://www.youtube.com/watch?v=nPtARJ2cYrg)
<hr>

### Method 2
```java
class Solution {
    public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
        List<Integer> answer = new ArrayList();
        distanceKHelper(root, target, k, answer);
        return answer;
    }
    
    public int distanceKHelper(TreeNode root, TreeNode target, int k, List<Integer> answer) {
        if (root == null) return -1;
        
        if (root == target) {
            kLevelDown(root, k, null, answer);
            return 1;
        }
        
        int leftDistance = distanceKHelper(root.left, target, k, answer);
        if (leftDistance != -1) {
            kLevelDown(root, k - leftDistance, root.left, answer);
            return leftDistance+1;
        }
        
        int rightDistance = distanceKHelper(root.right, target, k, answer);
        if (rightDistance != -1) {
            kLevelDown(root, k - rightDistance, root.right, answer);
            return rightDistance+1;
        }
        
        return -1;
    }
    
    public void kLevelDown(TreeNode root, int k, TreeNode blocker, List<Integer> answer) {
        if (root == blocker || k < 0 || root == null) return;
        
        if (k == 0) answer.add(root.val);
        
        kLevelDown(root.left, k-1, blocker, answer);
        kLevelDown(root.right, k-1, blocker, answer);
    }
}
```
> `Time Complexity` : **O(N)**   
> `Space Complexity` : **O(N)**   
---
Video Explanations -> [Print Nodes K Level Far](https://www.youtube.com/watch?v=B89In5BctFA), [Print K Levels Down](https://www.youtube.com/watch?v=KvcfuGcdDMg), [Node to Root Path](https://www.youtube.com/watch?v=1Kyc-zQS7eQ)        
Video Explanation (Optimized) -> [All Nodes Distance K in Binary Tree](https://www.youtube.com/watch?v=s22QClql9LU)
<hr>
