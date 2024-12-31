# 01 Matrix

## Problem Description

Given an `m x n` binary matrix `mat`, return the distance of the nearest `0` for each cell.

The distance between two adjacent cells is `1`.

### Example

#### Input:

```plaintext
mat = [
  [0, 0, 0],
  [0, 1, 0],
  [1, 1, 1]
]
```

#### Output:

```plaintext
[
  [0, 0, 0],
  [0, 1, 0],
  [1, 2, 1]
]
```

---

## Approach: Breadth-First Search (BFS)

### Key Idea

1. Use a multi-source BFS approach.
2. Start with all cells containing `0` in the queue.
3. Process the queue, updating the distances for neighboring `1` cells.
4. Ensure no cell is visited more than once.

---

### Code Implementation

```javascript
function updateMatrix(mat) {
  const m = mat.length;
  const n = mat[0].length;
  const directions = [
    [0, 1],
    [1, 0],
    [0, -1],
    [-1, 0], // Right, Down, Left, Up
  ];

  const queue = [];
  const dist = Array.from({ length: m }, () => Array(n).fill(Infinity));

  // Initialize the queue with all '0' cells and set their distance to 0
  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (mat[i][j] === 0) {
        queue.push([i, j]);
        dist[i][j] = 0;
      }
    }
  }

  // Perform BFS
  while (queue.length > 0) {
    const [x, y] = queue.shift();

    for (const [dx, dy] of directions) {
      const newX = x + dx;
      const newY = y + dy;

      // Check if the new cell is within bounds and can be updated
      if (
        newX >= 0 &&
        newX < m &&
        newY >= 0 &&
        newY < n &&
        dist[newX][newY] > dist[x][y] + 1
      ) {
        dist[newX][newY] = dist[x][y] + 1;
        queue.push([newX, newY]);
      }
    }
  }

  return dist;
}

// Example Usage
const mat = [
  [0, 0, 0],
  [0, 1, 0],
  [1, 1, 1],
];

console.log(updateMatrix(mat));
```

---

### Complexity Analysis

- **Time Complexity**: O(m × n)
  - Each cell is processed at most once.
- **Space Complexity**: O(m × n)
  - Space used by the `dist` array and the BFS queue.

---

## Explanation with Example

1. **Initialization**:
   - Start with all `0` cells in the queue with distance `0`.
   - Mark all other cells with `Infinity` in the `dist` array.
2. **BFS Process**:
   - Dequeue a cell, and for each of its neighbors:
     - If the neighbor's current distance is greater than the dequeued cell's distance + 1, update it.
     - Add the neighbor to the queue.
3. **Result**:
   - The `dist` array contains the shortest distance for each cell to the nearest `0`.

---

### Resources

- [LeetCode Problem - 01 Matrix](https://leetcode.com/problems/01-matrix/)
