# Bubble Sort Algorithm in JavaScript

## What is Bubble Sort?

Bubble Sort is a simple comparison-based sorting algorithm that works by repeatedly stepping through the list to be sorted, comparing adjacent items, and swapping them if they are in the wrong order. The process is repeated until no swaps are needed, indicating that the list is sorted.

## How Bubble Sort Works

1. **Compare adjacent elements**: Start from the first element of the list and compare it with the next element.
2. **Swap if needed**: If the first element is greater than the second, swap them.
3. **Repeat the process**: Move to the next element and repeat the comparison and swap process until the end of the list is reached.
4. **Repeat the full pass**: After one complete pass through the list, the largest element is placed in its correct position at the end. Repeat this for the remaining unsorted elements.

This algorithm continues to pass through the list until no more swaps are needed, meaning the list is sorted.

## Bubble Sort JavaScript Code

```javascript
function bubbleSort(arr) {
  let n = arr.length;
  let swapped;

  // Outer loop: each pass places the largest unsorted element at the end
  for (let i = 0; i < n - 1; i++) {
    swapped = false;

    // Inner loop: compare adjacent elements and swap if needed
    for (let j = 0; j < n - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        // Swap the elements
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;

        swapped = true;
      }
    }

    // If no two elements were swapped, the array is already sorted
    if (!swapped) {
      break;
    }
  }

  return arr;
}
```

## Time and Space Complexities

- **Best Case Complexity (O(n)):** The best case occurs when the array is already sorted. The algorithm performs a single pass through the list and detects no swaps, hence completing in linear time, O(n).

- **Average and Worst Case Complexity (O(n^2)):** In both the average and worst case, the algorithm needs to perform multiple passes through the list, comparing and possibly swapping elements. In the worst case (when the list is in reverse order), the algorithm performs O(n^2) comparisons and swaps.

- **Space Complexity (O(1)):** Bubble Sort is an in-place sorting algorithm, meaning it requires only a constant amount of extra space, O(1), for the swapping process.

## Resources and Explanation

For detailed explanation visit this [link](https://takeuforward.org/data-structure/bubble-sort-algorithm/)

For [video](https://www.youtube.com/watch?v=HGk_ypEuS24&ab_channel=takeUforward)
