# Solution to "383. Ransom Note"

## Problem Statement

Given two strings `ransomNote` and `magazine`, return `true` if `ransomNote` can be constructed from the letters of `magazine` and `false` otherwise.

Each letter in `magazine` can only be used once in `ransomNote`.

Example:

```
Input: ransomNote = "aa", magazine = "ab"
Output: false

Input: ransomNote = "aa", magazine = "aab"
Output: true
```

---

## Approach: Frequency Counting

### Explanation

1. **Count Characters:** Use a dictionary to count occurrences of each character in `magazine`.
2. **Check Availability:** For each character in `ransomNote`, check if it exists in the `magazine` count with sufficient frequency.
3. **Decision:** If any character is insufficient, return `false`; otherwise, return `true`.

---

## Implementation in Python

```python
from collections import Counter

def canConstruct(ransomNote, magazine):
    ransom_count = Counter(ransomNote)
    magazine_count = Counter(magazine)

    for char, count in ransom_count.items():
        if magazine_count[char] < count:
            return False

    return True

# Example usage
# ransomNote = "aa"
# magazine = "aab"
# print(canConstruct(ransomNote, magazine))  # Output: True
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n + m)` where `n` is the length of `ransomNote` and `m` is the length of `magazine`.
    - We count characters in both strings and iterate through the `ransomNote` count.
2. **Space Complexity:** `O(1)` as the character count dictionary is limited to 26 lowercase English letters.

---

## Example Run

Input:

```
ransomNote = "aa"
magazine = "aab"
```

Output:

```
True
```

---

## Edge Cases

1. Empty ransom note: `ransomNote = "", magazine = "abc"` → Output: `True`
2. Empty magazine: `ransomNote = "abc", magazine = ""` → Output: `False`
3. Exact match: `ransomNote = "abc", magazine = "abc"` → Output: `True`

---

## Conclusion

This solution efficiently determines whether the ransom note can be constructed from the magazine using character frequency counting.