# Bellman Ford Algorithm | Detect Negative Weight Cycle in Graphs
> Given a graph and a source vertex 'src' in graph, find shortest paths from src to all vertices in the given graph. The graph may contain **negative weight edges**. 
> We have discussed Dijkstra’s algorithm for this problem. Dijkstra’s algorithm is a Greedy algorithm and time complexity is **O((V+E)LogV)**. Dijkstra doesn’t work for Graphs 
> with **negative weight edges**, Bellman-Ford works for such graphs. Bellman-Ford is also simpler than Dijkstra and suites well for distributed systems. But **time complexity of 
> Bellman-Ford is O(VE)**, which is more than Dijkstra. 
> 
### Algorithm 
> Following are the detailed steps.
> Input: Graph and a source vertex src 
> Output: Shortest distance to all vertices from src. If there is a negative weight cycle, then shortest distances are not calculated, negative weight cycle is reported.
> 1) This step initializes distances from the source to all vertices as infinite and distance to the source itself as 0. Create an array dist[] of size |V| with all values 
> as infinite except dist[src] where src is source vertex.
> 2) This step calculates shortest distances. Do following |V|-1 times where |V| is the number of vertices in given graph.        
>    a) Do following for each edge u-v         
>        If dist[v] > dist[u] + weight of edge uv, then update dist[v]          
>          dist[v] = dist[u] + weight of edge uv         
> 3) This step reports if there is a negative weight cycle in graph. Do following for each edge u-v 
> If dist[v] > dist[u] + weight of edge uv, then “Graph contains negative weight cycle” 
> The idea of step 3 is, step 2 guarantees the shortest distances if the graph doesn’t contain a negative weight cycle. If we iterate through all edges one more time and get
> a shorter path for any vertex, then there is a negative weight cycle.
```java
class Main {
    private class Node {
        int src;
        int dest;
        int weight;
        Node(int src, int dest, int weight) {
            this.src = src;
            this.dest = dest;
            this.weight = weight;
        }
    }
    public static void main(String args[]) {
        int n = 6;
        ArrayList<Node> adj = new ArrayList<>();
            
        adj.add(new Node(3, 2, 6));
        adj.add(new Node(5, 3, 1));
        adj.add(new Node(0, 1, 5));
        adj.add(new Node(1, 5, -3));
        adj.add(new Node(1, 2, -2));
        adj.add(new Node(3, 4, -2));
        adj.add(new Node(2, 4, 3));
        
        Main obj = new Main();
        obj.bellmanFord(adj, n, 0);
    }
  
    public void bellmanFord(ArrayList<Node> edges, int N, int src) {
        int distance[] = new int[N];
        // Step 1: Initialize distances from src to all other vertices as INFINITE
        for(int i=0; i<N; i++) distance[i] = Integer.MAX_VALUE;
        
        distance[src] = 0;
        // Step 2: Relax all edges |V| - 1 times. A simple shortest path from src to any other vertex can have at-most |V| - 1 edges
        for(int i=0; i<N-1; i++) {
            for(Node node: edges) {
                if(distance[node.src] == Integer.MAX_VALUE) {
                    continue;
                }
                if(distance[node.src] + node.weight < distance[node.dest]) {
                    distance[node.dest] = distance[node.src] + node.weight;
                }
            }
        }
        // Step 3: check for negative-weight cycles. The above step guarantees shortest distances if graph doesn't
        // contain negative weight cycle. If we get a shorter path in the below loop, then there is a negative weight cycle.
        int flag = 0;
        for(Node node: edges) {
            if((distance[node.src] != Integer.MAX_VALUE) && (distance[node.src] + node.weight < distance[node.dest])) {
                flag = 1;
                System.out.println("Negative Cycle is present");
                break;
            }
        }
        // Step 4: Print the shortest distances from src to every vertex
        if(flag == 0) {
            for(int i=0; i<N; i++) {
                System.out.println(src + " -> " + i + " @ " + distance[i]);
            }
        }
    }  
}
```
> `Time Complexity` : **O(VE)** , where V is the number of nodes and E is the number of edges.           
> `Space Complexity` : **O(V)**, for distance array.    
---
Video Explanation -> [Pepcoding](https://www.youtube.com/watch?v=IjEX4rgxsvI), 
[Striver](https://www.youtube.com/watch?v=75yC1vbS8S8&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=28)
<hr>
