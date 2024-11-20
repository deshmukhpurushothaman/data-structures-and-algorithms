# Add Two Numbers Represented by Linked Lists

## Problem Statement

Given two non-negative integers represented by two singly linked lists, where each node contains a single digit, add the two numbers and return the sum as a linked list. The digits are stored in reverse order, and each of their nodes contain a single digit. Add the numbers and return it as a new linked list.

For example:

- Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
- Output: 7 -> 0 -> 8

---

## Approach

We iterate through both linked lists, adding corresponding digits along with any carry. If the sum of the digits is greater than or equal to 10, we carry over the tens place to the next node.

### Code

```javascript
function addTwoNumbers(l1, l2) {
  let carry = 0;
  let dummyHead = new ListNode(0); // Dummy node to simplify the code
  let current = dummyHead;

  while (l1 !== null || l2 !== null || carry !== 0) {
    // Get the values of the current nodes, default to 0 if the node is null
    let val1 = l1 !== null ? l1.val : 0;
    let val2 = l2 !== null ? l2.val : 0;

    // Calculate the sum and the new carry
    let sum = val1 + val2 + carry;
    carry = Math.floor(sum / 10);
    current.next = new ListNode(sum % 10);

    // Move to the next nodes
    current = current.next;
    if (l1 !== null) l1 = l1.next;
    if (l2 !== null) l2 = l2.next;
  }

  return dummyHead.next; // Return the next node of the dummy node, which is the head of the result
}
```

---

## Example Input and Output

### Input:

```text
(2 -> 4 -> 3) + (5 -> 6 -> 4)
```

### Output

```
7 -> 0 -> 8
```

## Example Usage:

```javascript
// Definition for a singly linked list node
class ListNode {
  constructor(val = 0, next = null) {
    this.val = val;
    this.next = next;
  }
}

// Helper function to print the linked list
function printLinkedList(node) {
  let result = [];
  while (node !== null) {
    result.push(node.val);
    node = node.next;
  }
  console.log(result.join(' -> '));
}

// Construct the input linked lists
const l1 = new ListNode(2, new ListNode(4, new ListNode(3)));
const l2 = new ListNode(5, new ListNode(6, new ListNode(4)));

// Add the two numbers
const result = addTwoNumbers(l1, l2);

// Print the result
printLinkedList(result); // Output: 7 -> 0 -> 8
```

---

## Summary

| Approach         | Time Complexity | Space Complexity | Notes                                            |
| ---------------- | --------------- | ---------------- | ------------------------------------------------ |
| Iterative Method | \( O(n) \)      | \( O(n) \)       | Requires extra space for the result linked list. |

---

## Resources

[Video Link](https://www.youtube.com/watch?v=XmRrGzR6udg&list=PLgUwDviBIf0rAuz8tVcM0AymmhTRsfaLU&index=6&ab_channel=takeUforward)
