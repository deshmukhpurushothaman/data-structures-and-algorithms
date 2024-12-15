# Longest Increasing Subsequence (LIS) | Memoization

## Problem Description

Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

### Example

#### Input:

```plaintext
nums = [10, 9, 2, 5, 3, 7, 101, 18]
```

#### Output:

```
4
```

### Explanation:

The longest increasing subsequence is `[2, 3, 7, 101]`.

---

## Approach: Memoization (Top-Down Dynamic Programming)

### Key Idea

The longest increasing subsequence problem can be solved using recursion with memoization. For each element in the array, we recursively determine whether to include it in the subsequence or skip it. To optimize, we store the results of previously computed states.

#### Steps:

1.  Use a recursive function `dp(index, prevIndex)` where:

    - `index` is the current position in the array.
    - `prevIndex` is the index of the previous element in the subsequence.
    - The function returns the length of the LIS starting from `index`, given that the previous element is at `prevIndex`.

2.  Transition:

    - If `nums[index] > nums[prevIndex]`, consider including `nums[index]` in the LIS.
    - Consider skipping `nums[index]`.

3.  Memoize results using a 2D array `memo[index][prevIndex + 1]` to avoid redundant calculations.

4.  Base Case:

    - When `index == nums.length`, return `0` (no more elements to process).

### Code Implementation

```javascript
function lengthOfLIS(nums) {
  const n = nums.length;

  // Create a memoization table
  const memo = Array.from({ length: n }, () => Array(n + 1).fill(-1));

  // Helper function for recursion with memoization
  function dp(index, prevIndex) {
    // Base case: if index is out of bounds, return 0
    if (index === n) return 0;

    // If already computed, return memoized value
    if (memo[index][prevIndex + 1] !== -1) {
      return memo[index][prevIndex + 1];
    }

    // Skip the current element
    let notTake = dp(index + 1, prevIndex);

    // Take the current element if it is part of the LIS
    let take = 0;
    if (prevIndex === -1 || nums[index] > nums[prevIndex]) {
      take = 1 + dp(index + 1, index);
    }

    // Store the result in the memo table
    return (memo[index][prevIndex + 1] = Math.max(take, notTake));
  }

  // Start the recursion
  return dp(0, -1);
}

// Example Usage
const nums = [10, 9, 2, 5, 3, 7, 101, 18];
console.log(`Length of LIS: ${lengthOfLIS(nums)}`);
```

---

### Complexity Analysis

- **Time Complexity**: O(n²)

  - We have `n` elements, and for each element, we calculate states for all previous indices.

- **Space Complexity**: O(n²)
  - Due to the memoization table `memo`.

---

### Example Walkthrough

#### Input:

```
nums = [10, 9, 2, 5, 3, 7, 101, 18]
```

#### Recursive Tree:

1. Start with `index = 0`, `prevIndex = -1`.
2. For `index = 0` (`10`), explore:
   - Include `10` in the LIS → Explore `index = 1` (`9`).
   - Skip `10` → Explore `index = 1` (`9`).

#### Memoization Table:

- Each state `memo[index][prevIndex + 1]` stores the LIS length from `index` with the given `prevIndex`.

#### Output:

The length of the LIS is `4` (corresponding to `[2, 3, 7, 101]`).

---

## Alternative Approaches

- **Dynamic Programming (Bottom-Up)**: Iterative DP solution with a 1D array.
- **Binary Search Optimization**: Reduces time complexity to O(n log n).

## Resources

[Video Link](https://www.youtube.com/watch?v=ekcwMsSIzVc&ab_channel=takeUforward)
