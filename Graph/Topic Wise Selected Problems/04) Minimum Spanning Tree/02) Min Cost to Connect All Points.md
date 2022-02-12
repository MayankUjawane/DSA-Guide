# Min Cost to Connect All Points
Question -> [Min Cost to Connect All Points](https://leetcode.com/problems/min-cost-to-connect-all-points/)    

### Using Prim's Algorithm
```java
class Solution {
    private class Pair {
        int val;
        int weight;
        
        Pair(int val, int weight) {
            this.val = val;
            this.weight = weight;
        }
    }
    
    public int minCostConnectPoints(int[][] points) {
        int n = points.length;
        if(n == 1) return 0;
        
        // S.C.-> O(V+E)
        List<List<Pair>> graph = new ArrayList();
        for(int i=0; i<n; i++) {
            graph.add(new ArrayList());
        }
        for(int i=0; i<n; i++) {
            for(int j=0; j<n; j++) {
                int x = Math.abs(points[i][0] - points[j][0]);
                int y = Math.abs(points[i][1] - points[j][1]);
                int w = x+y;
                
                graph.get(i).add(new Pair(j,w));
            }
        }
        // S.C.-> O(V), V = n
        boolean[] vis = new boolean[n];
        // S.C. -> O(V)
        Queue<Pair> pq = new PriorityQueue<>((x, y) -> x.weight - y.weight);
        pq.offer(new Pair(0,0));
        int cost = 0;
        // T.C.-> O((V+E)logV)
        while(n > 0) {
            Pair top = pq.poll();
            if(vis[top.val] == true) continue;
            
            vis[top.val] = true;
            cost += top.weight;
            n--;
            
            for(Pair ngb: graph.get(top.val)) {
                if(vis[ngb.val] == true) continue;
                pq.offer(ngb);
            }
        }
        return cost;
    }
}
```
> `Time Complexity` : **O((V+E)logV)**            
> `Space Complexity` : **O(V+E)** 
---   
