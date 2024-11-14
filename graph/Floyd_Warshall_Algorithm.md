# Floyd-Warshall Algorithm

## Introduction

The **Floyd-Warshall algorithm** is an all-pairs shortest path algorithm that finds the shortest paths between every pair of vertices in a weighted graph. It works with both directed and undirected graphs and can handle negative weights (but not negative cycles).

## Problem Statement

Given a graph with `n` vertices represented as a weighted adjacency matrix, the goal is to find the shortest distance between all pairs of vertices.

## Approach

1. **Graph Representation**: Use a 2D array `dist` where `dist[i][j]` represents the shortest distance from vertex `i` to vertex `j`.
2. **Initialization**:
   - Set `dist[i][i] = 0` for all `i`.
   - For an edge `(u, v)` with weight `w`, set `dist[u][v] = w`.
   - If there is no edge between `(u, v)`, set `dist[u][v] = Infinity`.
3. **Dynamic Programming Transition**:
   - For each pair `(i, j)`, update `dist[i][j]` using an intermediate vertex `k`.
   - The formula is: `dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])`.

## Steps

1. Initialize a distance matrix `dist` such that:
   - `dist[i][j] = 0` if `i == j`
   - `dist[i][j] = weight of edge (i, j)` if there is an edge between `i` and `j`
   - `dist[i][j] = Infinity` if there is no edge between `i` and `j`
2. Use three nested loops to iteratively update `dist` using intermediate vertices.

## Code Implementation (JavaScript)

```javascript
function floydWarshall(graph) {
  const dist = [];
  const n = graph.length;

  // Initialize the distance matrix
  for (let i = 0; i < n; i++) {
    dist[i] = [];
    for (let j = 0; j < n; j++) {
      if (i === j) {
        dist[i][j] = 0;
      } else if (graph[i][j] !== undefined) {
        dist[i][j] = graph[i][j];
      } else {
        dist[i][j] = Infinity;
      }
    }
  }

  // Floyd-Warshall algorithm
  for (let k = 0; k < n; k++) {
    for (let i = 0; i < n; i++) {
      for (let j = 0; j < n; j++) {
        if (dist[i][k] + dist[k][j] < dist[i][j]) {
          dist[i][j] = dist[i][k] + dist[k][j];
        }
      }
    }
  }

  // Return the distance matrix
  return dist;
}

// Example usage
const graph = [
  [0, 3, Infinity, 5],
  [2, 0, Infinity, 4],
  [Infinity, 1, 0, Infinity],
  [Infinity, Infinity, 2, 0],
];

console.log(floydWarshall(graph));
```

## Explanation

- **Initialization:** The `dist` matrix is created and initialized such that:

  - `dist[i][i] = 0` (distance from a node to itself).
  - For each edge `(i, j)` with weight `w`, set `dist[i][j] = w`.
  - If no edge exists between nodes `(i, j)`, set `dist[i][j] = Infinity`.

- **Three Nested Loops:**
  - For every possible intermediate vertex `k`, update all pairs `(i, j)` using `dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])`.
- **Result:** The `dist` matrix contains the shortest distances between all pairs of vertices.

## Complexity Analysis

- **Time Complexity:** **O(n^3)**, where `n` is the number of vertices. This is due to the three nested loops.
- **Space Complexity:** **O(n^2)** for storing the `dist` matrix.

## Example

### Input Graph (Adjacency Matrix)

```mathematica
graph = [
    [0, 3, Infinity, 5],
    [2, 0, Infinity, 4],
    [Infinity, 1, 0, Infinity],
    [Infinity, Infinity, 2, 0]
]
```

### Output

```csharp
[
    [0, 3, 7, 5],
    [2, 0, 6, 4],
    [3, 1, 0, 5],
    [5, 3, 2, 0]
]
```

## Resources

For a detailed explanation, check out this [video tutorial on Floyd-Warshall by takeUforward](https://www.youtube.com/watch?v=YbY8cVwWAvw&t=157s&ab_channel=takeUforward)
