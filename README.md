# Graphs
## Introduction
* In many applications, we need to connect different "physical" points, and perform data mining through the connectivity
  - E.g., find the best route: including the waypoints
  - <img width="541" alt="Screen Shot 2022-07-19 at 6 11 04 PM" src="https://user-images.githubusercontent.com/89602311/179863360-5ebec593-ec14-4f9b-824e-3e6d1cc14320.png">
* Applications of graphs
  - Electronic circuits
    - Printed circuit board
    - Integrated circuit
  - Transportation networks
    - Highway network
    - Flight network
  - Computer networks
    - Local area network
    - Internet
    - Web
  - Databases
    - Entity-relationship diagram
* <img width="314" alt="Screen Shot 2022-07-19 at 6 12 50 PM" src="https://user-images.githubusercontent.com/89602311/179863527-0b4ee3c8-aba0-4f33-b60f-e9554bc56003.png">
* A graph G is a pair (V, E) consists of
  - a set V, whose members are called vertices of G, and
  - a set E of pairs of vertices from V
    - The pairs are called edges of G
    - E.g., for vertices u and v, if they are connected, then there is an edge between them, this edge can be represented as a pair (u,v)
  - Directed edge
    - Ordered pair of vertices: (origin u, destination v)
  - Undirected edge
    - Unordered pair of vertices
  - <img width="250" alt="Screen Shot 2022-07-19 at 6 14 49 PM" src="https://user-images.githubusercontent.com/89602311/179863687-60b0685a-b203-46c3-8f26-529612443cba.png">
  - Directed graph (often shortened to digraph)
    - All the edges are directed
    - E.g., route network
  - Undirected graph
    - All the edges are undirected
    - E.g., flight network
  - A path is a sequence of distinct vertices, each adjacent to the next
  - A cycle is a path containing at least three vertices such that the last vertex on the path is adjacent to the first
  - A graph is called connected if there is a path from any vertex to any other vertex
* <img width="575" alt="Screen Shot 2022-07-19 at 6 16 58 PM" src="https://user-images.githubusercontent.com/89602311/179863887-6bc3abfb-1198-4f5b-a63c-5c82dad22e38.png">
## Objectives
* Mathematical concepts of a graph
* Graph representations
* Graph ADT
* Graph traversal
  - Breadth First Search (BFS)
  - Depth First Search (DFS)
* Shortest path
## Graph representations
* How to get an efficient computer representation of a graph
  - Look at the mathematical definition of a graph: A grpah G is a pair (V,E), consists of 
    - a set V, whose members are called the vertices of G, and
    - a set E of edges, which are pairs of vertices from V
  - Naturally a graph can be represented by sets
  - It turns out that sets, tables, (matrix, 2-D array), and lists can all be used to represent graphs
  - The key is the connectivity of vertices: specify the neighbors of each vertex
    - Question: how to specify the edges very efficiently
    - Answer: for a vertex, specify edges connecteed to it by specifying its neighbors as a set/array/list
* Graph representation by set
  - Use one set V for the vertices in the graph, and 
  - For each vertex v is an element of V, a subset Av of V is used to represent all vertices adjacent to v
    - It is easier to work with sets of vertices than with pairs of vertices
  - <img width="574" alt="Screen Shot 2022-07-19 at 6 33 54 PM" src="https://user-images.githubusercontent.com/89602311/179865509-e3dcc361-1861-4fa8-9ba2-785be20253c7.png">
    - If v is a number representing a vertex, the array entry neighbors[v] is the set of all vertices adjacent to the vertex v
* Graph representation by adjacency matrix
  - <img width="579" alt="Screen Shot 2022-07-19 at 6 34 48 PM" src="https://user-images.githubusercontent.com/89602311/179865590-903c642d-0682-47ef-8f98-a6290e588c03.png">
  - If v is a number representing a vertex, adjacency[v][w] is true if and only if vertex v is adjacent to vertex w
  - For directed graphs, adjacency[v][w] indicates whether the edge from v to w is in the graph or not
  - For undirected graphs, the adjacency table is symmetric
    - adjacency[v][w] = adjacency[w][v] for all v and w
