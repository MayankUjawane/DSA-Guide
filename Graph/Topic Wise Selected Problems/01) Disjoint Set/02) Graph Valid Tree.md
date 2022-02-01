# Graph Valid Tree
Question -> [Graph Valid Tree](https://www.codingninjas.com/codestudio/problems/graph-valid-tree_1376618)    

### Implementation
```java
public class Solution {
    public static Boolean checkGraph(int[][] edges, int n, int m) {
        // constructor takes O(n) time 
        UnionFind uf = new UnionFind(n);
        // time complexity for this is O(n), where n is the number of nodes
        for(int[] edge: edges) {
            int a = edge[0];
            int b = edge[1];
            // if a and b vertices are already in same component, then on connecting 
            // a and b they will create cycle and a tree does not have cycle
            if(!uf.isConnected(a, b)) {
                uf.union(a, b);
            } else {
                return false;
            }
        }
        // Tree has only one connected component
        return (uf.components == 1);
    }
    
    private static class UnionFind {
        int components;
        int[] rank, root;
        // T.C.-> O(n)
        UnionFind(int n) {
            // initially all vertices are not connected so components = n
            components = n;
            rank = new int[n];
            root = new int[n];
            for(int i=0; i<n; i++) {
                root[i] = i;
                rank[i] = 1;
            }
        }
        // T.C.-> O(1)
        public int find(int x) {
            if(x == root[x]) {
                return x;
            }
            return (root[x] = find(root[x]));
        }
        // T.C.-> O(1)
        public void union(int x, int y) {
            int rootX = root[x];
            int rootY = root[y];
            if(rootX != rootY) {
                if(rank[rootX] > rank[rootY]) {
                    root[rootY] = rootX;
                } else if(rank[rootX] < rank[rootY]) {
                    root[rootX] = rootY;
                } else {
                    root[rootY] = rootX;
                    rank[rootX]++;
                }
                // with union we merge two components so reduce components by 1
                components--;
            }
        }
        // T.C.-> O(1)
        public boolean isConnected(int x, int y) {
            return (find(x) == find(y));
        }
    }
}
```
> `Time Complexity` : **O(n)**     
> `Space Complexity` : **O(n) + O(n)**, for root and rank array.
---
