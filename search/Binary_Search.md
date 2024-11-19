# Binary Search Algorithm in JavaScript

## What is Binary Search?

Binary Search is a highly efficient algorithm for finding an element in a **sorted array**. It works by repeatedly dividing the search interval in half. If the value of the search key is less than the item in the middle of the interval, the search continues in the lower half; otherwise, it continues in the upper half. This process continues until the value is found or the interval is empty.

## How Binary Search Works

1. **Initialize the search range**: Start with two pointers, `low` and `high`, representing the range of indices to search (initially, `low` is 0, and `high` is the last index of the array).
2. **Find the middle**: Calculate the middle index `mid = (low + high) / 2`.
3. **Check the middle element**:
   - If the middle element is the target value, return the index.
   - If the middle element is greater than the target value, repeat the search in the left half (`high = mid - 1`).
   - If the middle element is less than the target value, repeat the search in the right half (`low = mid + 1`).
4. **Repeat** the process until the target value is found or the search range becomes invalid (`low > high`).

## Method 1: Binary Search (Iterative)

```javascript
function binarySearch(arr, target) {
  let low = 0;
  let high = arr.length - 1;

  while (low <= high) {
    let mid = Math.floor((low + high) / 2); // Find the middle index
    if (arr[mid] === target) {
      return mid; // Target found, return the index
    } else if (arr[mid] < target) {
      low = mid + 1; // Search in the right half
    } else {
      high = mid - 1; // Search in the left half
    }
  }

  return -1; // Target not found
}
```

## Time and Space Complexities

- **Time Complexity (O(log n)):** Binary Search significantly reduces the number of comparisons needed to find an element. In each step, the search range is halved, so the algorithm runs in logarithmic time, O(log n).

  - Best Case: If the target element is the middle element, the search completes in O(1) time.
  - Worst Case: The search narrows down the range step by step, so the worst-case time complexity is O(log n).

- **Space Complexity (O(1)):** Binary Search operates in constant space, O(1), because it uses only a few extra variables (low, high, mid) to track the current search range, regardless of the input size.

## Method 2: Recursive Binary Search JavaScript Code

```javascript
function recursiveBinarySearch(arr, target, low = 0, high = arr.length - 1) {
  // Base case: if the range is invalid
  if (low > high) {
    return -1; // Target not found
  }

  // Calculate the middle index
  let mid = Math.floor((low + high) / 2);

  // If the middle element is the target, return the index
  if (arr[mid] === target) {
    return mid;
  }

  // If the target is less than the middle element, search the left half
  if (arr[mid] > target) {
    return recursiveBinarySearch(arr, target, low, mid - 1);
  }

  // If the target is greater than the middle element, search the right half
  return recursiveBinarySearch(arr, target, mid + 1, high);
}
```

## Time and Space Complexities

- **Time Complexity (O(log n)):**

  - Best Case: If the middle element is the target, the search completes in O(1) time.
  - Worst Case: The search narrows down by halving the range in each recursive step. In the worst case, the time complexity is O(log n), as the search space is halved at each recursive call.

- **Space Complexity (O(log n)):**

  - Unlike the iterative version, the recursive version requires additional space for the function call stack. Each recursive call adds a new frame to the stack. In the worst case (when the search range is reduced step by step), the space complexity is O(log n), which is the height of the recursion tree.
