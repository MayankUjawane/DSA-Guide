# Min Cost to Connect All Points
Question -> [Min Cost to Connect All Points](https://leetcode.com/problems/min-cost-to-connect-all-points/)    

### Using Kruskal's Algorithm
```java
class Solution {
    private class Edge implements Comparable<Edge> {
        int point1;
        int point2;
        int weight;
        Edge(int point1, int point2, int weight) {
            this.point1 = point1;
            this.point2 = point2;
            this.weight = weight;
        }
        public int compareTo(Edge e) {
            return this.weight - e.weight;
        }
    }
    
    public int minCostConnectPoints(int[][] points) {
        int n = points.length;
        if(n == 1) return 0;
        // S.C.-> O(E)
        List<Edge> edges = new ArrayList();
        for(int i=0; i<n; i++) {
            for(int j=0; j<n; j++) {
                int x = Math.abs(points[i][0] - points[j][0]);
                int y = Math.abs(points[i][1] - points[j][1]);
                int w = x+y;
                edges.add(new Edge(i,j,w));
            }
        }
        // T.C.-> O(ElogE), here E = number of edges
        Collections.sort(edges);
      
        UnionFind uf = new UnionFind(n);
        int cost = 0;
        // T.C.-> O(E)
        for(Edge edge : edges) {
            if(uf.isSameComponent(edge.point1, edge.point2)) continue;
            uf.union(edge.point1, edge.point2);
            cost += edge.weight;
            if(uf.components == 1) return cost;
        }
        
        return cost;
    }
    
    private class UnionFind {
        int[] rank, root;
        int components;
      
        UnionFind(int n) {
            rank = new int[n];
            root = new int[n];
            components = n;
            for(int i=0; i<n; i++) {
                rank[i] = 1;
                root[i] = i;
            }
        }
        
        public int find(int x) {
            if(x == root[x]) return x;
            return root[x] = find(root[x]);
        }
        
        public boolean isSameComponent(int x, int y) {
            return (find(x) == find(y));
        }
        
        public void union(int x, int y) {
            int rootX = find(x);
            int rootY = find(y);
            if(rootX != rootY) {
                if(rank[rootX] > rank[rootY]) {
                    root[rootY] = rootX;
                } else if(rank[rootX] < rank[rootY]) {
                    root[rootX] = rootY;
                } else {
                    root[rootY] = rootX;
                    rank[rootX]++;
                }
                components--;
            }
        }
    }
}
```
> `Time Complexity` : **O(ElogE)**            
> `Space Complexity` : **O(E)** 
---   
