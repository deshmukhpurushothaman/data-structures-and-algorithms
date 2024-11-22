# Bellman-Ford Algorithm

## Problem Statement:

The Bellman-Ford algorithm is used to find the shortest paths from a source vertex to all other vertices in a weighted graph. Unlike Dijkstra's algorithm, it can handle graphs with negative weight edges. However, it cannot handle graphs with negative weight cycles.

---

## Approach:

The Bellman-Ford algorithm works by repeatedly relaxing all edges. Relaxation means updating the shortest path estimate for each edge if a shorter path is found. It performs this relaxation up to `V-1` times, where `V` is the number of vertices. Additionally, it performs one more iteration to detect negative weight cycles.

---

### Steps:

1. Initialize the distance to all vertices as `Infinity`, except for the source vertex, which is set to `0`.
2. Relax all edges `V-1` times:
   - For each edge `(u, v, weight)`, if `distance[u] + weight < distance[v]`, update `distance[v]`.
3. Check for negative weight cycles:
   - For each edge `(u, v, weight)`, if `distance[u] + weight < distance[v]`, a negative weight cycle exists.

---

### Code:

```javascript
function bellmanFord(graph, V, source) {
  // Initialize distances from source to all vertices as infinity
  let distances = new Array(V).fill(Infinity);
  distances[source] = 0;

  // Relax all edges V-1 times
  for (let i = 0; i < V - 1; i++) {
    for (let [u, v, weight] of graph) {
      if (distances[u] !== Infinity && distances[u] + weight < distances[v]) {
        distances[v] = distances[u] + weight;
      }
    }
  }

  // Check for negative weight cycles
  for (let [u, v, weight] of graph) {
    if (distances[u] !== Infinity && distances[u] + weight < distances[v]) {
      console.log('Graph contains a negative weight cycle');
      return;
    }
  }

  return distances;
}

// Example usage:
const graph = [
  [0, 1, -1],
  [0, 2, 4],
  [1, 2, 3],
  [1, 3, 2],
  [1, 4, 2],
  [3, 2, 5],
  [3, 1, 1],
  [4, 3, -3],
];

const V = 5; // Number of vertices
const source = 0;

console.log(bellmanFord(graph, V, source));
```

## Time and Space Complexity:

| Operation            | Time Complexity | Space Complexity | Notes                                                  |
| -------------------- | --------------- | ---------------- | ------------------------------------------------------ |
| Relaxation           | O(V \* E)       | O(V)             | V is the number of vertices, E is the number of edges. |
| Negative Cycle Check | O(E)            | O(1)             | Each edge is checked once after V-1 relaxations.       |

---

## Conclusion:

The Bellman-Ford algorithm is suitable for finding the shortest paths in graphs with negative weights, unlike Dijkstra’s algorithm. It is slower with a time complexity of `O(V * E)` but necessary when negative weights exist. It cannot handle graphs with negative weight cycles, as it detects but does not resolve them.

## Resources

[Video Link](https://www.youtube.com/watch?v=0vVofAhAYjc&t=1389s&ab_channel=takeUforward)
