## Selection Sort in JavaScript

### Explanation

Selection Sort is a simple comparison-based sorting algorithm. The algorithm divides the input array into two parts: a sorted subarray of items that is built up from left to right at the front (left) of the array, and a subarray of the remaining items that need to be sorted. The algorithm repeatedly selects the smallest (or largest, depending on sorting order) element from the unsorted subarray, swapping it with the leftmost unsorted element, and moving the subarray boundary one element to the right.

### Time Complexity

- **Worst-case time complexity:** O(n²)
- **Best-case time complexity:** O(n²)
- **Average-case time complexity:** O(n²)
  - The complexity remains O(n²) in all cases because even if the array is already sorted, the algorithm still traverses the entire array for each element.
- **Space Complexity:** O(1)
  - It is an **in-place** sorting algorithm, meaning it does not require additional storage space beyond a few variable assignments.

### Code Implementation

```javascript
function selectionSort(arr) {
  let n = arr.length;

  for (let i = 0; i < n - 1; i++) {
    // Find the minimum element in the unsorted subarray
    let minIndex = i;
    for (let j = i + 1; j < n; j++) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }

    // Swap the found minimum element with the first element of the unsorted subarray
    if (minIndex !== i) {
      [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]];
    }
  }
  return arr;
}

// Example Usage
const array = [64, 25, 12, 22, 11];
console.log('Sorted Array:', selectionSort(array));
```

## Resources and Explanation

For detailed explanation visit this [link](https://takeuforward.org/sorting/selection-sort-algorithm/)

For [video](https://www.youtube.com/watch?v=HGk_ypEuS24&ab_channel=takeUforward)