* Graph representation by adjacency matrix
  - <img width="603" alt="Screen Shot 2022-07-19 at 6 37 37 PM" src="https://user-images.githubusercontent.com/89602311/179865823-9b7e3e95-ec8f-4aef-b52c-ecac0c987e3a.png">
* Typically, a graph can be updated in real cases
  - E.g., with new vertices/edges added
  - Then matrix-based implementation may not be suitable
    - How to make the size dynamic
* Graph representation by adjacency list
  - <img width="613" alt="Screen Shot 2022-07-19 at 6 38 53 PM" src="https://user-images.githubusercontent.com/89602311/179865934-775574d7-410e-4d90-a5b2-c35e344fec40.png">
  - If v is a number representing a vertex, the array entry neighbors[v] is the list of all vertices adjacent to the vertex v
  - This is very similar as the set representation of a graph
  - The list in the declaration can be either contiguous or linked
* Adjacency matrix
  - <img width="589" alt="Screen Shot 2022-07-19 at 6 40 20 PM" src="https://user-images.githubusercontent.com/89602311/179866042-921104d9-c978-462f-a1c1-cba8482224fe.png">
* Adjacency list
  - <img width="661" alt="Screen Shot 2022-07-19 at 6 40 47 PM" src="https://user-images.githubusercontent.com/89602311/179866067-9f835aa1-4698-4420-b1f5-5f0e31958fd8.png">
* Graph representation by linked objects
  - <img width="647" alt="Screen Shot 2022-07-19 at 6 41 08 PM" src="https://user-images.githubusercontent.com/89602311/179866095-b19e5632-e10c-40d8-949c-02722ccf802b.png">
* <img width="627" alt="Screen Shot 2022-07-19 at 6 41 21 PM" src="https://user-images.githubusercontent.com/89602311/179866116-ed871747-be39-456a-bc27-fb5c4a429a61.png">
## Graph ADT
* adjacent(G, u, v): tests whether there is an edge from the vertex u to the vertex v;
* neighbors(G, v): lists all vertices u such that there is an edge from the vertex v to the vertex u;
* add_vertex(G, v): adds the vertex v, if it is not there;
* remove_vertex(G, v): removes the vertex v, if it is there;
* add_edge(G, u, v): adds the edge from the vertex u to the vertex v, if it is not there;
* remove_edge(G, u, v): removes the edge from the vertex u to the vertex v, if it is there;
* get_vertex_value(G, v): returns the value associated with the vertex v;
* set_vertex_value(G, v, x): sets the value associated with the vertex v to x
* Which graph representation to use?
  - E.g., adjacency matrix uses more space O(|V|^2)
  - E.g., adjacency list uses less space O(|V|+|E|)
  - E.g., adjacency matrix: easy to add/query/remove an edge in O(1)
  - E.g., adjacency list: add/query/remove an edge needs O(|V|) time
  - ...
  - Depends on the real application: similar as choosing th erigh implementation for lists
  - We will skip the complete comparison and implementation which are tedious
## Graph traversal
* Traversal
  - Proccess all the vertices in more systematical order
  - The traversal may start at any vertex in a graph
  - Two main methods for graph traversal
    - Depth-first traversal
    - Breadth-first traversal
* Depth-first traversal
  - Let w1, w2, ... wk be the vertices adjacent to v, w1 should be visited next and w2, ... wk will wait
  - After w1 is visited, all the vertices to which it is adjacent should be visited before returning to traverse w2, ... wk
  - The process continues recursively until all the vertices in the graph are visited
  - <img width="423" alt="Screen Shot 2022-07-21 at 5 10 03 PM" src="https://user-images.githubusercontent.com/89602311/180323510-47865c81-310a-4f7b-addb-5399b3b7e563.png">
* Two difficulties
  - First, the graph may contain cycles, the traversal algorithm may visit the same vertex repeatedly
    - Need to indicate wheter the vertex has been visited or not
  - Second, the graph may not be connected. The traversal algorithm may stop before it visits all vertices
    - Need a loop that tuns through all vertices to cover all components of the graph
