# Solution to "424. Longest Repeating Character Replacement"

## Problem Statement

Given a string `s` and an integer `k`, you can choose any character and change it to any other character at most `k` times. Return the length of the longest substring containing the same letter after performing the replacement.

---

## Approach: Sliding Window

### Explanation

We use a sliding window approach to find the longest substring with the same character after performing at most `k` replacements.

### Algorithm Steps

1. **Initialize:** Start with two pointers, `left` and `right`, both at the beginning of the string.
2. **Frequency Count:** Use a hashmap to count the frequency of characters within the window.
3. **Expand Window:** Expand the window by moving `right` and updating the count.
4. **Shrink Window:** If the window size minus the count of the most frequent character exceeds `k`, shrink the window by moving `left`.
5. **Track Maximum Length:** Keep track of the longest valid substring.

---

## Implementation in Python

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        count = {}
        left = 0
        max_count = 0
        max_length = 0

        for right in range(len(s)):
            count[s[right]] = count.get(s[right], 0) + 1
            max_count = max(max_count, count[s[right]])

            if (right - left + 1) - max_count > k:
                count[s[left]] -= 1
                left += 1

            max_length = max(max_length, right - left + 1)

        return max_length
```

---

## Example Run

Input:

```python
s = "AABABBA"
k = 1
solution = Solution()
print(solution.characterReplacement(s, k))
```

Output:

```
4
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - `n` is the length of the string. Each character is processed once.
2. **Space Complexity:** `O(1)`
    
    - The hashmap stores character counts, bounded by the alphabet size (`O(26)`).

---

## Edge Cases

1. `s = ""`, `k = 0` → Output: `0`.
2. All identical characters → Output: Length of `s`.
3. `k` larger than string length → Output: Length of `s`.

---

## Conclusion

This solution efficiently finds the longest substring with the same character after up to `k` replacements using the sliding window approach.