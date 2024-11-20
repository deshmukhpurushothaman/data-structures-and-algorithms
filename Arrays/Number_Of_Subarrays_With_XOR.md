# Number of Subarrays with XOR Equal to K

## Problem Statement

Given an array of integers and a target XOR `K`, find the total number of subarrays whose XOR equals `K`.

---

## XOR Explanation

The XOR (exclusive OR) operation is a binary operation where the result is `1` if and only if the two bits being compared are different. In the case of integers, it is applied bit by bit.

- **XOR Properties**:
  - `a ^ a = 0` (XOR of a number with itself is 0)
  - `a ^ 0 = a` (XOR of a number with 0 is the number itself)
  - XOR is **commutative** and **associative**.

For example:

- `5 ^ 3 = 6` (In binary, `101 ^ 011 = 110`)
- `6 ^ 6 = 0` (In binary, `110 ^ 110 = 000`)

In this problem, we are interested in the XOR of subarrays, meaning the XOR of all elements between any two indices of the array.

---

## Approach 1: Brute Force (Better Solution)

### Explanation

1. Use two nested loops to calculate the XOR of all subarrays.
2. If the XOR of a subarray equals `K`, increment the counter.

### Code

```javascript
function countSubarraysXORBruteForce(arr, K) {
  let count = 0;

  for (let i = 0; i < arr.length; i++) {
    let currentXOR = 0;

    for (let j = i; j < arr.length; j++) {
      currentXOR ^= arr[j]; // XOR each element

      if (currentXOR === K) {
        count++;
      }
    }
  }

  return count;
}

// Example usage
const arr = [4, 2, 2, 6, 4];
const K = 6;
console.log(countSubarraysXORBruteForce(arr, K)); // Output: 4
```

### Complexity

- **Time Complexity:** `O(n^2)`

  - Two nested loops for calculating all subarrays.

- **Space Complexity:** `O(1)`
  - No additional space is used.

---

## Approach 2: Better Solution Using Prefix XOR

### Explanation

1. Compute the prefix XOR for each element in the array.
2. If the XOR from the beginning of the array to index `i` is `prefixXOR[i]`, then the XOR of subarray [l, r] can be calculated as `prefixXOR[r] ^ prefixXOR[l-1]`.
3. For each subarray, check if the result equals `K` and count.

### Code

```javascript
function countSubarraysXORBetter(arr, K) {
  let count = 0;
  let prefixXOR = 0;
  let xorMap = new Map(); // Store the frequency of prefixXOR values

  // Initialize with the base case for an empty subarray
  xorMap.set(0, 1);

  for (let num of arr) {
    prefixXOR ^= num;

    // Check if (prefixXOR ^ K) exists in the map
    if (xorMap.has(prefixXOR ^ K)) {
      count += xorMap.get(prefixXOR ^ K);
    }

    // Store the current prefixXOR in the map
    xorMap.set(prefixXOR, (xorMap.get(prefixXOR) || 0) + 1);
  }

  return count;
}

// Example usage
const arr2 = [4, 2, 2, 6, 4];
const K2 = 6;
console.log(countSubarraysXORBetter(arr2, K2)); // Output: 4
```

### Complexity

- **Time Complexity:** `O(n)`

  - Single traversal of the array, with operations involving the map which take O(1) on average.

- **Space Complexity:** `O(n)`
  - Space for the hashmap storing prefix XOR values.

---

## Approach 3: Optimal Solution Using HashMap (Prefix XOR and Frequency Count)

### Explanation

This approach is the most efficient using the concept of prefix XOR and hashmap to store the frequency of XORs encountered. The idea is the same as the previous one but explained in more detail:

1. Maintain a running `prefixXOR`.
2. At each element, calculate the `currentPrefixXOR`, which is the XOR of all elements from index `0 to i`.
3. For each `currentPrefixXOR`, check if there exists a previous `prefixXOR` such that:
   - `currentPrefixXOR ^ previousPrefixXOR == K`
4. If it exists, increment the count by the number of times that prefix XOR has appeared.

### Code

```javascript
function countSubarraysXOROptimal(arr, K) {
  let count = 0;
  let prefixXOR = 0;
  let xorMap = new Map();

  // Initialize with the base case (empty subarray XOR is 0)
  xorMap.set(0, 1);

  for (let num of arr) {
    prefixXOR ^= num;

    // If prefixXOR ^ K exists, add the frequency count of that prefix
    if (xorMap.has(prefixXOR ^ K)) {
      count += xorMap.get(prefixXOR ^ K);
    }

    // Update the map with the current prefixXOR frequency
    xorMap.set(prefixXOR, (xorMap.get(prefixXOR) || 0) + 1);
  }

  return count;
}

// Example usage
const arr3 = [4, 2, 2, 6, 4];
const K3 = 6;
console.log(countSubarraysXOROptimal(arr3, K3)); // Output: 4
```

### Complexity

- **Time Complexity:** `O(n)`
  - Single traversal of the array with constant time hashmap operations.
- **Space Complexity:** `O(n)`
  - Space for the hashmap storing prefix XOR values.

---

## Summary

| Approach            | Time Complexity | Space Complexity | Notes                                             |
| ------------------- | --------------- | ---------------- | ------------------------------------------------- |
| Brute Force         | `O(n^2)`        | `O(1)`           | Inefficient for large arrays                      |
| Better (Prefix XOR) | `O(n)`          | `O(n)`           | Efficient with hashmap                            |
| Optimal (HashMap)   | `O(n)`          | `O(n)`           | Best approach with prefix XOR and frequency count |

---

## Resources

[Video Link](https://www.youtube.com/watch?v=eZr-6p0B7ME&ab_channel=takeUforward)