* <img width="551" alt="Screen Shot 2022-07-21 at 5 11 54 PM" src="https://user-images.githubusercontent.com/89602311/180323715-6e6d2266-d086-4381-aa78-984e5c97db1b.png">
* Breadth-first traversal
  - If the traversal has just visited a vertex v, then it next visits all the vertices adjacent to v
  - The vertices adjacent to those vertices adjacent to v are put in a queue and they are traversed after all vertices adjacent to v have been visited
  - The process continues until all the vertices in the graph are visited
  - A Queue is used for the breadth-first algorithm
* <img width="577" alt="Screen Shot 2022-07-21 at 5 13 46 PM" src="https://user-images.githubusercontent.com/89602311/180323956-ea4cc4d6-9fa4-4bfe-a42d-1b9bd12ccb1c.png">
* <img width="566" alt="Screen Shot 2022-07-21 at 5 13 58 PM" src="https://user-images.githubusercontent.com/89602311/180323979-14c71e08-ba56-44e1-b25a-020ac6dc4d71.png">
* Find a consistent visiting sequence for neighbors
  - When you implement the breadth-first search or the depth-first search, you need to use the adjacency matrix or the adjacency list of the given graph in order to determine the order of visiting nodes (reflected by the green parts)
  - You cannot randomly jump around from one node to another to visit nodes
* Given a undirected connected graph with uniformly weighted edges
  - BFS finds the shortest path from starting vertex to all the other vertices
  - traverse(v, visited, visit) in DFS, finds a maximal connected subgraph containing v
## Shortest Path
* If we have uniformly weighted edges, then BFS can find the shortest path from starting vertex to all other vertices
* What if the weights are not uniform?
  - In real applications, the weights may represent costs, time, or some quantity other than distance
  - The weights should be non-negative
  - Can we still use the idea of BFS?
* Let's use SP(S, T) to denote the distance along the shortest path from S to T
* For the graph below, we want to find the shortest path from S to T
* <img width="149" alt="Screen Shot 2022-07-21 at 5 47 29 PM" src="https://user-images.githubusercontent.com/89602311/180327690-c0dbc377-4494-4f24-b4e9-9a7dd8875592.png">
* If we run BFS, we found T within 2 moves, But do you think the cost to go to T along the edges (S, B) and (B, T) is the smallest?
  - No: along S->A->D->T, the total cost is 6, which is smaller
  - BFS can no long find the shortest path if the weights are non-uniform
  - What to do?
* Note
  - In the first iteration of BDS, we found that A is the closest to S, then the shortest path from S to A can be determined (why? Non-negative w.)
  - But we stil can't determine SP(S, B) (why?)
  - Do you think we can determind the shortest path from S to C after the second iteration? (why?)
    - We have confirmed SP(S, A) = 1
      - This is the foundation for further move
    - BAsed on S and A, we can further reach B, C, and D within 1 move
    - So far, dist(S, B) = 5, dist(S, C) = 3 and dist(S, D) = 4
    - We can confirm that SP(S, C) = 3
      - This is the shortest path within 2 moves or less, without revisit
      - Because the weights are non-negative, with more moves, the length of the path will only increase, so SP(S, C = 3)
  - <img width="154" alt="Screen Shot 2022-07-21 at 5 53 04 PM" src="https://user-images.githubusercontent.com/89602311/180328325-42d7d900-487a-46c1-ad04-859dc7ad2c12.png">
  - In the next move, can we determind SP(S,B) and SP(S,D)?
    - We have confirmed that SP(S, A) =1 and SP(S, C) = 3
    - Then with one more move we can reach B, D and T
      - For B, we can reach it from S or C, which path is shorter? From C to B, it's shorter, and dist(S, B) =4
      - For D, we can reach it from A or C, and it's shorter from A, and dist(S, D) =4
      - Similarly, dist(S, T) = 7
    - With the next move we can determine that SP(S,B) =4 and SP(S,D) = 4, because they are the shortest distance with one more move
  - <img width="152" alt="Screen Shot 2022-07-21 at 5 55 51 PM" src="https://user-images.githubusercontent.com/89602311/180328583-42f84201-8f19-4048-991c-4c62b8459c04.png">
  - So far, we have SP(S, A) =1, SP(S,C)=3, SP(S,B)=4, and SP(S,D)=4
  - What's the shortest path to T?
    - We can reach T from B, C, or D
    - From B, dist(S, T) = 7
    - From C, dist(S, T) = 7
    - From D, dist(S, T) = 6
    - Clearly, it's shorter from D, and SP(S, T) = 6
  - <img width="147" alt="Screen Shot 2022-07-21 at 5 59 04 PM" src="https://user-images.githubusercontent.com/89602311/180328893-f00055ec-18db-4d1a-bd75-237211a7bf3e.png">
