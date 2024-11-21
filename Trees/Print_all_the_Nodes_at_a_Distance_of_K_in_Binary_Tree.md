# Print all the Nodes at a Distance of K in Binary Tree

## Problem Statement

Given the root of a binary tree and a target node, print all nodes that are at a distance `K` from the target node. The distance between two nodes is the number of edges in the path connecting them.

---

## Approach: BFS or DFS with Backtracking

### Steps:

1. **Find the Target Node**: Perform a DFS to find the target node. During this traversal, maintain a parent map to keep track of each node's parent.
2. **BFS from the Target Node**: Once the target node is found, perform a BFS or DFS from the target node while keeping track of the nodes' distance from the target.
3. **Track Distance**: Track the distance from the target node and print the node values when the distance equals `K`.

---

### Code:

```javascript
class TreeNode {
  constructor(val = 0, left = null, right = null) {
    this.val = val;
    this.left = left;
    this.right = right;
  }
}

function printNodesAtDistanceK(root, target, K) {
  if (!root) return [];

  const parentMap = new Map();
  const result = [];

  // Helper function to populate the parent map
  function dfs(node, parent) {
    if (!node) return;
    parentMap.set(node, parent);
    dfs(node.left, node);
    dfs(node.right, node);
  }

  // Perform DFS to populate parent map
  dfs(root, null);

  // BFS to find all nodes at distance K
  const queue = [[target, 0]]; // [node, current distance]
  const visited = new Set();
  visited.add(target);

  while (queue.length > 0) {
    const [node, dist] = queue.shift();

    if (dist === K) {
      result.push(node.val);
    }

    if (node.left && !visited.has(node.left)) {
      visited.add(node.left);
      queue.push([node.left, dist + 1]);
    }
    if (node.right && !visited.has(node.right)) {
      visited.add(node.right);
      queue.push([node.right, dist + 1]);
    }
    const parent = parentMap.get(node);
    if (parent && !visited.has(parent)) {
      visited.add(parent);
      queue.push([parent, dist + 1]);
    }
  }

  return result;
}
```

---

## Example Usage:

```javascript
// Construct a binary tree
let root = new TreeNode(1);
root.left = new TreeNode(2);
root.right = new TreeNode(3);
root.left.left = new TreeNode(4);
root.left.right = new TreeNode(5);
root.right.left = new TreeNode(6);
root.right.right = new TreeNode(7);

// Target node is 2
let target = root.left; // Node with value 2

console.log(printNodesAtDistanceK(root, target, 2));
// Output: [4, 5, 6]
```

---

## Example Input and Output

### Input:

```
        1
       / \
      2   3
     / \ / \
    4  5 6  7
```

Target node `p = 2`, Distance `K = 2`

### Output:

```text
[4, 5, 6]
```

---

## Summary

| Approach                   | Time Complexity | Space Complexity | Notes                                                           |
| -------------------------- | --------------- | ---------------- | --------------------------------------------------------------- |
| BFS or DFS with Parent Map | O(n)            | O(n)             | Traverses the tree once and uses a parent map for backtracking. |

## Resources

[Video Link](https://www.youtube.com/watch?v=i9ORlEy6EsI&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=31&ab_channel=takeUforward)
