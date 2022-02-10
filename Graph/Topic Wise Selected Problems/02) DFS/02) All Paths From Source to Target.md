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
> `Time Complexity` : **O((2^V)\*V)**, where V represents the number of vertices.   
> * For a directed acyclic graph (DAG) with V vertices, there could be at most **2^{V - 1} - 1** possible paths to go from the starting vertex to the target vertex. We need **O(V)** time to build each such path.
> * Therefore, a loose upper bound on the time complexity would be **(2^{V - 1} - 1) \* O(V) = O(2^V \* V)**.          
> * Since we have overlapping between the paths, the actual time spent on the traversal will be lower to some extent.        
> 
> `Space Complexity` : **O(V)**   
> * The recursion depth can be no more than **V**, and we need **O(V)** space to store all the previously visited vertices while recursively traversing deeper with the current path. Please note that we don't count the space usage for the output, i.e., to store all the paths we obtained.
---
