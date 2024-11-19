
# Common Problems Solved Using the Slow and Fast Pointer Technique

The **Slow and Fast Pointer** technique is a versatile approach that can be applied to a variety of problems involving linked lists, arrays, and other data structures. Below are several common problems where this technique is frequently used:

## 1. **Detecting a Cycle in a Linked List**
The slow and fast pointers are commonly used to detect cycles in a linked list. If there is a cycle, the fast pointer (moving two steps at a time) will eventually meet the slow pointer (moving one step at a time) in a cycle.

### Algorithm:
- Initialize `slow` and `fast` pointers at the head of the linked list.
- Move `slow` one step at a time and `fast` two steps at a time.
- If `slow` and `fast` meet, there is a cycle.
- If `fast` reaches the end of the list (`fast === null` or `fast.next === null`), there is no cycle.

### Code Example:
```javascript
function hasCycle(head) {
    let slow = head;
    let fast = head;

    while (fast !== null && fast.next !== null) {
        slow = slow.next;
        fast = fast.next.next;

        if (slow === fast) {
            return true; // Cycle detected
        }
    }
    return false; // No cycle
}
```

## 2. **Finding the Starting Node of the Cycle in a Linked List**
Once a cycle is detected in a linked list, the slow and fast pointers can be used to find the node where the cycle begins.

### Algorithm:
1. Detect the cycle using the slow and fast pointer technique.
2. After detecting the cycle (when `slow === fast`), reset the `slow` pointer to the head of the linked list.
3. Move both `slow` and `fast` pointers one step at a time until they meet. The node where they meet is the start of the cycle.

### Code Example:
```javascript
function findCycleStart(head) {
    let slow = head;
    let fast = head;

    // Step 1: Detect the cycle
    while (fast !== null && fast.next !== null) {
        slow = slow.next;
        fast = fast.next.next;

        if (slow === fast) {
            break; // Cycle detected
        }
    }

    // Step 2: Find the start of the cycle
    slow = head;
    while (slow !== fast) {
        slow = slow.next;
        fast = fast.next;
    }

    return slow; // The start of the cycle
}
```

## 3. **Finding the Middle Element of a Linked List**
As discussed earlier, the slow and fast pointers can be used to find the middle of a linked list in a single traversal.

### Code Example:
```javascript
function findMiddle(head) {
    let slow = head;
    let fast = head;

    while (fast !== null && fast.next !== null) {
        slow = slow.next;
        fast = fast.next.next;
    }

    return slow; // The middle element
}
```

## 4. **Palindrome Linked List**
To check if a linked list is a palindrome, we can use the slow and fast pointer technique to find the middle of the list, reverse the second half of the list, and then compare the two halves.

### Algorithm:
1. Use the slow and fast pointers to find the middle of the linked list.
2. Reverse the second half of the list.
3. Compare the first half with the reversed second half.

### Code Example:
```javascript
function isPalindrome(head) {
    let slow = head;
    let fast = head;

    // Step 1: Find the middle of the linked list
    while (fast !== null && fast.next !== null) {
        slow = slow.next;
        fast = fast.next.next;
    }

    // Step 2: Reverse the second half of the list
    let prev = null;
    while (slow !== null) {
        let next = slow.next;
        slow.next = prev;
        prev = slow;
        slow = next;
    }

    // Step 3: Compare both halves
    let left = head;
    let right = prev;
    while (right !== null) {
        if (left.value !== right.value) {
            return false; // Not a palindrome
        }
        left = left.next;
        right = right.next;
    }

    return true; // Palindrome
}
```

## 5. **Finding the N-th Node from the End of a Linked List**
The slow and fast pointer technique can be used to find the N-th node from the end of the linked list in a single pass.

### Algorithm:
1. Move the fast pointer N nodes ahead.
2. Then, move both the slow and fast pointers one node at a time.
3. When the fast pointer reaches the end, the slow pointer will be at the N-th node from the end.

### Code Example:
```javascript
function findNthFromEnd(head, n) {
    let slow = head;
    let fast = head;

    // Move fast pointer n steps ahead
    for (let i = 0; i < n; i++) {
        if (fast === null) return null; // n is greater than the length of the list
        fast = fast.next;
    }

    // Move both pointers until fast reaches the end
    while (fast !== null) {
        slow = slow.next;
        fast = fast.next;
    }

    return slow; // The N-th node from the end
}
```

## 6. **Rearranging a Linked List**
You can use the slow and fast pointer technique to find the middle of the list and then rearrange the linked list into two halves. The second half can be reversed and merged with the first half.

### Algorithm:
1. Use slow and fast pointers to find the middle of the list.
2. Split the list into two halves.
3. Reverse the second half.
4. Merge the two halves back together.

## 7. **Cycle Length in a Linked List**
If a cycle is detected using the slow and fast pointers, we can use the two pointers to determine the length of the cycle.

### Algorithm:
1. After detecting the cycle (`slow === fast`), keep the slow pointer fixed and move the fast pointer around the cycle, counting the steps until it meets the slow pointer again.

### Code Example:
```javascript
function cycleLength(head) {
    let slow = head;
    let fast = head;

    while (fast !== null && fast.next !== null) {
        slow = slow.next;
        fast = fast.next.next;

        if (slow === fast) {
            let length = 0;
            do {
                fast = fast.next;
                length++;
            } while (slow !== fast);
            return length; // Length of the cycle
        }
    }

    return 0; // No cycle
}
```

## Conclusion

The slow and fast pointer technique is an efficient and elegant approach for solving a variety of linked list-related problems. It enables us to solve problems like cycle detection, palindrome checking, finding the middle node, and more in linear time with constant space. By adjusting the movement of the two pointers, this technique can be adapted to a wide range of use cases in graph and list-related problems.
