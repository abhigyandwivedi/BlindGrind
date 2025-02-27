# Solution to "13. Roman to Integer"

## Problem Statement

Given a Roman numeral, convert it to an integer.

---

## Approach: Hash Map and Iteration

### Explanation

1. **Use a Hash Map:** Map each Roman numeral to its integer value.
2. **Traverse the String:**
    - If the current numeral is smaller than the next one, subtract its value.
    - Otherwise, add its value.

---

## Implementation in Python

```python
class Solution:
    def romanToInt(self, s: str) -> int:
        roman_map = {
            'I': 1, 'V': 5, 'X': 10, 'L': 50,
            'C': 100, 'D': 500, 'M': 1000
        }
        total = 0
        n = len(s)

        for i in range(n):
            if i < n - 1 and roman_map[s[i]] < roman_map[s[i + 1]]:
                total -= roman_map[s[i]]
            else:
                total += roman_map[s[i]]

        return total
```

---

## Example Run

Input:

```python
s = "MCMXCIV"
solution = Solution()
print(solution.romanToInt(s))
```

Output:

```
1994
```

Explanation:

- M = 1000, CM = 900, XC = 90, IV = 4 → Total = 1994

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - We traverse the string once.
2. **Space Complexity:** `O(1)`
    
    - Constant space for the hash map.

---

## Edge Cases

1. Single character → Corresponding integer value.
2. Decreasing order → Sum all values.
3. Increasing order → Subtract where necessary.

---

## Conclusion

This approach efficiently converts Roman numerals to integers using a linear pass and conditional logic.