# Solution to "179. Largest Number"

## Problem Statement

Given a list of non-negative integers `nums`, arrange them such that they form the largest number.

Example:

```
Input: nums = [10, 2]
Output: "210"

Input: nums = [3, 30, 34, 5, 9]
Output: "9534330"
```

---

## Approach: Custom Sorting

### Explanation

1. **Convert to Strings:** Convert all integers in `nums` to strings for easy comparison.
2. **Custom Sort:** Sort the strings based on the concatenation order:
    - For two strings `x` and `y`, compare `x + y` and `y + x`.
    - If `x + y` > `y + x`, `x` should come before `y`.
3. **Edge Case:** If the result starts with `0`, return "0" (e.g., `[0, 0, 0]` should return "0").

---

## Implementation in Python

```python
from functools import cmp_to_key

def largestNumber(nums):
    # Convert integers to strings
    nums_str = list(map(str, nums))

    # Custom comparator
    def compare(x, y):
        if x + y > y + x:
            return -1
        elif x + y < y + x:
            return 1
        else:
            return 0

    # Sort using the custom comparator
    nums_str.sort(key=cmp_to_key(compare))

    # Join the sorted array
    result = ''.join(nums_str)

    # Handle edge case for leading zeros
    return '0' if result[0] == '0' else result

# Example usage
example1 = [10, 2]
example2 = [3, 30, 34, 5, 9]
print(largestNumber(example1))  # Output: "210"
print(largestNumber(example2))  # Output: "9534330"
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n log n)` - Sorting takes `O(n log n)` time with the custom comparator.
2. **Space Complexity:** `O(n)` - To store the string representations of the numbers.

---

## Example Run

Input:

```
nums = [3, 30, 34, 5, 9]
```

Output:

```
"9534330"
```

Input:

```
nums = [10, 2]
```

Output:

```
"210"
```

---

## Edge Cases

1. Single element returns itself.
2. All zeros return "0".
3. Large inputs work efficiently due to sorting-based approach.

---

## Conclusion

This solution leverages custom string sorting to form the largest possible number efficiently.