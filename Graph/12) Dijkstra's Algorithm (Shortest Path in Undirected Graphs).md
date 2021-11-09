# Dijkstra's Algorithm | Shortest Path in Undirected Graphs
> **Dijkstra's algorithm** is an algorithm for finding the **shortest paths** between nodes in a graph, which may represent, for example, road networks.
> **Dijkstra's algorithm** makes use of weights of the edges for finding the path that minimizes the total distance (weight) among the source node and
> all other nodes. This algorithm is also known as the **single-source shortest path algorithm**.
> Dijkstra's Algorithm is unable to handle **negative edges**.

```java
class Pair implements Comparable<Pair> {
    int value;
    int weight;
    Pair(int value, int weight) {
        this.value = value;
        this.weight = weight;
    }
    public int compareTo(Pair o) {
        return (this.weight - o.weight);
    }
}
class Main {
    public static void main(String args[]) {
        int n = 5;
        ArrayList<ArrayList<Pair>> adj = new ArrayList<ArrayList<Pair>>();
        
        for(int i=0; i<n; i++)
            adj.add(new ArrayList<Pair>>());
            
        adj.get(0).add(new Pair(1, 2));
        adj.get(1).add(new Pair(0, 2));
      
        adj.get(1).add(new Pair(2, 4));
        adj.get(2).add(new Pair(1, 4));
      
        adj.get(0).add(new Pair(3, 1));
        adj.get(3).add(new Pair(0, 1));
          
        adj.get(3).add(new Pair(2, 3));
        adj.get(2).add(new Pair(3, 3))
      
        adj.get(1).add(new Pair(4, 5));
        adj.get(4).add(new Pair(1, 5));
      
        adj.get(2).add(new Pair(4, 1));
        adj.get(4).add(new Pair(2, 1));
        
        Main obj = new Main();
        obj.shortestPath(0, adj, n);
    }
  
    public void shortestPath(int src, ArrayList<ArrayList<Pair>> adj, int N) {
        int[] distance = new int[N];
        for(int i=0; i<N; i++)
            distance[i] = Integer.MAX_VALUE;
        
        distance[src] = 0;
        PriorityQueue<Pair> pq = new PriorityQueue<>();
        pq.add(new Pair(src, 0);
      
        while(!pq.isEmpty()) {
            Pair node = pq.poll();
            for(Pair neighbour: adj.get(node.value)) {
                if(distance[node.value] + neighbour.weight < distance[neighbour.value]) {
                    distance[neighbour.value] = distance[node.value] + neighbour.weight;
                    pq.offer(new Pair(neighbour.value, distance[neighbour.value]));
                }
            }
        }
               
        for(int i=0; i<N; i++) {
            System.out.println(src + " -> " + i + " = " + distance[i]);  
        }  
    }
}
```
> `Time Complexity` : **O((V + E)(log V))**, where V is the number of nodes and E is the number of edges.   
> `Space Complexity` : **O(N) + O(N)**, for priority queue and distance array.    
---
Video Explanations -> (Dijkstra's Algorithm | Shortest Path in Undirected Graphs) [Striver](https://www.youtube.com/watch?v=jbhuqIASjoM&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=18), 
[Pepcoding](https://www.youtube.com/watch?v=sD0lLYlGCJE&list=PL-Jc9J83PIiHfqDcLZMcO9SsUDY4S3a-v&index=15)
<hr>

### Applications of Dijkstra’s Shortest Path Algorithm
> Dijkstra’s algorithm is one of the most popular algorithms for solving many single-source shortest path problems having non-negative edge weight in the graphs i.e., 
> it is to find the shortest distance between two vertices on a graph.
> Dijkstra’s Algorithm has several real-world use cases, some of which are as follows:
> * **Digital Mapping Services in Google Maps:** Many times we have tried to find the distance in G-Maps, from your location to the nearest desired location. 
> There encounters the Shortest Path Algorithm, as there are various routes/paths connecting them but it has to show the minimum distance, so Dijkstra’s Algorithm is used.
> * **Social Networking Applications:** In many applications you might have seen the app suggests the list of friends that a particular user may know. The standard Dijkstra
> algorithm can be applied using the shortest path between users measured through connections among them.
> * **IP routing to find Open shortest Path First:** Open Shortest Path First (OSPF) is a link-state routing protocol that is used to find the best path between the source 
> and the destination router using its own Shortest Path First. Dijkstra’s algorithm is widely used in the routing protocols required by the routers to update their 
> forwarding table. The algorithm provides the shortest cost path from the source router to other routers in the network.
> * **Telephone Network:** As we know, in a telephone network, each line has a bandwidth, ‘b’. The bandwidth of the transmission line is the highest frequency that that line 
> can support. Generally, if the frequency of the signal is higher in a certain line, the signal is reduced by that line. Bandwidth represents the amount of information that 
> can be transmitted by the line. If we imagine a city to be a graph, the vertices represent the switching stations, and the edges represent the transmission lines and 
> the weight of the edges represents ‘b’. So as you can see it can fall into the category of shortest distance problem, for which the Dijkstra is can be used.
> 
> Wherever addressing the need for shortest path explications either in the domain of robotics, transport, embedded systems, laboratory or production plants, etc, this 
> algorithm is applied.
