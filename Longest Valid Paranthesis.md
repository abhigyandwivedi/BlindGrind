# Solution to "32. Longest Valid Parentheses"

## Problem Statement

Given a string containing just the characters `'('` and `')'`, find the length of the longest valid (well-formed) parentheses substring.

---

## Approach: Dynamic Programming

### Explanation

We can solve this problem using dynamic programming. We maintain a `dp` array where `dp[i]` represents the length of the longest valid parentheses substring ending at index `i`.

### Algorithm Steps

1. Initialize a `dp` array with zeros of the same length as the input string.
2. Iterate through the string starting from index `1`.
3. If `s[i]` is `')'` and it forms a valid pair:
    - If `s[i - 1]` is `'('`, set `dp[i] = dp[i - 2] + 2`.
    - If `s[i - 1]` is `')'` and forms a valid substring, extend the previous valid substring.
4. Track the maximum value in the `dp` array as the result.

### Example Walkthrough

For example, given the input:

```
s = "(()())"
```

1. Initialize `dp` as:

```
dp = [0, 0, 0, 0, 0, 0]
```

1. Iterate through the string:

```
Index 1: '(' → skip
Index 2: ')' → dp[2] = dp[0] + 2 = 2
Index 3: '(' → skip
Index 4: ')' → dp[4] = dp[2] + 2 = 4
Index 5: ')' → dp[5] = dp[3] + 2 + dp[1] = 6
```

1. Result:

```
max(dp) = 6
```

---

## Implementation in Python

```python
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        n = len(s)
        dp = [0] * n
        max_len = 0

        for i in range(1, n):
            if s[i] == ')':
                if s[i - 1] == '(':
                    dp[i] = (dp[i - 2] if i >= 2 else 0) + 2
                elif i - dp[i - 1] > 0 and s[i - dp[i - 1] - 1] == '(':
                    dp[i] = dp[i - 1] + (dp[i - dp[i - 1] - 2] if i - dp[i - 1] >= 2 else 0) + 2
                max_len = max(max_len, dp[i])

        return max_len
```

---

## Example Run

Input:

```python
s = "(()())"
solution = Solution()
print(solution.longestValidParentheses(s))
```

Output:

```
6
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - We iterate through the string once, where `n` is the length of the string.
2. **Space Complexity:** `O(n)`
    
    - Extra space is used for the `dp` array.

---

## Edge Cases

1. Empty string → Result: `0`
2. Only opening or closing brackets → Result: `0`
3. Nested valid parentheses → Result: length of the valid substring

---

## Conclusion

This solution efficiently finds the longest valid parentheses substring using dynamic programming with linear time complexity and linear space complexity.