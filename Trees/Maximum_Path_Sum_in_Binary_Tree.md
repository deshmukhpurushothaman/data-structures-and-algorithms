# Maximum Path Sum in Binary Tree

## Problem Statement

Given a binary tree, find the maximum path sum. A path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node.

---

## Approach: Recursive Traversal with Global Maximum

### Steps:

1. Use a recursive function to calculate the maximum path sum for each node's left and right subtrees.
2. For each node, the maximum path sum passing through it can be:
   - Only the node value.
   - Node value + maximum sum from the left subtree.
   - Node value + maximum sum from the right subtree.
   - Node value + maximum sums from both left and right subtrees.
3. Update the global maximum at each step with the best value obtained.
4. Return the maximum path sum for the tree.

### Code:

```javascript
class TreeNode {
  constructor(val = 0, left = null, right = null) {
    this.val = val;
    this.left = left;
    this.right = right;
  }
}

function maxPathSum(root) {
  let globalMax = -Infinity;

  function helper(node) {
    if (node === null) return 0;

    // Recursively find the maximum path sums of left and right subtrees
    const leftMax = Math.max(helper(node.left), 0);
    const rightMax = Math.max(helper(node.right), 0);

    // Calculate the maximum path sum passing through the current node
    const localMax = node.val + leftMax + rightMax;

    // Update the global maximum
    globalMax = Math.max(globalMax, localMax);

    // Return the maximum sum for the current node excluding one branch
    return node.val + Math.max(leftMax, rightMax);
  }

  helper(root);
  return globalMax;
}
```

---

## Example Usage:

```javascript
// Construct a binary tree
let root = new TreeNode(-10);
root.left = new TreeNode(9);
root.right = new TreeNode(20);
root.right.left = new TreeNode(15);
root.right.right = new TreeNode(7);

console.log(maxPathSum(root)); // Output: 42
```

---

## Example Input and Output

### Input:

```text
      -10
      /  \
     9    20
         /  \
        15   7
```

### Output:

```text
42
```

---

## Summary

| Approach                            | Time Complexity | Space Complexity | Notes                                                                      |
| ----------------------------------- | --------------- | ---------------- | -------------------------------------------------------------------------- |
| Recursive Traversal with Global Max | O(n)            | O(h)             | Calculates the maximum path sum in a single traversal. `h` is tree height. |

## Resources

[Video Link](https://www.youtube.com/watch?v=WszrfSwMz58&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=18&ab_channel=takeUforward)
