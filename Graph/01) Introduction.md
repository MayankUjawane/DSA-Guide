# Introduction
>Watch this video [Introduction to Graphs and Its Types](https://www.youtube.com/watch?v=LCrovIMurxY&list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw&index=2)      
>  
>A **graph** is a data structure that consists of the following two components: 
> * A finite set of **vertices** also called as **nodes**. 
> * A finite set of ordered pair of the form (u, v) called as **edge**. The pair is ordered because (u, v) is not the **same** as (v, u) in case of a **directed graph**(di-graph). 
> The pair of the form (u, v) indicates that there is an **edge from vertex u to vertex v**. The edges may contain **weight/value/cost**.
> 
> ![Undirected Graph](https://cdn.programiz.com/sites/tutorial2program/files/graph-vertices-edges.jpg)            
>V = {0 , 1, 2, 3}    
>E = {(0, 1), (0, 2), (0, 3), (1, 2)}        
>G = { V, E }

# Types of Graphs
>One thing that needs to be understood is that graphs are usually defined based on two factors.
> * **The first factor is whether the graph is weighted or not**. In graph theory, we sometimes care only about the fact that two nodes are connected. Other times, 
> we also care about the cost of moving from node u to node v.
> * **The second factor is whether the graph is directed or not**. If there’s an edge from u to v, and we can only move from node u to node v, then the graph is called directed. 
> However, in undirected graphs, an edge between nodes u and v means that we can move from node u to node v and vice-versa.        
>We can always transform any undirected graph to a directed graph by separating each edge between u and v to two edges.

# Real Life Applications of Graph
>Graphs are used to represent many real-life applications: Graphs are used to represent **networks**. The networks may include paths in a city or telephone network or circuit 
>network. Graphs are also used in social networks like linkedIn, Facebook. For example, in Facebook, each person is represented with a vertex(or node). Each node is a structure 
>and contains information like person id, name, gender, and locale.
>
> * **Google maps** uses graphs for building transportation systems, where intersection of two(or more) roads are considered to be a vertex and the road connecting two vertices 
> is considered to be an edge, thus their navigation system is based on the algorithm to calculate the shortest path between two vertices.
> * In **Facebook**, users are considered to be the vertices and if they are friends then there is an edge running between them. Facebook’s Friend suggestion algorithm uses 
> graph theory. Facebook is an example of **undirected graph**.
> * In **World Wide Web**, web pages are considered to be the vertices. There is an edge from a page u to other page v if there is a link of page v on page u. This is an 
> example of **Directed graph**. It was the basic idea behind Google Page Ranking Algorithm.
> * In **Operating System**, we come across the Resource Allocation Graph where each process and resources are considered to be vertices. Edges are drawn from resources to the 
> allocated process, or from requesting process to the requested resource. If this leads to any formation of a cycle then a deadlock will occur.

# Complexities
>With graph data structures, we usually pay attention to the following complexities:           
> ### Space Complexity 
>The approximate amount of memory needed to store a graph in the chosen data structure.        
>
> ### Time Complexity
> * **Connection Checking Complexity:** The approximate amount of time needed to find whether two different nodes are neighbors or not.
> * **Neighbors Finding Complexity:** The approximate amount of time needed to find all the neighboring nodes of some goal node.
>
>We call two different nodes **“neighboring nodes”** if there’s an edge that connects the first node with the second.
