# Shortest Path in Directed Acyclic Graph - Topological Sort

To find the **shortest path in a Directed Acyclic Graph (DAG)**, we can leverage **Topological Sorting**. This approach is efficient because we only process each vertex and edge once, and the topological order ensures that we only relax edges once.

## Approach

1. **Topological Sort**: Find a topological ordering of the graph. In a DAG, a topological sort provides a linear ordering of vertices, such that for every directed edge \( u \to v \), vertex \( u \) comes before \( v \) in the ordering.
2. **Initialize Distances**: Set the distance from the source to itself as `0` and all other nodes as `Infinity`.
3. **Relax Edges in Topological Order**: Process each node in topological order, and for each node, relax all its outgoing edges (i.e., update distances of adjacent nodes if a shorter path is found).

## Code Implementation (JavaScript)

Here's how to implement this approach in JavaScript.

```javascript
function shortestPathDAG(vertices, edges, source) {
  const graph = Array.from({ length: vertices }, () => []);
  const distance = new Array(vertices).fill(Infinity);

  // Build adjacency list
  for (const [u, v, weight] of edges) {
    graph[u].push([v, weight]);
  }

  // Helper function to perform topological sort
  function topologicalSort() {
    const visited = new Array(vertices).fill(false);
    const stack = [];

    function dfs(node) {
      visited[node] = true;

      for (const [neighbor] of graph[node]) {
        if (!visited[neighbor]) {
          dfs(neighbor);
        }
      }
      stack.push(node);
    }

    for (let i = 0; i < vertices; i++) {
      if (!visited[i]) dfs(i);
    }

    return stack.reverse();
  }

  // Step 1: Perform topological sort
  const topologicalOrder = topologicalSort();

  // Step 2: Initialize distances from the source node
  distance[source] = 0;

  // Step 3: Relax edges in topological order
  for (const u of topologicalOrder) {
    if (distance[u] !== Infinity) {
      for (const [v, weight] of graph[u]) {
        if (distance[u] + weight < distance[v]) {
          distance[v] = distance[u] + weight;
        }
      }
    }
  }

  return distance;
}

// Example usage
const vertices = 6;
const edges = [
  [0, 1, 2],    // Edge from 0 to 1 with weight 2
  [0, 4, 1],    // Edge from 0 to 4 with weight 1
  [1, 2, 3],    // Edge from 1 to 2 with weight 3
  [2, 3, 6],    // Edge from 2 to 3 with weight 6
  [4, 2, 2],    // Edge from 4 to 2 with weight 2
  [4, 5, 4],    // Edge from 4 to 5 with weight 4
  [5, 3, 1]     // Edge from 5 to 3 with weight 1
];
const source = 0;

console.log("Shortest Distances from Source:", shortestPathDAG(vertices, edges, source));
```

## Explanation

1. **Graph Representation**: We use an adjacency list `graph`, where each entry is an array of `[neighbor, weight]` pairs for each vertex.
2. **Topological Sort**:
   - We perform DFS and push each vertex to a `stack` after visiting all its neighbors.
   - Once DFS is complete, we reverse the `stack` to get the topological order.
3. **Initialize Distances**:
   - Set the `distance` of the `source` to `0` and all other vertices to `Infinity`.
4. **Relaxation in Topological Order**:
   - For each node `u` in the topological order, we check its adjacent nodes `v`.
   - For each edge \( u \to v \) with weight `w`, if `distance[u] + w < distance[v]`, update `distance[v]`.

## Complexity Analysis

- **Time Complexity**: **O(V + E)**, where \( V \) is the number of vertices and \( E \) is the number of edges. This is because topological sorting takes \( O(V + E) \), and each edge is relaxed only once.
- **Space Complexity**: **O(V + E)** for storing the graph and the stack used in topological sorting.

## Example Output

Given the example input, the output might be:

```javascript
// Output
Shortest Distances from Source: [0, 2, 3, 8, 1, 5]
```

Here:
- Distance from `0` to `0` is `0`.
- Distance from `0` to `1` is `2`.
- Distance from `0` to `2` is `3`, etc. 

This solution provides the shortest path from the source to each node in a DAG efficiently.
