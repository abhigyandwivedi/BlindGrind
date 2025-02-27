# Solution to "5. Longest Palindromic Substring"

## Problem Statement

Given a string `s`, return the longest palindromic substring in `s`.

Example:

```
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
```

---

## Approach: Expand Around Center

### Explanation

1. **Expand from Center:** Treat each character (or pair) as a potential center and expand outward.
2. **Track Longest:** Update the longest palindrome found during expansion.

---

## Implementation in Python

```python
def longestPalindrome(s: str) -> str:
    if not s or len(s) == 1:
        return s

    start, end = 0, 0

    def expandAroundCenter(left: int, right: int) -> tuple:
        while left >= 0 and right < len(s) and s[left] == s[right]:
            left -= 1
            right += 1
        return left + 1, right - 1

    for i in range(len(s)):
        # Odd length palindrome
        l1, r1 = expandAroundCenter(i, i)
        if r1 - l1 > end - start:
            start, end = l1, r1

        # Even length palindrome
        l2, r2 = expandAroundCenter(i, i + 1)
        if r2 - l2 > end - start:
            start, end = l2, r2

    return s[start:end + 1]
```

---

## Example Run

Input:

```python
s = "babad"
print(longestPalindrome(s))
```

Output:

```
"bab" (or "aba")
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n^2)`
    
    - Each center expansion takes linear time.
2. **Space Complexity:** `O(1)`
    
    - Constant space used for pointers.

---

## Edge Cases

1. Single character → Return itself.
2. No palindrome → Return first character.
3. Entire string palindrome → Return full string.

---

## Conclusion

Expanding around centers ensures an efficient solution to find the longest palindromic substring with quadratic complexity.