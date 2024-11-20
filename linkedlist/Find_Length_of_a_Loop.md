# Find the Length of the Loop in a Linked List

## Problem Statement

Given a linked list, if the linked list contains a cycle, determine the length of the cycle (loop). If there is no cycle, return 0.

---

## Approach 1: Floyd’s Cycle-Finding Algorithm

To detect the cycle in the linked list, we can use **Floyd’s Cycle-Finding Algorithm** (also known as the **Tortoise and Hare Algorithm**). Once a cycle is detected, we can calculate the length of the cycle by moving one pointer around the cycle and counting the number of steps it takes to return to the same position.

### Steps:

1. Use two pointers, **slow** and **fast**.
2. Move **slow** by one step and **fast** by two steps at a time.
3. If **slow** and **fast** meet, then there is a cycle. Otherwise, there is no cycle.
4. Once a cycle is detected, keep **slow** fixed and move **fast** around the cycle until it meets **slow** again, while counting the number of steps to find the length of the cycle.

#### Code (Cycle Detection and Length Calculation)

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

function findCycleLength(head) {
  let meetingNode = detectCycle(head);
  if (meetingNode === null) return 0; // No cycle

  // Step 2: Calculate the length of the cycle
  let current = meetingNode;
  let length = 1;

  while (current.next !== meetingNode) {
    length++;
    current = current.next;
  }

  return length;
}
```

## Approach 2: Hashing

In this approach, we will use a **hash set** to track the nodes that have already been visited. If we encounter a node that we have already visited, it means we have found the cycle. Once the cycle is detected, we will count the number of nodes in the cycle.

### Steps:

1. Traverse the linked list while storing the nodes in a hash set.
2. If a node is already present in the hash set, we have detected the cycle.
3. Once the cycle is detected, count the nodes involved in the cycle by keeping track of how many steps it takes to revisit the starting node.

#### Code (Cycle Detection and Length Calculation using Hashing)

```javascript
class ListNode {
  constructor(val = 0, next = null) {
    this.val = val;
    this.next = next;
  }
}

function findCycleLength(head) {
  let visited = new Set();
  let current = head;
  let cycleStartNode = null;

  // Step 1: Detect the cycle by storing visited nodes in a hash set
  while (current !== null) {
    if (visited.has(current)) {
      cycleStartNode = current; // Cycle detected
      break;
    }
    visited.add(current);
    current = current.next;
  }

  // If no cycle was detected
  if (!cycleStartNode) {
    return 0;
  }

  // Step 2: Calculate the length of the cycle
  let length = 1;
  let node = cycleStartNode.next;
  while (node !== cycleStartNode) {
    length++;
    node = node.next;
  }

  return length;
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

// Construct a linked list with a cycle
let head = new ListNode(1);
head.next = new ListNode(2);
head.next.next = new ListNode(3);
head.next.next.next = new ListNode(4);
head.next.next.next.next = new ListNode(5);
head.next.next.next.next.next = head.next.next; // Creating a cycle here

// Find the cycle length
console.log(findCycleLength(head)); // Output: 3 (Length of the cycle: 3 -> 4 -> 5 -> 3)
```

---

## Example Input and Output

### Input:

```text
1 -> 2 -> 3 -> 4 -> 5
        ^---------|
```

### Output:

```text
3
```

---

## Summary

| Approach                        | Time Complexity | Space Complexity | Notes                                                               |
| ------------------------------- | --------------- | ---------------- | ------------------------------------------------------------------- |
| Floyd’s Cycle-Finding Algorithm | O(n)            | O(1)             | Efficiently detects and calculates cycle length using two pointers. |
| Hashing                         | O(n)            | O(n)             | Detects cycle and calculates cycle length by storing visited nodes. |

---

## Resources

[Video Link](https://www.youtube.com/watch?v=I4g1qbkTPus&list=PLgUwDviBIf0rAuz8tVcM0AymmhTRsfaLU&index=17&ab_channel=takeUforward)
