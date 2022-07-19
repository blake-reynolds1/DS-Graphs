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
