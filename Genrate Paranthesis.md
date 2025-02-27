# Solution to "22. Generate Parentheses"

## Problem Statement

Given `n` pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

---

## Approach: Backtracking

### Explanation

We can generate all valid combinations using a backtracking approach by maintaining counts of open and close parentheses.

### Algorithm Steps

1. **Base Case:**
    
    - If the current string has `2 * n` characters, add it to the result.
2. **Recursive Case:**
    
    - Add an open parenthesis if `open < n`.
    - Add a close parenthesis if `close < open`.

---

## Implementation in Python

```python
class Solution:
    def generateParenthesis(self, n: int) -> list[str]:
        result = []

        def backtrack(s='', open=0, close=0):
            if len(s) == 2 * n:
                result.append(s)
                return

            if open < n:
                backtrack(s + '(', open + 1, close)

            if close < open:
                backtrack(s + ')', open, close + 1)

        backtrack()
        return result
```

---

## Example Run

Input:

```python
n = 3
solution = Solution()
print(solution.generateParenthesis(n))
```

Output:

```
['((()))', '(()())', '(())()', '()(())', '()()()']
```

---

## Complexity Analysis

1. **Time Complexity:** `O(4^n / sqrt(n))`
    
    - Each valid sequence takes linear time to build.
2. **Space Complexity:** `O(4^n / sqrt(n))`
    
    - Extra space for recursion stack and result storage.

---

## Edge Cases

1. `n = 0` → Output: `[]` (No parentheses).
2. `n = 1` → Output: `['()']`.

---

## Conclusion

This solution efficiently generates all combinations of well-formed parentheses using backtracking, achieving optimal complexity for this type of problem.