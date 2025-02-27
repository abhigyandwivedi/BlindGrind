# Solution to "238. Product of Array Except Self"

## Problem Statement

Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

You must write an algorithm that runs in `O(n)` time and without using division.

Example:

```
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
Explanation:
For index 0: 2 * 3 * 4 = 24
For index 1: 1 * 3 * 4 = 12
For index 2: 1 * 2 * 4 = 8
For index 3: 1 * 2 * 3 = 6
```

---

## Approach: Prefix and Suffix Product

### Explanation

1. Create two arrays:
    - `prefix[i]` representing the product of all elements before `i`.
    - `suffix[i]` representing the product of all elements after `i`.
2. Multiply the corresponding values of `prefix` and `suffix` to get the final result.
3. Instead of using extra arrays, optimize using constant space by calculating the prefix and suffix on the fly.

---

## Implementation in Python

```python
def productExceptSelf(nums):
    n = len(nums)
    result = [1] * n

    # Calculate prefix product
    prefix = 1
    for i in range(n):
        result[i] = prefix
        prefix *= nums[i]

    # Calculate suffix product and multiply with prefix product
    suffix = 1
    for i in range(n - 1, -1, -1):
        result[i] *= suffix
        suffix *= nums[i]

    return result

# Example usage
nums = [1, 2, 3, 4]
print(productExceptSelf(nums))  # Output: [24, 12, 8, 6]
```

---

## Example Run

Input:

```python
nums = [5, 3, 4, 2]
print(productExceptSelf(nums))  # Output: [24, 40, 30, 60]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)` - We traverse the array twice, once for the prefix and once for the suffix.
2. **Space Complexity:** `O(1)` - We use constant extra space, ignoring the output array.

---

## Edge Cases

1. Single element: `nums = [1]` → Output: `[1]`
2. Contains zero: `nums = [1, 2, 0, 4]` → Output: `[0, 0, 8, 0]`
3. All ones: `nums = [1, 1, 1, 1]` → Output: `[1, 1, 1, 1]`

---

## Conclusion

This solution efficiently computes the product of array except self using the prefix and suffix approach with constant space and linear time complexity.