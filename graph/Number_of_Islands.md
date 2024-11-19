# Number of Islands Program in JavaScript (Graph Representation) using BFS and DFS

## Problem Description

The **Number of Islands** problem involves counting the number of connected components (or "islands") in a 2D grid, where each cell can either be land (`1`) or water (`0`). An island is surrounded by water and is formed by connecting adjacent lands (horizontally or vertically).

Given a grid, the goal is to determine how many islands exist in the grid.

### Input:

- A 2D grid consisting of `1`s (land) and `0`s (water).

### Output:

- The number of islands formed by connected `1`s.

## Approach

We will solve this problem using both **Depth First Search (DFS)** and **Breadth First Search (BFS)** techniques.

### Key Points:

- Treat each land cell (`1`) as a node and its adjacent land cells (up, down, left, right) as edges.
- For each unvisited land cell, perform a DFS or BFS to mark all reachable land cells connected to it, counting each island.

## 1. BFS Method

In the BFS approach, we will explore all adjacent land cells level by level. Starting from an unvisited land cell, we will use a queue to explore all connected land cells, marking them as visited.

### BFS Implementation:

```javascript
function numIslandsBFS(grid) {
  if (!grid || grid.length === 0) return 0;

  const rows = grid.length;
  const cols = grid[0].length;
  let islands = 0;

  const directions = [
    [0, 1], // right
    [0, -1], // left
    [1, 0], // down
    [-1, 0], // up
  ];

  const bfs = (i, j) => {
    const queue = [[i, j]];
    grid[i][j] = '0'; // Mark as visited
    while (queue.length) {
      const [x, y] = queue.shift();
      for (const [dx, dy] of directions) {
        const nx = x + dx,
          ny = y + dy;
        if (
          nx >= 0 &&
          ny >= 0 &&
          nx < rows &&
          ny < cols &&
          grid[nx][ny] === '1'
        ) {
          grid[nx][ny] = '0'; // Mark as visited
          queue.push([nx, ny]);
        }
      }
    }
  };

  // Iterate through the grid
  for (let i = 0; i < rows; i++) {
    for (let j = 0; j < cols; j++) {
      if (grid[i][j] === '1') {
        islands++;
        bfs(i, j); // Explore the island
      }
    }
  }

  return islands;
}
```

## 2. DFS Method

In the DFS approach, we will use a recursive function to visit all connected land cells starting from an unvisited land cell. The recursion will explore all directions (up, down, left, right) until all connected land cells are marked as visited.

### DFS Implementation:

```javascript
function numIslandsDFS(grid) {
  if (!grid || grid.length === 0) return 0;

  const rows = grid.length;
  const cols = grid[0].length;
  let islands = 0;

  const directions = [
    [0, 1], // right
    [0, -1], // left
    [1, 0], // down
    [-1, 0], // up
  ];

  const dfs = (i, j) => {
    if (i < 0 || j < 0 || i >= rows || j >= cols || grid[i][j] === '0') {
      return;
    }
    grid[i][j] = '0'; // Mark as visited
    for (const [dx, dy] of directions) {
      dfs(i + dx, j + dy); // Explore all directions
    }
  };

  // Iterate through the grid
  for (let i = 0; i < rows; i++) {
    for (let j = 0; j < cols; j++) {
      if (grid[i][j] === '1') {
        islands++;
        dfs(i, j); // Explore the island
      }
    }
  }

  return islands;
}
```

## Time and Space Complexities

### Time Complexity:

- Both BFS and DFS have the same time complexity of **O(m \* n)**, where:
  - m is the number of rows in the grid.
  - n is the number of columns in the grid.
- This is because each cell is visited at most once during the BFS or DFS traversal.

### Space Complexity:

- BFS: The space complexity is **O(m \* n)** in the worst case, because we might need to store all cells in the queue when all cells are land.
- DFS: The space complexity is **O(m \* n)** in the worst case due to the recursion stack depth, which can be as deep as the number of cells in the grid if all are land.
