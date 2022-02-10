# Find if Path Exists in Graph
Question -> [Find if Path Exists in Graph](https://leetcode.com/problems/find-if-path-exists-in-graph/)    

### Recursive
```java
class Solution {
    public boolean validPath(int n, int[][] edges, int source, int destination) {
        // S.C.-> O(V), where V = n = number of vertices
        boolean[] vis = new boolean[n];
        // S.C.-> O(V+E), where V = number of vertices and E = number of edges
        ArrayList<ArrayList<Integer>> graph = new ArrayList<>();
        // T.C.-> O(V)
        for(int i=0; i<n; i++) {
            graph.add(new ArrayList<>());
        }
        // T.C.-> O(E)
        for(int[] edge: edges) {
            int u = edge[0];
            int v = edge[1];
            graph.get(u).add(v);
            graph.get(v).add(u);
        }
        // dfs will take T.C.-> O(V+E) and S.C.-> O(V) for vertices
        return dfs(graph, vis, source, destination);
    }
    public boolean dfs(ArrayList<ArrayList<Integer>> graph, boolean[] vis, int s, int d) {
        if(s == d) {
            return true;
        }
        if(vis[s] == false) {
            vis[s] = true;
            for(int neighbour: graph.get(s)) {
                if(vis[neighbour] == false) {
                    boolean returnedAns = dfs(graph, vis, neighbour, d);
                    if(returnedAns == true) return true;
                }
            }
        }
        return false;
    }
}
```
> `Time Complexity` : **O(V+E)**     
> `Space Complexity` : **O(V+E)**
---
### Iterative
```java
class Solution {
    public boolean validPath(int n, int[][] edges, int start, int end) {
        // S.C.-> O(V+E), where V = number of vertices and E = number of edges
        List<List<Integer>> graph = new ArrayList<>();        
        for (int i = 0; i < n; i++) {
            graph.add(new ArrayList<>());
        }
        for (int[] edge : edges) {
            graph.get(edge[0]).add(edge[1]);
            graph.get(edge[1]).add(edge[0]);
        }
        // S.C.-> O(V)
        Deque<Integer> stack = new ArrayDeque<>();
        stack.push(start);
        // S.C.-> O(V), where V = n = number of vertices
        boolean visited[] = new boolean[n];
        
        // In the while loop, at most, we will visit vertex once.
        // The for loop inside the while loop will have a cumulative sum of at most E iterations 
        // since it will iterate over all of the node's neighbors for each node.
        // In total loop will run for O(V+E) times
        while (!stack.isEmpty()) {
            int node = stack.pop();
            // Check if we have reached the target node.
            if (node == end) {
                return true;
            }
            // Check if we've already visited this node.
            if (visited[node]) {
                continue;
            }
            visited[node] = true;
            
            // Add all neighbors to the stack.
            for (int neighbor : graph.get(node)) {
                stack.push(neighbor);
            }
        }
        return false;
    }
}
```
> `Time Complexity` : **O(V+E)**     
> `Space Complexity` : **O(V+E)**
---
