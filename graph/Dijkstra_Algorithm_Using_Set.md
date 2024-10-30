# Dijkstra's Algorithm - Using Set

**Dijkstra's Algorithm** is used to find the shortest path in a graph with non-negative weights. Using a **set** allows us to efficiently manage the vertices as we explore the graph, similar to how a priority queue might be used.

## Approach

1. **Initialize Distance Array**: Set the distance of the source node to `0` and all other nodes to `Infinity`.
2. **Set**: Use a set to store nodes with their current shortest known distances.
3. **Process Nodes**:
   - Pick the node with the smallest distance from the set.
   - For each adjacent node, update its distance if a shorter path is found through the current node.
4. **Update Set**: Update the set with the new distances for nodes.
5. **Output Distances**: After processing all nodes, the distance array contains the shortest paths from the source to all nodes.

## Code Implementation (JavaScript)

```javascript
function dijkstraUsingSet(vertices, edges, source) {
  const graph = Array.from({ length: vertices }, () => []);
  const distance = new Array(vertices).fill(Infinity);
  distance[source] = 0;

  // Build adjacency list
  for (const [u, v, weight] of edges) {
    graph[u].push([v, weight]);
    graph[v].push([u, weight]); // for undirected graphs
  }

  const set = new Set();
  set.add([source, 0]);

  while (set.size > 0) {
    // Find node with minimum distance
    let minNode = [...set].reduce((min, node) =>
      node[1] < min[1] ? node : min
    );
    set.delete(minNode);

    const [u, distU] = minNode;
    if (distU > distance[u]) continue;

    for (const [v, weight] of graph[u]) {
      const newDist = distU + weight;
      if (newDist < distance[v]) {
        set.delete([v, distance[v]]); // Remove the old distance if it exists
        distance[v] = newDist;
        set.add([v, newDist]); // Add the new distance
      }
    }
  }

  return distance;
}

// Example usage
const vertices = 5;
const edges = [
  [0, 1, 4],
  [0, 2, 1],
  [2, 1, 2],
  [1, 3, 5],
  [2, 3, 8],
  [3, 4, 3],
];
const source = 0;

console.log(
  'Shortest Distances from Source:',
  dijkstraUsingSet(vertices, edges, source)
);
```

## Complexity Analysis

- **Time Complexity**: **O((V + E) \* log V)** due to the use of a set for efficiently accessing the minimum distance.
- **Space Complexity**: **O(V + E)** for storing the graph and distances.

The set shows nodes being added and removed based on current shortest distances.
Path updates occur step-by-step, revealing the shortest path from the source to each node.
