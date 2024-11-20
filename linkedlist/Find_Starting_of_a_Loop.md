# Find the Starting Point of the Loop/Cycle in Linked List | Multiple Approaches

## Problem Statement

Given a linked list, if the linked list contains a cycle, determine the starting node of the cycle. If there is no cycle, return `null`.

---

## Approach 1: Floyd’s Cycle-Finding Algorithm (Tortoise and Hare)

### Steps:

1. **Detect the Cycle**: Use two pointers (`slow` and `fast`), where `slow` moves one step at a time and `fast` moves two steps at a time. If there is a cycle, `slow` and `fast` will eventually meet.
2. **Find the Cycle's Start**: Once a cycle is detected, move `slow` back to the head and keep `fast` at the meeting point. Now move both pointers one step at a time. The node where they meet again is the starting point of the cycle.

#### Code (Floyd’s Cycle-Finding Algorithm)

```javascript
class ListNode {
  constructor(val = 0, next = null) {
    this.val = val;
    this.next = next;
  }
}

function detectCycle(head) {
  let slow = head;
  let fast = head;

  // Step 1: Detect the cycle using Floyd’s Cycle-Finding Algorithm
  while (fast !== null && fast.next !== null) {
    slow = slow.next;
    fast = fast.next.next;

    if (slow === fast) {
      return slow; // Cycle detected, return the meeting node
    }
  }

  return null; // No cycle
}

function findCycleStart(head) {
  let meetingNode = detectCycle(head);
  if (meetingNode === null) return null; // No cycle

  let slow = head;

  // Step 2: Find the cycle's starting point
  while (slow !== meetingNode) {
    slow = slow.next;
    meetingNode = meetingNode.next;
  }

  return slow; // Starting point of the cycle
}
```

---

## Approach 2: Hashing (Using a Set)

### Steps:

1. Traverse the linked list and store each node's reference in a hash set.
2. If a node is already present in the hash set, it means we have encountered the start of the cycle. Return that node.
3. If no node repeats, return `null` indicating no cycle.

### Code (Using Hashing)

```javascript
function findCycleStart(head) {
  let visited = new Set();
  let current = head;

  while (current !== null) {
    if (visited.has(current)) {
      return current; // Cycle start detected
    }
    visited.add(current);
    current = current.next;
  }

  return null; // No cycle
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

// Construct a linked list with a cycle
let head = new ListNode(1);
head.next = new ListNode(2);
head.next.next = new ListNode(3);
head.next.next.next = new ListNode(4);
head.next.next.next.next = new ListNode(5);
head.next.next.next.next.next = head.next.next; // Creating a cycle here

// Find the cycle start
console.log(findCycleStart(head)); // Output: Node with value 3 (starting point of the cycle)
```

## Example Input and Output

### Input:

```text
1 -> 2 -> 3 -> 4 -> 5
        ^---------|
```

### Output

```
3
```

## Summary

| Approach                        | Time Complexity | Space Complexity | Notes                                                                 |
| ------------------------------- | --------------- | ---------------- | --------------------------------------------------------------------- |
| Floyd’s Cycle-Finding Algorithm | O(n)            | O(1)             | Efficiently detects the cycle and finds the start using two pointers. |
| Hashing                         | O(n)            | O(n)             | Detects the cycle start by storing visited nodes.                     |

## Resources

[Video Link](https://www.youtube.com/watch?v=2Kd0KKmmHFc&list=PLgUwDviBIf0rAuz8tVcM0AymmhTRsfaLU&index=19&ab_channel=takeUforward)
