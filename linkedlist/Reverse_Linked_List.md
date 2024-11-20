# Reverse a Linked List

## Problem Statement

Given the head of a singly linked list, reverse the list and return its head.

---

## Approaches

### 1. Iterative Approach

In this approach, we iterate through the linked list and reverse the `next` pointers of each node. We keep track of the previous node while traversing the list and update the `next` pointers accordingly.

#### Code (Iterative)

```javascript
function reverseList(head) {
  let prev = null;
  let current = head;

  while (current !== null) {
    let nextNode = current.next; // Store next node
    current.next = prev; // Reverse the current node's pointer
    prev = current; // Move prev to current node
    current = nextNode; // Move to the next node
  }

  return prev; // New head of the reversed list
}
```

---

## 2. Recursive Approach

In the recursive approach, we reverse the rest of the list first and then adjust the next pointer of the current node to point to the previous node.

### Code (Recursive)

```javascript
function reverseList(head) {
  if (head === null || head.next === null) {
    return head; // Base case: if the list is empty or has only one node
  }

  let rest = reverseList(head.next); // Recursively reverse the rest of the list
  head.next.next = head; // Make the next node point back to the current node
  head.next = null; // Set the current node's next to null (new tail)

  return rest; // Return the new head of the reversed list
}
```

## Example Input and Output

### Input:

```
1 -> 2 -> 3 -> 4 -> 5
```

### Output (Iterative Approach):

```
5 -> 4 -> 3 -> 2 -> 1
```

### Output (Recursive Approach):

```text
5 -> 4 -> 3 -> 2 -> 1
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

// Construct the input linked list
const list = new ListNode(
  1,
  new ListNode(2, new ListNode(3, new ListNode(4, new ListNode(5))))
);

// Reverse the linked list using the iterative approach
const reversedIterative = reverseList(list);
printLinkedList(reversedIterative); // Output: 5 -> 4 -> 3 -> 2 -> 1

// Reverse the linked list using the recursive approach
const reversedRecursive = reverseList(list);
printLinkedList(reversedRecursive); // Output: 5 -> 4 -> 3 -> 2 -> 1
```

---

## Summary

| Approach  | Time Complexity | Space Complexity | Notes                              |
| --------- | --------------- | ---------------- | ---------------------------------- |
| Iterative | \( O(n) \)      | \( O(1) \)       | In-place reversal using iteration. |
| Recursive | \( O(n) \)      | \( O(n) \)       | Recursion uses stack space.        |

## Resources

[Video Link](https://www.youtube.com/watch?v=D2vI2DNJGd8&list=PLgUwDviBIf0rAuz8tVcM0AymmhTRsfaLU&index=10&pp=iAQB)
