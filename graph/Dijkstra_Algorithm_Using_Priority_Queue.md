# Dijkstra's Algorithm - Using Priority Queue

**Dijkstra's Algorithm** is used to find the shortest path from a source node to all other nodes in a graph with non-negative weights. To improve efficiency, we can use a **priority queue** to ensure that we always expand the closest node next.

## Approach

1. **Initialize Distance Array**: Set the distance of the source node to `0` and all other nodes to `Infinity`.
2. **Priority Queue (Min-Heap)**: Use a min-heap to keep track of nodes with their distances in ascending order. Start by pushing the source node with distance `0`.
3. **Process Nodes**:
   - Pop the node with the smallest distance from the queue.
   - For each adjacent node, if the current distance plus edge weight is less than the stored distance, update the distance and push the adjacent node to the queue.
4. **Output Distances**: After processing all nodes, `distance` array contains the shortest path from the source to all other nodes.

## Code Implementation (JavaScript)

Here's how to implement Dijkstra's Algorithm with a priority queue in JavaScript.

```javascript
class MinHeap {
  constructor() {
    this.heap = [];
  }

  push(node) {
    this.heap.push(node);
    this.bubbleUp();
  }

  pop() {
    if (this.size() > 1) {
      this.swap(0, this.size() - 1);
      const min = this.heap.pop();
      this.bubbleDown(0);
      return min;
    } else {
      return this.heap.pop();
    }
  }

  size() {
    return this.heap.length;
  }

  bubbleUp() {
    let index = this.size() - 1;
    while (index > 0) {
      const parent = Math.floor((index - 1) / 2);
      if (this.heap[parent][1] <= this.heap[index][1]) break;
      this.swap(index, parent);
      index = parent;
    }
  }

  bubbleDown(index) {
    const left = 2 * index + 1;
    const right = 2 * index + 2;
    let smallest = index;

    if (left < this.size() && this.heap[left][1] < this.heap[smallest][1]) smallest = left;
    if (right < this.size() && this.heap[right][1] < this.heap[smallest][1]) smallest = right;

    if (smallest !== index) {
      this.swap(index, smallest);
      this.bubbleDown(smallest);
    }
  }

  swap(i, j) {
    [this.heap[i], this.heap[j]] = [this.heap[j], this.heap[i]];
  }
}

function dijkstra(vertices, edges, source) {
  const graph = Array.from({ length: vertices }, () => []);
  const distance = new Array(vertices).fill(Infinity);
  const minHeap = new MinHeap();
  
  // Build adjacency list
  for (const [u, v, weight] of edges) {
    graph[u].push([v, weight]);
    graph[v].push([u, weight]);  // assuming undirected graph
  }

  // Initialize
  distance[source] = 0;
  minHeap.push([source, 0]);

  while (minHeap.size() > 0) {
    const [u, distU] = minHeap.pop();
    
    if (distU > distance[u]) continue;

    for (const [v, weight] of graph[u]) {
      const newDist = distU + weight;
      if (newDist < distance[v]) {
        distance[v] = newDist;
        minHeap.push([v, newDist]);
      }
    }
  }

  return distance;
}

// Example usage
const vertices = 5;
const edges = [
  [0, 1, 4], [0, 2, 1], [2, 1, 2],
  [1, 3, 5], [2, 3, 8], [3, 4, 3]
];
const source = 0;

console.log("Shortest Distances from Source:", dijkstra(vertices, edges, source));
```

## Explanation

1. **Graph Representation**: We use an adjacency list `graph`, where each entry is an array of `[neighbor, weight]` pairs for each vertex.
2. **Priority Queue (Min-Heap)**: We implement a min-heap class `MinHeap` to keep track of nodes to process by distance.
3. **Initialize Distances**:
   - Set `distance[source] = 0` and all other vertices to `Infinity`.
4. **Process Each Node in Min-Heap Order**:
   - For each node `u`, we expand its neighbors and update their distances if a shorter path is found.
   - Push each neighbor `v` to the min-heap with the new distance.

## Complexity Analysis

- **Time Complexity**: **O((V + E) * log V)**, where \( V \) is the number of vertices and \( E \) is the number of edges, due to heap operations.
- **Space Complexity**: **O(V + E)** for storing the graph and min-heap.

## Example Output

Given the example input, the output might be:

```javascript
// Output
Shortest Distances from Source: [0, 3, 1, 6, 9]
```

This solution provides the shortest path from the source to each node efficiently using a priority queue.
