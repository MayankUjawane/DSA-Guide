# Bipartite Graph
> In layman language Bipartite Graph is a graph that can be coloured using two colours such that no two adjacent nodes have same colour.
> Definition of [Bipartite Graph](https://en.wikipedia.org/wiki/Bipartite_graph#:~:text=In%20the%20mathematical%20field%20of,the%20parts%20of%20the%20graph.)

### Using BFS
```java
class Solution {
    public boolean isBipartite(int V, ArrayList<ArrayList<Integer>> adj) {
        int colour[] = new int[V+1];
        // 0 -> Not coloured, 1 -> First Colour, 2 -> Second Colour
        for(int i=1; i<=V; i++) {
            if (colour[i] == 0) {
                if(!checkBipartite(adj, i, colour))
                    return false;
            }    
        }
        return true;
    }
    
    public boolean checkBipartite(ArrayList<ArrayList<Integer>> adj, int node, int[] colour) {
        Queue<Integer> q = new LinkedList();
        q.add(node);
        colour[node] = 1;
        
        while(!q.isEmpty()) {
            int top = q.poll();
            
            for(Integer neighbour: adj.get(top)) {
                if (colour[neighbour] == 0) {
                    colour[neighbour] = (colour[top] == 1) ? 2 : 1;
                    q.add(neighbour);
                } else if (colour[neighbour] == colour[node]) {
                    return false;
                }
            }
        }
        return true;
    }
}
```
> `Time Complexity` : **O(V + E)**, where V is the number of nodes and E is the number of edges.   
> `Space Complexity` : **O(N) + O(N)**, for visited array and Queue.    
---
Video Explanations -> [Bipartite Graph (BFS)](https://www.youtube.com/watch?v=nbgaEu-pvkU&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=10)  
<hr>

### Using DFS
```java
class Solution {
    public boolean isBipartite(int V, ArrayList<ArrayList<Integer>> adj) {
        int colour[] = new int[V+1];
        // 0 -> Not Coloured, 1 -> First Colour, 2 -> Second Colour
        for(int i=1; i<=V; i++) {
            if (colour[i] == 0) {
                colour[i] = 1;
                if(!checkBipartite(adj, i, colour))
                    return false;
            }    
        }
        return true;
    }
    
    public boolean checkBipartite(ArrayList<ArrayList<Integer>> adj, int node, int colour[]) {
        for(Integer neighbour: adj.get(node)) {
            if(colour[neighbour] == 0) {
                colour[neighbour] = (colour[node] == 1) ? 2 : 1;
                if(!checkBipartite(adj, neighbour, colour)) 
                    return false;
            } else if (colour[neighbour] == colour[node]) {
                return false;
            }
        }
        return true;
    }
}
```
> `Time Complexity` : **O(V + E)**, where V is the number of nodes and E is the number of edges.   
> `Space Complexity` : **O(N) + O(N)**, for visited array and recursion stack.    
---
Video Explanations -> [Bipartite Graph (DFS)](https://www.youtube.com/watch?v=uC884ske2uQ&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=11)  
<hr>
