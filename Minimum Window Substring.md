# Solution to "76. Minimum Window Substring"

## Problem Statement

Given two strings `s` and `t`, return the minimum window substring of `s` such that every character in `t` (including duplicates) is included in the window. If there is no such substring, return the empty string `""`.

Example:

```
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
```

---

## Approach: Sliding Window Technique

### Explanation

1. **Sliding Window:** Expand the window by moving the right pointer. Once all characters are covered, move the left pointer to minimize the window.
2. **Character Count:** Use two hash maps to track character counts for `t` and the current window.
3. **Update Minimum:** If a valid window is found, update the minimum window length and start index.

---

## Implementation in Python

```python
from collections import Counter

def minWindow(s: str, t: str) -> str:
    if not s or not t:
        return ""

    t_count = Counter(t)
    current_count = Counter()
    left, min_len, start = 0, float("inf"), 0
    required = len(t_count)
    formed = 0

    for right, char in enumerate(s):
        current_count[char] += 1
        if char in t_count and current_count[char] == t_count[char]:
            formed += 1

        while formed == required:
            if right - left + 1 < min_len:
                min_len = right - left + 1
                start = left

            current_count[s[left]] -= 1
            if s[left] in t_count and current_count[s[left]] < t_count[s[left]]:
                formed -= 1
            left += 1

    return s[start:start + min_len] if min_len != float("inf") else ""
```

---

## Example Run

Input:

```python
s = "ADOBECODEBANC"
t = "ABC"
print(minWindow(s, t))
```

Output:

```
BANC
```

---

## Complexity Analysis

1. **Time Complexity:** `O(S + T)`
    
    - `S` is the length of `s` and `T` is the length of `t`.
    - Each character in `s` is processed once.
2. **Space Complexity:** `O(S + T)`
    
    - Hash maps for character counts.

---

## Edge Cases

1. `s` is empty → Output: `""`
2. `t` is empty → Output: `""`
3. No valid window → Output: `""`

---

## Conclusion

This solution efficiently finds the smallest window containing all characters using the sliding window approach.