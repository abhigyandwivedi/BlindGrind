# Solution to "224. Basic Calculator"

## Problem Statement

Implement a basic calculator to evaluate a simple expression string containing non-negative integers, `+`, `-`, `(`, `)`, and empty spaces. The expression is guaranteed to be valid.

Example:

```
Input: "1 + (2 - (3 + 4))"
Output: -4
```

---

## Approach: Stack-Based Evaluation

### Explanation

1. **Use a Stack:** Push results of sub-expressions into a stack.
2. **Handle Parentheses:** When encountering `(`, push the current result and sign. When encountering `)`, evaluate the expression inside.
3. **Evaluate:** Add and subtract values based on signs.

---

## Implementation in Python

```python
def calculate(s: str) -> int:
    stack = []
    num, sign, result = 0, 1, 0

    for char in s:
        if char.isdigit():
            num = num * 10 + int(char)
        elif char in ['+', '-']:
            result += sign * num
            sign = 1 if char == '+' else -1
            num = 0
        elif char == '(':
            stack.append(result)
            stack.append(sign)
            result, sign = 0, 1
        elif char == ')':
            result += sign * num
            result *= stack.pop()  # sign before '('
            result += stack.pop()  # result before '('
            num = 0

    return result + sign * num
```

---

## Example Run

Input:

```python
expression = "1 + (2 - (3 + 4))"
print(calculate(expression))
```

Output:

```
-4
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each character is processed once.
2. **Space Complexity:** `O(n)`
    
    - Stack stores intermediate results.

---

## Edge Cases

1. Empty string → `0`
2. Only numbers → Sum of numbers
3. Nested parentheses → Properly evaluated

---

## Conclusion

Using a stack ensures correct evaluation of nested expressions while maintaining linear complexity.