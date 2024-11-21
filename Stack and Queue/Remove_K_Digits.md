# Remove K Digits

## Problem Statement:

Given a non-negative integer `num` represented as a string, and an integer `k`, remove `k` digits from the number so that the new number is the smallest possible number. The result must not have leading zeros, except if the number is zero.

---

## Approach 1: Using Stack

### Explanation:

We can use a stack to solve this problem efficiently. The idea is to maintain a monotonically increasing sequence of digits. As we iterate through the number, we remove digits from the stack when we encounter a smaller digit than the top of the stack. This ensures that we are left with the smallest possible number after removing `k` digits.

### Code:

```javascript
function removeKdigits(num, k) {
  let stack = [];

  for (let digit of num) {
    while (k > 0 && stack.length > 0 && stack[stack.length - 1] > digit) {
      stack.pop();
      k--;
    }
    stack.push(digit);
  }

  // Remove any remaining digits if k > 0
  while (k > 0) {
    stack.pop();
    k--;
  }

  // Remove leading zeros
  let result = stack.join('').replace(/^0+/, '');

  // If the result is empty, return '0'
  return result === '' ? '0' : result;
}
```

### Time and Space Complexity:

| Operation         | Time Complexity | Space Complexity | Notes                                                |
| ----------------- | --------------- | ---------------- | ---------------------------------------------------- |
| `removeKdigits()` | O(n)            | O(n)             | Each digit is pushed and popped from the stack once. |

### Space Complexity:

- O(n) for the stack used to store digits.

---

## Approach 2: Greedy with Priority Queue

### Explanation:

We can also solve this problem using a priority queue (min-heap) to select the smallest digits at each step. This approach, however, is less efficient than the stack-based solution due to the overhead of maintaining the heap.

### Code:

```javascript
function removeKdigits(num, k) {
  let pq = new MinPriorityQueue();
  let result = '';

  for (let digit of num) {
    pq.enqueue(digit);
    if (pq.size() > k) {
      result += pq.dequeue();
    }
  }

  // Remove leading zeros
  result = result.replace(/^0+/, '');

  // If the result is empty, return '0'
  return result === '' ? '0' : result;
}
```

### Time and Space Complexity:

| Operation         | Time Complexity | Space Complexity | Notes                                                                      |
| ----------------- | --------------- | ---------------- | -------------------------------------------------------------------------- |
| `removeKdigits()` | O(n log n)      | O(n)             | Inserting into and removing from the heap takes log n time for each digit. |

### Space Complexity:

- O(n) due to the priority queue storing the digits.

---

## Conclusion:

| Approach                   | Time Complexity | Space Complexity | Notes                                                  |
| -------------------------- | --------------- | ---------------- | ------------------------------------------------------ |
| Stack-based Approach       | O(n)            | O(n)             | Efficient and optimal solution for removing digits.    |
| Greedy with Priority Queue | O(n log n)      | O(n)             | Slower than the stack approach due to heap operations. |
