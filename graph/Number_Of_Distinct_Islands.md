# Number of Distinct Islands

## Problem Statement

Given a 2D grid of `0`s and `1`s where `1` represents land and `0` represents water, find the number of distinct islands. An island is a group of `1`s that are 4-connected (up, down, left, right).

- Two islands are considered distinct if they have different shapes, or they are positioned differently on the grid.

---

## Approach

### Explanation

To detect distinct islands:

1. **Flood Fill with DFS**: We will use DFS to explore all the cells connected to a starting cell that is part of an island.
2. **Island Shape**: We will track the relative positions of the cells in the island starting from a reference point. This allows us to uniquely identify each island.
3. **Normalize Shape**: The key idea is to normalize the shape of the island using the relative positions of the cells (compared to the starting cell). We store each island's shape as a unique representation.
4. **Distinctness**: We maintain a set of visited cells to ensure each land cell is counted only once and that the same shape of island is counted once.

### Steps

1. Traverse through the grid, and whenever we find a `1` (part of an island), we start a DFS to explore the entire island.
2. During the DFS, record the relative positions of each cell in the island, starting from a fixed point (e.g., the top-leftmost cell of the island).
3. Convert the recorded relative positions into a unique shape representation.
4. Use a set to store unique island shapes.

---

### Code in JavaScript

```javascript
function numDistinctIslands(grid) {
  const rows = grid.length;
  const cols = grid[0].length;
  const visited = new Set(); // To track visited cells
  const shapes = new Set(); // To store unique island shapes

  // Directions: Up, Down, Left, Right
  const directions = [
    [-1, 0], // Up
    [1, 0], // Down
    [0, -1], // Left
    [0, 1], // Right
  ];

  // Helper function to perform DFS and capture the island shape
  function dfs(x, y, shape, originX, originY) {
    // Mark the current cell as visited
    visited.add(`${x},${y}`);
    // Record the relative position of the current cell
    shape.push([x - originX, y - originY]);

    // Explore all four directions
    for (const [dx, dy] of directions) {
      const newX = x + dx;
      const newY = y + dy;

      // Ensure the cell is within bounds and not visited
      if (
        newX >= 0 &&
        newX < rows &&
        newY >= 0 &&
        newY < cols &&
        grid[newX][newY] === 1 &&
        !visited.has(`${newX},${newY}`)
      ) {
        dfs(newX, newY, shape, originX, originY);
      }
    }
  }

  // Traverse the grid
  for (let i = 0; i < rows; i++) {
    for (let j = 0; j < cols; j++) {
      if (grid[i][j] === 1 && !visited.has(`${i},${j}`)) {
        // Initialize the shape for a new island
        const shape = [];
        // Start DFS from this cell
        dfs(i, j, shape, i, j);
        // Convert the shape to a string and add to the set of unique shapes
        shapes.add(JSON.stringify(shape));
      }
    }
  }

  return shapes.size; // Return the number of distinct islands
}

// Example usage
const grid = [
  [1, 1, 0, 0, 0],
  [1, 0, 0, 1, 1],
  [0, 0, 0, 1, 0],
  [0, 0, 1, 1, 0],
];

console.log(numDistinctIslands(grid)); // Output: 2
```

---

## Complexity

- **Time Complexity:** \(O(m \times n)\)

  - Where m is the number of rows and n is the number of columns in the grid.
  - We visit each cell at most once during the DFS traversal.

- **Space Complexity:** \(O(m \times n)\)

  - We use extra space to store the visited set and the shapes of the islands.
  - The space complexity is also impacted by the recursive call stack during DFS, which in the worst case can be the size of the grid.

---

## Summary

- The problem involves using DFS to explore each island and track its shape.
- By normalizing the shape of each island using relative positions, we can detect distinct islands regardless of their position in the grid.
- The solution uses a set to store unique island shapes, ensuring that duplicate islands are not counted multiple times.

## Resources

[Video Link](https://www.youtube.com/watch?v=7zmgQSJghpo&list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn&index=16&ab_channel=takeUforward)
