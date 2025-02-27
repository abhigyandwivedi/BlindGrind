# Solution to "150. Evaluate Reverse Polish Notation"

## Problem Statement

Given an array of strings `tokens` representing an arithmetic expression in Reverse Polish Notation (RPN), evaluate the expression.

Example:

```
Input: tokens = ["2", "1", "+", "3", "*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9

Input: tokens = ["4", "13", "5", "/", "+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
```

---

## Approach: Stack-Based Evaluation

### Explanation

1. **Use a Stack:** Traverse the `tokens` array and push operands onto the stack.
2. **Evaluate Operators:** When encountering an operator (`+`, `-`, `*`, `/`), pop the top two operands, perform the operation, and push the result back onto the stack.
3. **Final Result:** After processing all tokens, the stack will contain the final result.

---

## Implementation in Python

```python
def evalRPN(tokens):
    stack = []

    for token in tokens:
        if token not in {"+", "-", "*", "/"}:
            stack.append(int(token))
        else:
            b = stack.pop()
            a = stack.pop()
            if token == "+":
                stack.append(a + b)
            elif token == "-":
                stack.append(a - b)
            elif token == "*":
                stack.append(a * b)
            elif token == "/":
                # Truncate towards zero
                stack.append(int(a / b))

    return stack[0]

# Example usage
print(evalRPN(["2", "1", "+", "3", "*"]))     # Output: 9
print(evalRPN(["4", "13", "5", "/", "+"]))   # Output: 6
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)` where `n` is the number of tokens. Each token is processed once.
2. **Space Complexity:** `O(n)` for the stack holding intermediate results.

---

## Example Run

Input:

```python
print(evalRPN(["2", "1", "+", "3", "*"]))     # Output: 9
print(evalRPN(["4", "13", "5", "/", "+"]))   # Output: 6
```

---

## Edge Cases

1. Single operand: `["3"]` → Output: `3`
2. Negative results: `["4", "5", "-"]` → Output: `-1`
3. Division truncation: `["10", "3", "/"]` → Output: `3` (truncated towards zero)

---

## Conclusion

This solution efficiently evaluates RPN expressions using a stack, ensuring linear time complexity for processing all tokens.