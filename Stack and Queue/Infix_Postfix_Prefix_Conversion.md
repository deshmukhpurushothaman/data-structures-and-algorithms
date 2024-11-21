# Prefix, Infix, and Postfix Conversion

## Problem Statement

Given an arithmetic expression in infix notation, convert it to prefix or postfix notation. Additionally, we will define and explore the three types of expressions:

- **Infix Notation**: The operator is between two operands. Example: `A + B`
- **Postfix Notation** (Reverse Polish Notation): The operator comes after the operands. Example: `A B +`
- **Prefix Notation** (Polish Notation): The operator comes before the operands. Example: `+ A B`

---

## Approach for Conversion

### 1. Infix to Postfix Conversion

**Algorithm**:

1. Initialize an empty stack for operators and an empty list for the result.
2. Iterate through the infix expression:
   - If the character is an operand (number/letter), append it to the result.
   - If the character is an opening parenthesis `(`, push it onto the stack.
   - If the character is a closing parenthesis `)`, pop from the stack to the result until an opening parenthesis `(` is encountered.
   - If the character is an operator, pop operators from the stack to the result while they have higher or equal precedence than the current operator, then push the current operator onto the stack.
3. At the end of the expression, pop all operators from the stack to the result.

**Operator Precedence**:

- `*`, `/` > `+`, `-`

---

### Code (Infix to Postfix):

```javascript
function infixToPostfix(infix) {
  let stack = [];
  let result = [];
  let precedence = { '+': 1, '-': 1, '*': 2, '/': 2, '^': 3 };

  for (let char of infix) {
    if (/[a-zA-Z0-9]/.test(char)) {
      result.push(char); // Operand, add to result
    } else if (char === '(') {
      stack.push(char); // Left parenthesis, push to stack
    } else if (char === ')') {
      while (stack.length && stack[stack.length - 1] !== '(') {
        result.push(stack.pop()); // Pop till '('
      }
      stack.pop(); // Pop '('
    } else {
      while (
        stack.length &&
        precedence[stack[stack.length - 1]] >= precedence[char]
      ) {
        result.push(stack.pop()); // Pop operators with higher precedence
      }
      stack.push(char); // Push the current operator to stack
    }
  }

  while (stack.length) {
    result.push(stack.pop()); // Pop all remaining operators
  }

  return result.join('');
}
```

---

## 2. Infix to Prefix Conversion

### Algorithm:

1. Reverse the infix expression.
2. Convert the reversed expression to postfix.
3. Reverse the postfix expression to get the prefix expression.

---

### Code (Infix to Prefix):

```javascript
function infixToPrefix(infix) {
  // Reverse the infix expression
  infix = infix.split('').reverse().join('');
  // Replace '(' with ')' and vice versa
  infix = infix
    .replace(/\(/g, 'temp')
    .replace(/\)/g, '(')
    .replace(/temp/g, ')');

  // Convert reversed infix to postfix
  let postfix = infixToPostfix(infix);

  // Reverse the postfix to get prefix
  return postfix.split('').reverse().join('');
}
```

---

## 3. Postfix to Infix Conversion

### Algorithm:

1. Iterate through the postfix expression:
   - If the character is an operand, push it onto the stack.
   - If the character is an operator, pop two operands from the stack, form an infix expression by placing the operator between them, and push it back onto the stack.
2. The final element in the stack is the required infix expression.

---

### Code (Postfix to Infix):

```javascript
function postfixToInfix(postfix) {
  let stack = [];

  for (let char of postfix) {
    if (/[a-zA-Z0-9]/.test(char)) {
      stack.push(char); // Operand, push to stack
    } else {
      let operand2 = stack.pop();
      let operand1 = stack.pop();
      let expression = `(${operand1} ${char} ${operand2})`; // Form infix expression
      stack.push(expression); // Push back to stack
    }
  }

  return stack.pop(); // Final result
}
```

## 4. Postfix to Prefix Conversion

### Algorithm:

1. Reverse the postfix expression.
2. Convert the reversed postfix expression to infix.
3. Reverse the infix expression to get the prefix expression.

---

### Code (Postfix to Prefix):

```javascript
function postfixToPrefix(postfix) {
  // Reverse the postfix expression
  postfix = postfix.split('').reverse().join('');
  // Convert reversed postfix to infix
  let infix = postfixToInfix(postfix);
  // Reverse the infix to get prefix
  return infix.split('').reverse().join('');
}
```

---

## Example Usage:

```javascript
let infix = '(A+B)*(C-D)';
let postfix = infixToPostfix(infix);
let prefix = infixToPrefix(infix);

console.log('Infix to Postfix: ', postfix); // Output: AB+CD-*
console.log('Infix to Prefix: ', prefix); // Output: *+AB-CD
```

## Example Input and Output

### Input:

```
Infix: (A+B)*(C-D)
```

### Output

```
Postfix: AB+CD-*
Prefix: *+AB-CD
```

---

## Summary

| Conversion        | Time Complexity | Space Complexity | Notes                                                            |
| ----------------- | --------------- | ---------------- | ---------------------------------------------------------------- |
| Infix to Postfix  | O(n)            | O(n)             | Requires a stack for operators and operands processing.          |
| Infix to Prefix   | O(n)            | O(n)             | Utilizes infix to postfix and then reverses the result.          |
| Postfix to Infix  | O(n)            | O(n)             | Uses a stack to construct the infix expression.                  |
| Postfix to Prefix | O(n)            | O(n)             | Reverses postfix to infix and then reverses it again for prefix. |

## Resources

[Video Link](https://www.youtube.com/watch?v=4pIc9UBHJtk&list=PLgUwDviBIf0pOd5zvVVSzgpo6BaCpHT9c&index=4&ab_channel=takeUforward)
