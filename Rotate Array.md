# Solution to "189. Rotate Array"

## Problem Statement

Given an array, rotate the array to the right by `k` steps, where `k` is non-negative.

---

## Approach: Reverse Method

### Explanation

1. Reverse the entire array.
2. Reverse the first `k` elements.
3. Reverse the remaining `n - k` elements.

This ensures that the array is rotated to the right by `k` steps efficiently.

### Algorithm Steps

1. Reverse the entire array.
2. Reverse the first `k` elements.
3. Reverse the remaining elements.

---

## Implementation in Python

```python
class Solution:
    def rotate(self, nums: list[int], k: int) -> None:
        n = len(nums)
        k %= n

        # Helper function to reverse a sublist
        def reverse(start, end):
            while start < end:
                nums[start], nums[end] = nums[end], nums[start]
                start += 1
                end -= 1

        # Reverse the entire array
        reverse(0, n - 1)
        # Reverse the first k elements
        reverse(0, k - 1)
        # Reverse the remaining elements
        reverse(k, n - 1)
```

---

## Example Run

Input:

```python
nums = [1, 2, 3, 4, 5, 6, 7]
k = 3
solution = Solution()
solution.rotate(nums, k)
print(nums)
```

Output:

```
[5, 6, 7, 1, 2, 3, 4]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each reversal takes linear time.
2. **Space Complexity:** `O(1)`
    
    - In-place rotation without extra space.

---

## Edge Cases

1. `k = 0` → No rotation.
2. `k > n` → Rotate by `k % n` steps.
3. Single element → No change.

---

## Conclusion

This solution efficiently rotates the array to the right by `k` steps using the reverse approach.