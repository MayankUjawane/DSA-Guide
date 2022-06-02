# Preorder Inorder Postorder Traversals in One Traversal

### Implementation
```java
public void treeTraversal(TreeNode root) {
    List<Integer> pre = new ArrayList();
    List<Integer> in = new ArrayList();
    List<Integer> post = new ArrayList();

    if(root == null) return post;

    Stack<Pair> st = new Stack();
    st.push(new Pair(root,1));

    while(st.size() > 0) {
        Pair top = st.peek();

        if(top.state == 1) {
            pre.add(top.node.val);
            if(top.node.left != null) {
                st.push(new Pair(top.node.left,1));
            }
            top.state++;
        } else if(top.state == 2) {
            in.add(top.node.val);
            if(top.node.right != null) {
                st.push(new Pair(top.node.right,1));
            }
            top.state++;
        } else {
            post.add(top.node.val);
            st.pop();
        }
    }
}
```
> `Time Complexity` **O(3N)**     
> `Space Complexity` **O(3N)**    
----   
YouTube video [One Traversal](https://youtu.be/ySp2epYvgTE?list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk)
