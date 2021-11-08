# Dijkstra's Algorithm | Shortest Path in Undirected Graphs
> **Dijkstra's algorithm** is an algorithm for finding the **shortest paths** between nodes in a graph, which may represent, for example, road networks.
> **Dijkstra's algorithm** makes use of weights of the edges for finding the path that minimizes the total distance (weight) among the source node and
> all other nodes. This algorithm is also known as the **single-source shortest path algorithm**.

```java
private class Pair implements Comparable<Pair> {
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
        int n = 6;
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
