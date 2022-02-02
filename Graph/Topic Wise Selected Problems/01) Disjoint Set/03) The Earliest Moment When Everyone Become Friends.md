# The Earliest Moment When Everyone Become Friends
Question -> [The Earliest Moment When Everyone Become Friends](https://www.codingninjas.com/codestudio/problems/the-earliest-moment-when-everyone-become-friends_1376604)    

### Implementation
```java
public class Solution {
    public static int minTime(int[][] logs, int n) {
          // T.C.-> O(nlogn), where n = logs.length i.e. rows
          // we have sort the array in increasing order of timestamp
          Arrays.sort(logs, new Comparator<int[]>() {
            public int compare(int[] entry1, int[] entry2) {
                if (entry1[0] > entry2[0])
                    return 1;
                else
                    return -1;
            }
          });
          // T.C.-> O(n)
          UnionFind uf = new UnionFind(n);
          for(int log[]: logs) {
              int timestamp = log[0];
              int idA = log[1];
              int idB = log[2];
              uf.union(idA, idB, timestamp);
              // when all the vertices got connected then we will have only one set
              if(uf.components == 1) return timestamp;
          }
          // we have more than one set so return -1
          return -1;
    }
    private static class UnionFind {
        int[] rank, root;
        int components;
        UnionFind(int n) {
            components = n;
            rank = new int[n];
            root = new int[n];
            for(int i=0; i<n; i++) {
                root[i] = i;
                rank[i] = 1;
            }
        }
        public int find(int x) {
            if(x == root[x]) return x;
            return root[x] = find(root[x]);
        }
        public void union(int x, int y, int timestamp) {
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
> `Time Complexity` : **O(nlogn)**     
> `Space Complexity` : **O(n) + O(n)**, for root and rank array.
---
