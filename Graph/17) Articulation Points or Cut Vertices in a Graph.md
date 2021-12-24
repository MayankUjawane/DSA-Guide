# Articulation Points or Cut Vertices in a Graph  
> A vertex in an undirected connected graph is an articulation point (or cut vertex) if removing it (and edges through it) disconnects the graph. 
> Articulation points represent vulnerabilities in a connected network – single points whose failure would split the network into 2 or more components.

```java
class Main {
    public static void main(String args[]) {
        int n = 5;
        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();
        for(int i=0; i<n; i++) 
            adj.add(new ArrayList<Integer>());
            
        adj.get(0).add(1);
        adj.get(1).add(0);
      
        adj.get(0).add(2);
        adj.get(2).add(0);
          
        adj.get(1).add(2);
        adj.get(2).add(1);
      
        adj.get(1).add(3);
        adj.get(3).add(1);
      
        adj.get(3).add(4);
        adj.get(4).add(3);
        
        Main obj = new Main();
        obj.findArticulationPoint(adj, n);
    }
  
    public void findArticulationPoint(ArrayList<ArrayList<Integer>> adj, int N) {
        int vis[] = new int[N];
        int disc[] = new int[N]; //discover time
        int low[] = new int[N];  //low time
        int isArticulation[] = new int[N];
        int time = 0;
        for(int i=0; i<N; i++) {
            if(vis[i] == false) {
                dfs(i, -1, vis, disc, low, isArticulation, time, adj);
            }
        }
        for(int i=0; i<N; i++) {
            if(isArticulation[i] == true) System.out.println(i);
        }
    }
  
    public void dfs(int node, int parent, int[] vis, int[] disc, int[] low, int[] isArticulation, int time, ArrayList<ArrayList<Integer>> adj) {
        vis[node] = true;
        disc[node] = low[node] = time++;
        int child = 0;
        for(Integer neighbour: adj.get(node)) {
            if(neighbour == parent) continue;
            if(vis[neighbour] == true) {
                low[node] = Math.min(low[node], disc[neighbour]);
            } else {
                child++; //child will be equal to the number of dfs calls
                dfs(neighbour, node, vis, disc, low, isArticulation, time, adj);
                low[node] = Math.min(low[node], low[neighbour]);
                if((low[neighbour] >= disc[node]) && (parent != -1)) {
                    isArticulation[node] = true;
                }
            }
        }
        if((parent == -1) && (child > 1)) isArticulation[node] = true; //for the starting node
    }  
}
```
> `Time Complexity` : **O(V + E)** , where V is the number of nodes and E is the number of edges.   
> `Space Complexity` : **O(N) + O(N) + O(N) + O(N)**, for discover array, low array, visited array and recursion stack.    
---
Video Explanation -> Articulation Point -> [Pepcoding](https://www.youtube.com/watch?v=sAk4W8q0Rmw&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=24), 
[Striver](https://www.youtube.com/watch?v=3t3JHswP7mw&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=27)
<hr>
