# Check for Balanced Binary Tree

## Problem Statement

A binary tree is considered balanced if the height difference between the left and right subtrees of every node is at most 1. Write a program to determine if a binary tree is balanced.

---

## Approach 1: Recursive Height Calculation

### Steps:

1. For each node, calculate the height of the left and right subtrees.
2. Check if the absolute difference between the heights of the left and right subtrees is greater than 1. If yes, return false.
3. Recursively perform the above steps for all nodes.

### Code:

```javascript
class TreeNode {
  constructor(val = 0, left = null, right = null) {
    this.val = val;
    this.left = left;
    this.right = right;
  }
}

function isBalanced(root) {
  function height(node) {
    if (node === null) return 0;

    const leftHeight = height(node.left);
    const rightHeight = height(node.right);

    // If any subtree is unbalanced, return -1
    if (
      leftHeight === -1 ||
      rightHeight === -1 ||
      Math.abs(leftHeight - rightHeight) > 1
    ) {
      return -1;
    }

    return Math.max(leftHeight, rightHeight) + 1;
  }

  return height(root) !== -1;
}
```

---

## Example Usage:

```javascript
// Construct a balanced binary tree
let root = new TreeNode(1);
root.left = new TreeNode(2);
root.right = new TreeNode(3);
root.left.left = new TreeNode(4);
root.left.right = new TreeNode(5);
root.right.right = new TreeNode(6);

console.log(isBalanced(root)); // Output: true

// Construct an unbalanced binary tree
let unbalancedRoot = new TreeNode(1);
unbalancedRoot.left = new TreeNode(2);
unbalancedRoot.left.left = new TreeNode(3);

console.log(isBalanced(unbalancedRoot)); // Output: false
```

---

## Example Input and Output

### Input (Balanced Tree):

```text
    1
   / \
  2   3
 / \
4   5
```

### Output

```
true
```

### Input (Unbalanced Tree):

```text
    1
   /
  2
 /
3
```

### Output

```
false
```

---

## Summary

| Approach                     | Time Complexity | Space Complexity | Notes                                                                       |
| ---------------------------- | --------------- | ---------------- | --------------------------------------------------------------------------- |
| Recursive Height Calculation | O(n)            | O(h)             | Efficiently checks balance and height in a single pass. `h` is tree height. |

---

## Resources

[Video Link](https://www.youtube.com/watch?v=Yt50Jfbd8Po&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=16&ab_channel=takeUforward)
