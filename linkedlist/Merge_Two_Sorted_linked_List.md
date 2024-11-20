# Merge Two Sorted Linked Lists

## Problem Statement

Given two sorted singly linked lists, merge them into a single sorted linked list.

---

## Approach

We use a two-pointer technique where we compare the nodes of the two lists, adding the smaller node to the result list, and move the pointer forward in the list from which the node was taken. This continues until one of the lists is fully traversed. At that point, we simply append the remaining nodes of the other list to the result.

### Code

```javascript
function mergeTwoLists(l1, l2) {
  // Create a dummy node to simplify handling edge cases
  let dummy = new ListNode(0);
  let current = dummy;

  while (l1 !== null && l2 !== null) {
    if (l1.val < l2.val) {
      current.next = l1; // Link smaller node to the merged list
      l1 = l1.next; // Move pointer in l1
    } else {
      current.next = l2; // Link smaller node to the merged list
      l2 = l2.next; // Move pointer in l2
    }
    current = current.next; // Move to the next node in the merged list
  }

  // If one list is exhausted, append the remaining nodes of the other list
  if (l1 !== null) {
    current.next = l1;
  } else {
    current.next = l2;
  }

  return dummy.next; // Return the merged list (skipping the dummy node)
}
```

## Example Input and Output

### Input:

```
l1 = 1 -> 2 -> 4
l2 = 1 -> 3 -> 4
```

### Output

```
1 -> 1 -> 2 -> 3 -> 4 -> 4
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
const l1 = new ListNode(1, new ListNode(2, new ListNode(4)));
const l2 = new ListNode(1, new ListNode(3, new ListNode(4)));

// Merge the two sorted lists
const mergedList = mergeTwoLists(l1, l2);

// Print the merged list
printLinkedList(mergedList); // Output: 1 -> 1 -> 2 -> 3 -> 4 -> 4
```

## Summary

| Approach  | Time Complexity | Space Complexity | Notes                      |
| --------- | --------------- | ---------------- | -------------------------- |
| Iterative | \( O(n + m) \)  | \( O(1) \)       | Merges two lists in place. |

## Resources

[Video Link](https://www.youtube.com/watch?v=jXu-H7XuClE&list=PLgUwDviBIf0rAuz8tVcM0AymmhTRsfaLU&index=24&pp=iAQB)
