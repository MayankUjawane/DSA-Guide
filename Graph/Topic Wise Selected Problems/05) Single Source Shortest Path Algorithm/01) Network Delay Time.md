# Network Delay Time
Question -> [Network Delay Time](https://leetcode.com/problems/network-delay-time/)    

### Implementation
```java
class Solution {
    public int networkDelayTime(int[][] times, int n, int k) {
        List<List<Pair>> adj = new ArrayList();
        for(int i=0; i<n+1; i++) {
            adj.add(new ArrayList());
        }
        for(int[] time : times) {
            int u = time[0];
            int v = time[1];
            int w = time[2];
            adj.get(u).add(new Pair(v,w));
        }
        
        int[] distance = new int[n+1];
        for(int i=1; i<n+1; i++) {
            distance[i] = Integer.MAX_VALUE;
        }
      
        Queue<Pair> pq = new PriorityQueue<>((x,y) -> x.weight - y.weight);
        pq.add(new Pair(k,0));
        distance[k] = 0;
        
        while(!pq.isEmpty()) {
            Pair top = pq.poll();
            if(distance[top.val] == Integer.MAX_VALUE) continue;
            if(top.weight > distance[top.val]) continue;
            
            for(Pair ngb: adj.get(top.val)) {
                if(distance[top.val] + ngb.weight < distance[ngb.val]) {
                    distance[ngb.val] = distance[top.val] + ngb.weight;
                    pq.offer(new Pair(ngb.val, distance[ngb.val]));
                }
            }
        }
        
        int max = Integer.MIN_VALUE;
        for(int i=1; i<n+1; i++) {
            if(distance[i] == Integer.MAX_VALUE) return -1;
            if(distance[i] > max) {
                max = distance[i];
            }
        }
        return max;
    }
    
    private class Pair {
        int val; 
        int weight; 
        Pair(int val, int weight) {
            this.val = val;
            this.weight = weight;
        }
    }
}
```
> Here N is the number of nodes and E is the number of total edges in the given network.
> 
> `Time complexity` : **O(N+ElogN)**
> 
> Dijkstra's Algorithm takes O(ElogN). Finding the minimum time required in distance array takes O(N).
> 
> The maximum number of vertices that could be added to the priority queue is E. Thus, push and pop operations on the priority queue take O(logE) time. 
> The value of E can be at most N * (N - 1). Therefore, O(logE) is equivalent to O(logN^2) which in turn equivalent to O(2⋅logN). 
> Hence, the time complexity for priority queue operations equals O(logN).
> 
> Although the number of vertices in the priority queue could be equal to E, we will only visit each vertex only once. 
> If we encounter a vertex for the second time, then top node time will be greater than distance[top.val], and we can continue to the next vertex in the priority queue. 
> Hence, in total E edges will be traversed and for each edge, there could be one priority queue insertion operation.       
> Hence, the time complexity is equal to O(N+ElogN).              
>
> `Space complexity` : **O(N + E)**
>
> Building the adjacency list will take O(E) space. Dijkstra's algorithm takes O(E) space for priority queue because each vertex could be added to the priority queue 
> N−1 time which makes it N∗(N−1) and O(N^2) is equivalent to O(E). direction array takes O(N) space.
--- 
