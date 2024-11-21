# Lowest Common Ancestor in Binary Tree

## Problem Statement

Given the root of a binary tree and two nodes `p` and `q`, find the lowest common ancestor (LCA) of the two nodes. The LCA of two nodes is defined as the lowest node in the tree that has both `p` and `q` as descendants.

---

## Approach: Recursive Traversal

### Steps:

1. If the current node is `null`, return `null`.
2. If the current node matches either `p` or `q`, return the current node.
3. Recursively find the LCA in the left and right subtrees.
4. If both left and right recursive calls return non-null values, the current node is the LCA.
5. If only one of the recursive calls returns a non-null value, propagate that value upwards.

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

function lowestCommonAncestor(root, p, q) {
  if (root === null || root === p || root === q) {
    return root;
  }

  const left = lowestCommonAncestor(root.left, p, q);
  const right = lowestCommonAncestor(root.right, p, q);

  if (left !== null && right !== null) {
    return root; // This is the LCA
  }

  return left !== null ? left : right; // Return the non-null subtree
}
```

---

## Example Usage:

```javascript
// Construct a binary tree
let root = new TreeNode(3);
root.left = new TreeNode(5);
root.right = new TreeNode(1);
root.left.left = new TreeNode(6);
root.left.right = new TreeNode(2);
root.right.left = new TreeNode(0);
root.right.right = new TreeNode(8);
root.left.right.left = new TreeNode(7);
root.left.right.right = new TreeNode(4);

let p = root.left; // Node with value 5
let q = root.left.right.right; // Node with value 4

console.log(lowestCommonAncestor(root, p, q).val); // Output: 5
```

---

## Example Input and Output

### Input:

```
        3
       / \
      5   1
     / \ / \
    6  2 0  8
      / \
     7   4
```

Nodes p = 5 and q = 4

### Output:

```text
5
```

---

## Summary

| Approach            | Time Complexity | Space Complexity | Notes                                                   |
| ------------------- | --------------- | ---------------- | ------------------------------------------------------- |
| Recursive Traversal | O(n)            | O(h)             | Traverses the tree once. `h` is the height of the tree. |

## Resources

[Video Link](https://www.youtube.com/watch?v=_-QHfMDde90&list=PLgUwDviBIf0q8Hkd7bK2Bpryj2xVJk8Vk&index=28&ab_channel=takeUforward)
