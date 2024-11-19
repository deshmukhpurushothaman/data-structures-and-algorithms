# Breadth First Search (BFS) Algorithm in JavaScript

## What is Breadth First Search (BFS)?

Breadth First Search (BFS) is an algorithm for traversing or searching tree or graph data structures. It starts at the root (or an arbitrary node in the case of a graph) and explores all of its neighbors at the present depth level before moving on to nodes at the next depth level.

BFS is particularly useful in problems like finding the shortest path in an unweighted graph, level-order traversal of trees, and searching for a solution in a maze.

## Key Concepts

1. **Graph Representation**: BFS is typically implemented on graphs represented using an adjacency list or adjacency matrix.
2. **Queue**: BFS uses a queue data structure to explore nodes level by level. This ensures that nodes are explored in the order they are discovered.
3. **Exploration**: All neighbors of a node are explored before moving to the next level of nodes.

## How BFS Works

1. **Start from a node**: Begin traversal from the starting node.
2. **Explore neighbors**: Visit all neighboring nodes and mark them as visited.
3. **Use a queue**: The queue helps to keep track of the nodes to visit next. The first node added to the queue is the first one to be processed (FIFO).
4. **Repeat until the queue is empty**: Continue visiting neighbors and adding unvisited ones to the queue, until no more nodes are left to explore.

## BFS Algorithm Implementation in JavaScript

### BFS Implementation (Iterative Using Queue)

```javascript
function bfs(graph, start) {
  const visited = new Set(); // To track visited nodes
  const queue = [start]; // Queue to store nodes to be processed

  visited.add(start); // Mark the start node as visited

  while (queue.length > 0) {
    const node = queue.shift(); // Remove the first element from the queue

    console.log(node); // Process the node (e.g., print or store it)

    // Visit all unvisited neighbors of the current node
    for (let neighbor of graph[node]) {
      if (!visited.has(neighbor)) {
        visited.add(neighbor); // Mark as visited
        queue.push(neighbor); // Add neighbor to the queue
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

bfs(graph, 'A');
// Output: A, B, C, D, E, F
```

## Time and Space Complexities

### Time Complexity:

- **BFS Time Complexity is O(V + E)**, where:
  - `V` is the number of vertices (nodes) in the graph.
  - `E` is the number of edges in the graph.

This is because we visit each vertex and each edge at most once.

### Space Complexity:

- **BFS Space Complexity is O(V)**, where:
  - We store each node in the `visited` set.
  - We store the nodes in the queue at each level of traversal, and in the worst case, the queue could contain all the vertices in the graph.

## Applications of BFS

1. **Shortest Path in Unweighted Graph:** BFS finds the shortest path from a starting node to all other nodes in an unweighted graph.
2. **Level-order Traversal:** BFS is used in binary trees to print nodes at each level in a level-order fashion.
3. **Finding Connected Components:** BFS can identify all nodes connected to a particular node in an undirected graph.
4. **Solving Puzzles:** BFS is used in puzzles like finding the shortest path in mazes or solving the "8 puzzle problem" (sliding tiles).
5. **Web Crawling:** BFS is used to crawl websites, processing each page (node) before moving to linked pages.
