# Cycle Detection in Undirected Graph    
### Logic
> Using any traversal if we reach to a visited node and that node is not the parent node then this means that the cycle is present in the graph.

### Using BFS
```java
private class Pair {
    int node;
    int parent;
    public Node(int node, int parent) {
        this.node = node;
        this.parent = parent;
    }
}
class Solution {
    public boolean isCycle(int V, ArrayList<ArrayList<Integer> adj) {
        boolean visited[] = new boolean[V+1];
        for(int i=1; i<=V; i++) {
            if (visited[i] == false) {
                if(checkForCycle(adj, i, visited))
                    return true;
            }    
        }
        return false;
    }
    
    public boolean checkForCycle(ArrayList<ArrayList<Integer> adj, int node, boolean[] visited) {
        Queue<Pair> q = new LinkedList();
        q.add(new Pair(node, -1));
        visited[node] = true;
        
        while(!q.isEmpty()) {
            int node = q.peek().node;
            int parent = q.peek().parent;
            q.poll();
            
            for(Integer it: adj.get(node)) {
                if (visited[it] == false) {
                    visited[it] = true;
                    q.add(new Pair(it, node));
                } else if (it != parent) {
                    return true;
                }
            }
        }
        return false;
    }
}
```
> `Time Complexity` : **O(V + E)**, where V is the number of nodes and E is the number of edges.   
> `Space Complexity` : **O(N) + O(N)**, for visited array and Queue.    
---
Video Explanations -> [Cycle Detection in Undirected Graph using BFS](https://www.youtube.com/watch?v=A8ko93TyOns&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=8)  
<hr>

### Using DFS
```java
class Solution {
    public boolean isCycle(int V, ArrayList<ArrayList<Integer> adj) {
        boolean visited[] = new boolean[V+1];
        for(int i=1; i<=V; i++) {
            if (visited[i] == false) {
                if(checkForCycle(adj, visited, i, -1))
                    return true;
            }    
        }
        return false;
    }
    
    public boolean checkForCycle(ArrayList<ArrayList<Integer> adj, boolean[] visited, int node, int parent) {
        visited[node] = true;
        
        for(Integer neighbour: adj.get(node)) {
            if(visited[neighbour] == false) {
                if(checkForCycle(adj, visited, neighbour, node)) 
                    return true;
            } else if (neighbour != parent) {
                return true;
            }
        }
        return false;
    }
}
```
> `Time Complexity` : **O(V + E)**, where V is the number of nodes and E is the number of edges.   
> `Space Complexity` : **O(N) + O(N)**, for visited array and recursion stack.    
---
Video Explanations -> [Cycle Detection in Undirected Graph using DFS](https://www.youtube.com/watch?v=Y9NFqI6Pzd4&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=9)  
<hr>
