# Remove Nth Node from the End of the LinkedList | Multiple Approaches

## Problem Statement

Given a linked list, remove the `n`th node from the end of the list and return its head.

---

## Approach 1: Two Passes (Using Length Calculation)

### Steps:

1. Traverse the list to calculate its length.
2. Calculate the position of the node to remove by using the formula: `position = length - n`.
3. Traverse the list again to reach the node at the calculated position and remove it.

#### Code (Two Passes)

```javascript
class ListNode {
  constructor(val = 0, next = null) {
    this.val = val;
    this.next = next;
  }
}

function removeNthFromEnd(head, n) {
  let length = 0;
  let current = head;

  // Step 1: Calculate the length of the linked list
  while (current !== null) {
    length++;
    current = current.next;
  }

  // Step 2: Find the (length - n)th node
  let dummy = new ListNode(0);
  dummy.next = head;
  current = dummy;
  for (let i = 0; i < length - n; i++) {
    current = current.next;
  }

  // Step 3: Remove the nth node from the end
  current.next = current.next.next;

  return dummy.next;
}
```

---

## Approach 2: One Pass (Using Two Pointers)

### Steps:

1. Use two pointers, `first` and `second`. Move `first` pointer `n+1` steps ahead.
2. Move both pointers one step at a time until `first` reaches the end of the list.
3. The `second` pointer will be at the node before the `nth` node from the end. Remove the next node.

### Code (One Pass)

```javascript
function removeNthFromEnd(head, n) {
  let dummy = new ListNode(0);
  dummy.next = head;
  let first = dummy;
  let second = dummy;

  // Step 1: Move first n+1 steps ahead
  for (let i = 1; i <= n + 1; i++) {
    first = first.next;
  }

  // Step 2: Move both pointers until first reaches the end
  while (first !== null) {
    first = first.next;
    second = second.next;
  }

  // Step 3: Remove the nth node from the end
  second.next = second.next.next;

  return dummy.next;
}
```

---

## Example Usage:

```javascript
// Helper function to print the linked list
function printLinkedList(node) {
  let result = [];
  while (node !== null) {
    result.push(node.val);
    node = node.next;
  }
  console.log(result.join(' -> '));
}

// Construct a linked list: 1 -> 2 -> 3 -> 4 -> 5
let head = new ListNode(1);
head.next = new ListNode(2);
head.next.next = new ListNode(3);
head.next.next.next = new ListNode(4);
head.next.next.next.next = new ListNode(5);

// Remove the 2nd node from the end (node with value 4)
head = removeNthFromEnd(head, 2);
printLinkedList(head); // Output: 1 -> 2 -> 3 -> 5
```

---

## Example Input and Output

### Input:

```text
1 -> 2 -> 3 -> 4 -> 5
```

### Output:

```
1 -> 2 -> 3 -> 5
```

---

## Summary

| Approach                        | Time Complexity | Space Complexity | Notes                                                                 |
| ------------------------------- | --------------- | ---------------- | --------------------------------------------------------------------- |
| Two Passes (Length Calculation) | O(n)            | O(1)             | First pass to find the length, second pass to remove the nth node.    |
| One Pass (Two Pointers)         | O(n)            | O(1)             | Efficiently removes the nth node in a single pass using two pointers. |

---

## Resources

[Video Link](https://www.youtube.com/watch?v=3kMKYQ2wNIU&list=PLgUwDviBIf0rAuz8tVcM0AymmhTRsfaLU&index=10&ab_channel=takeUforward)
