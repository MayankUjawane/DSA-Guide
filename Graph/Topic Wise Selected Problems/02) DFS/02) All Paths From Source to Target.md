# All Paths From Source to Target
Question -> [All Paths From Source to Target](https://leetcode.com/problems/all-paths-from-source-to-target/)    

### Implementation
```java
class Solution {
    // given that the graph is DAG so there will be no cycles, so not required to maintain visited array
    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        List<List<Integer>> paths = new ArrayList<>();
        if (graph == null || graph.length == 0) {
            return paths;
        }

        // T.C.-> O(E) since loop will only for edges
        // S.C.-> O(V) since dfs can go deep till all vertices so maximum recursion stack will take O(V)
        dfs(graph, 0, new ArrayList<>(), paths);
        return paths;
    }

    void dfs(int[][] graph, int node, List<Integer> path, List<List<Integer>> paths) {
        if (node == graph.length - 1) {
            path.add(node);
            paths.add(new ArrayList<>(path));
            path.remove(path.size() - 1);
            return;
        }
        
        for(int neighbour: graph[node]) {
            path.add(node);
            dfs(graph, neighbour, path, paths);
            path.remove(path.size() - 1);
        }
    }
}
```
> `Time Complexity` : **O(E)**     
> `Space Complexity` : **O(V)**
---
