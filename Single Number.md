# Solution to "136. Single Number"

## Problem Statement

Given a non-empty array of integers `nums`, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use constant extra space.

---

## Approach: Bit Manipulation (XOR)

### Explanation

We can efficiently find the single number using the XOR operation.

1. **Properties of XOR:**
    
    - `a ^ a = 0` (any number XORed with itself is `0`)
    - `a ^ 0 = a` (any number XORed with `0` remains unchanged)
    - XOR is commutative and associative: `a ^ b ^ c = c ^ a ^ b`
2. **Approach:**
    
    - XOR all numbers together.
    - Pairs of duplicate numbers will cancel out (`x ^ x = 0`).
    - The remaining value will be the single number.

### Example Walkthrough

For example, given the array:

```
nums = [4, 1, 2, 1, 2]
```

1. Perform XOR operation step-by-step:

```
4 ^ 1 ^ 2 ^ 1 ^ 2
```

1. Simplifying:

```
(4 ^ (1 ^ 1) ^ (2 ^ 2)) = 4 ^ 0 ^ 0 = 4
```

The single number is `4`.

---

## Implementation in Python

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        result = 0
        for num in nums:
            result ^= num
        return result
```

---

## Example Run

Input:

```python
nums = [4, 1, 2, 1, 2]
solution = Solution()
print(solution.singleNumber(nums))
```

Output:

```
4
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - We iterate through the array once, where `n` is the length of `nums`.
2. **Space Complexity:** `O(1)`
    
    - No extra space is used apart from a few variables.

---

## Edge Cases

1. If the array has only one element, return that element.
2. If all elements appear twice except one, it works as expected.

---

## Conclusion

This efficient solution uses bit manipulation to find the single number with linear time complexity and constant space complexity.