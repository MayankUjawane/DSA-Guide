# Shortest Path in Undirected Graph with Unit Weights    

```java
class Solution {
    public int[] shortestPath(ArrayList<ArrayList<Integer>> graph, int N, int src) {
        int[] distance = new int[N];
        for(int i=0; i<distance.length; i++) {
            distance[i] = Integer.MAX_VALUE;
        }
        Queue<Integer> q = new LinkedList();
        q.offer(src);
        distance[src] = 0;
        
        while(!q.isEmpty()) {
            int node = q.poll();
            for(int neighbour: graph.get(node)) {
                if(distance[node] + 1 < distance[neighbour]) {
                    distance[neighbour] = distance[node] + 1;
                    q.offer(neighbour);
                }
            }
        }
        return distance;
    }
}
```
> `Time Complexity` : **O(V + E)**, where V is the number of nodes and E is the number of edges.   
> `Space Complexity` : **O(N) + O(N)**, for distance array and queue.    
---
Video Explanations -> [Shortest Path in Undirected Graph with Unit Weights](https://www.youtube.com/watch?v=hwCWi7-bRfI&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=17)  
<hr>
