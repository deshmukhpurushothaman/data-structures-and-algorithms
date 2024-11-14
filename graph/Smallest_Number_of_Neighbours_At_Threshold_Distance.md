# Find the City With the Smallest Number of Neighbors at a Threshold Distance

## Problem Statement

Given:

- An integer `n` representing the number of cities, numbered from `0` to `n-1`.
- An array `edges`, where each element is a triplet `[from, to, weight]` representing a bidirectional road between two cities with a distance `weight`.
- An integer `distanceThreshold`.

The goal is to find the city such that the number of cities within a `distanceThreshold` from it is the smallest. If there are multiple such cities, return the city with the greatest number.

## Approach

### Floyd-Warshall Algorithm

1. **Graph Representation**: Create an `n x n` matrix `dist` initialized with `Infinity` except for the diagonal elements, which are `0`.
2. **Edge Initialization**: For each edge `(from, to, weight)`, set `dist[from][to] = weight` and `dist[to][from] = weight` since the graph is undirected.
3. **Dynamic Programming**: Use the Floyd-Warshall algorithm to find all-pairs shortest paths.
4. **Count Neighbors**: For each city, count the number of other cities reachable within the `distanceThreshold`.
5. **Select the Result**: Find the city with the smallest number of reachable neighbors. If multiple cities have the same number, select the one with the greatest index.

## Code Implementation (JavaScript)

```javascript
function findTheCity(n, edges, distanceThreshold) {
  // Initialize distance matrix
  const dist = Array.from({ length: n }, () => Array(n).fill(Infinity));

  // Distance to itself is 0
  for (let i = 0; i < n; i++) {
    dist[i][i] = 0;
  }

  // Populate initial distances from edges
  for (const [from, to, weight] of edges) {
    dist[from][to] = weight;
    dist[to][from] = weight; // because the graph is undirected
  }

  // Floyd-Warshall Algorithm
  for (let k = 0; k < n; k++) {
    for (let i = 0; i < n; i++) {
      for (let j = 0; j < n; j++) {
        if (dist[i][k] + dist[k][j] < dist[i][j]) {
          dist[i][j] = dist[i][k] + dist[k][j];
        }
      }
    }
  }

  // Find the city with the smallest number of neighbors within the threshold
  let minReachable = Infinity;
  let resultCity = -1;

  for (let i = 0; i < n; i++) {
    let count = 0;
    for (let j = 0; j < n; j++) {
      if (i !== j && dist[i][j] <= distanceThreshold) {
        count++;
      }
    }

    // Choose the city with fewer neighbors; if tie, select the larger index
    if (count < minReachable || (count === minReachable && i > resultCity)) {
      minReachable = count;
      resultCity = i;
    }
  }

  return resultCity;
}

// Example usage
const n = 4;
const edges = [
  [0, 1, 3],
  [1, 2, 1],
  [1, 3, 4],
  [2, 3, 1],
];
const distanceThreshold = 4;

console.log(findTheCity(n, edges, distanceThreshold)); // Output: 3
```

## Explanation

1. **Graph Representation:** The `dist` matrix is used to store the shortest paths between each pair of nodes.
2. **Floyd-Warshall Algorithm:** This algorithm updates the matrix to find the shortest paths between all pairs of nodes.
3. **Counting Neighbors:** For each city, count the number of reachable cities within the threshold.
4. **Result Selection:** Select the city with the minimum count of reachable cities within the distance threshold. If there are ties, select the city with the larger index.

## Complexity Analysis

- **Time Complexity:** `O(n^3)` due to the three nested loops of the Floyd-Warshall algorithm.
- **Space Complexity:** `O(n^2)` for storing the distances.

## Example

Given:

- **n = 4** (4 cities)
- **Edges:**

  - [0, 1, 3]
  - [1, 2, 1]
  - [1, 3, 4]
  - [2, 3, 1]

- **Distance Threshold = 4**

## Explanation:

1. Compute all-pairs shortest paths using the Floyd-Warshall algorithm.
2. Count reachable neighbors for each city:
   - City 0: 2 neighbors (within distance 4)
   - City 1: 3 neighbors (within distance 4)
   - City 2: 3 neighbors (within distance 4)
   - City 3: 2 neighbors (within distance 4)
3. Result: City `3` (smallest number of neighbors; tie-breaking by largest index).

---

This solution finds the city with the smallest number of reachable neighbors within the specified distance threshold using the Floyd-Warshall algorithm.
