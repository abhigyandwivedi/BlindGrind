# Solution to "8. String to Integer (atoi)"

## Problem Statement

Implement the `myAtoi(string s)` function, which converts a string to a 32-bit signed integer (similar to the C/C++ `atoi` function).

Example:

```
Input: s = "  -42"
Output: -42
```

---

## Approach: Step-by-Step Parsing

### Explanation

1. **Trim Whitespaces:** Ignore leading and trailing spaces.
2. **Handle Sign:** Check for '+' or '-'.
3. **Convert Digits:** Read characters until a non-digit appears.
4. **Clamp Result:** Ensure the result is within the 32-bit signed integer range `[-2^31, 2^31 - 1]`.

---

## Implementation in Python

```python
def myAtoi(s: str) -> int:
    s = s.lstrip()  # Remove leading whitespaces
    if not s:
        return 0

    sign = 1
    start = 0

    # Handle sign
    if s[0] == '-':
        sign = -1
        start = 1
    elif s[0] == '+':
        start = 1

    # Convert digits
    result = 0
    while start < len(s) and s[start].isdigit():
        result = result * 10 + int(s[start])
        start += 1

    result *= sign

    # Clamp to 32-bit signed integer range
    int_min, int_max = -2**31, 2**31 - 1
    if result < int_min:
        return int_min
    if result > int_max:
        return int_max

    return result
```

---

## Example Run

Input:

```python
s = "  -42"
print(myAtoi(s))
```

Output:

```
-42
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each character is processed once.
2. **Space Complexity:** `O(1)`
    
    - Only a few variables are used.

---

## Edge Cases

1. Empty string → Return `0`.
2. Invalid input like "words and 987" → Return `0`.
3. Out-of-bounds values → Clamp to `[-2^31, 2^31 - 1]`.

---

## Conclusion

This approach efficiently converts a string to an integer while handling signs, non-digit characters, and integer overflow.