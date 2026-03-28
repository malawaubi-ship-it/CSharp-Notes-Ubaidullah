# Module 11: Exploring Graphs

1. Learning outcomes

By the end of this topic you should be able to:
learn graphs concepts, its application, adjacency list and matrix, node, edge and graph implementation, depth-first search and breadth-first search, application of Kruskal's and Prim's algorithms, as well as colouring and shortest path.
 

Prescribed Reading
Jamro, M., 2018. C# Data Structures and Algorithms: Explore the possibilities of C# for developing a variety of efficient applications. Packt Publishing Ltd. 
Page 202 – 257.  
Time Allocation:
2 Hours
 
2. Exploring Graphs

Adjacency list: An adjacency list represents a graph as an array of linked lists. The index of the array represents a vertex and each element in its linked list represents the other vertices that form an edge with the vertex.
Depth-first search (DFS) is an algorithm for traversing or searching tree or graph data structures. The algorithm starts at the root node (selecting some arbitrary node as the root node in the case of a graph) and explores as far as possible along each branch before backtracking. Extra memory, usually a stack, is needed to keep track of the nodes discovered so far along a specified branch which helps in backtracking of the graph.
Breadth-first search (BFS) is an algorithm for searching a tree data structure for a node that satisfies a given property. It starts at the tree root and explores all nodes at the present depth prior to moving on to the nodes at the next depth level. Extra memory, usually a queue, is needed to keep track of the child nodes that were encountered but not yet explored.
3. Search Algorithms

Search Algorithms: There are many types of search algorithms including Kruskal and Prim
Kruskal's algorithm is a minimum spanning tree algorithm that takes a graph as input and finds the subset of the edges of that graph which
	•	 form a tree that includes every vertex
	•	has the minimum sum of weights among all the trees that can be formed from the graph
Prim’s algorithm always starts with a single node, and it moves through several adjacent nodes, to explore all of the connected edges along the way. The idea behind Prim’s algorithm is simple, a spanning tree means all vertices must be connected. So, the two disjoint subsets of vertices must be connected to make a Spanning Tree.
12.1. Notes
12.1. Notes
	•	2. Stack
	•	3. Queue
