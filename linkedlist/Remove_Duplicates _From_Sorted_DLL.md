# Remove Duplicates from Sorted Doubly Linked List

## Problem Statement

Given a sorted doubly linked list, remove all duplicates such that each element appears only once.

---

## Approach

Since the list is sorted, we can easily identify duplicates by comparing each node with its next node. If two consecutive nodes have the same value, we skip the next node and remove it from the list.

### Steps:

1. Traverse the list from the head.
2. For each node, compare it with the next node:
   - If the current node's value is the same as the next node, remove the next node.
   - Otherwise, move to the next node.
3. Continue this process until the end of the list.

#### Code (Remove Duplicates from Sorted DLL)

```javascript
class ListNode {
  constructor(val = 0, next = null, prev = null) {
    this.val = val;
    this.next = next;
    this.prev = prev;
  }
}

function removeDuplicates(head) {
  let current = head;

  while (current !== null && current.next !== null) {
    if (current.val === current.next.val) {
      // Skip the duplicate node
      current.next = current.next.next;

      // If the next node is not null, update its previous pointer
      if (current.next !== null) {
        current.next.prev = current;
      }
    } else {
      current = current.next;
    }
  }

  return head;
}
```

---

## Example Usage:

```javascript
// Helper function to print the doubly linked list
function printDLL(node) {
  let result = [];
  while (node !== null) {
    result.push(node.val);
    node = node.next;
  }
  console.log(result.join(' <-> '));
}

// Construct a sorted doubly linked list with duplicates
let head = new ListNode(1);
head.next = new ListNode(1);
head.next.prev = head;
head.next.next = new ListNode(2);
head.next.next.prev = head.next;
head.next.next.next = new ListNode(3);
head.next.next.next.prev = head.next.next;
head.next.next.next.next = new ListNode(3);
head.next.next.next.next.prev = head.next.next.next;

// Remove duplicates from the sorted DLL
head = removeDuplicates(head);
printDLL(head); // Output: 1 <-> 2 <-> 3
```

## Example Input and Output

### Input:

```
1 <-> 1 <-> 2 <-> 3 <-> 3

```

### Output

```
1 <-> 2 <-> 3
```

---

## Summary

| Approach                          | Time Complexity | Space Complexity | Notes                                                                                       |
| --------------------------------- | --------------- | ---------------- | ------------------------------------------------------------------------------------------- |
| Traversal with pointer comparison | O(n)            | O(1)             | Efficiently removes duplicates by comparing each node with its next node in the sorted DLL. |

---

## Resources

[Video Link](https://www.youtube.com/watch?v=YJKVTnOJXSY&list=PLgUwDviBIf0rAuz8tVcM0AymmhTRsfaLU&index=22&ab_channel=takeUforward)
