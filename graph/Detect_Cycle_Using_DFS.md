# Detect Cycle in an Undirected Graph Using DFS

## Problem Statement

Given an undirected graph represented as an adjacency list or matrix, determine whether there is a cycle present in the graph using Depth-First Search (DFS) traversal.

---

## Approach

### Explanation

- We can detect a cycle in an undirected graph using DFS by keeping track of visited nodes and the parent node from which the current node is reached.
- During DFS traversal, if we encounter a visited node that is not the parent of the current node, a cycle is detected.

### Steps

1. Use a set to keep track of visited nodes.
2. Perform DFS traversal starting from any unvisited node.
3. If a visited node is found that is not the parent of the current node, a cycle exists.

---

### Code in JavaScript

```javascript
function hasCycleDFS(graph) {
  const visited = new Set();

  // Helper function for DFS traversal
  function dfs(node, parent) {
    visited.add(node);

    for (const neighbor of graph[node]) {
      if (!visited.has(neighbor)) {
        // Continue DFS traversal
        if (dfs(neighbor, node)) {
          return true;
        }
      } else if (neighbor !== parent) {
        // If the neighbor is visited and not the parent, we found a cycle
        return true;
      }
    }

    return false;
  }

  // Check all components of the graph
  for (const node in graph) {
    if (!visited.has(Number(node))) {
      if (dfs(Number(node), -1)) {
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

console.log(hasCycleDFS(graph)); // Output: true
```

---

## Complexity

- **Time Complexity:** \(O(V + E)\)
  - Each node and edge is processed once during the DFS traversal.
- **Space Complexity:** \(O(V)\)
  - Space is required for the visited set and the call stack (due to recursion) in the DFS traversal.

---

## Summary

- This approach uses DFS traversal to explore the graph while keeping track of the parent node for each node being visited.
- If we encounter a node that has been visited and is not the parent, it indicates a cycle.

## Resources

[Video Link](https://www.youtube.com/watch?v=zQ3zgFypzX4&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=12&ab_channel=takeUforward)
