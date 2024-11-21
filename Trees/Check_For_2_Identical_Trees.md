# Check if Two Trees are Identical

## Problem Statement

Given the roots of two binary trees, determine if the two trees are identical. Two binary trees are considered identical if they have the same structure and their nodes have the same values.

---

## Approach: Recursive Comparison

### Steps:

1. If both trees are `null`, they are identical.
2. If only one of the trees is `null`, they are not identical.
3. Check the current nodes' values. If they differ, the trees are not identical.
4. Recursively check the left and right subtrees of both trees.

### Code:

```javascript
class TreeNode {
  constructor(val = 0, left = null, right = null) {
    this.val = val;
    this.left = left;
    this.right = right;
  }
}

function isIdentical(tree1, tree2) {
  // Base cases
  if (tree1 === null && tree2 === null) return true;
  if (tree1 === null || tree2 === null) return false;

  // Check current nodes and their subtrees
  return (
    tree1.val === tree2.val &&
    isIdentical(tree1.left, tree2.left) &&
    isIdentical(tree1.right, tree2.right)
  );
}
```

---

## Example Usage:

```javascript
// Tree 1
let tree1 = new TreeNode(1);
tree1.left = new TreeNode(2);
tree1.right = new TreeNode(3);

// Tree 2
let tree2 = new TreeNode(1);
tree2.left = new TreeNode(2);
tree2.right = new TreeNode(3);

console.log(isIdentical(tree1, tree2)); // Output: true

// Modify tree2 to make it different
tree2.right.val = 4;
console.log(isIdentical(tree1, tree2)); // Output: false
```

---

## Example Input and Output

### Input (Identical Trees):

**Tree 1:**

```
    1
   / \
  2   3
```

**Tree 2**

```
    1
   / \
  2   3
```

### Output

```
true
```

### Input (Non-Identical Trees):

**Tree 1:**

```text
    1
   / \
  2   3
```

**Tree 2**

```
    1
   / \
  2   4
```

### Output

```
false
```

---

## Summary

| Approach             | Time Complexity | Space Complexity | Notes                                                                   |
| -------------------- | --------------- | ---------------- | ----------------------------------------------------------------------- |
| Recursive Comparison | O(n)            | O(h)             | Compares nodes and subtrees recursively. `h` is the height of the tree. |

## Resources

[Video Link](https://www.youtube.com/watch?v=BhuvF_-PWS0&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=20&ab_channel=takeUforward)
