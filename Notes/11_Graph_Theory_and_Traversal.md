# Module 11: Graph Theory and Traversal

## Learning Outcomes

By the end of this module you should be able to:
- Describe what a graph is and the key terminology used.
- Distinguish between directed and undirected graphs.
- Implement Breadth-First Search (BFS) and Depth-First Search (DFS).

---

## What is a Graph?

A **graph** is a collection of **nodes (vertices)** connected by **edges**.
Unlike trees, graphs can have cycles and each node can have any number of connections.

Graphs model real-world networks: social networks (people are nodes, friendships are edges),
road maps (cities are nodes, roads are edges), and computer networks.

---

## Key Terminology

| Term | Description |
|------|-------------|
| Vertex (Node) | A point in the graph |
| Edge | A connection between two vertices |
| Directed graph | Edges have a direction (one-way) |
| Undirected graph | Edges have no direction (two-way) |
| Weighted graph | Edges have a numeric cost/weight |
| Adjacent | Two vertices connected by an edge |
| Path | A sequence of vertices connected by edges |
| Cycle | A path that starts and ends at the same vertex |

---

## Graph Representations in C#

### Adjacency List (Most Common)

Each vertex stores a list of its neighbours.
Space-efficient for **sparse** graphs (few edges compared to vertices).

```csharp
using System;
using System.Collections.Generic;

public class Graph
{
    private int vertices;
    private Dictionary<int, List<int>> adjacencyList;

    public Graph(int vertices)
    {
        this.vertices  = vertices;
        adjacencyList  = new Dictionary<int, List<int>>();
        for (int idx = 0; idx < vertices; idx++)
            adjacencyList[idx] = new List<int>();
    }

    public void AddEdge(int from, int to)
    {
        adjacencyList[from].Add(to);
        adjacencyList[to].Add(from); // remove this line for directed graphs
    }

    public void PrintGraph()
    {
        foreach (var kvp in adjacencyList)
        {
            Console.Write($"Vertex {kvp.Key}: ");
            Console.WriteLine(string.Join(" -> ", kvp.Value));
        }
    }
}
```

### Adjacency Matrix

A 2D boolean array where `matrix[i][j] = true` means there is an edge from i to j.
Efficient for **dense** graphs but uses O(V²) space.

```csharp
bool[,] matrix = new bool[5, 5];
matrix[0, 1] = true; // edge from 0 to 1
matrix[1, 0] = true; // undirected — symmetric
matrix[1, 2] = true;
matrix[2, 1] = true;
```

---

## Breadth-First Search (BFS)

BFS explores the graph **level by level** — visiting all neighbours of the current node before moving deeper.
It uses a **queue** internally.

Use BFS to find the **shortest path** in an unweighted graph.

```csharp
public void BFS(int startVertex)
{
    bool[] visited = new bool[vertices];
    Queue<int> queue = new Queue<int>();

    visited[startVertex] = true;
    queue.Enqueue(startVertex);

    Console.Write("BFS Order: ");
    while (queue.Count > 0)
    {
        int vertex = queue.Dequeue();
        Console.Write($"{vertex} ");

        foreach (int neighbour in adjacencyList[vertex])
        {
            if (!visited[neighbour])
            {
                visited[neighbour] = true;
                queue.Enqueue(neighbour);
            }
        }
    }
    Console.WriteLine();
}
```

---

## Depth-First Search (DFS)

DFS explores as **deep as possible** in one direction before backtracking.
It uses a **stack** (or the call stack via recursion) internally.

Use DFS for cycle detection, topological sorting, and solving mazes.

```csharp
public void DFS(int startVertex)
{
    bool[] visited = new bool[vertices];
    Console.Write("DFS Order: ");
    DFSRecursive(startVertex, visited);
    Console.WriteLine();
}

private void DFSRecursive(int vertex, bool[] visited)
{
    visited[vertex] = true;
    Console.Write($"{vertex} ");

    foreach (int neighbour in adjacencyList[vertex])
    {
        if (!visited[neighbour])
            DFSRecursive(neighbour, visited);
    }
}
```

---

## Full Example

```csharp
class Program
{
    static void Main()
    {
        Graph g = new Graph(6);
        g.AddEdge(0, 1);
        g.AddEdge(0, 2);
        g.AddEdge(1, 3);
        g.AddEdge(2, 4);
        g.AddEdge(3, 5);

        g.PrintGraph();
        g.BFS(0); // BFS Order: 0 1 2 3 4 5
        g.DFS(0); // DFS Order: 0 1 3 5 2 4
    }
}
```

---

## BFS vs DFS

| Property | BFS | DFS |
|----------|-----|-----|
| Data structure | Queue | Stack / Recursion |
| Order | Level by level | As deep as possible |
| Shortest path | Yes (unweighted) | No |
| Memory | O(V) — can be large for wide graphs | O(V) — better for deep graphs |
| Use cases | Shortest path, web crawling | Topological sort, cycle detection, maze solving |

---

## Summary

Graphs are one of the most versatile data structures in computer science.
BFS and DFS are the two fundamental traversal strategies, each with distinct strengths.
Understanding them opens the door to advanced topics such as Dijkstra's algorithm,
minimum spanning trees, and network flow.

Reference: Jamro, M. (2018). *C# Data Structures and Algorithms*. Packt Publishing.
