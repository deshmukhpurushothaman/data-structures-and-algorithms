# Coin Change Problem (Leetcode #322)

The Coin Change problem asks: Given `n` coin denominations and an integer `amount`, what is the minimum number of coins required to make the given amount? If no combination can make the amount, return `-1`.

---

## Problem Statement

- **Given**:
  - A set of coin denominations `coins[]`.
  - An integer `amount`, representing the total amount.
- **Objective**:
  - Find the fewest number of coins that sum up to `amount`. If it's impossible, return `-1`.

---

## Approach 1: Dynamic Programming (Bottom-Up)

### Description

We can use a 1D DP array where `dp[i]` represents the minimum number of coins required to make the amount `i`. The state transition formula is:

```plaintext
dp[i] = min(dp[i], dp[i - coin] + 1) for all coins
```

### Code Implementation

```javascript
function coinChange(coins, amount) {
  // Initialize the DP array
  const dp = Array(amount + 1).fill(Infinity);
  dp[0] = 0; // Base case: 0 coins needed to make amount 0

  // Iterate through amounts from 1 to 'amount'
  for (let i = 1; i <= amount; i++) {
    for (let coin of coins) {
      if (i >= coin) {
        dp[i] = Math.min(dp[i], dp[i - coin] + 1);
      }
    }
  }

  // Return the result
  return dp[amount] === Infinity ? -1 : dp[amount];
}

// Example Usage
const coins = [1, 2, 5];
const amount = 11;
console.log(`Fewest coins needed: ${coinChange(coins, amount)}`);
```

### Complexity Analysis

- **Time Complexity**: O(amount × n)

  - `amount` is the total amount to be formed.
  - `n` is the number of coin denominations.
  - For each amount, we iterate through all coins.

- **Space Complexity**: O(amount)
  - The `dp` array of size `amount + 1` is used.

---

### Example Walkthrough

#### Input:

```plaintext
coins = [1, 2, 5], amount = 11
```

#### DP Table Updates:

1. Initialize: `dp = [0, Infinity, Infinity, ..., Infinity]` (length = `amount + 1`)
2. Process:

- For amount `1`: `dp[1] = min(dp[1], dp[1 - 1] + 1) = 1`
- For amount `2`: `dp[2] = min(dp[2], dp[2 - 1] + 1, dp[2 - 2] + 1) = 1`
- For amount `3`: `dp[3] = min(dp[3], dp[3 - 1] + 1) = 2`
- ...
- For amount `11`: `dp[11] = min(dp[11], dp[11 - 1] + 1, dp[11 - 2] + 1, dp[11 - 5] + 1) = 3`

Final `dp` array: `[0, 1, 1, 2, 2, 1, 2, 2, 3, 3, 2, 3].`

#### Output

```plaintext
3
```

---

## Approach 2: Breadth-First Search (BFS)

### Description

Alternatively, we can approach this problem using BFS. Starting with an amount of 0, we explore all possible amounts by adding coins one by one. This ensures we find the minimum number of coins needed for each amount.

### Code Implementation

```javascript
function coinChange(coins, amount) {
  if (amount === 0) return 0;

  const queue = [0]; // BFS queue
  const visited = Array(amount + 1).fill(false);
  visited[0] = true;
  let steps = 0;

  while (queue.length > 0) {
    let len = queue.length;
    steps++;

    for (let i = 0; i < len; i++) {
      let currentAmount = queue.shift();

      for (let coin of coins) {
        let nextAmount = currentAmount + coin;

        if (nextAmount === amount) return steps;
        if (nextAmount < amount && !visited[nextAmount]) {
          visited[nextAmount] = true;
          queue.push(nextAmount);
        }
      }
    }
  }

  return -1;
}

// Example usage
const coins = [1, 2, 5];
const amount = 11;
console.log(`Fewest coins needed: ${coinChange(coins, amount)}`);
```

### Complexity Analysis

- **Time Complexity**: O(amount × n)

  - `amount` is the total amount, and `n` is the number of coin denominations.
  - BFS explores every possible combination of coins to form the amount.

- **Space Complexity**: O(amount)
  - We store the `visited` array to track visited amounts.

## Summary

- **Dynamic Programming (Bottom-Up):** Efficient with time complexity O(amount × n) and space complexity O(amount).
- **BFS:** Offers an alternative approach with similar time complexity but potentially more intuitive for small to medium inputs.

## Key Takeaway

For this problem, Dynamic Programming provides an optimal solution, while BFS offers a more intuitive exploration-based approach. Choose the approach based on the size of the input and the complexity constraints.
