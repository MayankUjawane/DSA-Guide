# Disjoint Set Union (DSU)
> **Disjoint Set Union or DSU** data structure is also called **Union Find** because of its two main operations.
>
> This data structure provides the following capabilities. We are given several elements, each of which is a separate set. 
> A DSU will have an operation to combine any two sets, and it will be able to tell in which set a specific element is.
>
> Thus this data structure consists of two operations:
>
> * **union_sets(a, b)** - merges the two specified sets (the set in which the element a is located, and the set in which the element b is located)
> * **find_set(v)** - returns the representative (also called leader) of the set that contains the element v. This representative is an element of its corresponding set. 
> It is selected in each set by the data structure itself (and can change over time, namely after union_sets calls). This representative can be used to check if 
> two elements are part of the same set or not. a and b are exactly in the same set, if find_set(a) == find_set(b). Otherwise they are in different sets.
> 
> The data structure allows you to do each of these operations in almost **O(1) time on average**.

### Build an efficient data structure
> We will store the sets in the form of trees: each tree will correspond to one set. And the root of the tree will be the representative/leader of the set.
>
> In the following image you can see the representation of such trees.
>
> ![Image](https://cp-algorithms.com/img/DSU_example.png)
>
> In the beginning, every element starts as a single set, therefore each vertex is its own tree. Then we combine the set containing the element 1 and the set containing 
> the element 2. Then we combine the set containing the element 3 and the set containing the element 4. And in the last step, we combine the set containing the element 1 
> and the set containing the element 3.
>
> For the implementation this means that we will have to maintain an array parent that stores a reference to its immediate ancestor in the tree.

### Naive Implementation
```java
class DSU {
    int[] parent = new int[100];
    
    public void makeSet() {
        for(int i=0; i<100; i++) {
            parent[i] = i;
        }
    }
    
    public void findSet(int v) {
        if(v == parent[v]) return v;
        return findSet(parent[v]);
    }
    
    public void unionSet(int a, int b) {
        a = findSet(a);
        b = findSet(b);
        
        if(a != b) 
            parent[b] = a;
    }
}
```
> `Time Complexity` : **O(N)** for both operations        
> `Space Complexity` : **O(N)**, for parent array.    
---
### Optimized Code
```java
class DSU {
    int[] parent = new int[100];
    int[] rank = new int[100];
    
    public void makeSet() {
        for(int i=0; i<100; i++) {
            parent[i] = i;
            rank[v] = 0;
        }
    }
    
    public int findSet(int v) {
        if(v == parent[v]) return v;
        return parent[v] = findSet(parent[v]);
    }
    
    public void unionSet(int a, int b) {
        int parentA = findSet(a);
        int parentB = findSet(b);
        
        if(parentA != parentB) {
            if(rank[parentA] < rank[parentB]) {
                parent[parentA] = parentB;
            } else if(rank[parentA] > rank[parentB]) {
                parent[parentB] = parentA;
            } else {
                parent[parentB] = parentA;
                rank[parentA]++;
            }
        }
    }
}
```
> `Time Complexity` : **O(1)**  
> `Space Complexity` : **O(N) + O(N)**, for parent array and rank array.    
---
Video Explanations -> [Pepcoding](https://www.youtube.com/watch?v=qHZxfNKUMXw&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=26), 
[Striver](https://www.youtube.com/watch?v=3gbO7FDYNFQ&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=23)
<hr>

### Path compression optimization
> This optimization is designed for speeding up find_set.
>
> If we call find_set(v) for some vertex v, we actually find the representative p for all vertices that we visit on the path between v and the actual representative p. 
> The trick is to make the paths for all those nodes shorter, by setting the parent of each visited vertex directly to p.
> 
> You can see the operation in the following image. On the left there is a tree, and on the right side there is the compressed tree after calling find_set(7), 
> which shortens the paths for the visited nodes 7, 5, 3 and 2.
>
> ![Path compression of call find_set(7)](https://cp-algorithms.com/img/DSU_path_compression.png)
>
> The new implementation of find_set is as follows:
> ```java
>     public int findSet(int v) {
>         if(v == parent[v]) 
>             return v;
>         return parent[v] = findSet(parent[v]);
>     }
> ```
> The simple implementation does what was intended: first find the representative of the set (root vertex), and then in the process of stack unwinding the visited nodes 
> are attached directly to the representative.
>
> his simple modification of the operation already achieves the time complexity **O(logn)** per call on average (here without proof). There is a second modification, that will 
> make it even faster.
-----
### Union by Rank
> In this optimization we will change the union_set operation. To be precise, we will change which tree gets attached to the other one. In the naive implementation the 
> second tree always got attached to the first one. In practice that can lead to trees containing chains of length O(n). With this optimization we will avoid this by 
> choosing very carefully which tree gets attached.
> 
> In this approach we use the depth of the tree (more precisely, the upper bound on the tree depth, because the depth will get smaller when applying path compression).
> 
> Here is the implementation of union by rank:
> ```java
>     public void unionSet(int a, int b) {
>         a = findSet(a);
>         b = findSet(b);
>         
>         if(parentA != parentB) {
>             if(rank[a] < rank[b]) {
>                 parent[a] = b;
>             } else if(rank[a] > rank[b]) {
>                 parent[b] = a;
>             } else {
>                 parent[b] = a;
>                 rank[a]++;
>             }
>         }
>     }
> ```
-----
### Time complexity
> If we combine both optimizations - path compression with union by rank - we will reach nearly constant time queries. It turns out, that the 
> final amortized time complexity is **O(α(n))**, where α(n) is the inverse Ackermann function, which grows very slowly. In fact it grows so slowly, that it doesn't exceed 4 for > all reasonable n (approximately n<10<sup>600</sup>).
> 
> Amortized complexity is the total time per operation, evaluated over a sequence of multiple operations. The idea is to guarantee the total time of the entire sequence, 
> while allowing single operations to be much slower then the amortized time. E.g. in our case a **single call might take O(logn) in the worst case**, but if we do m such calls > back to back we will end up with an **average time of O(α(n))**.
> 
> Also, it's worth mentioning that DSU with union by rank, but without path compression works in **O(logn)** time per query.
