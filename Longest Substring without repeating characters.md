# Solution to "3. Longest Substring Without Repeating Characters"

## Problem Statement

Given a string `s`, find the length of the longest substring without repeating characters.

Example:

```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

---

## Approach: Sliding Window Technique

### Explanation

1. **Use a HashSet:** Maintain a set to track characters in the current window.
2. **Expand the window:** Move the right pointer to include new characters.
3. **Shrink the window:** If a character repeats, move the left pointer until the window is valid again.
4. **Track the maximum length:** Update the result whenever a longer valid substring is found.

---

## Implementation in Python

```python
def lengthOfLongestSubstring(s):
    char_set = set()
    left = 0
    max_length = 0

    for right in range(len(s)):
        while s[right] in char_set:
            char_set.remove(s[left])
            left += 1
        char_set.add(s[right])
        max_length = max(max_length, right - left + 1)

    return max_length

# Example usage
# s = "abcabcbb"
# print(lengthOfLongestSubstring(s))  # Output: 3
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)` where `n` is the length of the string.
    - Each character is processed once by the right pointer and once by the left pointer.
2. **Space Complexity:** `O(min(n, m))` where `m` is the character set size.
    - The set stores characters currently in the window.

---

## Example Run

Input:

```
"abcabcbb"
```

Output:

```
3
```

---

## Edge Cases

1. Empty string: `s = ""` → Output: `0`
2. All unique characters: `s = "abcdef"` → Output: `6`
3. Single character: `s = "bbbb"` → Output: `1`

---

## Conclusion

This solution efficiently finds the longest substring without repeating characters using the sliding window technique.