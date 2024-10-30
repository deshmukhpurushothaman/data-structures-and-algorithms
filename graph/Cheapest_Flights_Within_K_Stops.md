# Cheapest Flights Within K Stops

This problem involves finding the minimum cost of a flight from a starting city to a destination city, with at most `K` stops. This is a variation of the shortest path problem, where stops are limited, making it ideal for a modified BFS or Dijkstra's algorithm approach.

## Problem Statement

**Given:**

- n cities labeled from `0` to `n-1`.
- A list of flights, where each flight `[from, to, price]` represents a direct flight with a price from one city to another.
- A starting city (`src`) and a destination city (`dst`).
- An integer `K`, representing the maximum number of stops allowed.

Return the minimum cost to travel from src to dst within K stops. If it's not possible, return -1.

## Approach

1. **Graph Representation:** Create an adjacency list where each city points to its neighboring cities along with the price of flights.
2. **Min-Heap/Priority Queue:** Use a priority queue to explore the cheapest flights first.
3. **Track Costs and Stops:** For each city reached, record both the current cost to reach it and the number of stops taken so far.
4. **Terminate Early:** If we reach the destination city with the required conditions, return the cost. If the conditions are not met, continue until all possible paths have been explored up to `K` stops.

This approach is similar to Dijkstra’s Algorithm but includes a constraint on the number of stops.

## Code Implementation (JavaScript)

The following code implements the solution using a priority queue and an adjacency list.

```javascript
function findCheapestPrice(n, flights, src, dst, K) {
  const graph = Array.from({ length: n }, () => []);

  // Build adjacency list
  for (const [from, to, price] of flights) {
    graph[from].push([to, price]);
  }

  // Priority queue: stores [current cost, current city, stops used]
  const minHeap = [[0, src, 0]];
  const costs = Array.from({ length: n }, () => Infinity);
  costs[src] = 0;

  while (minHeap.length) {
    const [currentCost, city, stops] = minHeap.shift();

    // If destination is reached with stops within allowed K
    if (city === dst) return currentCost;
    if (stops > K) continue;

    // Explore neighbors
    for (const [nextCity, price] of graph[city]) {
      const newCost = currentCost + price;

      if (newCost < costs[nextCity] || stops < K) {
        costs[nextCity] = newCost;
        minHeap.push([newCost, nextCity, stops + 1]);
        minHeap.sort((a, b) => a[0] - b[0]); // Ensure minHeap sorted by cost
      }
    }
  }

  return -1;
}

// Example usage
const n = 4;
const flights = [
  [0, 1, 100],
  [1, 2, 100],
  [2, 3, 100],
  [0, 2, 500],
];
const src = 0;
const dst = 3;
const K = 1;

console.log(findCheapestPrice(n, flights, src, dst, K)); // Output: 200
```

## Explanation

1. **Graph Representation:** Each node (city) has a list of direct flights with costs.
2. **Priority Queue Management:** We maintain the queue by pushing in paths with increasing cost, so the queue processes paths with the least cost first.
3. **Tracking Stops:** Stops are counted for each path; if stops exceed K, we skip that path.

## Complexity Analysis

- **Time Complexity:** **O(E \* log(V))** where E is the number of edges (flights) and V is the number of vertices (cities), due to heap operations and edge relaxation.
- **Space Complexity:** **O(V + E)** for storing the graph and additional data structures.

## Example

With the example graph of 4 cities and the following flights:

- 0 → 1 with price 100
- 1 → 2 with price 100
- 2 → 3 with price 100
- 0 → 2 with price 500
  Starting from city `0`, destination city `3` with up to `1` stop:

- Output: `200` (Path: 0 → 1 → 2)

This solution efficiently finds the cheapest flight within K stops using a priority queue.
