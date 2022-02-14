# Minimum Height Trees
Question -> [Minimum Height Trees](https://leetcode.com/problems/minimum-height-trees/)    

### Implementation
```java
class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {
        List<Integer> result = new ArrayList();
        // If the tree only has 2 or less nodes
        if(n <= 2) {
            for(int i=0; i<n; i++) {
                result.add(i);
            }
            return result;
        }
        
        int[] degree = new int[n];
        List<List<Integer>> adj = new ArrayList();
        for(int i=0; i<n; i++) {
            adj.add(new ArrayList());
        }
        for(int[] edge: edges) {
            adj.get(edge[0]).add(edge[1]);
            adj.get(edge[1]).add(edge[0]);
            degree[edge[0]]++;
            degree[edge[1]]++;
        }
        
        Queue<Integer> q = new LinkedList();
        // adding the first layer of leaves to the Queue
        for(int i=0; i<n; i++) {
            if(degree[i] == 1) q.add(i);
        }
        
        // Trim the leaves until reaching the centroids
        int remainingNodes = n;
        // we are radially removing all the leaf nodes till we are left with 1 or 2 centroid nodes of the graph
        while(remainingNodes > 2) {
            int size = q.size();
            remainingNodes -= size;
            
            // removing the current leaf nodes
            for(int i=0; i<size; i++) {
                int top = q.poll();

                for(int ngb: adj.get(top)) {
                    degree[ngb]--;
                    // adding the new leaf nodes to the Queue
                    if(degree[ngb] == 1) q.add(ngb);
                }    
            }
        }
        
        // at the end Queue will contain only centroid or root nodes
        while(!q.isEmpty()) {
            result.add(q.poll());
        }
        
        return result;
    }
}
``` 
> `Time Complexity` : **O(V+E) = O(V)** in question it is given that E=V-1              
> `Space Complexity` : **O(V)**   
---
