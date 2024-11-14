# Prim's Algorithm - Minimum Spanning Tree (MST)

## Introduction

**Prim's Algorithm** is a greedy algorithm used to find the **Minimum Spanning Tree (MST)** of a weighted, undirected graph. The MST of a graph is a subset of the edges that connect all the vertices together without any cycles and with the minimum possible total edge weight.

## Approach

1. **Initialization**:
   - Choose an arbitrary starting vertex and mark it as visited.
   - Use a priority queue (or min-heap) to keep track of the edges with the smallest weights.
2. **Greedy Selection**:
   - Select the edge with the minimum weight that connects a visited vertex to an unvisited vertex.
   - Add this edge to the MST and mark the new vertex as visited.
3. **Repeat**:
   - Continue adding edges until all vertices are included in the MST.

## Code Implementation (JavaScript)

```javascript
class MinHeap {
  constructor() {
    this.heap = [];
  }

  push(node) {
    this.heap.push(node);
    this.bubbleUp(this.heap.length - 1);
  }

  pop() {
    if (this.size() === 1) return this.heap.pop();
    const min = this.heap[0];
    this.heap[0] = this.heap.pop();
    this.bubbleDown(0);
    return min;
  }

  size() {
    return this.heap.length;
  }

  bubbleUp(index) {
    while (index > 0) {
      const parentIndex = Math.floor((index - 1) / 2);
      if (this.heap[parentIndex][0] <= this.heap[index][0]) break;
      [this.heap[parentIndex], this.heap[index]] = [
        this.heap[index],
        this.heap[parentIndex],
      ];
      index = parentIndex;
    }
  }

  bubbleDown(index) {
    const length = this.size();
    let smallest = index;

    const leftChildIndex = 2 * index + 1;
    const rightChildIndex = 2 * index + 2;

    if (
      leftChildIndex < length &&
      this.heap[leftChildIndex][0] < this.heap[smallest][0]
    ) {
      smallest = leftChildIndex;
    }

    if (
      rightChildIndex < length &&
      this.heap[rightChildIndex][0] < this.heap[smallest][0]
    ) {
      smallest = rightChildIndex;
    }

    if (smallest !== index) {
      [this.heap[smallest], this.heap[index]] = [
        this.heap[index],
        this.heap[smallest],
      ];
      this.bubbleDown(smallest);
    }
  }
}

function primsAlgorithm(graph, n) {
  const mst = [];
  const visited = new Array(n).fill(false);
  const minHeap = new MinHeap();

  // Start with vertex 0
  minHeap.push([0, 0, -1]); // [weight, node, parent]

  while (minHeap.size() > 0) {
    const [weight, currentNode, parent] = minHeap.pop();

    if (visited[currentNode]) continue;

    visited[currentNode] = true;
    if (parent !== -1) {
      mst.push([parent, currentNode, weight]);
    }

    for (const [neighbor, edgeWeight] of graph[currentNode]) {
      if (!visited[neighbor]) {
        minHeap.push([edgeWeight, neighbor, currentNode]);
      }
    }
  }

  return mst;
}

// Example usage
const n = 5; // Number of vertices
const graph = [
  [
    [1, 2],
    [3, 6],
  ], // Node 0 connections
  [
    [0, 2],
    [2, 3],
    [3, 8],
    [4, 5],
  ], // Node 1 connections
  [
    [1, 3],
    [4, 7],
  ], // Node 2 connections
  [
    [0, 6],
    [1, 8],
  ], // Node 3 connections
  [
    [1, 5],
    [2, 7],
  ], // Node 4 connections
];

console.log(primsAlgorithm(graph, n));
```

## Explanation

- **Graph Representation:** The graph is represented as an adjacency list where each node has a list of `[neighbor, weight]` pairs.
- **Min-Heap:** A custom min-heap is used to keep track of the edges with the smallest weights efficiently.
- **Visited Array:** Keeps track of which vertices have already been included in the MST.
- **Building the MST:** We start from an arbitrary vertex (vertex `0` in this example), push its neighbors to the heap, and repeatedly select the minimum edge connecting a visited vertex to an unvisited one.

## Complexity Analysis

- **Time Complexity:** O(E log V), where `E` is the number of edges and `V` is the number of vertices. This is due to using a min-heap to select the minimum weight edge efficiently.
- **Space Complexity:** **O(V + E)** for storing the graph and the min-heap.

## Example

### Input Graph

```makefile
Vertices: 5
Edges: [(0, 1, 2), (0, 3, 6), (1, 2, 3), (1, 3, 8), (1, 4, 5), (2, 4, 7), (3, 4, 9)]
```

### Output

```csharp
[
  [0, 1, 2],
  [1, 2, 3],
  [1, 4, 5],
  [0, 3, 6]
]
```

## Explanation

- The output represents the edges in the Minimum Spanning Tree (MST) with their weights.
- The edges `[0, 1, 2]`, `[1, 2, 3]`, `[1, 4, 5]`, and `[0, 3, 6]` form the MST with a total weight of `16`.

## Resources

For a detailed explanation, check out this [video tutorial](https://www.youtube.com/watch?v=mJcZjjKzeqk&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=45&ab_channel=takeUforward)
