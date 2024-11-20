# Detect Cycle in an Undirected Graph Using BFS

## Problem Statement

Given an undirected graph represented as an adjacency list or matrix, determine whether there is a cycle present in the graph using a Breadth-First Search (BFS) traversal.

---

## Approach

### Explanation

- We can detect a cycle in an undirected graph by performing BFS traversal while keeping track of visited nodes.
- During traversal, if we encounter a node that has already been visited and is not the parent of the current node, we have detected a cycle.

### Steps

1. Maintain a visited set to track visited nodes.
2. Perform BFS traversal using a queue, starting from any unvisited node.
3. For each node, track its parent (the node it was reached from).
4. If a neighboring node is visited and it is not the parent, a cycle is detected.

---

### Code in JavaScript

```javascript
function hasCycleBFS(graph) {
  const visited = new Set();

  // Helper function to perform BFS traversal
  function bfs(node) {
    const queue = [[node, -1]]; // Queue stores [current node, parent]

    visited.add(node);

    while (queue.length > 0) {
      const [current, parent] = queue.shift();

      for (const neighbor of graph[current]) {
        if (!visited.has(neighbor)) {
          visited.add(neighbor);
          queue.push([neighbor, current]);
        } else if (neighbor !== parent) {
          // If the neighbor is visited and is not the parent, we have a cycle
          return true;
        }
      }
    }

    return false;
  }

  // Traverse all components of the graph
  for (const node in graph) {
    if (!visited.has(Number(node))) {
      if (bfs(Number(node))) {
        return true;
      }
    }
  }

  return false;
}

// Example usage
const graph = {
  0: [1, 2],
  1: [0, 2],
  2: [0, 1, 3],
  3: [2],
};

console.log(hasCycleBFS(graph)); // Output: true
```

---

## Complexity

- **Time Complexity:** \(O(V + E)\)
  - Each node and edge is processed once.
- **Space Complexity:** \(O(V)\)
  - Space is required for the visited set and the queue used for BFS traversal.

---

## Summary

- This approach works by performing a BFS traversal and keeping track of the parent node to ensure we don't falsely detect a cycle through the direct parent node.
- If we encounter a previously visited node that is not the parent, it indicates a cycle.

## Resources

[Video Link](https://www.youtube.com/watch?v=BPlrALf1LDU&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=11&ab_channel=takeUforward)
