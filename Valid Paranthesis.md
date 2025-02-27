#ValidParanthesis  #stack #validparanthesispython  
Time Complexity:O(n)
Space Complexity:O(n)

```python

from collections import deque

def is_valid(self, s: str) -> bool:
    stack = deque()
    mapping = {")": "(", "}": "{", "]": "["}  # Matching pairs
    for char in s:
        if char in mapping:
            top_element = (
                stack.pop() if stack else "#"
            )  # Pop or set a dummy value
            if mapping[char] != top_element:
                return False  # Mismatch case
        else:
            stack.append(char)
    return not stack

print(is_valid(None,"()"))
print(is_valid(None,"()[]{}"))
print(is_valid(None,"(]"))
print(is_valid(None,"([])"))


```
# Solution to "20. Valid Parentheses"

## Problem Statement

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

Example:

```
Input: s = "()[]{}"
Output: true

Input: s = "(]"
Output: false
```

---

## Approach: Stack-based Solution

### Explanation

1. **Use a Stack:**
    - Push open brackets (`(`, `{`, `[`) onto the stack.
    - When encountering a closing bracket (`)`, `}`, `]`), check the top of the stack:
        - If the top is the matching opening bracket, pop it.
        - Otherwise, the string is invalid.
2. **Final Check:**
    - If the stack is empty after processing the string, the input is valid.

---

## Implementation in Python

```python
def isValid(s):
    stack = []
    bracket_map = {')': '(', '}': '{', ']': '['}

    for char in s:
        if char in bracket_map:
            top_element = stack.pop() if stack else '#'
            if bracket_map[char] != top_element:
                return False
        else:
            stack.append(char)

    return not stack

# Example usage
example1 = "()[]{}"
example2 = "(]"
print(isValid(example1))  # Output: True
print(isValid(example2))  # Output: False
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)` - We traverse the string once, performing constant-time stack operations.
2. **Space Complexity:** `O(n)` - In the worst case, all opening brackets are stored in the stack.

---

## Example Run

Input:

```
s = "()[]{}"
```

Output:

```
True
```

Input:

```
s = "(]"
```

Output:

```
False
```

---

## Edge Cases

1. Empty string returns `True`.
2. Single closing bracket returns `False`.
3. Mixed but improperly nested brackets return `False`.

---

## Conclusion

This solution efficiently validates parentheses using a stack, ensuring correct order and type matching.