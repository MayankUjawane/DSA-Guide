# Breadth First Search
> BFS is a traversing algorithm where you should start traversing from a selected node (source or starting node) and traverse the graph layerwise thus exploring 
> the neighbour nodes (nodes which are directly connected to source node). You must then move towards the next-level neighbour nodes.     

```java
class Graph {
    public static void main(String[] args) {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int T = Integer.parseInt(br.readLine().trim());
        while(T-- > 0) {
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
            BFS obj = new BFS();
            ArrayList<Integer> ans = obj.bfsOfGraph(V, adj);
            for(int i = 0; i < ans.size(); i++) 
                System.out.print(ans.get(i) + " ");
        }
    }
}

class BFS {
    public ArrayList<Integer> bfsOfGraph(int V, ArrayList<ArrayList<Integer>> adj) {
        ArrayList<Integer> bfs = new ArrayList<>(); 
        boolean vis[] = new boolean[V+1]; 
        Queue<Integer> q = new LinkedList<>();
        q.add(0); 
        vis[1] = true; 
        
        while (!q.isEmpty()) {
            Integer node = q.poll();
            bfs.add(node); 
 
            // Get all adjacent vertices of the dequeued vertex s
            // If a adjacent has not been visited, then mark it
            // visited and enqueue it
            for(Integer it: adj.get(node)) {
                if(vis[it] == false) {
                    vis[it] = true; 
                    q.add(it); 
                } 
            }
        }
        
        return bfs; 
    }
}
```
> `Time Complexity` : **O(V + E)**, where V is the number of nodes and E is the number of edges.   
> `Space Complexity` : **O(N) + O(N)**, for visited array and queue.    
---
Video Explanations -> [Breadth First Search](https://www.youtube.com/watch?v=UeE67iCK2lQ&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=6)  
<hr>
