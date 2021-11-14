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

### Code
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
    
    public void findSet(int v) {
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
Video Explanations -> Prim's Algorithm -> [Pepcoding](https://www.youtube.com/watch?v=qHZxfNKUMXw&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=26), 
[Striver](https://www.youtube.com/watch?v=3gbO7FDYNFQ&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=23)
<hr>
