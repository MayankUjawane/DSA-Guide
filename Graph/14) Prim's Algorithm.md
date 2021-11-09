### Prim's Algorithm
> Prim’s Algorithm use Greedy approach to find the minimum spanning tree. In Prim’s Algorithm we grow the spanning tree from a starting position. 
> We add vertex to the growing spanning tree in Prim's algorithm.

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
          
          for(int i=0; i<N; i++) {
              int u = pq.poll().value;
              mstSet[u] = true;
              
              for(Pair neighbour: adj.get(u)) {
                  if(mstSet[neighbour.value] == false && neighbour.weight < key[neighbour.value]) {
                      parent[neighbour.value] = u;
                      key[neighbour.value] = neighbour.weight;
                      pq.offer(new Pair(neighbour.value, key[neighbour.value]));
                  }
              }
          }
          
          for(int i=0; i<N; i++) {
              System.out.println(parent[i] + " - " + i);
          }
    }
}
```
> `Time Complexity` : **O((V + E)(log V))**, where V is the number of nodes and E is the number of edges.   
> `Space Complexity` : **O(N) + O(N) + O(N) + O(N)**, for priority queue, key array, parent array and mstSet array.    
---
Video Explanations -> [Prim's Algorithm](https://www.youtube.com/watch?v=8KPEROaLK-0&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=22)  
<hr>
