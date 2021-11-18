# Kosaraju Algorithm
> Kosaraju algorithm is used to find the number of **Strongly Connected Components (SCC)** in a graph.     
> A directed graph is strongly connected if there is a path between all pairs of vertices. A strongly connected component (SCC) of a directed graph is a **maximal 
> strongly connected** subgraph. For example, there are 3 SCCs in the following graph. 
> ![SCC](https://media.geeksforgeeks.org/wp-content/cdn-uploads/SCC.png)      
> We can find all strongly connected components in **O(V+E)** time using Kosaraju’s algorithm. Kosaraju’s algorithm contains 3 steps-
> * Create an empty stack ‘S’ and do DFS traversal of a graph. In DFS traversal, after calling recursive DFS for adjacent vertices of a vertex, push the vertex to 
> stack(i.e., post order). In the above graph, if we start DFS from vertex 0, we get vertices in stack as 1, 2, 4, 3, 0 **(Topological order)**.
> * Reverse directions of all edges to obtain the transpose graph.
> * One by one pop a vertex from S while S is not empty. Let the popped vertex be ‘v’. Take v as source and do DFS (call DFSUtil(v)). The DFS starting from v prints 
> strongly connected component of v.

```java
class Main {
    public static void main(String args[]) {
        int n = 5;
        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();
        for(int i=0; i<n; i++) 
            adj.add(new ArrayList<Integer>());
            
        adj.get(0).add(1);
        adj.get(1).add(2);
        adj.get(2).add(0);
        adj.get(1).add(3);
        adj.get(3).add(4);
        
        Main obj = new Main();
        obj.kosaraju(adj, n);
    }
  
    public void kosaraju(ArrayList<ArrayList<Integer>> adj, int N) {
        boolean[] vis = new boolean[N];
        Stack<Integer> st = new Stack<>();
        //Setp-1 Sorting the nodes in topological order and storing them in the stack
        boolean topo = true;
        for(int i=0; i<N; i++) {
            if(vis[i] == false) {
                dfs(i, vis, st, topo, adj);
            }
        }
        
        //Step-2 Transpose Graph
        ArrayList<ArrayList<Integer>> transposeGraph = new ArrayList<>();
        for(int i=0; i<N; i++) 
            transposeGraph.add(new ArrayList<Integer>());
      
        for(int i=0; i<N; i++) {
            vis[i] = false; //making the nodes unvisited again so that we can use vis array again in the step-3
            for(Integer neighbour: adj.get(i)) {
                transposeGraph.get(neighbour).add(i);
            }  
        }  
      
        //Setp-3 Traverse the transposed graph in the order of vetices stored in the Stack
        topo = false;
        while(!st.isEmpty()) {
            int node = st.pop();
            if(!vis[node]) {
                System.out.print("SCC: ");
                dfs(node, vis, st, topo, transposeGraph);  
                System.out.println();
            }
        }  
    }
  
    public void dfs(int node, boolean[] vis, Stack<Integer> st, boolean topo, ArrayList<ArrayList<Integer>> adj) {
        vis[node] = true;
        if(topo == false) System.out.print(node + " ");
        for(Integer neighbour: adj.get(node)) {
            if(vis[neighbour] == false) {
                dfs(neighbour, vis, st, topo, adj);  
            }  
        }
        if(topo) {
            st.push(node);
        }
    }  
}
```
> `Time Complexity` : **O(V + E) + O(V + E) + O(V + E)** , where V is the number of nodes and E is the number of edges.   
> The Kosaraju's Algorithm calls DFS, finds reverse of the graph and again calls DFS. DFS takes O(V+E) for a graph represented using adjacency list. 
> Reversing a graph also takes O(V+E) time. For reversing the graph, we simple traverse all adjacency lists.        
> 
> `Space Complexity` : **O(V + E) + O(V) + O(V) + O(V)**, for transponse graph, stack, visited array and recursion stack.    
---
Video Explanation -> [Pepcoding](https://www.youtube.com/watch?v=QtdE7QPsWiU), 
[Striver](https://www.youtube.com/watch?v=V8qIqJxCioo&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=27)
<hr>
