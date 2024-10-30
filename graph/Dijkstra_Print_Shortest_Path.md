# Dijkstra's Algorithm in JavaScript

Dijkstra's algorithm is a popular algorithm for finding the shortest path from a source node to all other nodes in a graph with non-negative weights.

## Step-by-step Explanation

1. **Initialize the graph**: Represent the graph using an adjacency list or matrix.
2. **Create a priority queue**: This will help to get the next node with the smallest distance.
3. **Set initial distances**: Initialize distances to all nodes as infinity, except for the starting node which is set to 0.
4. **Iterate through the nodes**: Update the distances to each neighboring node if a shorter path is found.
5. **Stop when all nodes are processed**: The algorithm continues until all nodes have been visited.

## Implementation

```javascript
class Graph {
  constructor() {
    this.nodes = {};
  }

  addNode(name) {
    this.nodes[name] = {};
  }

  addEdge(from, to, weight) {
    this.nodes[from][to] = weight;
    this.nodes[to][from] = weight; // For undirected graph
  }

  dijkstra(start) {
    const distances = {};
    const visited = {};
    const priorityQueue = new MinPriorityQueue();

    // Initialize distances and queue
    for (let node in this.nodes) {
      distances[node] = Infinity;
      visited[node] = false;
    }
    distances[start] = 0;
    priorityQueue.enqueue(start, 0);

    while (!priorityQueue.isEmpty()) {
      const { element: currentNode } = priorityQueue.dequeue();
      visited[currentNode] = true;

      for (let neighbor in this.nodes[currentNode]) {
        const weight = this.nodes[currentNode][neighbor];
        if (!visited[neighbor]) {
          const newDistance = distances[currentNode] + weight;

          if (newDistance < distances[neighbor]) {
            distances[neighbor] = newDistance;
            priorityQueue.enqueue(neighbor, newDistance);
          }
        }
      }
    }
    return distances;
  }
}

// MinPriorityQueue implementation
class MinPriorityQueue {
  constructor() {
    this.elements = [];
  }

  enqueue(element, priority) {
    this.elements.push({ element, priority });
    this.elements.sort((a, b) => a.priority - b.priority);
  }

  dequeue() {
    return this.elements.shift();
  }

  isEmpty() {
    return this.elements.length === 0;
  }
}

// Example usage
const graph = new Graph();
graph.addNode('A');
graph.addNode('B');
graph.addNode('C');
graph.addNode('D');

graph.addEdge('A', 'B', 1);
graph.addEdge('A', 'C', 4);
graph.addEdge('B', 'C', 2);
graph.addEdge('B', 'D', 5);
graph.addEdge('C', 'D', 1);

const distances = graph.dijkstra('A');
console.log(distances);
```

## Explanation of the Code

- **Graph Class**: Represents the graph structure and contains methods for adding nodes and edges.
- **dijkstra Method**: Implements Dijkstra's algorithm to calculate the shortest paths from the starting node.
- **MinPriorityQueue Class**: A simple priority queue implementation to store nodes based on their distances.
- **Example Usage**: Demonstrates how to create a graph, add nodes and edges, and calculate the shortest paths from a starting node.

## Complexity

- **Time Complexity**: **O((V+E)logV)**, where V is the number of vertices and E is the number of edges.
- **Space Complexity**: **O(V)** for storing distances and the priority queue.

## Conclusion

Dijkstra's algorithm is an efficient way to find the shortest path in graphs with non-negative weights. This implementation can be easily adapted for directed or weighted graphs.
