# Topological Sort
> A permutation of vertices for a Directed Acyclic Graph is called Topological Sort if for all directed edges uv, u appears before v in the ordering.
  
### Using DFS
```java
class Solution {
    public void topologicalSort(int V, ArrayList<ArrayList<Integer>> graph) {
        Stack<Integer> st = new Stack();
        boolean[] visited = new boolean[V+1];
        
        for(int i=1; i<=V; i++) {
            if(visited[i] == false) {
                findTopologicalSort(graph, visited, st, i);
            }
        }
        
        while(!st.isEmpty()) {
            System.out.println(st.pop());
        }
    }
    
    public void findTopologicalSort(ArrayList<ArrayList<Integer>> graph, boolean[] visited, Stack<Integer> stack, int node) {
        visited[node] = true;
        for(int neighbour: graph.get(node)) {
            if(visited[neighbour] == false)
                findTopologicalSort(graph, visited, stack, neighbour);
        }
        stack.push(node);
    }
}
```
> `Time Complexity` : **O(V + E)**, where V is the number of nodes and E is the number of edges.   
> `Space Complexity` : **O(N) + O(N) + O(N)**, for visited array, stack and recursion stack.    
---
Video Explanations -> 1)[Topological Sort](https://www.youtube.com/watch?v=6Vi5Td_a8B8&list=PL-Jc9J83PIiHfqDcLZMcO9SsUDY4S3a-v&index=17), 
 2)[Topological Sort](https://www.youtube.com/watch?v=Yh6EFazXipA&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=13)
<hr>

### Using BFS
```java
class Solution {
    public void topologicalSort(int V, ArrayList<ArrayList<Integer>> graph) {
        int[] topologicalSortArray = new int[V];
        int[] inDegree = new int[V+1];
        for(int i=1; i<=V; i++) {
            for(Integer neighbour: graph.get(i)) {
                inDegree[neighbour]++;
            }
        }
        
        Queue<Integer> q = new LinkedList();
        for(int i=1; i<inDegree.size(); i++) {
            if(inDegree[i] == 0) {
                q.add(i);
            }
        }
        int ind = 0;
        while(!q.isEmpty()) {
            int node = q.remove();
            topologicalSortArray[ind++] = node;
            for(int neighbour: graph.get(node)) {
                inDegree[neighbour]--;
                if(inDegree[neighbour] == 0) 
                    q.add(neighbour);
            }
        }
        for(int i: topologicalSortArray) {
            System.out.println(i);
        }
    }
}
```
> `Time Complexity` : **O(V + E)**, where V is the number of nodes and E is the number of edges.   
> `Space Complexity` : **O(N) + O(N) + O(N)**, for indegree array, topological sort array and queue.    
---
Video Explanations -> [Topological Sort (BFS) | Kahn's Algorithm](https://www.youtube.com/watch?v=rZv_jHZva34&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=14)  
<hr>
