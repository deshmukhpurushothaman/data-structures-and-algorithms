# Check for Balanced Parentheses | Stack and Queue

## Problem Statement

Given a string containing parentheses `()`, curly braces `{}`, and square brackets `[]`, check whether the parentheses are balanced. A string is considered balanced if:

- Every opening bracket has a corresponding closing bracket.
- The brackets are properly nested.

---

## Approach: Using Stack

### Steps:

1. Iterate through the string.
2. For every opening bracket (`(`, `{`, or `[`), push it onto the stack.
3. For every closing bracket (`)`, `}`, or `]`), check if the stack is empty. If it is, return `false`.
4. If the stack is not empty, pop the top element and check if it matches the corresponding opening bracket.
5. After the loop, if the stack is empty, the parentheses are balanced. Otherwise, they are not.

---

### Code:

```javascript
function isValid(s) {
  const stack = [];
  const matchingBracket = {
    '(': ')',
    '{': '}',
    '[': ']',
  };

  for (let char of s) {
    if (matchingBracket[char]) {
      // If it's an opening bracket, push to stack
      stack.push(char);
    } else {
      // If it's a closing bracket, check for match
      const last = stack.pop();
      if (matchingBracket[last] !== char) {
        return false;
      }
    }
  }

  // If the stack is empty, it's balanced
  return stack.length === 0;
}
```

---

## Example Usage for Queue:

```javascript
console.log(isValidUsingQueue('()')); // Output: true
console.log(isValidUsingQueue('()[]{}')); // Output: true
console.log(isValidUsingQueue('(]')); // Output: false
console.log(isValidUsingQueue('([)]')); // Output: false
console.log(isValidUsingQueue('{[]}')); // Output: true
```

---

## Example Input and Output for Queue

### Input:

```
"()[]{}"
```

### Output

```
true
```

---

## Summary

| Approach             | Time Complexity | Space Complexity | Notes                                                           |
| -------------------- | --------------- | ---------------- | --------------------------------------------------------------- |
| Stack-based Solution | O(n)            | O(n)             | Efficient and simple approach using a stack for matching pairs. |
| Queue-based Solution | O(n)            | O(n)             | Less common approach, uses a queue to simulate matching pairs.  |

## Resources

[Video Link](https://www.youtube.com/watch?v=xwjS0iZhw4I&list=PLgUwDviBIf0pOd5zvVVSzgpo6BaCpHT9c&index=3&ab_channel=takeUforward)
