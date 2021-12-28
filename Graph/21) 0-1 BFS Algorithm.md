# 0-1 BFS Algorithm
> 0-1 BFS is used when you have a graph G with V vertices and E edges. The graph is a weighted graph but the weights have a contraint that they can only be 0 or 1 and you have
> to find the shortest path from src to destination.             

[Question](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/graphs/pepcoder-and-reversing-official/ojquestion)    
  
### Optimal Approach (0-1 BFS)  
```java
import java.io.*;
import java.util.*;

public class Main {
    private static class Pair {
        int node;
        int weight;
        Pair(int node, int weight) {
            this.node = node;
            this.weight = weight;
        }
    }

    public static void main(String[] args) {
      Scanner sc = new Scanner(System.in);
      int n = sc.nextInt(); //total vertices
      int m = sc.nextInt(); //total edges

      ArrayList<ArrayList<Pair>> graph = new ArrayList<>();
      for(int i=0; i<n+1; i++) {
          graph.add(new ArrayList<>());
      }

      for(int i=0; i<m; i++) {
          int a = sc.nextInt();
          int b = sc.nextInt();

          //add original edge with weight 0
          graph.get(a).add(new Pair(b, 0));
          //add opposite edge with weight 1
          graph.get(b).add(new Pair(a, 1));
      }

      System.out.println(minReversedEdges(graph, 1, n));
    }

    public static int minReversedEdges(ArrayList<ArrayList<Pair>> graph, int src, int dest) {
        boolean[] visited = new boolean[dest+1];
        Deque<Pair> deque = new LinkedList<Pair>();
        deque.addFirst(new Pair(src, 0));

        while(!deque.isEmpty()) {
            Pair p = deque.removeFirst();
            if(p.node == dest) return p.weight;

            visited[p.node] = true;

            for(Pair neighbour: graph.get(p.node)) {
                if(!visited[neighbour.node]) {
                    if(neighbour.weight == 1) {
                        deque.addLast(new Pair(neighbour.node, p.weight+1));
                    } else {
                        deque.addFirst(new Pair(neighbour.node, p.weight+0));
                    }
                }
            }
        }
        return -1;
    }
}
```
> `Time Complexity` : **O(V+E)** , where V is the number of nodes and E is the number of edges.           
> `Space Complexity` : **O(V) + O(V)**, for visited array and deque.    
---
Video Explanation -> [Pepcoding](https://www.youtube.com/watch?v=Xqq7uELiYnE)
<hr>

### Naive Solution — Dijkstra's Algorithm
```java
import java.io.*;
import java.util.*;

public class Main {
    private static class Pair implements Comparable<Pair> {
        int node;
        int weight;

        Pair(int node, int weight) {
            this.node = node;
            this.weight = weight;
        }
        public int compareTo(Pair o) {
            return (this.weight - o.weight);
        }
    }

    public static void main(String[] args) throws NumberFormatException, IOException{
      Scanner sc = new Scanner(System.in);
      int n = sc.nextInt();
      int m = sc.nextInt();

      ArrayList<ArrayList<Pair>> graph = new ArrayList<>();
      for(int i=0; i<n+1; i++) {
          graph.add(new ArrayList<>());
      }

      for(int i=0; i<m; i++) {
          int a = sc.nextInt();
          int b = sc.nextInt();

          //add original edge with weight 0
          graph.get(a).add(new Pair(b, 0));
          //add opposite edge with weight 1
          graph.get(b).add(new Pair(a, 1));
      }
      int minimunNumberOfReversedEdges = minEdges(graph, 1, n);
      if (minimunNumberOfReversedEdges == Integer.MAX_VALUE) {
          minimunNumberOfReversedEdges = -1;
      }
      System.out.println(minimunNumberOfReversedEdges);
    }

    public static int minEdges(ArrayList<ArrayList<Pair>> graph, int src, int dest) {
        int[] distance = new int[dest+1];
        for(int i=1; i<distance.length; i++) {
            distance[i] = Integer.MAX_VALUE;
        }
        PriorityQueue<Pair> pq = new PriorityQueue<Pair>();
        pq.offer(new Pair(src, 0));
        distance[src] = 0;

        while(!pq.isEmpty()) {
            Pair p = pq.poll();
            if(p.node == dest) return distance[dest];

            for(Pair neighbour: graph.get(p.node)) {
                if(distance[p.node] + neighbour.weight < distance[neighbour.node]) {
                    distance[neighbour.node] = distance[p.node] + neighbour.weight;
                    pq.offer(new Pair(neighbour.node, distance[neighbour.node]));
                }
            }
        }
        return distance[dest];
    }
}
```
> `Time Complexity` : **O(V+E)logV**, where V is the number of nodes and E is the number of edges.           
> `Space Complexity` : **O(V) + O(V)**, for distance array and PriorityQueue.    
---
