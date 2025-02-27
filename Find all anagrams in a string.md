# Solution to "438. Find All Anagrams in a String"

## Problem Statement

Given two strings `s` and `p`, find all start indices of `p`'s anagrams in `s`.

Example:

```
Input: s = "cbaebabacd", p = "abc"
Output: [0, 6]
```

Explanation:

- The substring starting at index `0` is "cba", which is an anagram of "abc".
- The substring starting at index `6` is "bac", which is an anagram of "abc".

---

## Approach: Sliding Window with Frequency Count

### Explanation

1. **Frequency Count:** Count the frequency of characters in `p`.
2. **Sliding Window:** Maintain a window of size `len(p)` over `s` and update frequencies.
3. **Matching Check:** If the window's frequency matches `p`'s frequency, record the start index.

---

## Implementation in Python

```python
from collections import Counter

def findAnagrams(s, p):
    p_count = Counter(p)
    s_count = Counter()
    result = []

    for i in range(len(s)):
        # Add the current character to the window
        s_count[s[i]] += 1

        # Remove character outside the window
        if i >= len(p):
            if s_count[s[i - len(p)]] == 1:
                del s_count[s[i - len(p)]]
            else:
                s_count[s[i - len(p)]] -= 1

        # Compare counts
        if s_count == p_count:
            result.append(i - len(p) + 1)

    return result
```

---

## Example Run

Input:

```python
s = "cbaebabacd"
p = "abc"
print(findAnagrams(s, p))  # Output: [0, 6]
```

Output:

```
[0, 6]
```

Explanation:

- Anagrams "cba" and "bac" start at indices `0` and `6`.

---

## Complexity Analysis

1. **Time Complexity:** `O(N)`
    
    - Each character is processed once in the sliding window.
2. **Space Complexity:** `O(1)`
    
    - Fixed space for storing character counts.

---

## Edge Cases

1. If `s` or `p` is empty, return `[]`.
2. If `p` is longer than `s`, return `[]`.

---

## Conclusion

This approach efficiently finds all anagram start indices using a sliding window and character counts.