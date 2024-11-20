# Flood Fill Algorithm

## Introduction

The **Flood Fill algorithm** is used to determine and change the connected region in a multi-dimensional array (e.g., an image or a grid), starting from a specific node (pixel or cell) and replacing its color or value. It works similarly to the "paint bucket" tool in image editing software, filling contiguous regions with a new color/value.

---

## Problem Statement

Given a 2D grid (matrix) representing an image, and a starting pixel `(sr, sc)`, change the color of all connected cells with the same original color as the starting pixel to a new specified color.

---

## Approach: Depth-First Search (DFS)

### Pseudocode

1. If the starting pixel already has the new color, no change is needed.
2. Recursively traverse all 4-connected neighboring pixels (up, down, left, right).
3. Change the color if it matches the starting pixel's color.

### Code in JavaScript

```javascript
function floodFill(image, sr, sc, newColor) {
  const originalColor = image[sr][sc];
  if (originalColor === newColor) return image; // No change needed if color is same

  function dfs(x, y) {
    // Boundary and validity checks
    if (
      x < 0 ||
      x >= image.length ||
      y < 0 ||
      y >= image[0].length ||
      image[x][y] !== originalColor
    ) {
      return;
    }

    // Change color
    image[x][y] = newColor;

    // Recursively apply dfs in 4 directions
    dfs(x + 1, y); // Down
    dfs(x - 1, y); // Up
    dfs(x, y + 1); // Right
    dfs(x, y - 1); // Left
  }

  dfs(sr, sc); // Start the flood fill
  return image;
}

// Example usage
const image = [
  [1, 1, 1],
  [1, 1, 0],
  [1, 0, 1],
];
const sr = 1,
  sc = 1,
  newColor = 2;
console.log(floodFill(image, sr, sc, newColor));
// Output: [
//   [2, 2, 2],
//   [2, 2, 0],
//   [2, 0, 1]
// ]
```

### Complexity

- **Time Complexity:** \(O(N)\), where \(N\) is the number of pixels in the image. Each pixel is visited once.
- **Space Complexity:** \(O(N)\) due to the recursive stack (in the worst case).

---

## Approach: Breadth-First Search (BFS)

Description
Instead of using recursion (DFS), we can use a queue to iteratively explore all connected cells using BFS.

```javascript
function floodFillBFS(image, sr, sc, newColor) {
  const originalColor = image[sr][sc];
  if (originalColor === newColor) return image;

  const directions = [
    [1, 0], // Down
    [-1, 0], // Up
    [0, 1], // Right
    [0, -1], // Left
  ];
  const queue = [[sr, sc]];

  while (queue.length > 0) {
    const [x, y] = queue.shift();

    // Change color
    image[x][y] = newColor;

    // Explore neighbors
    for (const [dx, dy] of directions) {
      const newX = x + dx;
      const newY = y + dy;
      if (
        newX >= 0 &&
        newX < image.length &&
        newY >= 0 &&
        newY < image[0].length &&
        image[newX][newY] === originalColor
      ) {
        queue.push([newX, newY]);
      }
    }
  }

  return image;
}

// Example usage
const imageBFS = [
  [1, 1, 1],
  [1, 1, 0],
  [1, 0, 1],
];
console.log(floodFillBFS(imageBFS, sr, sc, newColor));
// Output: [
//   [2, 2, 2],
//   [2, 2, 0],
//   [2, 0, 1]
// ]
```

### Complexity

- **Time Complexity:** \(O(N)\), where \(N\) is the number of pixels.
- **Space Complexity:** \(O(N)\) due to the queue storage (in the worst case).

---

## Summary

- DFS Approach is often more memory-intensive due to recursive calls.
- BFS Approach uses a queue and may have better stack behavior, especially for large grids.
- The choice of approach depends on memory and stack size considerations, as well as problem constraints.

## Resources

[Video link](https://www.youtube.com/watch?v=C-2_uSRli8o&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=10&ab_channel=takeUforward)
