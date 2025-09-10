# Condensation Graph - Strongly Connected Components

A C++ implementation of Kosaraju's algorithm for finding strongly connected components (SCCs) in directed graphs and constructing the condensation graph.

## 📋 Overview

This project implements a complete solution for analyzing strongly connected components in directed graphs using **Kosaraju's two-pass algorithm**. The algorithm finds all SCCs and constructs a condensation graph where each SCC is represented as a single vertex.

A **strongly connected component** is a maximal set of vertices such that there is a path from each vertex to every other vertex within the component. The **condensation graph** is a directed acyclic graph (DAG) formed by contracting each strongly connected component to a single vertex.

## 🔬 Algorithm Description

**Kosaraju's Algorithm** is a linear-time algorithm that works in two main phases:

1. **First DFS Pass**: Perform DFS on the original graph G to compute finishing times for all vertices
2. **Graph Transposition**: Create G^T (transpose of G) by reversing all edge directions  
3. **Second DFS Pass**: Perform DFS on G^T in decreasing order of finishing times from step 1

Each DFS tree in the second pass corresponds to one strongly connected component.

### Time Complexity: O(V + E)
### Space Complexity: O(V + E)

## 🏗️ Project Structure

```
CondensationGraph/
├── main.cpp                    # Main program and input/output handling
├── SimpleDirectedGraph.h       # Graph class declaration
├── SimpleDirectedGraph.cpp     # Graph implementation with Kosaraju's algorithm
├── Vertex.h                    # Vertex class declaration  
├── Vertex.cpp                  # Vertex implementation
├── MyExceptions.h              # Custom exception classes
├── MyExceptions.cpp            # Exception implementations
├── CondensationGraph.vcxproj   # Visual Studio project file
├── CondensationGraph.vcxproj.filters # Visual Studio filters
└── README.md                   # This file
```

## 🔧 Key Components

### SimpleDirectedGraph Class
- **Adjacency List Representation**: Efficient storage using `vector<Vertex*>`
- **DFS Implementation**: Complete depth-first search with proper vertex coloring
- **Graph Transposition**: O(V + E) algorithm to reverse all edges
- **Condensation Construction**: Builds the final condensed graph

### Vertex Class  
- **Index Management**: Handles both user (1-indexed) and internal (0-indexed) numbering
- **Color Coding**: Three-state coloring for DFS traversal:
  - `0` (White): Unvisited
  - `1` (Gray): Currently being processed  
  - `2` (Black): Completely processed
- **SCC Tracking**: Maintains representative vertex for each component

### Exception Handling
- **ValueNotSupportedException**: Invalid graph parameters (negative values)
- **OutOfBoundsException**: Vertex indices outside valid range
- **InvalidEdgeException**: Self-loops or other invalid edge cases

## 📥 Input Format

```
n m
u1 v1
u2 v2
...
um vm
```

**Parameters:**
- `n`: Number of vertices (positive integer)
- `m`: Number of directed edges (non-negative integer)  
- `ui vi`: Directed edge from vertex ui to vertex vi (1-indexed)

**Constraints:**
- Vertices must be in range [1, n]
- No self-loops allowed (ui ≠ vi)
- Duplicate edges are allowed

## 📤 Output Format

```
condensed_vertices condensed_edges
```

The program outputs two integers representing the number of vertices and edges in the condensation graph.

## 💡 Example

### Input:
```
6
8
1 2
1 3  
3 2
2 4
4 3
5 4
5 6
6 5
```

### Visualization:
```
Original Graph:
1 → 2 → 4 ← 5
↓   ↓   ↑   ↓
3 ←─┘   3   6
        ↑   ↓
        └───┘

SCCs: {1}, {2,3,4}, {5,6}
```

### Output:
```
3 2
```

**Explanation**: The condensation graph has 3 vertices (one for each SCC) and 2 edges between the components.


## 🔍 Algorithm Implementation Details

### First DFS (Finish Time Calculation)
```cpp
list<int> finishedListDFS() {
    // Performs DFS on original graph
    // Returns vertices in finishing time order
}
```

### Graph Transposition  
```cpp
SimpleDirectedGraph getTransposeGraph() {
    // Creates G^T by reversing all edges
    // Maintains vertex numbering
}
```

### Second DFS (SCC Identification)
```cpp
SimpleDirectedGraph treesDFS(list<int> loopOrder) {
    // Performs DFS on transpose graph
    // Each DFS tree = one SCC
    // Constructs condensation graph
}
```


---

**Author**: Algorithm Implementation for Educational Purposes  
**Last Updated**: September 2025
