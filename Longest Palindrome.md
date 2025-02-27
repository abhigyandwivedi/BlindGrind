# Solution to "409. Longest Palindrome"

## Problem Statement

Given a string `s` which consists of lowercase or uppercase letters, return the length of the longest palindrome that can be built with those letters.

Example:

```
Input: s = "abccccdd"
Output: 7
Explanation: One possible palindrome is "dccaccd".
```

---

## Approach: Using HashMap (Counter)

### Explanation

1. Count the frequency of each character using a hash map.
2. For each character, add the largest even count to the palindrome length.
3. If there is any character with an odd count, we can place one in the middle.

---

## Implementation in Python

```python
from collections import Counter

def longestPalindrome(s: str) -> int:
    char_count = Counter(s)
    length = 0
    odd_found = False

    for count in char_count.values():
        length += count // 2 * 2
        if count % 2 == 1:
            odd_found = True

    return length + 1 if odd_found else length

# Example usage
s = "abccccdd"
print(longestPalindrome(s))  # Output: 7
```

---

## Example Run

Input:

```python
s = "aabbccd"
print(longestPalindrome(s))  # Output: 7
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)` - where `n` is the length of the string `s`. We traverse the string once to count frequencies.
2. **Space Complexity:** `O(1)` - Since the hash map stores at most 52 characters (26 lowercase + 26 uppercase).

---

## Edge Cases

1. Single character: `s = "a"` → Output: `1`
2. All even counts: `s = "aabb"` → Output: `4`
3. All odd counts: `s = "abc"` → Output: `1`

---

## Conclusion

This solution efficiently calculates the length of the longest possible palindrome by leveraging character frequencies.