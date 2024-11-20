# Maximum Width of Binary Tree

## Problem Statement

The **maximum width** of a binary tree is defined as the maximum number of nodes present at any level of the tree. The width of a level is the number of nodes between the leftmost and rightmost non-null nodes in the level, including any `null` nodes in between.

---

## Approach: Level Order Traversal with Indexing

We perform a **Breadth-First Search (BFS)** using a queue. For each node, we calculate its position (index) in a virtual binary tree. Using the indices, we compute the width of each level as the difference between the rightmost and leftmost indices plus one.

### Code

```javascript
function widthOfBinaryTree(root) {
  if (root === null) return 0;

  let maxWidth = 0;
  let queue = [[root, 0]]; // Each element is [node, index]

  while (queue.length > 0) {
    let levelSize = queue.length;
    let minIndex = queue[0][1]; // Index of the leftmost node in this level
    let firstIndex, lastIndex;

    for (let i = 0; i < levelSize; i++) {
      let [node, index] = queue.shift();
      // Normalize index to prevent overflow
      index -= minIndex;

      if (i === 0) firstIndex = index; // First index at this level
      if (i === levelSize - 1) lastIndex = index; // Last index at this level

      // Add children to the queue with their respective indices
      if (node.left) queue.push([node.left, 2 * index + 1]);
      if (node.right) queue.push([node.right, 2 * index + 2]);
    }

    // Calculate the width of the current level
    maxWidth = Math.max(maxWidth, lastIndex - firstIndex + 1);
  }

  return maxWidth;
}
```

## Summary

| Approach          | Time Complexity | Space Complexity | Notes                                     |
| ----------------- | --------------- | ---------------- | ----------------------------------------- |
| BFS with Indexing | \( O(n) \)      | \( O(w) \)       | \( w \) is the maximum width of the tree. |

---

## Example Input and Output

### Input:

```text
       1
      / \
     2   3
    /     \
   4       5
```

### Output:

```
Maximum Width: 4
```

```
// Example Usage:
const tree = {
    value: 1,
    left: {
        value: 2,
        left: { value: 4, left: null, right: null },
        right: null,
    },
    right: {
        value: 3,
        left: null,
        right: { value: 5, left: null, right: null },
    },
};

console.log(widthOfBinaryTree(tree)); // Output: 4
```

## Resources

[Video Link](https://www.youtube.com/watch?v=ZbybYvcVLks&ab_channel=takeUforward)
