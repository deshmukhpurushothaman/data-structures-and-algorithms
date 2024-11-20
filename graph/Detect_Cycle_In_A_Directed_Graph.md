# Detect Cycle in a Directed Graph Using DFS

## Problem Statement

Given a directed graph, determine if there is a cycle present in the graph using Depth-First Search (DFS). A cycle in a directed graph occurs when there is a path in the graph that starts and ends at the same vertex.

---

## Approach

### Explanation

To detect a cycle in a directed graph using DFS, we use a **recursive DFS approach** while maintaining two auxiliary data structures:

- **Visited Set**: Keeps track of nodes that have been fully processed.
- **Recursion Stack (or Recursion Path Set)**: Keeps track of nodes that are currently being processed in the DFS call stack.

During the DFS:

1. If we visit a node that is already in the recursion stack (i.e., it's part of the current path of DFS), a cycle is detected.
2. After visiting all neighbors of a node, we mark it as fully processed by removing it from the recursion stack.

---

### Steps

1. Traverse through all the nodes of the graph.
2. If the node is not visited, start a DFS from that node.
3. In the DFS, mark the node as visited and add it to the recursion stack.
4. For every adjacent node, if it's not visited, recursively call DFS for that node.
5. If the node is already in the recursion stack, a cycle is detected.
6. After exploring all neighbors of a node, remove it from the recursion stack to mark it as fully processed.

---

### Code in JavaScript

```javascript
function hasCycle(graph) {
  const visited = new Set();
  const recursionStack = new Set();

  // Helper function for DFS traversal
  function dfs(node) {
    if (recursionStack.has(node)) {
      return true; // Cycle detected
    }

    if (visited.has(node)) {
      return false; // Node already fully processed
    }

    visited.add(node);
    recursionStack.add(node);

    // Explore neighbors (directed edges)
    for (const neighbor of graph[node]) {
      if (dfs(neighbor)) {
        return true; // Cycle detected in a neighbor
      }
    }

    // Backtrack: remove node from recursion stack
    recursionStack.delete(node);
    return false;
  }

  // Check all nodes in the graph
  for (const node in graph) {
    if (!visited.has(Number(node))) {
      if (dfs(Number(node))) {
        return true;
      }
    }
  }

  return false;
}

// Example usage
const graph = {
  0: [1],
  1: [2],
  2: [0],
  3: [4],
};

console.log(hasCycle(graph)); // Output: true (Cycle exists: 0 -> 1 -> 2 -> 0)
```

---

## Complexity

- **Time Complexity:** \(O(V + E)\)

  - Where `V` is the number of vertices and `E` is the number of edges in the graph. Every node and edge is processed at most once during DFS traversal.

- **Space Complexity:** \(O(V)\)
  - Space is required for the visited set, recursion stack, and for storing the graph.

---

## Summary

- To detect a cycle in a directed graph, we use DFS and keep track of the nodes currently being explored (recursion stack).
- If we revisit a node that is already in the recursion stack, it means there's a cycle in the graph.
- This approach efficiently detects cycles by ensuring that each node and edge is processed only once.

## Resources

- [Video Link](https://www.youtube.com/watch?v=9twcmtQj4DU&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=19&ab_channel=takeUforward)

- [Article](https://takeuforward.org/data-structure/detect-cycle-in-a-directed-graph-using-dfs-g-19/)
