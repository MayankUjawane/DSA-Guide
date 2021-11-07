# Longest Path in Directed Acyclic Graph
> In topological sorting of a graph the vertices which have fewer dependencies are printed before the vertices 
> which have relatively greater dependencies.
> Idea is to traverse through the vertices of graph according to topological sorting of the graph because of this for every
> node, the nodes on which they depends will already get traversed before them.
```java
private class Pair {
    int value;
    int weight;
    Pair(int value, int weight) {
        this.value = value;
        this.weight = weight;
    }
}
class Main {
    public static void main(String args[]) {
        int n = 6;
        ArrayList<ArrayList<Pair>> adj = new ArrayList<ArrayList<Pair>>();
        
        for(int i=0; i<n; i++)
            adj.add(new ArrayList<Pair>>());
            
        adj.get(0).add(new Pair(1, 2));
        adj.get(0).add(new Pair(4, 1));
        adj.get(1).add(new Pair(2, 3));
        adj.get(2).add(new Pair(3, 6));
        adj.get(4).add(new Pair(2, 2));
        adj.get(4).add(new Pair(5, 4));
        adj.get(5).add(new Pair(3, 1));
        
        Main obj = new Main();
        obj.longestPath(0, adj, n);
    }
    public void longestPath(int src, ArrayList<ArrayList<Pair>> adj, int N) {
        Stack<Integer> st = new Stack();
        boolean[] visited = new boolean[N];
        for(int i=0; i<N; i++) {
            if(visited[i] == false) {
                topologicalSort(i, adj, visited, st);
            }
        }
        // stack will contain topological sorting of graph
        int[] distance = new int[N];
        for(int i=0; i<N; i++)
            distance[i] = Integer.MIN_VALUE;
        
        distance[src] = 0;
        while(!st.isEmpty()) {
            int node = st.pop();
            // for the nodes which occur before source node in topological order can not be reached therefore for them 
            // distance[node] is equal to Integer.MIN_VALUE
            // if node has been reached previously then distance[node] will not be equal to Integer.MIN_VALUE
            if(distance[node] != Integer.MIN_VALUE) {
                for(Pair neighbour: adj.get(node)) {
                    if(distance[node] + neighbour.weight > distance[neighbour.value]) {
                        distance[neighbour.value] = distance[node] + neighbour.weight;
                    }
                }
            }
        }
    }
    public void topologicalSort(int node, ArrayList<ArrayList<Integer>> adj, boolean visited[], Stack<Integer> st) {
        visited[node] = true;
        for(Pair neighbour: adj.get(node)) {
            if(visited[neighbour.value] == false) {
                topologicalSort(neighbour.value, adj, visited, st);
            }
        }
        st.push(node);
    }
}
```
> `Time Complexity` : **O(2(V + E))**, where V is the number of nodes and E is the number of edges.   
> `Space Complexity` : **O(N) + O(N) + O(N) + O(N)**, for stack, visited array, distance array and recursion stack.    
---
Video Explanations -> [Longest Path in Directed Acyclic Graph](https://www.youtube.com/watch?v=jdTnoCBSOVM)  
<hr>
