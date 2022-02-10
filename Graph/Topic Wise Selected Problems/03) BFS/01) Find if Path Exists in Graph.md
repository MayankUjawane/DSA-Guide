# Find if Path Exists in Graph
Question -> [Find if Path Exists in Graph](https://leetcode.com/problems/find-if-path-exists-in-graph/)    

```java
class Solution {
    public boolean validPath(int n, int[][] edges, int start, int end) {
        if(start == end) return true;
        
        // S.C.-> O(V+E), where V = number of vertices and E = number of edges
        List<List<Integer>> graph = new ArrayList<>();        
        // T.C.-> O(V)
        for (int i = 0; i < n; i++) {
            graph.add(new ArrayList<>());
        }
        // T.C.-> O(E)
        for (int[] edge : edges) {
            graph.get(edge[0]).add(edge[1]);
            graph.get(edge[1]).add(edge[0]);
        }
        
        // S.C.-> O(V), where V = n = number of vertices
        boolean visited[] = new boolean[n];
        // S.C.-> O(V)
        Queue<Integer> q = new LinkedList<>();
        q.offer(start);
        visited[start] = true;
        
        // In total this loop will run for O(E) times
        while (!q.isEmpty()) {
            int node = q.poll();
            // Add all unvisited neighbors to the queue.
            for (int neighbor : graph.get(node)) {
                if(neighbor == end) return true;
                if(!visited[neighbor]) {
                    q.offer(neighbor);
                    visited[node] = true;
                }
            }
        }
        // No path exists between start and end
        return false;
    }
}
```
> `Time Complexity` : **O(V+E)**     
> `Space Complexity` : **O(V+E)**
---
