# Reverse a Doubly Linked List (DLL)

## Problem Statement

Given the head of a doubly linked list (DLL), reverse the DLL in place, such that the last node becomes the head and all the `prev` and `next` pointers are correctly updated.

---

## Approach

We traverse the doubly linked list, swapping the `next` and `prev` pointers for each node. Finally, we update the head to the last node.

### Code

```javascript
function reverseDLL(head) {
  if (!head) return null; // Empty list, return null

  let current = head;
  let temp = null;

  while (current) {
    // Swap the `next` and `prev` pointers
    temp = current.prev;
    current.prev = current.next;
    current.next = temp;

    // Move to the next node (which is the previous node due to swap)
    current = current.prev;
  }

  // Update head to the new head (previously the last node)
  if (temp) {
    head = temp.prev;
  }

  return head;
}
```

## Example Input and Output

### Input:

```text
1 <-> 2 <-> 3 <-> 4
```

### Output

```
4 <-> 3 <-> 2 <-> 1
```

## Example Usage:

```javascript
// Definition for a DLL node
class Node {
  constructor(value) {
    this.value = value;
    this.prev = null;
    this.next = null;
  }
}

// Helper function to print the DLL
function printDLL(head) {
  const result = [];
  let current = head;
  while (current) {
    result.push(current.value);
    current = current.next;
  }
  console.log(result.join(' <-> '));
}

// Construct the DLL
const head = new Node(1);
const second = new Node(2);
const third = new Node(3);
const fourth = new Node(4);

head.next = second;
second.prev = head;
second.next = third;
third.prev = second;
third.next = fourth;
fourth.prev = third;

// Print original list
console.log('Original DLL:');
printDLL(head);

// Reverse the DLL
const reversedHead = reverseDLL(head);

// Print reversed list
console.log('Reversed DLL:');
printDLL(reversedHead);
```

## Summary

| Approach         | Time Complexity | Space Complexity | Notes                    |
| ---------------- | --------------- | ---------------- | ------------------------ |
| Iterative Method | \( O(n) \)      | \( O(1) \)       | Swaps pointers in place. |

---

## Resources

[Video Link](https://www.youtube.com/watch?v=u3WUW2qe6ww&list=PLgUwDviBIf0rAuz8tVcM0AymmhTRsfaLU&index=5&pp=iAQB)
