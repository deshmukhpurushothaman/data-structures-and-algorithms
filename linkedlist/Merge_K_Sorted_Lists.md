# Merge K Sorted Lists

## Problem Statement

Given an array of `k` sorted linked lists, merge them into a single sorted linked list.

---

## Approach

To merge multiple sorted linked lists efficiently, we can use a **Min-Heap (Priority Queue)** or a **Divide and Conquer** approach.

### Approach 1: Using Min-Heap (Priority Queue)

We can use a min-heap (priority queue) to always extract the smallest element among the heads of the `k` lists. The time complexity of extracting the smallest element is \(O(\log k)\), and since we have `n` total elements, the overall time complexity is \(O(n \log k)\).

#### Code (Min-Heap)

```javascript
class ListNode {
  constructor(val = 0, next = null) {
    this.val = val;
    this.next = next;
  }
}

function mergeKLists(lists) {
  const minHeap = new MinPriorityQueue({ priority: (x) => x.val });
  let dummy = new ListNode(0);
  let current = dummy;

  // Push all list heads into the min-heap
  for (let list of lists) {
    if (list !== null) {
      minHeap.push(list);
    }
  }

  // Pop the smallest element from the heap, and add the next node from the corresponding list
  while (minHeap.size() > 0) {
    let node = minHeap.pop().element;
    current.next = node;
    current = current.next;

    // If there is a next node, add it to the heap
    if (node.next !== null) {
      minHeap.push(node.next);
    }
  }

  return dummy.next;
}
```

---

## Approach 2: Divide and Conquer

We can use a divide and conquer approach to merge the lists pair by pair. Initially, merge two lists, then merge the result with the next list, and so on. The time complexity for each merge is
`O(n)`, and since we halve the number of lists in each step, the overall time complexity is `O(nlogk)`.

### Code (Divide and Conquer)

```javascript
function mergeKLists(lists) {
  if (lists.length === 0) return null;

  function mergeTwoLists(l1, l2) {
    let dummy = new ListNode(0);
    let current = dummy;

    while (l1 !== null && l2 !== null) {
      if (l1.val < l2.val) {
        current.next = l1;
        l1 = l1.next;
      } else {
        current.next = l2;
        l2 = l2.next;
      }
      current = current.next;
    }

    if (l1 !== null) current.next = l1;
    if (l2 !== null) current.next = l2;

    return dummy.next;
  }

  while (lists.length > 1) {
    let mergedLists = [];
    for (let i = 0; i < lists.length; i += 2) {
      let l1 = lists[i];
      let l2 = lists[i + 1] || null;
      mergedLists.push(mergeTwoLists(l1, l2));
    }
    lists = mergedLists;
  }

  return lists[0];
}
```

---

## Example Input and Output

### Input:

```
l1 = 1 -> 4 -> 5
l2 = 1 -> 3 -> 4
l3 = 2 -> 6
```

### Output:

```text
1 -> 1 -> 2 -> 3 -> 4 -> 4 -> 5 -> 6
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
const l1 = new ListNode(1, new ListNode(4, new ListNode(5)));
const l2 = new ListNode(1, new ListNode(3, new ListNode(4)));
const l3 = new ListNode(2, new ListNode(6));

// Merge the k sorted lists
const mergedList = mergeKLists([l1, l2, l3]);

// Print the merged list
printLinkedList(mergedList); // Output: 1 -> 1 -> 2 -> 3 -> 4 -> 4 -> 5 -> 6
```

## Summary

| Approach                  | Time Complexity | Space Complexity | Notes                                                         |
| ------------------------- | --------------- | ---------------- | ------------------------------------------------------------- |
| Min-Heap (Priority Queue) | O(n log k)      | O(k)             | Uses a priority queue to always extract the smallest element. |
| Divide and Conquer        | O(n log k)      | O(1)             | Merges lists pair by pair.                                    |
|  |

## Resources

[Video Link](https://www.youtube.com/watch?v=1zktEppsdig&list=PLgUwDviBIf0rAuz8tVcM0AymmhTRsfaLU&index=26&pp=iAQB)
