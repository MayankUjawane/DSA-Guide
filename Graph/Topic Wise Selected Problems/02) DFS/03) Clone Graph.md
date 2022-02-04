# Clone Graph
Question -> [Clone Graph](https://leetcode.com/problems/clone-graph/)    

### Implementation
```java
class Solution {
    public Node cloneGraph(Node node) {
        if(node == null) {
            return null;
        }
        // T.C.-> O(N), where N = number of nodes, since we are performing dfs for every Node once
        // S.C.-> O(N), where N = number of nodes, since dfs can go deep till all the nodes
        return dfs(node, new HashMap<>());
    }
    public Node dfs(Node node, Map<Node,Node> map) {
        // Create node for clone graph
        Node cloneNode = new Node(node.val);
        
        // Map cloneNode with original node
        map.put(node, cloneNode);
        
        // iterate over all neighbors
        for(Node neighbor: node.neighbors) {
            Node cloneNeighbor;
            // if we had already created the clone node for this neighbor
            if(map.containsKey(neighbor)) {
                cloneNeighbor = map.get(neighbor); 
            } else {
                cloneNeighbor = dfs(neighbor, map);
            }
            // add the clone neighbor
            cloneNode.neighbors.add(cloneNeighbor);
        }
        
        return cloneNode;
    }
}
```
> `Time Complexity` : **O(N)**, where N = number of nodes     
> `Space Complexity` : **O(N)**, where N = number of nodes
---
Video Explanations -> [Clone Graph](https://www.youtube.com/watch?v=e5tNvT1iUXs)
<hr>
