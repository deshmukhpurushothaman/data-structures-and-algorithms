# Diameter of Binary Tree

## Problem Statement

The **diameter** of a binary tree is the length of the longest path between any two nodes in the tree. The path may or may not pass through the root.

---

## Approach 1: Recursive Solution

We calculate the height of each subtree and determine the diameter using the sum of the heights of the left and right subtrees at each node.

### Code

```javascript
function diameterOfBinaryTree(root) {
  let diameter = 0;

  function dfs(node) {
    if (node === null) return 0; // Base case: height of null node is 0

    let leftHeight = dfs(node.left);
    let rightHeight = dfs(node.right);

    // Update diameter at each node
    diameter = Math.max(diameter, leftHeight + rightHeight);

    // Return height of the current node
    return Math.max(leftHeight, rightHeight) + 1;
  }

  dfs(root);
  return diameter;
}
```

---

## Summary

| Approach      | Time Complexity | Space Complexity | Notes                                    |
| ------------- | --------------- | ---------------- | ---------------------------------------- |
| Recursive DFS | \( O(n) \)      | \( O(h) \)       | Computes height and diameter in one pass |

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

### Output:

```text
Diameter: 3
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

console.log(diameterOfBinaryTree(tree)); // Output: 3
```

## Resources

[Video Link](https://www.youtube.com/watch?v=Rezetez59Nk&ab_channel=takeUforward)
