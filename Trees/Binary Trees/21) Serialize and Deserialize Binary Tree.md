# Serialize and Deserialize Binary Tree
Try to solve the question [Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/) first with your own.     

### Using Preorder Traversal
```java
class Solution {
    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        serialize(root, sb);
        return sb.toString();
    }
    
    public void serialize(TreeNode root, StringBuilder sb) {
        if (root == null) {
            sb.append("null,");
            return;
        };
        
        sb.append(root.val).append(",");
        serialize(root.left, sb);
        serialize(root.right, sb);
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        String[] arr = data.split(",");
        int[] index = {-1};
        return deserialize(arr, index);
    }
    
    public TreeNode deserialize(String[] arr, int[] index) {
        index[0]++;
        
        if (index[0] == arr.length || arr[index[0]].equals("null")) return null;    
        
        TreeNode root = new TreeNode(Integer.parseInt(arr[index[0]]));
        root.left = deserialize(arr, index);
        root.right = deserialize(arr, index);
        
        return root;
    }
}      
```
> `Time Complexity` : **O(N)**    
> `Space Complexity` : **O(N)**    
---
### Using Level-order Traversal
```java
class Solution {
    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        if (root == null) return "";
        StringBuilder sb = new StringBuilder();
        Queue<TreeNode> queue = new LinkedList();
        queue.offer(root);
        
        while (queue.size() > 0) {
            TreeNode top = queue.poll();
            if (top == null) {
                sb.append("null,");
                continue;
            } else {
                sb.append(top.val).append(",");
            }

            queue.offer(top.left);
            queue.offer(top.right);
        }
        
        return sb.toString();
    }
    
    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data.equals("")) return null;
        String[] arr = data.split(",");
        
        Queue<TreeNode> queue = new LinkedList();
        TreeNode root = new TreeNode(Integer.parseInt(arr[0]));
        queue.offer(root);
        
        for(int index = 1; index < arr.length; index++) {
            TreeNode node = queue.poll();
            
            if (!arr[index].equals("null")) {
                TreeNode left = new TreeNode(Integer.parseInt(arr[index]));
                node.left = left;
                queue.offer(left);
            }

            if (++index < arr.length && !arr[index].equals("null")) {
                TreeNode right = new TreeNode(Integer.parseInt(arr[index]));
                node.right = right;
                queue.offer(right);
            }
        }
        
        return root;
    }
}      
```
> `Time Complexity` : **O(N)**    
> `Space Complexity` : **O(N)**    
---
Video Explanations -> [Serialize and Deserialize Binary Tree](https://www.youtube.com/watch?v=-YbXySKJsX8&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=37)  
<hr>
