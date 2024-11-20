# Sort a Linked List

## Problem Statement

Given the head of a singly linked list, sort the list in ascending order.

---

## Approach

We can sort a linked list using various algorithms, such as **Merge Sort** and **Quick Sort**. However, **Merge Sort** is often preferred because it works in \( O(n \log n) \) time complexity, and it is efficient for linked lists as it doesn't require random access like Quick Sort.

### Approach: Merge Sort

In this approach, we recursively divide the linked list into two halves, sort each half, and then merge the two sorted halves.

#### Code (Merge Sort)

```javascript
class ListNode {
  constructor(val = 0, next = null) {
    this.val = val;
    this.next = next;
  }
}

function sortList(head) {
  if (head === null || head.next === null) {
    return head; // Base case: a list with 0 or 1 node is already sorted
  }

  // Step 1: Split the list into two halves
  let middle = getMiddle(head);
  let left = head;
  let right = middle.next;
  middle.next = null;

  // Step 2: Recursively sort both halves
  left = sortList(left);
  right = sortList(right);

  // Step 3: Merge the sorted halves
  return merge(left, right);
}

// Helper function to find the middle of the list
function getMiddle(head) {
  let slow = head;
  let fast = head;

  while (fast !== null && fast.next !== null) {
    slow = slow.next;
    fast = fast.next.next;
  }
  return slow;
}

// Helper function to merge two sorted lists
function merge(left, right) {
  let dummy = new ListNode(0);
  let current = dummy;

  while (left !== null && right !== null) {
    if (left.val < right.val) {
      current.next = left;
      left = left.next;
    } else {
      current.next = right;
      right = right.next;
    }
    current = current.next;
  }

  if (left !== null) current.next = left;
  if (right !== null) current.next = right;

  return dummy.next;
}
```

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

// Construct the input linked list
const l1 = new ListNode(4, new ListNode(2, new ListNode(1, new ListNode(3))));

// Sort the linked list
const sortedList = sortList(l1);

// Print the sorted list
printLinkedList(sortedList); // Output: 1 -> 2 -> 3 -> 4
```

---

## Example Input and Output

### Input

```
4 -> 2 -> 1 -> 3
```

### Output

```
1 -> 2 -> 3 -> 4
```

---

## Summary

| Approach   | Time Complexity | Space Complexity | Notes                                               |
| ---------- | --------------- | ---------------- | --------------------------------------------------- |
| Merge Sort | O(n log n)      | O(log n)         | Recursively splits and merges the list efficiently. |
| Quick Sort | O(n log n)      | O(log n)         | Not as efficient for linked lists as Merge Sort.    |

---

## Resources

[Video Link](https://www.youtube.com/watch?v=8ocB7a_c-Cc&list=PLgUwDviBIf0rAuz8tVcM0AymmhTRsfaLU&index=27&t=1077s&pp=iAQB)
