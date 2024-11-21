# Vertical Order Traversal of Binary Tree

## Problem Statement

Given the root of a binary tree, return the vertical order traversal of its nodes' values. Nodes should be sorted by their vertical distance from the root, with ties broken by level order and then by value.

---

## Approach: BFS with HashMap and Sorting

### Steps:

1. Use a `Map` to store nodes at each vertical distance. The keys of the map represent the vertical distance, and the values are lists of nodes at that distance.
2. Perform a level-order traversal (BFS) while keeping track of:
   - The vertical distance (`col`).
   - The level of each node.
3. Add nodes to the map based on their vertical distance and level.
4. After traversal, sort the map keys (vertical distances) and for each vertical level, sort the nodes first by level and then by value.
5. Return the final sorted result.

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

function verticalTraversal(root) {
  if (!root) return [];

  // Map to store nodes by column and level
  const columnTable = new Map();
  const queue = [[root, 0, 0]]; // [node, column, level]

  while (queue.length > 0) {
    const [node, col, level] = queue.shift();

    if (!columnTable.has(col)) {
      columnTable.set(col, []);
    }
    columnTable.get(col).push([level, node.val]);

    if (node.left) queue.push([node.left, col - 1, level + 1]);
    if (node.right) queue.push([node.right, col + 1, level + 1]);
  }

  // Sort the map keys (columns) and sort nodes by level and value
  const sortedColumns = [...columnTable.keys()].sort((a, b) => a - b);
  const result = [];

  for (const col of sortedColumns) {
    const columnNodes = columnTable.get(col);
    columnNodes.sort((a, b) => {
      if (a[0] !== b[0]) return a[0] - b[0]; // Sort by level
      return a[1] - b[1]; // Sort by value
    });
    result.push(columnNodes.map(([_, val]) => val));
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
root.left.right = new TreeNode(6);
root.right.left = new TreeNode(5);
root.right.right = new TreeNode(7);

console.log(verticalTraversal(root));
// Output: [[4], [2], [1, 5, 6], [3], [7]]
```

---

## Example Input and Output

### Input:

```
        1
       / \
      2   3
     / \ / \
    4  6 5  7
```

### Output:

```
[[4], [2], [1, 5, 6], [3], [7]]
```

---

## Summary

| Approach                | Time Complexity | Space Complexity | Notes                                                                 |
| ----------------------- | --------------- | ---------------- | --------------------------------------------------------------------- |
| BFS with HashMap & Sort | O(n log n)      | O(n)             | Handles vertical levels and resolves ties with level order and value. |

## Resources

[Video Link](https://www.youtube.com/watch?v=q_a6lpbKJdw&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=22&ab_channel=takeUforward)
