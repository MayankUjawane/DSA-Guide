# Optimize Water Distribution
Question -> [Optimize Water Distribution](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/graphs/optimize-water-distribution-official/ojquestion)    

### Implementation
```java
import java.io.*;
import java.util.*;

class Main {
    public static int minCostToSupplyWater(int n, int[] wells, int[][] pipes) {
        ArrayList<ArrayList<Pair>> graph = new ArrayList<>();
        for(int i=0; i<=n; i++) {
          graph.add(new ArrayList<>());
        }
        for(int i=0; i<pipes.length; i++) {
          int u = pipes[i][0];
          int v = pipes[i][1];
          int w = pipes[i][2];
          graph.get(u).add(new Pair(v, w));
          graph.get(v).add(new Pair(u, w));
        }
        for(int i=1; i<=wells.length; i++) {
          graph.get(i).add(new Pair(0, wells[i-1]));
          graph.get(0).add(new Pair(i, wells[i-1]));
        }

        PriorityQueue<Pair> pq = new PriorityQueue<>();
        boolean[] vis = new boolean[n+1];
        pq.offer(new Pair(0, 0));
        int cost = 0;
        while(!pq.isEmpty()) {
          Pair rem = pq.poll();
          if(!vis[rem.vertex]) {
              vis[rem.vertex] = true;
              cost += rem.weight;
              for(Pair nbr: graph.get(rem.vertex)) {
                  if(!vis[nbr.vertex]) {
                      pq.offer(nbr);
                  }
              }
          }
        }
        return cost;
    }

    private static class Pair implements Comparable<Pair>{
        int vertex;
        int weight;
        Pair(int vertex, int weight) {
          this.vertex = vertex;
          this.weight = weight;
        }

        public int compareTo(Pair o) {
          return this.weight - o.weight;
        }
    }
}
```
> `Time Complexity` : **O(V+E)logV** 
---    
Video Explanations -> [Optimize Water Distribution](https://youtu.be/gc6ShDTldb4)  
<hr>
