# Cycle Detection in Directed Graph

### Using DFS
```java
class Solution {
    public boolean isCycle(int V, ArrayList<ArrayList<Integer>> adj) {
        boolean visited[] = new boolean[V+1];
        boolean dfsVisited[] = new boolean[V+1];
        for(int i=1; i<=V; i++) {
            if (visited[i] == false) {
                if(checkCycle(adj, visited, dfsVisited, i))
                    return true;
            }    
        }
        return false;
    }
    
    public boolean checkCycle(ArrayList<ArrayList<Integer>> adj, boolean[] visited, boolean[] dfsVisited, int node) {
        visited[node] = true;
        dfsVisited[node] = true;
        for(Integer neighbour: adj.get(node)) {
            if(visited[neighbour] == false) {
                if(checkCycle(adj, visited, dfsVisited, neighbour)) 
                    return true;
            } else if (dfsVisited[neighbour] == true) {
                return true;
            }
        }
        dfsVisited[node] = false;
        return false;
    }
}
```
> `Time Complexity` : **O(V + E)**, where V is the number of nodes and E is the number of edges.   
> `Space Complexity` : **O(N) + O(N) + O(N)**, for visited array, dfs visited array and recursion stack.    
---
Video Explanations -> [Cycle Detection in Directed Graph using DFS](https://www.youtube.com/watch?v=uzVUw90ZFIg&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=12)  
<hr>
