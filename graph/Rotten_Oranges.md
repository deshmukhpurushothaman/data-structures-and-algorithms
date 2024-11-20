# Rotten Oranges Problem

## Problem Statement

Given a grid of dimensions `m x n` where each cell can have one of the following values:

- `0`: representing an empty cell.
- `1`: representing a fresh orange.
- `2`: representing a rotten orange.

Every minute, any fresh orange that is **4-directionally adjacent** (up, down, left, right) to a rotten orange becomes rotten.

### Objective

Determine the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return `-1`.

---

## Approach: Breadth-First Search (BFS)

### Explanation

The problem can be solved using a BFS approach where we treat each rotten orange as a source node and perform multi-source BFS traversal.

### Steps

1. Initialize a queue to store the coordinates of all initially rotten oranges.
2. Use a `directions` array to simplify the traversal in four directions (up, down, left, right).
3. Count the number of fresh oranges.
4. Process the queue using BFS. At each step, rot the adjacent fresh oranges and decrement the fresh count.
5. Continue the process until no more oranges can be rotted. If any fresh oranges remain, return `-1`.

### Code in JavaScript

```javascript
function orangesRotting(grid) {
  const rows = grid.length;
  const cols = grid[0].length;
  let freshCount = 0;
  const queue = [];

  // Step 1: Initialize the queue with all initially rotten oranges and count fresh ones
  for (let r = 0; r < rows; r++) {
    for (let c = 0; c < cols; c++) {
      if (grid[r][c] === 2) {
        queue.push([r, c]);
      } else if (grid[r][c] === 1) {
        freshCount++;
      }
    }
  }

  // Edge case: No fresh oranges to begin with
  if (freshCount === 0) return 0;

  const directions = [
    [1, 0], // Down
    [-1, 0], // Up
    [0, 1], // Right
    [0, -1], // Left
  ];
  let minutes = 0;

  // Step 2: BFS traversal
  while (queue.length > 0) {
    const size = queue.length;
    let madeProgress = false;

    for (let i = 0; i < size; i++) {
      const [x, y] = queue.shift();

      // Check all 4 directions
      for (const [dx, dy] of directions) {
        const newX = x + dx;
        const newY = y + dy;

        if (
          newX >= 0 &&
          newX < rows &&
          newY >= 0 &&
          newY < cols &&
          grid[newX][newY] === 1
        ) {
          // Rotten the fresh orange
          grid[newX][newY] = 2;
          freshCount--;
          queue.push([newX, newY]);
          madeProgress = true;
        }
      }
    }

    // If we made progress in this minute, increment time
    if (madeProgress) minutes++;
  }

  // Step 3: Check if any fresh oranges remain
  return freshCount === 0 ? minutes : -1;
}

// Example usage
const grid = [
  [2, 1, 1],
  [1, 1, 0],
  [0, 1, 1],
];
console.log(orangesRotting(grid)); // Output: 4
```

## Complexity

- **Time Complexity:** \(O(m \* n)\) where m is the number of rows and n is the number of columns. Every cell is processed at most once.
- **Space Complexity:** \(O(m \* n)\) for the queue, in the worst case.

---

## Summary

- The BFS approach simulates the rotting process minute by minute.
- It handles multi-source propagation (all initially rotten oranges) simultaneously, ensuring efficient traversal.
- If any fresh oranges remain at the end, we return `-1` as it is impossible to rot all oranges.

## Resources

[Video Link](https://www.youtube.com/watch?v=yf3oUhkvqA0&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=10&ab_channel=takeUforward)
