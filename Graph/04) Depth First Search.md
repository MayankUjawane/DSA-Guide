# Depth First Search
> DFS technique starts with a root node and then traverses the adjacent nodes of the root node by going deeper into the graph. In the DFS technique, the nodes are 
> traversed depth-wise until there are no more children to explore.
> Once we reach the leaf node (no more child nodes), the DFS backtracks and starts with other nodes and carries out traversal in a similar manner. DFS technique uses 
> a **Stack** data structure to store the nodes that are being traversed.    

```java
class Graph {
    public static void main(String[] args) {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String[] s = br.readLine().trim().split(" ");
        int V = Integer.parseInt(s[0]);
        int E = Integer.parseInt(s[1]);
        
        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();
        for(int i = 0; i < V; i++)
            adj.add(i, new ArrayList<Integer>());
        for(int i = 0; i < E; i++) {
            String[] S = br.readLine().trim().split(" ");
            int u = Integer.parseInt(S[0]);
            int v = Integer.parseInt(S[1]);
            adj.get(u).add(v);
            adj.get(v).add(u);
        }
        
        DFS obj = new DFS();
        ArrayList<Integer> ans = new ArrayList<>();
        boolean visited[] = new boolean[V+1];
        for(int i=1; i<=V; i++) {
            if (visited[i] == false) {
                obj.dfs(i, visited, adj, ans);
            }    
        }
        for(int i = 0; i < ans.size(); i++) 
            System.out.print(ans.get(i) + " ");  
    }
}

class DFS {
    public void dfs(int node, boolean visited[], ArrayList<ArrayList<Integer>> adj, ArrayList<Integer> ans) {
        ans.add(node);
        visited[node] = true;
        for(int it: adj.get(node)) {
            if (visited[it] == false) {
                dfs(it, visited, adj, ans);
            }    
        } 
    }
}
```
> `Time Complexity` : **O(V + E)**, where V is the number of nodes and E is the number of edges.   
> `Space Complexity` : **O(N) + O(N)**, for visited array and recursion stack.    
---
Video Explanations -> [Depth First Search](https://www.youtube.com/watch?v=uDWljP2PGmU&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=7)  
<hr>
