# Smallest String With Swaps
Question -> [Smallest String With Swaps](https://leetcode.com/problems/smallest-string-with-swaps/)    

### Implementation
```java
class Solution {
    public String smallestStringWithSwaps(String s, List<List<Integer>> pairs) {
        int size = s.length();
        // T.C.-> O(n), where n = s.length()
        UnionFind uf = new UnionFind(size);
        // T.C.-> O(m), where m = pairs.size()
        // making sets of connected indices
        for(List<Integer> pair: pairs) {
            int a = pair.get(0);
            int b = pair.get(1);
            uf.union(a, b);
        }
        
        // adding characters of the same set in the PriorityQueues
        // S.C.-> O(n) + O(n), for Map and PriorityQueue (PQ will contain all characters of the string)
        Map<Integer, PriorityQueue<Character>> charGroups = new HashMap<>();
        // T.C.-> O(n)
        for(int i=0; i<size; i++) {
            int root = uf.find(i);
            charGroups.putIfAbsent(root, new PriorityQueue<>());
            charGroups.get(root).offer(s.charAt(i)); 
        }
        // making the final string
        // S.C.-> O(n)
        StringBuilder sb = new StringBuilder();
        // T.C.-> O(n)
        for(int i=0; i<size; i++) {
            int root = uf.find(i);
            sb.append(charGroups.get(root).poll());
        }
        
        return sb.toString();
    }
    private class UnionFind {
        int[] rank, root;
        
        UnionFind(int n) {
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
}
```
> `Time Complexity` : **O(n)**     
> `Space Complexity` : **O(n)**
---
