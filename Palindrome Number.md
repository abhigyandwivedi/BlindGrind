# 9. Palindrome Number

## Problem Statement

Given an integer `x`, return `true` if `x` is a palindrome integer.

An integer is a **palindrome** when it reads the same backward as forward.

### Example

**Input:**

```
x = 121
```

**Output:**

```
true
```

**Explanation:** 121 reads the same backward as forward.

**Input:**

```
x = -121
```

**Output:**

```
false
```

**Explanation:** From left to right, it reads -121. From right to left, it becomes 121-. Negative numbers are not palindromic.

---

## Approach 1: Reverse the Integer

### Idea

To determine if an integer `x` is a palindrome:

1. If `x` is negative, immediately return `false` (negative numbers cannot be palindromic).
2. Reverse the digits of `x`.
3. Compare the reversed number with the original number.
4. If they are the same, return `true`; otherwise, return `false`.

---

## Implementation (Python)

```python
def isPalindrome(x: int) -> bool:
    if x < 0:
        return False

    # Convert to string and reverse
    original = str(x)
    reversed_str = original[::-1]

    return original == reversed_str
```

---

## Example Run

For `x = 121`:

1. Convert `121` to string → `'121'`.
2. Reverse the string → `'121'`.
3. Compare original `'121'` with reversed `'121'` → They match.
4. Return `true`.

For `x = -121`:

1. Since `x` is negative, return `false` immediately.

---

## Complexity Analysis

### Time Complexity

- **O(n):** where `n` is the number of digits in `x`.
- Reversing the string takes linear time.

### Space Complexity

- **O(1):** Constant space used for variables.

---

## Edge Cases

1. `x = 0` → Output: `true` (Single-digit numbers are palindromic).
2. `x = -121` → Output: `false` (Negative numbers are not palindromic).
3. `x = 10` → Output: `false` (Reversed is `01`).

---

## Conclusion

This solution efficiently checks if an integer is a palindrome by reversing the integer and comparing it with the original. It works for both positive and zero values while excluding negative cases by design.