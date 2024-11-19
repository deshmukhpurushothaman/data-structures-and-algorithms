## Insertion Sort in JavaScript

### Explanation

Insertion Sort is a simple sorting algorithm that builds the final sorted array one item at a time. It is much less efficient on large lists than more advanced algorithms like quicksort, heapsort, or merge sort. However, it can be useful for small data sets or when the input is mostly sorted.

The algorithm works by taking elements from the unsorted part of the array and inserting them at the correct position in the sorted part.

### Time Complexity

- **Worst-case time complexity:** O(n²)
- **Best-case time complexity:** O(n) when the input array is already sorted.
- **Average-case time complexity:** O(n²)
- **Space Complexity:** O(1)

### Code Implementation

```javascript
function insertionSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    let key = arr[i]; // Element to be compared
    let j = i - 1;

    // Move elements of arr[0..i-1], that are greater than key,
    // to one position ahead of their current position
    while (j >= 0 && arr[j] > key) {
      arr[j + 1] = arr[j];
      j--;
    }
    arr[j + 1] = key; // Insert the key at the correct position
  }
  return arr;
}

// Example Usage
const array = [12, 11, 13, 5, 6];
console.log('Sorted Array:', insertionSort(array));
```

## Resources and Explanation

For detailed explanation visit this [link](https://takeuforward.org/data-structure/insertion-sort-algorithm/)

For [video](https://www.youtube.com/watch?v=HGk_ypEuS24&ab_channel=takeUforward)
