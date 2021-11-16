# Prim's Algorithm
> Prim’s Algorithm use Greedy approach to find the minimum spanning tree. In Prim’s Algorithm we grow the spanning tree from a starting position. 
> We add vertex to the growing spanning tree in Prim's algorithm.
> 
> Consider the example below:
> ![Image](https://he-s3.s3.amazonaws.com/media/uploads/16597fe.jpg)    
> In Prim’s Algorithm, we will start with an arbitrary node (it doesn’t matter which one) and mark it. In each iteration we will mark a new vertex that is adjacent to the 
> one that we have already marked. As a greedy algorithm, Prim’s algorithm will select the cheapest edge and mark the vertex. So we will simply choose the edge with weight 1. 
> In the next iteration we have three options, edges with weight 2, 3 and 4. So, we will select the edge with weight 2 and mark the vertex. Now again we have three options,
> edges with weight 3, 4 and 5. But we can’t choose edge with weight 3 as it is creating a cycle. So we will select the edge with weight 4 and we end up with the minimum
> spanning tree of total cost 7 ( = 1 + 2 + 4).

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
      
        adj.get(1).add(new Pair(2, 3));
        adj.get(2).add(new Pair(1, 3));
      
        adj.get(0).add(new Pair(3, 6));
        adj.get(3).add(new Pair(0, 6));
          
        adj.get(1).add(new Pair(3, 8));
        adj.get(3).add(new Pair(1, 8))
      
        adj.get(1).add(new Pair(4, 5));
        adj.get(4).add(new Pair(1, 5));
      
        adj.get(2).add(new Pair(4, 7));
        adj.get(4).add(new Pair(2, 7));
        
        Main obj = new Main();
        obj.primsAlgo(adj, n);
    }
  
    public void primsAlgo(ArrayList<ArrayList<Pair>> adj, int N) {
          int key[] = new int[N];
          int parent[] = new int[N];
          boolean mstSet[] = new boolean[N];
          for(int i=0; i<N; i++) {
              key[i] = Integer.MAX_VALUE;
              mstSet[i] = false;
              parent[i] = -1;
          }
          PriorityQueue<Pair> pq = new PriorityQueue<>();
          key[0] = 0;
          pq.offer(new Pair(0, key[0]));
          
          while(!pq.isEmpty()) {
              int u = pq.poll().value;
              if(mstSet[u] == true) continue;
              mstSet[u] = true;
              for(Pair neighbour: adj.get(u)) {
                  if(mstSet[neighbour.value] == false && neighbour.weight < key[neighbour.value]) {
                      parent[neighbour.value] = u;
                      key[neighbour.value] = neighbour.weight;
                      pq.offer(new Pair(neighbour.value, key[neighbour.value]));
                  }
              }
          }
          
          for(int i=1; i<N; i++) {
              System.out.println(parent[i] + "->" + i);
          }
    }
    
    class Node implements Comparable<Node> {
        int value;
        int parent;
        int weight;
        Node(int value, int weight) {
            this.value = value;
            this.parent = parent;
            this.weight = weight;
        }
        public int compareTo(Node o) {
            return (this.weight - o.weight);
        }
    }
    
    public void primsAlgo2(ArrayList<ArrayList<Pair>> adj, int N) {
          boolean visited[] = new boolean[N];
          PriorityQueue<Node> pq = new PriorityQueue<>();
          pq.offer(new Node(0, -1, 0));
          
          while(!pq.isEmpty()) {
              Node node = pq.poll();
              if(!visited[node.value]) {
                  visited[node.value] = true;
                  if(node.parent != -1) {
                      System.out.println(node.parent + "->" + node.value + "@" + node.weight);
                  }
                  for(Pair neighbour: adj.get(node.value)) {
                      if(!visited[neighbour.value]) {
                          pq.offer(new Node(neighbour.value, node.value, neighbour.weight));
                      }
                  }
              }
          }
    }
}
```
### Complexities:
> `Time Complexity` of the Prim’s Algorithm is **O((V + E)(log V))**(where V is the number of nodes and E is the number of edges) because each vertex is inserted in the 
> priority queue only once and insertion in priority queue take logarithmic time.      
> `Space Complexity` : **O(N) + O(N) + O(N) + O(N)**, for priority queue, key array, parent array and mstSet array.    
---
Video Explanations -> Prim's Algorithm -> [Pepcoding](https://www.youtube.com/watch?v=Vw-sktU1zmc&list=PL-Jc9J83PIiHfqDcLZMcO9SsUDY4S3a-v&index=16), 
Striver- [Intuition](https://www.youtube.com/watch?v=HnD676J56ak&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=21)
<hr> 
