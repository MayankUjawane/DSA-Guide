# Bridges or Cut Edges in a Graph  
> Those edges are called bridges in a graph on whose removal the graph is broken into two or more number of components.

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
        obj.findBridges(adj, n);
    }
  
    public void findBridges(ArrayList<ArrayList<Integer>> adj, int N) {
        int vis[] = new int[N];
        int disc[] = new int[N]; //discover time
        int low[] = new int[N];  //low time
        int time = 0;
        for(int i=0; i<N; i++) {
            if(vis[i] == false) {
                dfs(i, -1, vis, disc, low, time, adj);
            }
        }
    }
  
    public void dfs(int node, int parent, int[] vis, int[] disc, int[] low, int time, ArrayList<ArrayList<Integer>> adj) {
        vis[node] = true;
        disc[node] = low[node] = time++;
        
        for(Integer neighbour: adj.get(node)) {
            if(neighbour == parent) continue;
            if(vis[neighbour] == true) {
                low[node] = Math.min(low[node], disc[neighbour]);
            } else {
                dfs(neighbour, node, vis, disc, low, time, adj);
                low[node] = Math.min(low[node], low[neighbour]);
              
                if(low[neighbour] > disc[node]) {
                    System.out.println(node + "->" + neighbour);
                }
            }
        }
    }  
}
```
> `Time Complexity` : **O(V + E)** , where V is the number of nodes and E is the number of edges.   
> `Space Complexity` : **O(N) + O(N) + O(N) + O(N)**, for discover array, low array, visited array and recursion stack.    
---
Video Explanation -> [Pepcoding](https://www.youtube.com/watch?v=BsxYwt7A9Wc&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=24), 
[Striver](https://www.youtube.com/watch?v=2rjZH0-2lhk&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=25)
<hr>
