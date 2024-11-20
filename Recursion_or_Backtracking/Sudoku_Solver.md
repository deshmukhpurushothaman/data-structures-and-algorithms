# Sudoku Solver Using Backtracking

## Problem Statement

The goal is to solve a 9x9 Sudoku puzzle by filling the empty cells (`.` or `0`) while following these rules:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the nine 3x3 sub-boxes must contain the digits `1-9` without repetition.

## Approach: Backtracking

The backtracking approach involves trying to place each number from `1` to `9` in an empty cell and then recursively checking if it leads to a solution. If placing a number doesn't lead to a solution, the cell is reset (backtracking).

### Algorithm Steps

1. Find an empty cell in the Sudoku board.
2. For each number `1` to `9`:
   - Place the number in the cell if it is valid (i.e., does not violate Sudoku rules).
   - Recursively attempt to fill the board.
   - If successful, the puzzle is solved; if not, backtrack by removing the number.
3. Repeat until the board is completely filled.

---

## Code Implementation

```javascript
function solveSudoku(board) {
  const size = 9;

  function isValid(board, row, col, num) {
    const startRow = Math.floor(row / 3) * 3;
    const startCol = Math.floor(col / 3) * 3;

    for (let i = 0; i < size; i++) {
      // Check row
      if (board[row][i] === num.toString()) return false;

      // Check column
      if (board[i][col] === num.toString()) return false;

      // Check 3x3 sub-box
      const subRow = startRow + Math.floor(i / 3);
      const subCol = startCol + (i % 3);
      if (board[subRow][subCol] === num.toString()) return false;
    }

    return true;
  }

  function solve() {
    for (let row = 0; row < size; row++) {
      for (let col = 0; col < size; col++) {
        if (board[row][col] === '.') {
          // Try placing numbers from 1 to 9
          for (let num = 1; num <= 9; num++) {
            if (isValid(board, row, col, num)) {
              board[row][col] = num.toString();

              // Recursively attempt to solve
              if (solve()) {
                return true;
              }

              // Backtrack
              board[row][col] = '.';
            }
          }
          return false; // No valid number found, trigger backtracking
        }
      }
    }
    return true; // All cells filled
  }

  solve();
}

// Example Usage
const board = [
  ['5', '3', '.', '.', '7', '.', '.', '.', '.'],
  ['6', '.', '.', '1', '9', '5', '.', '.', '.'],
  ['.', '9', '8', '.', '.', '.', '.', '6', '.'],
  ['8', '.', '.', '.', '6', '.', '.', '.', '3'],
  ['4', '.', '.', '8', '.', '3', '.', '.', '1'],
  ['7', '.', '.', '.', '2', '.', '.', '.', '6'],
  ['.', '6', '.', '.', '.', '.', '2', '8', '.'],
  ['.', '.', '.', '4', '1', '9', '.', '.', '5'],
  ['.', '.', '.', '.', '8', '.', '.', '7', '9'],
];

solveSudoku(board);
console.log(board);
```

---

## Explanation

1. `isValid` Function:
   - Checks if placing a number is valid based on Sudoku rules (row, column, and 3x3 sub-box).
2. `solve` Function:
   - Uses a recursive approach to try placing numbers in each empty cell.
   - Backtracks if a placement doesn't lead to a solution by resetting the cell.

---

## Complexity Analysis

- **Time Complexity:** **O(9(n×n))**
  - In the worst case, each cell can have up to 9 possibilities.
  - The backtracking significantly reduces this complexity in practice by pruning invalid paths.
- **Space Complexity:** **O(n2)**
  - The space complexity is for storing the board itself and recursive calls.

## Notes

- The provided implementation works on a 9x9 board but can be generalized for other sizes by changing the `size` variable and updating constraints accordingly.
- Backtracking is efficient for solving Sudoku puzzles, although it may be slow for certain complex configurations due to its exhaustive search nature.

## Resources

[Video Link](https://www.youtube.com/watch?v=FWAIf_EVUKE&list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9&index=18&ab_channel=takeUforward)
