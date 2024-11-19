# Merge Sort Algorithm

**Merge Sort** is a divide-and-conquer algorithm that splits an array into halves, sorts each half, and merges them back together in sorted order.

## Algorithm Steps

1. **Divide**: Recursively divide the array into two halves until each subarray has one or zero elements.
2. **Conquer**: Sort the subarrays recursively.
3. **Combine**: Merge the sorted subarrays to produce a sorted result.

---

## Code Implementation (JavaScript)

```javascript
function mergeSort(arr) {
  if (arr.length <= 1) {
    return arr; // Base case: single element is already sorted
  }

  // Split the array in half
  const mid = Math.floor(arr.length / 2);
  const left = arr.slice(0, mid);
  const right = arr.slice(mid);

  // Recursively sort both halves
  const sortedLeft = mergeSort(left);
  const sortedRight = mergeSort(right);

  // Merge the sorted halves
  return merge(sortedLeft, sortedRight);
}

function merge(left, right) {
  let result = [];
  let i = 0;
  let j = 0;

  // Compare elements of both arrays and merge in sorted order
  while (i < left.length && j < right.length) {
    if (left[i] < right[j]) {
      result.push(left[i]);
      i++;
    } else {
      result.push(right[j]);
      j++;
    }
  }

  // Add remaining elements, if any
  while (i < left.length) {
    result.push(left[i]);
    i++;
  }

  while (j < right.length) {
    result.push(right[j]);
    j++;
  }

  return result;
}

// Example usage
const array = [38, 27, 43, 3, 9, 82, 10];
const sortedArray = mergeSort(array);
console.log('Sorted Array:', sortedArray);
```

## Complexity Analysis

- **Time Complexity: O(n log n)**
  - The array is repeatedly divided into halves (`log n` levels of recursion), and each level performs O(n) operations to merge the subarrays.
- **Space Complexity: O(n)**
  - Temporary arrays are used during the merging process.

## Resources and Explanation

For detailed explanation visit this [link](https://takeuforward.org/data-structure/merge-sort-algorithm/)
