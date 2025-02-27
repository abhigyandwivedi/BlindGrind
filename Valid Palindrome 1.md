# Solution to "125. Valid Palindrome"

## Problem Statement

Given a string `s`, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

Example:

```
Input: s = "A man, a plan, a canal: Panama"
Output: true
```

---

## Approach: Two Pointers

### Explanation

1. **Clean the String:** Convert `s` to lowercase and keep only alphanumeric characters.
2. **Use Two Pointers:** Start one pointer at the beginning and another at the end of the string.
3. **Check Palindrome:** Compare characters from both ends, moving inward.

---

## Implementation in Python

```python
def isPalindrome(s):
    cleaned = ''.join(char.lower() for char in s if char.isalnum())
    left, right = 0, len(cleaned) - 1

    while left < right:
        if cleaned[left] != cleaned[right]:
            return False
        left += 1
        right -= 1

    return True

# Example usage
s = "A man, a plan, a canal: Panama"
result = isPalindrome(s)
print(result)
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)` - We traverse the string once to clean it and once more for comparison.
2. **Space Complexity:** `O(n)` - The cleaned string takes additional space.

---

## Example Run

Input:

```
s = "A man, a plan, a canal: Panama"
```

Output:

```
true
```

---

## Edge Cases

1. An empty string returns `true`.
2. Strings with only non-alphanumeric characters return `true`.

---

## Conclusion

This solution efficiently checks if a string is a valid palindrome by ignoring cases and non-alphanumeric characters.