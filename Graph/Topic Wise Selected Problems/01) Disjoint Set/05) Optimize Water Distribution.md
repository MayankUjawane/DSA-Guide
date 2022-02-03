# Optimize Water Distribution
Question -> [Optimize Water Distribution](https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/graphs/optimize-water-distribution-official/ojquestion)    

### Implementation
```java
public static int minCostToSupplyWater(int n, int[] wells, int[][] pipes) {
    ArrayList<Edge> graph = new ArrayList<>();
    // T.C.-> O(m), where m = pipes.length = number of edges
    for(int i=0; i<pipes.length; i++) {
        int u = pipes[i][0];
        int v = pipes[i][1];
        int w = pipes[i][2];
        graph.add(new Edge(u, v, w));
    }
    // add extra node as root node 0, and connect all 0 and i with costs wells[i]
    // T.C.-> O(n), where n = wells.length = number of vertices
    for(int i=1; i<=wells.length; i++) {
        graph.add(new Edge(0, i, wells[i-1]));
    }
    // T.C.-> (E+V)log(E+V), where E=E+V
    Collections.sort(graph);
    // T.C.-> O(n+1), where n = number of vertices
    UnionFind uf = new UnionFind(n+1);
    int cost = 0;
    // T.C.-> O(E+V)
    for(Edge edge: graph) {
        int u = edge.vertex;
        int v = edge.neighbour;
        int w = edge.weight;
        // if we add u and v vertices of same component then they will create cycle
        if(uf.isSameComponent(u, v)) continue;
        uf.union(u, v);
        cost += w;
        // component=1 means add vertices got connected
        if(uf.component == 1) return cost;
    }
    return cost;
}
  
private static class Edge implements Comparable<Edge>{
    int vertex;
    int neighbour;
    int weight;
    Edge(int vertex, int neighbour, int weight) {
        this.vertex = vertex;
        this.neighbour = neighbour;
        this.weight = weight;
    }

    public int compareTo(Edge o) {
        return this.weight - o.weight;
    }
}
  
private static class UnionFind {
    int[] root, rank;
    int component;
    UnionFind(int n) {
        root = new int[n];
        rank = new int[n];
        component = n;
        for(int i=0; i<n; i++) {
            root[i] = i;
            rank[i] = 1;
        }
    }
    public int find(int x) {
        if(x == root[x]) {
            return x;
        }
        return root[x] = find(root[x]);
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
            component--;
        }
    }
    public boolean isSameComponent(int x, int y) {
        return (find(x) == find(y));
    }
}
```
> `Time Complexity` : **O(V+E)log(V+E)** 
---   