* The confirmed shortest paths to some vertices are the foundation for the next move
* For every move, we find one more vertex to which we have the shortest path
* Dijstra's Algorithm
  - The algorithm keeps a set S of vertices whose shortest distance from source is known
  - Initially source is the only vertex in S
  - At each step, a remaining vertex (not in S), for which the shortest path from source has been found, is added to S
    - Which vertex shouddl be added to S at each step?
    - Choose the remaining vertex which has the shortest distance so far, with one more step from a vertex in S
    - Proof: if there is a shorter path through x, then x must have been chosen in some previous step
  - <img width="203" alt="Screen Shot 2022-07-21 at 6 01 07 PM" src="https://user-images.githubusercontent.com/89602311/180329062-f3c2a751-bc03-4505-b560-17892ce457f6.png">
* Dijkstra's Algorithm (cont.)
  - We can implement this absed on adjacency matrix
    - Suitable for random access: any vertex can be added to S, so updates on distances need random access
    - The non-uniform weights can be directly stored in the adjacency matrix
  - <img width="545" alt="Screen Shot 2022-07-21 at 6 04 08 PM" src="https://user-images.githubusercontent.com/89602311/180329334-19f1aef4-21e0-4b4c-8997-8263ccaae95e.png">
* <img width="562" alt="Screen Shot 2022-07-21 at 6 04 18 PM" src="https://user-images.githubusercontent.com/89602311/180329352-11d7b92e-28fc-4f94-9d69-7749cd85581f.png">
* Find SP for each vertex
* Assume that vertex 0 is the source
* If there is a tie, we can pick the vertex with the smallest label
* <img width="469" alt="Screen Shot 2022-07-21 at 6 04 59 PM" src="https://user-images.githubusercontent.com/89602311/180329423-442670d0-011a-40bc-bccb-ac5c227c4708.png">
* <img width="596" alt="Screen Shot 2022-07-21 at 6 05 16 PM" src="https://user-images.githubusercontent.com/89602311/180329446-d78309f8-4448-440c-8013-c746b9298dca.png">
* <img width="604" alt="Screen Shot 2022-07-21 at 6 05 26 PM" src="https://user-images.githubusercontent.com/89602311/180329458-3121a3ce-1191-4c91-b412-a0ac55a232d5.png">
* <img width="594" alt="Screen Shot 2022-07-21 at 6 05 34 PM" src="https://user-images.githubusercontent.com/89602311/180329472-d550cb73-f9cb-4057-9568-f1a00b58b207.png">
* <img width="595" alt="Screen Shot 2022-07-21 at 6 05 46 PM" src="https://user-images.githubusercontent.com/89602311/180329487-b06ed368-9d79-4159-a834-fe8b87f1316c.png">
* <img width="608" alt="Screen Shot 2022-07-21 at 6 05 57 PM" src="https://user-images.githubusercontent.com/89602311/180329499-a03faf86-a6b3-4e23-a5ef-b334d87d7982.png">
* <img width="607" alt="Screen Shot 2022-07-21 at 6 06 07 PM" src="https://user-images.githubusercontent.com/89602311/180329513-cc2b5fb3-c5c6-498b-ba89-71deca02939b.png">
* <img width="603" alt="Screen Shot 2022-07-21 at 6 06 20 PM" src="https://user-images.githubusercontent.com/89602311/180329532-4ed7b2bd-f2af-42e1-b430-bfb05a1508cc.png">
## Self Test
* How to store a graph in a file? Adjacency matrix
* How to implement an iterative DFS? Use a stack
* How to get the actual shortest path, instead of the length of the shortest path? Add one more array, associated with distances, to record the previous vertex along the shortest path
## Extended Readings
* Degree of a vertex 
  - https://en.wikipedia.org/wiki/Degree_(graph_theory
