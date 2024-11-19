# Quick Sort Algorithm

**Quick Sort** is a highly efficient sorting algorithm based on the divide-and-conquer strategy. It works by selecting a pivot element and partitioning the array around the pivot, such that elements smaller than the pivot are on the left and elements greater than the pivot are on the right.

## Algorithm Steps

1. **Choose a Pivot**: Pick an element as a pivot. Common strategies include picking the first element, the last element, a random element, or the median.
2. **Partitioning**: Rearrange the array such that elements less than the pivot are on the left and elements greater are on the right.
3. **Recursively Sort**: Recursively apply the same procedure to the left and right subarrays.

---

## Code Implementation (JavaScript)

```javascript
function quickSort(arr) {
  if (arr.length <= 1) {
    return arr; // Base case: an array of one element is already sorted
  }

  // Choosing the pivot (last element in this case)
  const pivot = arr[arr.length - 1];
  const left = [];
  const right = [];

  // Partitioning step
  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] < pivot) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }

  // Recursively sorting the left and right partitions and merging them with the pivot
  return [...quickSort(left), pivot, ...quickSort(right)];
}

// Example usage
const array = [10, 80, 30, 90, 40, 50, 70];
const sortedArray = quickSort(array);
console.log('Sorted Array:', sortedArray);
```

## Another Method

This method has out of bound exception in the pointers while loop check.

```javascript
function quickSort(arr, low = 0, high = arr.length - 1) {
  if (low < high) {
    // Find the partition index
    let pivotIndex = partition(arr, low, high);

    // Recursively sort elements before and after partition
    quickSort(arr, low, pivotIndex - 1);
    quickSort(arr, pivotIndex + 1, high);
  }
  return arr;
}

function partition(arr, low, high) {
  let pivot = arr[low]; // Choose the first element as the pivot
  let i = low;
  let j = high;

  while (i < j) {
    // Move 'i' to the right while elements are less than or equal to the pivot
    while (arr[i] <= pivot && i <= high - 1) {
      i++;
    }
    // Move 'j' to the left while elements are greater than the pivot
    while (arr[j] > pivot && j >= low + 1) {
      j--;
    }
    // If 'i' is still less than 'j', swap the elements
    if (i < j) {
      [arr[i], arr[j]] = [arr[j], arr[i]];
    }
  }
  // Swap the pivot element with the element at index 'j'
  [arr[low], arr[j]] = [arr[j], arr[low]];
  return j; // Return the index of the pivot
}

// Example usage
const array = [10, 80, 30, 90, 40, 50, 70];
console.log('Sorted Array:', quickSort(array));
```

## Method 3

```javascript
function quickSort(arr, low = 0, high = arr.length - 1) {
  if (low < high) {
    // Find the partition index
    let pivotIndex = partition(arr, low, high);

    // Recursively sort elements before and after partition
    quickSort(arr, low, pivotIndex - 1);
    quickSort(arr, pivotIndex + 1, high);
  }
  return arr;
}

function partition(arr, low, high) {
  // Select the first element as the pivot
  let pivot = arr[low];
  let left = low + 1;
  let right = high;

  while (left <= right) {
    // Move left index while the element is less than the pivot
    while (left <= right && arr[left] <= pivot) {
      left++;
    }
    // Move right index while the element is greater than the pivot
    while (left <= right && arr[right] > pivot) {
      right--;
    }

    // Swap elements at left and right pointers if necessary
    if (left < right) {
      [arr[left], arr[right]] = [arr[right], arr[left]];
    }
  }

  // Place the pivot in its correct position
  [arr[low], arr[right]] = [arr[right], arr[low]];
  return right; // Return the partition index
}

// Example usage
const array = [10, 80, 30, 90, 40, 50, 70];
const sortedArray = quickSort(array);
console.log('Sorted Array:', sortedArray);
```

## Complexity Analysis

- **Time Complexity:**

  - **Best Case: O(n log n)** - Occurs when the pivot splits the array into two equal halves.
  - **Average Case: O(n log n)** - Random distribution of elements.
  - **Worst Case: O(n^2)** - Occurs when the pivot is the smallest or largest element, resulting in unbalanced partitions. (Can be mitigated with randomization).

- **Space Complexity: O(log n)** for recursive calls (stack space) in the best/average case. In the worst case, it can degrade to **O(n)**.
  - For method 2 the space complexity is **O(1)**

## Resources and Explanation

For detailed explanation visit this [link](https://takeuforward.org/data-structure/quick-sort-algorithm/)
