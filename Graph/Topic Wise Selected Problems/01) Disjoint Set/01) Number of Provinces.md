# Number of Provinces
Question -> [Number of Provinces](https://leetcode.com/problems/number-of-provinces/submissions/)    

### Method 1
```java
class Solution {
    int rank[];
    int root[];
    
    public int findCircleNum(int[][] isConnected) {
        int n = isConnected.length;
        // considering 1 based indexing
        rank = new int[n+1];
        root = new int[n+1];
        // T.C.-> O(n)
        for(int i=1; i<=n; i++) {
            rank[i] = 1;
            root[i] = i;
        }
        
        // T.C.-> O(row*col) 
        for(int i=0; i<isConnected.length; i++) {
            for(int j=0; j<isConnected[i].length; j++) {
                if(i == j) continue; 
                if(isConnected[i][j] == 1) {
                    union(i+1, j+1);
                }
            }
        }
        
        int count = 0;
        // T.C.-> O(n)
        for(int i=1; i<root.length; i++) {
            // when found root node increment count
            if(i == root[i]) {
                count++;
            }
        }
        
        return count;
    }
    
    // T.C.-> O(1)
    public int find(int x) {
        if(x == root[x]) {
            return x;
        }

        return root[x] = find(root[x]);
    }
    
    // T.C.-> O(1)   
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
        }
    }
}
```
> `Time Complexity` : **O(n) + O(row\*col) + O(n)**     
> `Space Complexity` : **O(n) + O(n)**, for rank and root array
---
### Method 2
```java
class Solution {
    public int findCircleNum(int[][] isConnected) {
        if (isConnected == null || isConnected.length == 0) {
            return 0;
        }

        int n = isConnected.length;
        // Constructor will take O(n) time
        UnionFind uf = new UnionFind(n);
        // T.C.-> O(row*col)
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if(i == j) continue;
                if (isConnected[i][j] == 1) {
                    uf.union(i, j);
                }
            }
        }

        return uf.getCount();
    }

    class UnionFind {
        private int[] root;
        private int[] rank;
        private int count;

        // T.C.-> O(n)
        UnionFind(int size) {
            root = new int[size];
            rank = new int[size];
            // Initially all the vertices are not connected
            count = size;
            for (int i = 0; i < size; i++) {
                root[i] = i;
                rank[i] = 1;
            }
        }
        
        // T.C.-> O(1)
        int find(int x) {
            if (x == root[x]) {
                return x;
            }
            return root[x] = find(root[x]);
        }
        
        // T.C.-> O(1)
        void union(int x, int y) {
            int rootX = find(x);
            int rootY = find(y);
            if (rootX != rootY) {
                if (rank[rootX] > rank[rootY]) {
                    root[rootY] = rootX;
                } else if (rank[rootX] < rank[rootY]) {
                    root[rootX] = rootY;
                } else {
                    root[rootY] = rootX;
                    rank[rootX] += 1;
                }
                // we merge two vertices so count get decremented 
                count--;
            }
        }

        // T.C.-> O(1)
        int getCount() {
            return count;
        }
    }
}
```
> `Time Complexity` : **O(row\*col)**     
> `Space Complexity` : **O(n) + O(n)**, for rank and root array
---
