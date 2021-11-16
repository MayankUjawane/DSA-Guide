# Kruskal's Algorithm  
> Kruskal’s Algorithm builds the spanning tree by adding edges one by one into a growing spanning tree. Kruskal's algorithm follows greedy approach as in each 
> iteration it finds an edge which has least weight and add it to the growing spanning tree.

```java
class Node {
    int src;
    int dest;
    int weight;
    Node(int src, int dest, int weight) {
        this.src = src;
        this.dest = dest;
        this.weight = weight;
    }
}

class SortComparator implements Comparator<Node> {
    @Override
    public int compare(Node node1, Node node2) {
        return (node1.weight - node2.weight);  
    }  
}

class Main {
    public static void main(String args[]) {
        int n = 5;
        ArrayList<Node> adj = new ArrayList<>();
        adj.add(new Node(0, 1, 2));
        adj.add(new Node(0, 3, 6));
        adj.add(new Node(1, 3, 8));
        adj.add(new Node(1, 2, 3));
        adj.add(new Node(1, 4, 5));
        adj.add(new Node(2, 4, 7));
        
        Main obj = new Main();
        obj.kruskalAlgo(adj, n);
    }
  
    public void kruskalAlgo(ArrayList<Node> adj, int N) {
        //sorting will take ElogE time, where E is the number of edges.
        Collections.sort(adj, new SortComparator());
        int[] parent = new int[N];
        int[] rank = new int[N];
        for(int i=0; i<N; i++) {
            parent[i] = i;
            rank[i] = 0;
        }  
      
        ArrayList<Node> mst = new ArrayList<>();
        int mstCost = 0;
        for(Node n: adj) {
            if(findParent(n.src, parent) != findParent(n.dest, parent)) {
                mst.add(n);
                mstCost += n.weight;
                union(n.src, n.dest, parent, rank);
            }  
        }  
      
        System.out.println(mstCost);
        for(Node n: mst) {
            System.our.println(n.src + " -> " + n.dest + " @ " + n.weight);  
        }  
    }
  
    public int findParent(int node, int[] parent) {
        if(node == parent[node]) return node;
        return parent[node] = findParent(parent[node]);
    }  
  
    public void union(int a, int b, int[] parent, int[] rank) {
        a = findParent(a, parent);
        b = findParent(b, parent);
        if(a != b) {
            if(rank[a] < rank[b]) {
                parent[a] = b;  
            } else if(rank[a] > rank[b]) {
                parent[b] = a;  
            } else {
                parent[b] = a;
                rank[a]++;
            }  
        }
    }  
}
```
> `Time Complexity` : **O(E(logE)) + O(E x O(4))** ,i.e., approximately **O(E(logE))**, where **E** is the number of edges.   
> `Space Complexity` : **O(N) + O(N)**, for parent array and rank array.    
---
Video Explanation -> [Kruskal's Algorithm](https://www.youtube.com/watch?v=1KRmCzBl_mQ&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=24)
<hr>

### Algorithm Steps:
> * Sort the graph edges with respect to their weights.
> * Start adding edges to the MST from the edge with the smallest weight until the edge of the largest weight.
> * Only add edges which doesn't form a cycle , edges which connect only disconnected components.
> So now the question is how to check if 2 vertices are connected or not ?
> 
> This could be done using **DFS** which starts from the first vertex, then check if the second vertex is visited or not. But DFS will make time complexity large as 
> it has an order of **O(V + E)** where V is the number of vertices, E is the number of edges. So the best solution is **Disjoint Sets**:
> Disjoint sets are sets whose intersection is the empty set so it means that they don't have any element in common.
>
> Consider following example:
> ![Example](https://he-s3.s3.amazonaws.com/media/uploads/6322896.jpg)          
> In Kruskal’s algorithm, at each iteration we will select the edge with the lowest weight. So, we will start with the lowest weighted edge first i.e., 
> the edges with weight 1. After that we will select the second lowest weighted edge i.e., edge with weight 2. Notice these two edges are totally disjoint. 
> Now, the next edge will be the third lowest weighted edge i.e., edge with weight 3, which connects the two disjoint pieces of the graph. Now, we are not 
> allowed to pick the edge with weight 4, that will create a cycle and we can’t have any cycles. So we will select the fifth lowest weighted edge i.e., edge 
> with weight 5. Now the other two edges will create cycles so we will ignore them. In the end, we end up with a minimum spanning tree with total cost 11 ( = 1 + 2 + 3 + 5).

### Time Complexity:
> In Kruskal’s algorithm, most time consuming operation is **sorting** which takes **O(ElogE)** and the total complexity of the Disjoint-Set operations 
> will be **O(ElogV)**(without path compression), so the overall Time Complexity of the algorithm is **O(ElogE)** or **O(ElogV)**.       
> [Time Complexity Video](https://www.youtube.com/watch?v=3rrNH_AizMA)
