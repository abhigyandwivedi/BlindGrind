# 647. Palindromic Substrings

## Problem Statement

Given a string `s`, return _the number of palindromic substrings in it_.
A string is a **palindrome** when it reads the same backward as forward.
A **substring** is a contiguous sequence of characters within the string.

### Example 1:

```text
Input: s = "abc"
Output: 3
Explanation: Three palindromic substrings are "a", "b", and "c".
```

### Example 2:

```text
Input: s = "aaa"
Output: 6
Explanation: Six palindromic substrings are "a", "a", "a", "aa", "aa", and "aaa".
```

---

## Solution Approach

We'll use the **expand around center** approach. The idea is to treat each character (and pair of characters) as a potential center and expand outward while counting palindromic substrings.

For each character in the string, we'll:

1. Expand around the character (odd-length palindromes).
2. Expand around the gap between the character and the next one (even-length palindromes).

### Implementation in Python

```python
class Solution:
    def countSubstrings(self, s: str) -> int:
        def expand_around_center(left: int, right: int) -> int:
            count = 0
            while left >= 0 and right < len(s) and s[left] == s[right]:
                count += 1
                left -= 1
                right += 1
            return count

        total_count = 0
        for i in range(len(s)):
            # Count odd-length palindromes
            total_count += expand_around_center(i, i)
            # Count even-length palindromes
            total_count += expand_around_center(i, i + 1)

        return total_count
```

---

## Example Run

For `s = "aaa"`:

1. Single character palindromes: `"a"`, `"a"`, `"a"` → Count = 3
2. Two-character palindromes: `"aa"`, `"aa"` → Count = 2
3. Three-character palindrome: `"aaa"` → Count = 1

Total count = 3 + 2 + 1 = 6

---

## Complexity Analysis

### Time Complexity

- **O(n^2)**
    - For each character, we expand outward while checking for palindromic properties.
    - In the worst case, each expansion takes _O(n)_ time, and we perform this for each character, resulting in _O(n^2)_ overall.

### Space Complexity

- **O(1)**
    - We use constant extra space, as no additional data structures are required apart from variables.

---

## Alternative Approaches

### 1. Dynamic Programming Approach

Another approach to solve this problem is by using dynamic programming. We'll use a 2D table `dp[i][j]` where:

- `dp[i][j]` is `True` if the substring `s[i..j]` is a palindrome.

**Approach:**

1. All single characters are palindromic (`dp[i][i] = True`).
2. Check pairs of characters: `dp[i][i+1] = (s[i] == s[i+1])`.
3. For longer substrings, `dp[i][j] = (s[i] == s[j] and dp[i+1][j-1])`.

**Python Implementation:**

```python
class Solution:
    def countSubstrings(self, s: str) -> int:
        n = len(s)
        dp = [[False] * n for _ in range(n)]
        count = 0

        # Iterate over the length of substring
        for length in range(1, n + 1):
            for i in range(n - length + 1):
                j = i + length - 1
                if s[i] == s[j]:
                    if length == 1 or length == 2:
                        dp[i][j] = True
                    else:
                        dp[i][j] = dp[i + 1][j - 1]

                if dp[i][j]:
                    count += 1

        return count
```

**Example Run:** For `s = "aaa"`, the `dp` table would look like this:

```
    a   a   a
  ----------------
a | T   T   T
  |     T   T
a |         T
```

Total palindromic substrings = 6.

**Time Complexity:** `O(n^2)`

- We iterate through all pairs `(i, j)` where `i <= j`.

**Space Complexity:** `O(n^2)`

- We maintain a 2D DP table of size `n x n`.

---

## Conclusion

The "expand around center" method offers an optimal solution for this problem, balancing efficiency and simplicity. The dynamic programming approach, while slightly more complex, provides an alternative solution that can be useful for understanding palindromic substring patterns more clearly.