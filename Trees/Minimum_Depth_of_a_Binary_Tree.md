# Minimum Depth of a Binary Tree

## Problem Description

The **minimum depth** of a binary tree is the number of nodes along the shortest path from the root node down to the nearest leaf node.

### Example

#### Input:

```
    3
   / \
  9   20
      /  \
     15   7
```

#### Output:

```plaintext
2
```

#### Explanation:

The minimum depth is the path `[3, 20]`.

---

## Approach 1: Recursive Depth-First Search (DFS)

### Key Idea

1. Use recursion to traverse the tree.
2. For each node:

   - If it’s a leaf node, return `1`.
   - Recursively calculate the minimum depth of the left and right subtrees.
   - Return the minimum of the two depths plus `1`.

3. Handle the edge case where only one child is `null` by ensuring we don’t take a depth of `0` for a valid subtree.

---

### Code Implementation

```javascript
function minDepth(root) {
  if (!root) return 0; // Base case: if tree is empty

  // If one of the subtrees is null, return depth of the other subtree
  if (!root.left) return 1 + minDepth(root.right);
  if (!root.right) return 1 + minDepth(root.left);

  // Return the minimum depth of the two subtrees
  return 1 + Math.min(minDepth(root.left), minDepth(root.right));
}

// Example Usage
class TreeNode {
  constructor(val = 0, left = null, right = null) {
    this.val = val;
    this.left = left;
    this.right = right;
  }
}

const root = new TreeNode(3);
root.left = new TreeNode(9);
root.right = new TreeNode(20, new TreeNode(15), new TreeNode(7));

console.log(`Minimum Depth: ${minDepth(root)}`);
```

---

### Complexity Analysis

- **Time Complexity**: O(n)
  - Every node is visited once.
- **Space Complexity**: O(h)
  - Recursive stack space depends on the height of the tree (`h`).

---

## Approach 2: Breadth-First Search (BFS)

### Key Idea

1. Use a queue to perform level-order traversal.
2. Track the depth as you move through each level.
3. As soon as you encounter a leaf node, return the current depth.

---

### Code Implementation

```javascript
function minDepth(root) {
  if (!root) return 0; // Base case: if tree is empty

  const queue = [{ node: root, depth: 1 }];

  while (queue.length > 0) {
    const { node, depth } = queue.shift();

    // If we encounter a leaf node, return its depth
    if (!node.left && !node.right) return depth;

    // Add left and right children to the queue if they exist
    if (node.left) queue.push({ node: node.left, depth: depth + 1 });
    if (node.right) queue.push({ node: node.right, depth: depth + 1 });
  }
}

// Example Usage
class TreeNode {
  constructor(val = 0, left = null, right = null) {
    this.val = val;
    this.left = left;
    this.right = right;
  }
}

const root = new TreeNode(3);
root.left = new TreeNode(9);
root.right = new TreeNode(20, new TreeNode(15), new TreeNode(7));

console.log(`Minimum Depth: ${minDepth(root)}`);
```

---

### Complexity Analysis

- **Time Complexity**: O(n)
  - Each node is processed once.
- **Space Complexity**: O(n)
  - Queue size can grow up to the number of nodes at the deepest level.

---

## Comparison of Approaches

| Approach | Time Complexity | Space Complexity | Notes                      |
| -------- | --------------- | ---------------- | -------------------------- |
| DFS      | O(n)            | O(h)             | Simple, but deeper stacks. |
| BFS      | O(n)            | O(n)             | Finds the depth faster.    |

---

### Resources

- [Minimum Depth of Binary Tree | Leetcode](https://leetcode.com/problems/minimum-depth-of-binary-tree/)
- [DFS vs BFS for Tree Traversals](https://www.geeksforgeeks.org/bfs-vs-dfs-binary-tree/)
