# Longest Subarray with Sum K

## Problem Statement

Given an array of integers and a target sum `K`, find the length of the longest subarray that sums to `K`.

---

## Approach 1: Brute Force (Better Solution)

### Explanation

1. Use two nested loops to calculate the sum of all subarrays.
2. If the sum of a subarray equals `K`, calculate its length and update the maximum length found so far.

### Code

```javascript
function longestSubarrayBruteForce(arr, K) {
  let maxLength = 0;

  for (let i = 0; i < arr.length; i++) {
    let currentSum = 0;

    for (let j = i; j < arr.length; j++) {
      currentSum += arr[j];

      if (currentSum === K) {
        maxLength = Math.max(maxLength, j - i + 1);
      }
    }
  }

  return maxLength;
}

// Example usage
const arr = [1, 2, 3, 7, 1, 5];
const K = 8;
console.log(longestSubarrayBruteForce(arr, K)); // Output: 2
```

## Complexity

- **Time Complexity:** `O(n^2)`
  - Two nested loops for calculating all subarrays.
- **Space Complexity:** `O(1)`
  - No additional space is used.

---

## Approach 2: Optimal Solution Using HashMap

### Explanation

1. Use a hashmap to store the cumulative sum and its first occurrence index.
2. Traverse the array while maintaining the cumulative sum:
   - If `currentSum - K` exists in the hashmap, it means there’s a subarray with sum `K`.
   - Calculate the length of this subarray and update the maximum length.
3. If `currentSum` is not in the hashmap, store it with its index.

### Code

```javascript
function longestSubarrayOptimal(arr, K) {
  const sumMap = new Map(); // To store cumulative sum and its first occurrence index
  let currentSum = 0;
  let maxLength = 0;

  for (let i = 0; i < arr.length; i++) {
    currentSum += arr[i];

    // Check if the current sum equals K
    if (currentSum === K) {
      maxLength = i + 1;
    }

    // Check if (currentSum - K) exists in the map
    if (sumMap.has(currentSum - K)) {
      maxLength = Math.max(maxLength, i - sumMap.get(currentSum - K));
    }

    // Store the current sum if it's not already in the map
    if (!sumMap.has(currentSum)) {
      sumMap.set(currentSum, i);
    }
  }

  return maxLength;
}

// Example usage
const arr2 = [1, 2, 3, 7, 1, 5];
const K2 = 8;
console.log(longestSubarrayOptimal(arr2, K2)); // Output: 2
```

### Complexity

- **Time Complexity:** `O(n)`
  - Single traversal of the array.
- **Space Complexity:** `O(n)`
  - Space for the hashmap storing cumulative sums.

---

## Approach 3: Two Pointer Technique (Sliding Window)

### Explanation

1. Use two pointers (`start` and `end`) to represent the window.
2. Maintain a variable `currentSum` to track the sum of elements in the window.
3. Adjust the window:
   - If `currentSum < K`, expand the window by moving `end`.
   - If `currentSum > K`, shrink the window by moving `start`.
   - If `currentSum === K`, calculate the length of the current window and update the maximum length.

### Code

```javascript
function longestSubarrayTwoPointer(arr, K) {
  let start = 0;
  let currentSum = 0;
  let maxLength = 0;

  for (let end = 0; end < arr.length; end++) {
    currentSum += arr[end];

    // Shrink the window until the sum is <= K
    while (currentSum > K) {
      currentSum -= arr[start];
      start++;
    }

    // Check if the sum equals K
    if (currentSum === K) {
      maxLength = Math.max(maxLength, end - start + 1);
    }
  }

  return maxLength;
}

// Example usage
const arr3 = [1, 2, 3, 7, 1, 5];
const K3 = 8;
console.log(longestSubarrayTwoPointer(arr3, K3)); // Output: 2
```

### Complexity

- **Time Complexity:** `O(n)`
  - Single traversal of the array.
- **Space Complexity:** `O(1)`
  - No additional space is used.

---

## Summary

| Approach              | Time Complexity | Space Complexity | Notes                        |
| --------------------- | --------------- | ---------------- | ---------------------------- |
| Brute Force           | `O(n^2)`        | `O(1)`           | Inefficient for large arrays |
| Optimal (HashMap)     | `O(n)`          | `O(n)`           | Efficient with extra space   |
| Two Pointer (Sliding) | `O(n)`          | `O(1)`           | Best for non-negative arrays |

**Note**: The two-pointer method works efficiently only if the array contains non-negative integers.
