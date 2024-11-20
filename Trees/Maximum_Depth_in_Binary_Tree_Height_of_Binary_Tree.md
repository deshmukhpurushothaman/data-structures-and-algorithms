# Maximum Depth of a Binary Tree / Height of Binary Tree

## Problem Statement

The **maximum depth** (or height) of a binary tree is the number of nodes along the longest path from the root node down to the farthest leaf node.

---

## Approach 1: Recursive Solution (Depth-First Search)

We use recursion to calculate the height of the left and right subtrees for each node, then return the maximum of the two heights plus one (for the current node).

### Code

```javascript
function maxDepth(root) {
  if (root === null) return 0; // Base case: Empty tree has height 0

  let leftHeight = maxDepth(root.left);
  let rightHeight = maxDepth(root.right);

  return Math.max(leftHeight, rightHeight) + 1;
}
```

### Complexity

- Time Complexity: `O(n)`

  - Each node is visited once.

- Space Complexity: `O(h)`
  - Where h is the height of the tree (due to the recursive call stack)

---

## Approach 2: Iterative Solution (Level-Order Traversal)

We perform a Breadth-First Search (BFS) using a queue. For each level of the tree, we increment the depth count.

### Code

```javascript
function maxDepth(root) {
  if (root === null) return 0; // Empty tree has height 0

  let queue = [root];
  let depth = 0;

  while (queue.length > 0) {
    let levelSize = queue.length; // Number of nodes at the current level
    depth++;

    for (let i = 0; i < levelSize; i++) {
      let node = queue.shift();

      // Add child nodes to the queue
      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }
  }

  return depth;
}
```

### Complexity

- **Time Complexity:** `O(n)`

  - Each node is visited once.

- **Space Complexity:** `O(w)`
  - Where w is the maximum width of the tree (the number of nodes at the widest level).

---

## Summary

| Approach      | Time Complexity | Space Complexity | Notes                           |
| ------------- | --------------- | ---------------- | ------------------------------- |
| Recursive DFS | \( O(n) \)      | \( O(h) \)       | Simple and elegant              |
| Iterative BFS | \( O(n) \)      | \( O(w) \)       | Uses a queue for level tracking |

---

## Example Input and Output

### Input:

```text
       1
      / \
     2   3
    / \
   4   5
```

## Output:

```text
Maximum Depth: 3
```

```
// Example Usage:
const tree = {
    value: 1,
    left: {
        value: 2,
        left: { value: 4, left: null, right: null },
        right: { value: 5, left: null, right: null },
    },
    right: { value: 3, left: null, right: null },
};

console.log(maxDepth(tree)); // Output: 3
```

## Resources

[Video Link](https://www.youtube.com/watch?v=eD3tmO66aBA&t=269s&ab_channel=takeUforward)
