# Solution to "14. Longest Common Prefix"

## Problem Statement

Given an array of strings `strs`, find the longest common prefix string among them.

If there is no common prefix, return an empty string `""`.

---

## Approach: Horizontal Scanning

### Explanation

We compare each string with the current prefix and shorten the prefix until it matches all strings.

### Algorithm Steps

1. **Initialize:** Set the first string as the initial prefix.
2. **Iterate:** Compare the prefix with each string.
3. **Update:** Trim the prefix if a mismatch occurs.
4. **Return:** If the prefix becomes empty, return `""`.

---

## Implementation in Python

```python
class Solution:
    def longestCommonPrefix(self, strs: list[str]) -> str:
        if not strs:
            return ""

        prefix = strs[0]
        for s in strs[1:]:
            while not s.startswith(prefix):
                prefix = prefix[:-1]
                if not prefix:
                    return ""
        return prefix
```

---

## Example Run

Input:

```python
strs = ["flower", "flow", "flight"]
solution = Solution()
print(solution.longestCommonPrefix(strs))
```

Output:

```
"fl"
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n * m)`
    
    - `n` is the number of strings.
    - `m` is the length of the shortest string.
2. **Space Complexity:** `O(1)`
    
    - Constant space used for the prefix variable.

---

## Edge Cases

1. Empty list → Output: `""`.
2. No common prefix → Output: `""`.
3. Single string → Output: The string itself.

---

## Conclusion

This solution efficiently finds the longest common prefix by iteratively comparing strings and shortening the prefix as needed.