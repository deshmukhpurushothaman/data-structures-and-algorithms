# Depth First Search (DFS) Algorithm in JavaScript

## What is Depth First Search (DFS)?

Depth First Search (DFS) is a graph traversal algorithm that explores as far as possible along each branch before backtracking. It starts from a node (often called the "root" or "starting" node) and explores as deep as possible along one branch before backtracking and exploring the next branch.

DFS can be implemented using either **recursion** or **a stack** (iterative).

## Key Concepts

1. **Graph Representation**: In DFS, the graph is typically represented as an adjacency list or matrix.
2. **Traversal**: DFS visits each node once, and it explores deeper into the graph before backtracking.
3. **Backtracking**: If there are no more nodes to visit on the current path, DFS backtracks to the previous node to explore alternate paths.

## How DFS Works

1. **Start from a node**: Begin traversal from the starting node.
2. **Explore neighbors**: Visit an unvisited neighboring node and mark it as visited.
3. **Recursive Call**: Continue the DFS on the newly visited node (either recursively or iteratively).
4. **Backtrack**: If no unvisited neighbors exist, backtrack to the previous node and continue exploring other unvisited neighbors.

## DFS Implementation in JavaScript

### 1. **Recursive DFS Implementation**

In this version, DFS is implemented using recursion. The function calls itself on unvisited neighbors of the current node.

```javascript
function dfsRecursive(graph, node, visited = new Set()) {
  // Mark the node as visited
  visited.add(node);

  // Process the node (optional)
  console.log(node);

  // Visit all unvisited neighbors
  for (let neighbor of graph[node]) {
    if (!visited.has(neighbor)) {
      dfsRecursive(graph, neighbor, visited);
    }
  }
}
```

### Example Usage:

```javascript
let graph = {
  A: ['B', 'C'],
  B: ['A', 'D', 'E'],
  C: ['A', 'F'],
  D: ['B'],
  E: ['B', 'F'],
  F: ['C', 'E'],
};

dfsRecursive(graph, 'A');
// Output: A, B, D, E, F, C
```

### 2. Iterative DFS Implementation (using Stack)

In this version, DFS is implemented using an explicit stack rather than recursion.

```javascript
function dfsIterative(graph, start) {
  const visited = new Set();
  const stack = [start];

  while (stack.length > 0) {
    const node = stack.pop();

    if (!visited.has(node)) {
      visited.add(node);
      console.log(node); // Process the node

      // Add all unvisited neighbors to the stack
      for (let neighbor of graph[node]) {
        if (!visited.has(neighbor)) {
          stack.push(neighbor);
        }
      }
    }
  }
}
```

### Example Usage:

```javascript
let graph = {
  A: ['B', 'C'],
  B: ['A', 'D', 'E'],
  C: ['A', 'F'],
  D: ['B'],
  E: ['B', 'F'],
  F: ['C', 'E'],
};

dfsIterative(graph, 'A');
// Output: A, C, F, E, B, D
```

## Time and Space Complexities

### Time Complexity:

- **DFS Time Complexity is O(V + E)**, where:
  - `V` is the number of vertices (nodes) in the graph.
  - `E` is the number of edges in the graph.

This is because each node and edge is visited once in the traversal.

### Space Complexity:

- **DFS Space Complexity:**
  - **Recursive DFS:** The space complexity is **O(V)** due to the recursion stack.
  - **Iterative DFS:** The space complexity is **O(V)** because we store the nodes in the stack and the visited set.

## Applications of DFS:

1. **Pathfinding:** DFS is used in pathfinding algorithms like finding a path from one node to another.
2. **Topological Sorting:** In directed acyclic graphs (DAGs), DFS can be used to perform topological sorting.
3. **Cycle Detection:** DFS can be used to detect cycles in a graph (especially in directed graphs).
4. **Connected Components:** DFS is used to find all connected components in a graph.
5. **Solving Puzzles:** DFS is useful in problems like mazes, where you need to explore all possible paths.
