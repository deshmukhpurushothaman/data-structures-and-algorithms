# Next Greater Element - Multiple Approaches

## Problem Statement:

Given an array of integers, find the next greater element for each element of the array. The next greater element is the first element that is greater than the current element, and it appears to the right of the current element in the array. If no such element exists, the next greater element is -1.

---

## Approach 1: Brute Force

### Explanation:

In this approach, for each element in the array, we check all the elements to the right of it to find the next greater element.

### Code:

```javascript
function nextGreaterElement(arr) {
  let result = [];
  for (let i = 0; i < arr.length; i++) {
    let found = false;
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] > arr[i]) {
        result[i] = arr[j];
        found = true;
        break;
      }
    }
    if (!found) {
      result[i] = -1;
    }
  }
  return result;
}
```

---

### Time and Space Complexities

| Operation              | Time Complexity | Space Complexity | Notes                                              |
| ---------------------- | --------------- | ---------------- | -------------------------------------------------- |
| `nextGreaterElement()` | O(n^2)          | O(n)             | Brute force approach checks all pairs of elements. |

### Space Complexity:

- O(n) for storing the result array.

---

## Approach 2: Stack-based Approach

### Explanation:

We can use a stack to optimize the process. We iterate through the array from right to left. For each element, we pop elements from the stack that are less than or equal to the current element, as they can't be the next greater element for any of the remaining elements. The current element is then pushed onto the stack, and we record the next greater element from the stack.

### Code:

```javascript
function nextGreaterElement(arr) {
  let result = new Array(arr.length).fill(-1);
  let stack = [];

  for (let i = arr.length - 1; i >= 0; i--) {
    while (stack.length > 0 && stack[stack.length - 1] <= arr[i]) {
      stack.pop();
    }

    if (stack.length > 0) {
      result[i] = stack[stack.length - 1];
    }

    stack.push(arr[i]);
  }

  return result;
}
```

---

### Time and Space Complexities

| Operation              | Time Complexity | Space Complexity | Notes                                                          |
| ---------------------- | --------------- | ---------------- | -------------------------------------------------------------- |
| `nextGreaterElement()` | O(n)            | O(n)             | Each element is pushed and popped from the stack at most once. |

### Space Complexity:

- O(n) due to the stack used to store elements.

---

## Approach 3: Optimized Using Map (Monotonic Stack)

### Explanation:

In this approach, we use a map to store the next greater element for each element, which allows us to avoid searching repeatedly for the next greater element.

### Code:

```javascript
function nextGreaterElement(arr) {
  let result = new Array(arr.length).fill(-1);
  let stack = [];
  let map = new Map();

  for (let i = 0; i < arr.length; i++) {
    while (stack.length > 0 && arr[stack[stack.length - 1]] < arr[i]) {
      let index = stack.pop();
      map.set(arr[index], arr[i]);
    }
    stack.push(i);
  }

  for (let i = 0; i < arr.length; i++) {
    if (map.has(arr[i])) {
      result[i] = map.get(arr[i]);
    }
  }

  return result;
}
```

### Time and Space Complexities

| Operation              | Time Complexity | Space Complexity | Notes                                                         |
| ---------------------- | --------------- | ---------------- | ------------------------------------------------------------- |
| `nextGreaterElement()` | O(n)            | O(n)             | Using a map and stack ensures each element is processed once. |

### Space Complexity:

- O(n) for storing the map and stack.

---

## Conclusion

| Approach             | Time Complexity | Space Complexity | Notes                                                        |
| -------------------- | --------------- | ---------------- | ------------------------------------------------------------ |
| Brute Force          | O(n^2)          | O(n)             | A simple but inefficient approach that checks all pairs.     |
| Stack-based Approach | O(n)            | O(n)             | Efficient approach using a stack, reducing time complexity.  |
| Optimized Using Map  | O(n)            | O(n)             | Uses a map to store results and optimize further operations. |
