# Solution to "49. Group Anagrams"

## Problem Statement

Given an array of strings `strs`, group the anagrams together. You can return the answer in any order.

---

## Approach: Hash Map with Sorted Key

### Explanation

We can use a hash map where the key is the sorted version of each string and the value is a list of strings that match that sorted key.

### Algorithm Steps

1. Initialize an empty dictionary `anagram_map`.
2. For each string `s` in `strs`:
    - Sort the characters in `s`.
    - Use the sorted string as a key.
    - Append `s` to the list corresponding to that key.
3. Return the values of the hash map.

---

## Implementation in Python

```python
from collections import defaultdict

class Solution:
    def groupAnagrams(self, strs: list[str]) -> list[list[str]]:
        anagram_map = defaultdict(list)

        for s in strs:
            sorted_key = ''.join(sorted(s))
            anagram_map[sorted_key].append(s)

        return list(anagram_map.values())
```

---

## Example Run

Input:

```python
strs = ["eat", "tea", "tan", "ate", "nat", "bat"]
solution = Solution()
print(solution.groupAnagrams(strs))
```

Output:

```
[['eat', 'tea', 'ate'], ['tan', 'nat'], ['bat']]
```

Explanation:

- Words like "eat", "tea", and "ate" have the same sorted form `"aet"` and are grouped together.

---

## Complexity Analysis

1. **Time Complexity:** `O(n * k log k)`
    
    - `n` is the number of strings, and `k` is the maximum length of a string.
    - Sorting each string takes `O(k log k)`.
2. **Space Complexity:** `O(nk)`
    
    - Storage for the hash map and grouped lists.

---

## Edge Cases

1. Empty list → Return an empty list.
2. Single word → Return a list with one group containing the word.
3. All unique words → Each word forms its own group.

---

## Conclusion

This solution efficiently groups anagrams using a hash map and a sorted key approach.