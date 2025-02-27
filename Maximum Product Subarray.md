# Solution to "152. Maximum Product Subarray"

## Problem Statement

Given an integer array `nums`, find the contiguous subarray within an array (containing at least one number) which has the largest product.

---

## Approach: Dynamic Programming with Two Variables

### Explanation

We use two variables, `max_product` and `min_product`, to track the maximum and minimum product ending at the current index. This is because a negative number can turn the smallest product into the largest when multiplied.

### Algorithm Steps

1. Initialize `max_product`, `min_product`, and `result` with the first element of `nums`.
2. Iterate through `nums` from index `1` to `n-1`.
3. For each element:
    - Store `temp_max` as the current `max_product`.
    - Update `max_product` as the maximum of:
        - Current number `nums[i]`
        - `nums[i] * temp_max`
        - `nums[i] * min_product`
    - Update `min_product` similarly.
    - Update `result` as the maximum of `result` and `max_product`.
4. Return `result`.

---

## Implementation in Python

```python
class Solution:
    def maxProduct(self, nums: list[int]) -> int:
        if not nums:
            return 0

        max_product = nums[0]
        min_product = nums[0]
        result = nums[0]

        for i in range(1, len(nums)):
            current = nums[i]
            temp_max = max_product

            max_product = max(current, temp_max * current, min_product * current)
            min_product = min(current, temp_max * current, min_product * current)

            result = max(result, max_product)

        return result
```

---

## Example Run

Input:

```python
nums = [2, 3, -2, 4]
solution = Solution()
print(solution.maxProduct(nums))
```

Output:

```
6
```

Explanation:

- The subarray `[2, 3]` has the maximum product of `6`.

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - We traverse the array once.
2. **Space Complexity:** `O(1)`
    
    - Only constant space is used for variables.

---

## Edge Cases

1. Single element → Return the element itself.
2. All negative numbers → The highest single negative or product of even count negatives.
3. Zero in array → Restart product calculation.

---

## Conclusion

This solution efficiently finds the maximum product subarray using dynamic programming with constant space.