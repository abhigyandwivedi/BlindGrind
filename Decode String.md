# Solution to "394. Decode String"

## Problem Statement

Given an encoded string, return its decoded string. The encoding rule is: `k[encoded_string]`, where the encoded_string inside the square brackets is repeated exactly `k` times.

---

## Approach: Stack

### Explanation

1. Use a stack to keep track of characters, numbers, and brackets.
2. When encountering a digit, build the multiplier.
3. When encountering `[`, push the current string and multiplier onto the stack.
4. When encountering `]`, pop from the stack, build the repeated string, and continue.
5. Finally, join all characters to form the decoded string.

### Algorithm Steps

1. **Stack Initialization:** Use a stack to store characters and counts.
2. **Iteration:**
    - If a digit is found, accumulate it as the multiplier.
    - If `[` is found, push the current string and multiplier onto the stack.
    - If `]` is found, pop the last string and multiplier, repeat the string, and append it back.
    - Otherwise, append characters to the current string.
3. **Result Formation:** Join characters and return the final decoded string.

---

## Implementation in Python

```python
class Solution:
    def decodeString(self, s: str) -> str:
        stack = []
        current_string = ''
        current_num = 0

        for char in s:
            if char.isdigit():
                current_num = current_num * 10 + int(char)
            elif char == '[':
                stack.append((current_string, current_num))
                current_string, current_num = '', 0
            elif char == ']':
                last_string, num = stack.pop()
                current_string = last_string + current_string * num
            else:
                current_string += char

        return current_string
```

---

## Example Run

Input:

```python
s = "3[a2[bc]]"
solution = Solution()
print(solution.decodeString(s))
```

Output:

```
"abcbcabcbcabcbc"
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each character is processed once, and string multiplication takes linear time.
2. **Space Complexity:** `O(n)`
    
    - Stack stores intermediate strings and multipliers.

---

## Edge Cases

1. Single-level encoding → `3[a]` → `"aaa"`.
2. Nested encoding → `2[3[a]b]` → `"aaabaaab"`.
3. Empty string → `""` → `""`.

---

## Conclusion

This solution efficiently decodes a given string using a stack-based approach to handle nested and sequential encoding.