# Topological Sort in Graphs

## Problem Statement

Topological Sort is an ordering of the vertices in a Directed Acyclic Graph (DAG) where for every directed edge `u -> v`, vertex `u` comes before `v` in the ordering. Topological sorting is used in various applications, such as task scheduling, course scheduling, build systems, etc.

### Example

Consider the graph:

```
 5 → 0 ← 4
 ↓    ↑
 2 → 3 → 1
```

A valid topological order is: `[4, 5, 2, 3, 1, 0]`.

---

## Approach: Using Depth First Search (DFS)

### Algorithm Steps

1. Create an empty stack to store the result.
2. Create a `visited` set to keep track of visited nodes.
3. For each unvisited node, perform a DFS traversal and push the node onto the stack after visiting all its adjacent nodes.
4. The stack contains the nodes in topologically sorted order (after all DFS calls are complete).

### Code (DFS-based Topological Sort):

```javascript
function topologicalSort(graph) {
  const visited = new Set();
  const stack = [];

  function dfs(node) {
    if (visited.has(node)) return;
    visited.add(node);
    for (const neighbor of graph[node]) {
      dfs(neighbor);
    }
    stack.push(node);
  }

  for (let node in graph) {
    if (!visited.has(parseInt(node))) {
      dfs(parseInt(node));
    }
  }

  return stack.reverse(); // Reverse the stack to get the correct order
}

// Example usage
const graph = {
  5: [0],
  4: [0, 1],
  3: [1],
  2: [3],
  1: [],
  0: [],
};
console.log(topologicalSort(graph)); // Output: [4, 5, 2, 3, 1, 0]
```

## Approach: Using Kahn's Algorithm (BFS-based)

### Algorithm Steps

1. Calculate the in-degree (number of incoming edges) for each node.
2. Initialize a queue with all nodes that have an in-degree of 0.
3. While the queue is not empty:
   - Dequeue a node and add it to the topological order.
   - Reduce the in-degree of each of its neighbors by 1.
   - If any neighbor's in-degree becomes 0, add it to the queue.
4. If all nodes are processed, return the topological order. If not, the graph has a cycle and topological sorting is not possible.

## Code (BFS-based Topological Sort - Kahn's Algorithm):

```javascript
function topologicalSortKahn(graph) {
  const inDegree = {};
  const queue = [];
  const topoOrder = [];

  // Initialize in-degree of all nodes
  for (const node in graph) {
    inDegree[node] = 0;
  }
  for (const node in graph) {
    for (const neighbor of graph[node]) {
      inDegree[neighbor] = (inDegree[neighbor] || 0) + 1;
    }
  }

  // Enqueue nodes with in-degree 0
  for (const node in inDegree) {
    if (inDegree[node] === 0) {
      queue.push(parseInt(node));
    }
  }

  while (queue.length > 0) {
    const current = queue.shift();
    topoOrder.push(current);
    for (const neighbor of graph[current]) {
      inDegree[neighbor]--;
      if (inDegree[neighbor] === 0) {
        queue.push(neighbor);
      }
    }
  }

  if (topoOrder.length === Object.keys(graph).length) {
    return topoOrder;
  } else {
    throw new Error('Graph has a cycle, topological sorting is not possible.');
  }
}

// Example usage
const graph2 = {
  5: [0],
  4: [0, 1],
  3: [1],
  2: [3],
  1: [],
  0: [],
};
console.log(topologicalSortKahn(graph2)); // Output: [4, 5, 2, 3, 1, 0]
```

---

## Complexity Analysis

- **Time Complexity: O(V+E)**, where V is the number of vertices and E is the number of edges.
- **Space Complexity: O(V)** for storing the stack (DFS) or queue (BFS) and the visited nodes or in-degree map.

---

## Use Cases of Topological Sorting

1. **Task Scheduling:** Determining the order of tasks given dependencies.
2. **Course Scheduling:** Determining the order of courses to complete given prerequisites.
3. **Build Systems:** Determining the order of file compilation.
4. **Dependency Resolution:** Determining dependencies in complex systems.

## Notes

- Topological sorting is only possible for Directed Acyclic Graphs (DAGs).
- If a cycle is detected, topological sorting is not possible.

## Resources

- [Video 1](https://www.youtube.com/watch?v=5lZ0iJMrUMk&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=21&pp=iAQB)
- [Article](https://takeuforward.org/data-structure/topological-sort-algorithm-dfs-g-21/)
- [Video 2 Kahn's Algorithm](https://www.youtube.com/watch?v=73sneFXuTEg&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=22&ab_channel=takeUforward)
- [Article of Khan's Algorithm](https://takeuforward.org/data-structure/kahns-algorithm-topological-sort-algorithm-bfs-g-22/)
