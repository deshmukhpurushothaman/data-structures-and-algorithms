# Shortest Path in Undirected Graph with Unit Weights

In an undirected graph with **unit weights** (where each edge has a weight of 1), the **Breadth-First Search (BFS)** algorithm is ideal for finding the shortest path from a source node to all other nodes. BFS processes nodes in layers, guaranteeing that each node is visited in the order of increasing distance from the source.

## Approach

1. **Initialize Distance Array**: Set the distance of the source node to `0` and all other nodes to `Infinity`.
2. **Queue for BFS**: Use a queue to perform BFS starting from the source node.
3. **BFS Traversal**: For each node `u`, check all adjacent nodes `v`. If the current distance to `u` plus 1 is less than the distance to `v`, update `distance[v]` and add `v` to the queue.
4. **Output Distances**: After BFS completes, `distance` array contains the shortest path from the source to all other nodes.

## Code Implementation (JavaScript)

Here's how to implement this approach in JavaScript.

```javascript
function shortestPathUnitWeights(vertices, edges, source) {
  const graph = Array.from({ length: vertices }, () => []);
  const distance = new Array(vertices).fill(Infinity);
  const queue = [source];
  distance[source] = 0;

  // Build adjacency list
  for (const [u, v] of edges) {
    graph[u].push(v);
    graph[v].push(u);  // because the graph is undirected
  }

  // BFS
  while (queue.length > 0) {
    const u = queue.shift();

    for (const v of graph[u]) {
      if (distance[u] + 1 < distance[v]) {
        distance[v] = distance[u] + 1;
        queue.push(v);
      }
    }
  }

  return distance;
}

// Example usage
const vertices = 6;
const edges = [
  [0, 1], [0, 2], [1, 2], [1, 3],
  [2, 4], [3, 4], [3, 5]
];
const source = 0;

console.log("Shortest Distances from Source:", shortestPathUnitWeights(vertices, edges, source));
```

## Explanation

1. **Graph Representation**: We use an adjacency list `graph`, where each entry is an array of neighboring nodes.
2. **Initialize Distance**: Set `distance[source] = 0` and other distances to `Infinity`.
3. **BFS Traversal**:
   - Start from the source node, updating the distance for each neighboring node `v`.
   - Add `v` to the queue to process its neighbors next.
4. **Result**: The `distance` array contains the shortest path from the source to each node.

## Complexity Analysis

- **Time Complexity**: **O(V + E)**, where \( V \) is the number of vertices and \( E \) is the number of edges, as BFS visits each vertex and edge once.
- **Space Complexity**: **O(V + E)** for storing the graph and the queue used in BFS.

## Example Output

Given the example input, the output might be:

```javascript
// Output
Shortest Distances from Source: [0, 1, 1, 2, 2, 3]
```

Here:
- Distance from `0` to `0` is `0`.
- Distance from `0` to `1` is `1`.
- Distance from `0` to `2` is `1`, etc.

This solution provides the shortest path from the source to each node in an undirected graph with unit weights.
