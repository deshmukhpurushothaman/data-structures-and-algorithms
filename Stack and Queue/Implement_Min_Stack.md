# Min Stack

## Problem Statement:

Design a stack that supports the following operations:

- `push(x)` — Push element `x` onto the stack.
- `pop()` — Removes the element on the top of the stack.
- `top()` — Get the top element.
- `getMin()` — Retrieve the minimum element in the stack.

## Approach:

The stack should allow constant time access to the minimum element. To achieve this, we can maintain two stacks:

1. **Main stack**: To store the actual elements.
2. **Min stack**: To store the minimum element at each level of the stack.

### Key Idea:

- Whenever we push a new element, we compare it with the current minimum element. If the new element is smaller, it becomes the new minimum. We push the smaller of the two values onto the min stack.
- Whenever we pop an element, we also pop from the min stack to ensure that the min stack always contains the correct minimum element at each level.

### Operations:

1. `push(x)`:
   - Push `x` onto the main stack.
   - Push the minimum of `x` and the current minimum onto the min stack.
2. `pop()`:

   - Pop the top element from both the main stack and the min stack.

3. `top()`:

   - Return the top element from the main stack.

4. `getMin()`:
   - Return the top element of the min stack (which is always the minimum of the stack).

---

## Code (JavaScript):

```javascript
class MinStack {
  constructor() {
    this.stack = [];
    this.minStack = [];
  }

  push(x) {
    this.stack.push(x);
    if (
      this.minStack.length === 0 ||
      x <= this.minStack[this.minStack.length - 1]
    ) {
      this.minStack.push(x);
    } else {
      this.minStack.push(this.minStack[this.minStack.length - 1]);
    }
  }

  pop() {
    this.stack.pop();
    this.minStack.pop();
  }

  top() {
    return this.stack[this.stack.length - 1];
  }

  getMin() {
    return this.minStack[this.minStack.length - 1];
  }
}
```

---

## Example Usage:

```javascript
let minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);

console.log(minStack.getMin()); // Output: -3
minStack.pop();
console.log(minStack.top()); // Output: 0
console.log(minStack.getMin()); // Output: -2
```

---

## Time and Space Complexity:

| Operation  | Time Complexity | Space Complexity | Notes                                                                  |
| ---------- | --------------- | ---------------- | ---------------------------------------------------------------------- |
| `push(x)`  | O(1)            | O(1)             | We are pushing onto two stacks, but the operations take constant time. |
| `pop()`    | O(1)            | O(1)             | Popping from both stacks takes constant time.                          |
| `top()`    | O(1)            | O(1)             | Accessing the top element of the stack takes constant time.            |
| `getMin()` | O(1)            | O(1)             | Accessing the top element of the min stack takes constant time.        |

### Space Complexity:

- The space complexity is O(n) because we maintain two stacks, one for the main elements and one for the minimum values.

---

## Approach 2: Single Stack with Pairing

### Explanation:

We use a single stack to store elements as pairs: each pair contains the actual element and the minimum element at the time of insertion. Every time a new element is pushed, we update the minimum element if the new element is smaller than the current minimum.

### Code:

```javascript
class MinStack {
  constructor() {
    this.stack = [];
  }

  push(x) {
    let min = this.stack.length === 0 ? x : Math.min(x, this.getMin());
    this.stack.push([x, min]);
  }

  pop() {
    this.stack.pop();
  }

  top() {
    return this.stack[this.stack.length - 1][0];
  }

  getMin() {
    return this.stack[this.stack.length - 1][1];
  }
}
```

### Approach 2: Single Stack with Pairing

| Operation  | Time Complexity | Space Complexity | Notes                                                                  |
| ---------- | --------------- | ---------------- | ---------------------------------------------------------------------- |
| `push(x)`  | O(1)            | O(1)             | Each element is pushed with its minimum value in constant time.        |
| `pop()`    | O(1)            | O(1)             | Popping from the stack takes constant time.                            |
| `top()`    | O(1)            | O(1)             | Accessing the top element takes constant time.                         |
| `getMin()` | O(1)            | O(1)             | The minimum value is always stored in the pair, so it's constant time. |

### Space Complexity:

- O(n) due to storing pairs (element + minimum) in the stack.

---

## Approach 3: Using a Linked List

### Explanation:

- We can use a linked list where each node stores:

  - The value of the current element.
  - The minimum value up to that point in the list. This way, we can traverse the list to get the minimum value.

### Code:

```javascript
class MinStack {
  constructor() {
    this.head = null;
  }

  push(x) {
    let min = this.head ? Math.min(x, this.head.min) : x;
    let newNode = { value: x, min: min, next: this.head };
    this.head = newNode;
  }

  pop() {
    if (this.head) {
      this.head = this.head.next;
    }
  }

  top() {
    return this.head ? this.head.value : null;
  }

  getMin() {
    return this.head ? this.head.min : null;
  }
}
```

### Approach 3: Using a Linked List

| Operation  | Time Complexity | Space Complexity | Notes                                                           |
| ---------- | --------------- | ---------------- | --------------------------------------------------------------- |
| `push(x)`  | O(1)            | O(1)             | Each push operation takes constant time to insert a node.       |
| `pop()`    | O(1)            | O(1)             | Popping from the head of the list takes constant time.          |
| `top()`    | O(1)            | O(1)             | Accessing the value at the head takes constant time.            |
| `getMin()` | O(1)            | O(1)             | The minimum value is stored in the node, so it's constant time. |

### Space Complexity:

- O(n) due to storing each node in the linked list.

## Conclusion

| Approach                  | Time Complexity         | Space Complexity | Notes                                                                 |
| ------------------------- | ----------------------- | ---------------- | --------------------------------------------------------------------- |
| Two Stacks                | O(1) for each operation | O(n)             | Efficient with two stacks to maintain minimums at each level.         |
| Single Stack with Pairing | O(1) for each operation | O(n)             | Uses a single stack with pairs to track minimums along with elements. |

## Resources

[Video Link](https://www.youtube.com/watch?v=NdDIaH91P0g&list=PLgUwDviBIf0pOd5zvVVSzgpo6BaCpHT9c&index=5&ab_channel=takeUforward)
