# Count Subarrays with Sum Equal to K

## Problem Statement

Given an array of integers and a target sum `K`, find the total number of subarrays whose sum equals `K`.

---

## Approach 1: Brute Force

### Explanation

1. Use two nested loops to iterate through all possible subarrays.
2. Calculate the sum of each subarray and check if it equals `K`.
3. Increment a counter if a subarray with sum `K` is found.

### Code

```javascript
function countSubarraysBruteForce(arr, K) {
  let count = 0;

  for (let i = 0; i < arr.length; i++) {
    let currentSum = 0;

    for (let j = i; j < arr.length; j++) {
      currentSum += arr[j];

      if (currentSum === K) {
        count++;
      }
    }
  }

  return count;
}

// Example usage
const arr = [1, 1, 1];
const K = 2;
console.log(countSubarraysBruteForce(arr, K)); // Output: 2
```

### Complexity

- **Time Complexity:** `O(n^2)`
  - Two nested loops for calculating all subarrays.
- **Space Complexity:** `O(1)`
  - No additional space is used.

---

## Approach 2: Optimal Solution Using HashMap

### Explanation

1. Use a hashmap to store the cumulative sum and its frequency.
2. Traverse the array while maintaining the cumulative sum:
   - If `currentSum - K` exists in the hashmap, it means there are subarrays ending at the current index with sum `K`.
   - Increment the count by the frequency of `currentSum - K`.
   - Update the hashmap with the current cumulative sum.
3. This reduces the need to compute the sum of every subarray explicitly.

### Code

```javascript
function countSubarraysOptimal(arr, K) {
  const sumMap = new Map(); // To store cumulative sum and its frequency
  let currentSum = 0;
  let count = 0;

  // Initialize the map with a default sum of 0
  sumMap.set(0, 1);

  for (let num of arr) {
    currentSum += num;

    // Check if (currentSum - K) exists in the map
    if (sumMap.has(currentSum - K)) {
      count += sumMap.get(currentSum - K);
    }

    // Update the map with the current cumulative sum
    sumMap.set(currentSum, (sumMap.get(currentSum) || 0) + 1);
  }

  return count;
}

// Example usage
const arr2 = [1, 2, 3];
const K2 = 3;
console.log(countSubarraysOptimal(arr2, K2)); // Output: 2
```

### Complexity

- **Time Complexity:** `O(n)`
  - Single traversal of the array.
- **Space Complexity:** `O(n)`
  Space for the hashmap storing cumulative sums.

---

## Summary

| Approach          | Time Complexity | Space Complexity | Notes                        |
| ----------------- | --------------- | ---------------- | ---------------------------- |
| Brute Force       | `O(n^2)`        | `O(1)`           | Inefficient for large arrays |
| Optimal (HashMap) | `O(n)`          | `O(n)`           | Efficient with extra space   |

## Resources

[Video Link](https://www.youtube.com/watch?v=xvNwoz-ufXA&list=PLgUwDviBIf0oF6QL8m22w1hIDC1vJ_BHz&index=33&ab_channel=takeUforward)
