# Solution to "844. Backspace String Compare"

## Problem Statement

Given two strings `s` and `t`, return `true` if they are equal when both are typed into empty text editors. `'#'` means a backspace character.

---

## Approach: Stack Simulation

### Explanation

1. **Use a Stack:** Simulate the backspace operation using a stack.
2. **Push and Pop:**
    - If the character is not `#`, push it onto the stack.
    - If the character is `#` and the stack is not empty, pop the last character.
3. **Compare Stacks:** After processing both strings, compare the final stacks.

---

## Implementation in Python

```python
class Solution:
    def backspaceCompare(self, s: str, t: str) -> bool:
        def buildString(string):
            stack = []
            for char in string:
                if char != '#':
                    stack.append(char)
                elif stack:
                    stack.pop()
            return ''.join(stack)

        return buildString(s) == buildString(t)
```

---

## Example Run

Input:

```python
s = "ab#c"
t = "ad#c"
solution = Solution()
print(solution.backspaceCompare(s, t))
```

Output:

```
True
```

Explanation:

- Both `s` and `t` become "ac" after processing backspaces.

---

## Complexity Analysis

1. **Time Complexity:** `O(n + m)`
    
    - We process each string once.
2. **Space Complexity:** `O(n + m)`
    
    - Stacks store processed characters.

---

## Edge Cases

1. Both strings empty → `True`
2. Only `#` characters → `True`
3. Mismatched strings after processing → `False`

---

## Conclusion

This stack-based approach efficiently compares two strings after considering backspace operations.