# Solution to "242. Valid Anagram"

## Problem Statement

Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

Example:

```
Input: s = "anagram", t = "nagaram"
Output: true
```

---

## Approach: Hash Map

### Explanation

1. **Count Characters:** Use a hash map (dictionary in Python) to count occurrences of each character in `s`.
2. **Compare with `t`:** Subtract the counts based on characters in `t`.
3. **Check Counts:** If all counts are zero, it's an anagram.

---

## Implementation in Python

```python
def isAnagram(s, t):
    if len(s) != len(t):
        return False

    count = {}

    for char in s:
        count[char] = count.get(char, 0) + 1

    for char in t:
        if char not in count or count[char] == 0:
            return False
        count[char] -= 1

    return True

# Example usage
s = "anagram"
t = "nagaram"
result = isAnagram(s, t)
print(result)
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)` - We traverse both strings once.
2. **Space Complexity:** `O(1)` - The hash map holds a fixed number of characters (26 lowercase letters).

---

## Example Run

Input:

```
s = "anagram", t = "nagaram"
```

Output:

```
true
```

---

## Edge Cases

1. If the lengths differ, return `false`.
2. If both strings are empty, return `true`.

---

## Conclusion

This solution efficiently checks if two strings are anagrams using character counts.