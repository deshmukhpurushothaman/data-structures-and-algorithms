
# 0/1 Knapsack Problem: Recursion to Space Optimized Approach

The 0/1 Knapsack problem is a classic optimization problem that asks:
Given `n` items, each with a weight `w[i]` and value `v[i]`, and a knapsack with capacity `W`, what is the maximum value we can fit into the knapsack, considering that each item can either be included or excluded (0/1).

---

## Problem Statement
- **Given**:
  - A set of `n` items, each with a weight `w[i]` and a value `v[i]`.
  - A knapsack of capacity `W`.
- **Objective**:
  - Maximize the total value in the knapsack without exceeding the capacity `W`.

---

## Approach 1: Recursive Solution

### Description
The recursive approach involves exploring all possible combinations of including or excluding each item and finding the maximum value that can be achieved.

### Recursive Solution Code

```javascript
function knapsackRecursive(weights, values, n, W) {
    // Base case: no items left or capacity becomes 0
    if (n === 0 || W === 0) {
        return 0;
    }

    // If weight of the nth item is more than capacity W, skip this item
    if (weights[n - 1] > W) {
        return knapsackRecursive(weights, values, n - 1, W);
    } else {
        // Consider both cases: including and excluding the current item
        return Math.max(
            values[n - 1] + knapsackRecursive(weights, values, n - 1, W - weights[n - 1]),
            knapsackRecursive(weights, values, n - 1, W)
        );
    }
}

// Example usage
const weights = [1, 3, 4, 5];
const values = [1, 4, 5, 7];
const capacity = 7;
console.log(knapsackRecursive(weights, values, weights.length, capacity)); // Output: 9
```

### Complexity
- **Time Complexity**: \(O(2^n)\)
  - Each item can be included or excluded, leading to \(2^n\) possibilities.
- **Space Complexity**: \(O(n)\)
  - Recursion stack space.

---

## Approach 2: Dynamic Programming (Bottom-Up)

### Description
We use a 2D DP array where `dp[i][j]` represents the maximum value that can be achieved with the first `i` items and capacity `j`. The transition is:
\[ \text{dp}[i][j] = \max(\text{dp}[i - 1][j], \text{values}[i - 1] + \text{dp}[i - 1][j - \text{weights}[i - 1]]) \]

### Code

```javascript
function knapsackDP(weights, values, n, W) {
    const dp = Array.from({ length: n + 1 }, () => Array(W + 1).fill(0));

    for (let i = 1; i <= n; i++) {
        for (let j = 1; j <= W; j++) {
            if (weights[i - 1] <= j) {
                dp[i][j] = Math.max(
                    values[i - 1] + dp[i - 1][j - weights[i - 1]],
                    dp[i - 1][j]
                );
            } else {
                dp[i][j] = dp[i - 1][j];
            }
        }
    }

    return dp[n][W];
}

// Example usage
console.log(knapsackDP(weights, values, weights.length, capacity)); // Output: 9
```

### Complexity
- **Time Complexity**: \(O(n \times W)\)
- **Space Complexity**: \(O(n \times W)\)

---

## Approach 3: Space Optimized DP (1D Array)

### Description
We can optimize space by using a 1D array, as the current state only depends on the previous row. We iterate backward to avoid overwriting values prematurely.

### Code

```javascript
function knapsackSpaceOptimized(weights, values, n, W) {
    const dp = Array(W + 1).fill(0);

    for (let i = 0; i < n; i++) {
        for (let j = W; j >= weights[i]; j--) {
            dp[j] = Math.max(dp[j], values[i] + dp[j - weights[i]]);
        }
    }

    return dp[W];
}

// Example usage
console.log(knapsackSpaceOptimized(weights, values, weights.length, capacity)); // Output: 9
```

### Complexity
- **Time Complexity**: \(O(n \times W)\)
- **Space Complexity**: \(O(W)\)
  - Optimized to use only one-dimensional space.

---

## Summary

- **Recursive Approach**: Simple but exponential complexity.
- **DP Table (2D)**: Reduces time complexity with \(O(n \times W)\) space.
- **Space-Optimized DP (1D)**: Optimizes space to \(O(W)\) while maintaining time complexity.

### Key Takeaway
The space-optimized DP approach is efficient and widely used for large inputs, leveraging previous state computations in a single array to achieve optimal results.
