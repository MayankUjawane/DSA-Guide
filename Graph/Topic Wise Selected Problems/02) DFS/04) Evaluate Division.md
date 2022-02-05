# Evaluate Division
Question -> [Evaluate Division](https://leetcode.com/problems/evaluate-division/)    

### Implementation
```java
class Solution {
    public double[] calcEquation(List<List<String>> equations, double[] values, List<List<String>> queries) {
        // S.C.-> O(n) where n=equations.length
        Map<String, List<Pair>> graph = new HashMap<>();
        // T.C.-> O(n) where n=equations.length
        for(int i=0; i<equations.size(); i++) {
            String a = equations.get(i).get(0);
            String b = equations.get(i).get(1);
            double value = values[i];
            graph.putIfAbsent(a, new ArrayList<>());
            graph.get(a).add(new Pair(b, value));
            graph.putIfAbsent(b, new ArrayList<>());
            double v = 1/value;
            graph.get(b).add(new Pair(a, 1.0/value));
        }
        
        double[] ans = new double[queries.size()];
        // this loop will run for m times where m=queries.size() 
        // and each time dfs call will take O(n) so T.C.-> O(m*n)
        for(int i=0; i<queries.size(); i++) {
            String a = queries.get(i).get(0);
            String b = queries.get(i).get(1);
            if(!graph.containsKey(a) || !graph.containsKey(b)) {
                ans[i] = -1.0;
            } else {
                ans[i] = dfs(graph, new HashSet(), a, b);
            }
        }
        return ans;
    }
    // T.C.-> O(E) where E=number of vertices in the graph, at max E=equations.length=n
    // S.C.-> O(V) where V=number of vertices in the component of src, at max V=total nodes of graph
    public double dfs(Map<String,List<Pair>> graph, Set<String> vis, String src, String dest) {
        if(src.equals(dest)) return 1.0;
        vis.add(src);
        for(Pair neighbor: graph.get(src)) {
            if(vis.contains(neighbor.key)) continue;
            double returnedAns = dfs(graph, vis, neighbor.key, dest);
            if(returnedAns > 0) return returnedAns*(neighbor.value);
        }
        // -1.0 will be returned when src and dest does not belong to the same component
        return -1.0;
    }
    private class Pair {
        String key;
        double value;
        Pair(String key, double value) {
            this.key = key;
            this.value = value;
        }
    }
}
```
> `Time Complexity` : **O(m\*n)**, where n = equations.length and m = queries.size()     
> `Space Complexity` : **O(n)**
---
