# Merge Intervals

## Problem Statement

Given an array of intervals where intervals[i] = [start_i, end_i], merge all overlapping intervals and return an array of the non-overlapping intervals that cover all the intervals in the input.

### Example

**Input**: `[[1, 3], [2, 6], [8, 10], [15, 18]]`  
**Output**: `[[1, 6], [8, 10], [15, 18]]`  
**Explanation**: Intervals [1, 3] and [2, 6] overlap, so they are merged into [1, 6].

---

## Approach

### Explanation

1. **Sort Intervals**: First, sort the intervals based on the start time.
2. **Merging Logic**:
   - Initialize an empty list `merged` to store merged intervals.
   - Iterate through the intervals:
     - If the `merged` list is empty or the current interval does not overlap with the last interval in `merged`, simply add it to `merged`.
     - If there is an overlap, merge the current interval with the last interval in `merged` by updating the end time of the last interval.

---

### Steps

1. Sort the intervals by their starting time.
2. Initialize a result array to keep track of merged intervals.
3. Traverse through the intervals, checking for overlaps and merging accordingly.

---

### Code in JavaScript

```javascript
function mergeIntervals(intervals) {
  if (intervals.length === 0) return [];

  // Step 1: Sort the intervals based on the start time
  intervals.sort((a, b) => a[0] - b[0]);

  // Step 2: Initialize the result array with the first interval
  const merged = [intervals[0]];

  // Step 3: Traverse through the sorted intervals
  for (let i = 1; i < intervals.length; i++) {
    const lastMergedInterval = merged[merged.length - 1];
    const currentInterval = intervals[i];

    // Step 4: Check if intervals overlap
    if (currentInterval[0] <= lastMergedInterval[1]) {
      // Merge intervals by updating the end time
      lastMergedInterval[1] = Math.max(
        lastMergedInterval[1],
        currentInterval[1]
      );
    } else {
      // No overlap, add the current interval to the result
      merged.push(currentInterval);
    }
  }

  return merged;
}

// Example usage
const intervals = [
  [1, 3],
  [2, 6],
  [8, 10],
  [15, 18],
];
console.log(mergeIntervals(intervals)); // Output: [[1, 6], [8, 10], [15, 18]]
```

---

### Complexity

- **Time Complexity**: `O(n log n)`

  - Sorting the intervals takes `O(n log n)`.
  - Merging intervals takes `O(n)`.
  - Overall complexity is `O(n log n)`.

- **Space Complexity**: `O(n)`
  - The space complexity is `O(n)` due to the result array holding merged intervals.

---

## Summary

- The key idea is to first sort the intervals based on their start times.
- By checking overlaps and merging intervals as we traverse, we efficiently combine overlapping intervals into one.
- The algorithm ensures that all overlapping intervals are merged, producing a non-overlapping set of intervals.

## Resources

- [Video Link](https://www.youtube.com/watch?v=2JzRBPFYbKE&ab_channel=takeUforward)
