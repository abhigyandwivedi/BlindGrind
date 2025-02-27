# Solution to "31. Next Permutation"

## Problem Statement

Given an array of integers `nums`, find the next lexicographical permutation of the array. If no such permutation exists, rearrange it as the lowest possible order (sorted in ascending order).

---

## Approach: Two-Pointer Technique

### Explanation

To find the next permutation, we follow these steps:

1. **Find the first decreasing element:** Traverse from the right and find the first index `i` such that `nums[i] < nums[i+1]`.
2. **Find the next larger element:** Find the smallest number to the right of `nums[i]` that is larger than `nums[i]`.
3. **Swap:** Swap `nums[i]` and that number.
4. **Reverse:** Reverse the portion of the array to the right of `i`.

If no such `i` exists, the array is the last permutation, so reverse the entire array to get the first permutation.

### Algorithm Steps

1. Find the rightmost index `i` where `nums[i] < nums[i+1]`.
2. If `i` doesn't exist, reverse the array and return.
3. Find the rightmost index `j` where `nums[j] > nums[i]`.
4. Swap `nums[i]` and `nums[j]`.
5. Reverse the subarray from `i+1` to the end.

---

## Implementation in Python

```python
class Solution:
    def nextPermutation(self, nums: list[int]) -> None:
        n = len(nums)
        i = n - 2

        # Step 1: Find the first decreasing element from the right
        while i >= 0 and nums[i] >= nums[i + 1]:
            i -= 1

        if i >= 0:
            # Step 2: Find the next larger element
            j = n - 1
            while nums[j] <= nums[i]:
                j -= 1
            # Step 3: Swap
            nums[i], nums[j] = nums[j], nums[i]

        # Step 4: Reverse the right part
        left, right = i + 1, n - 1
        while left < right:
            nums[left], nums[right] = nums[right], nums[left]
            left += 1
            right -= 1
```

---

## Example Run

Input:

```python
nums = [1, 2, 3]
solution = Solution()
solution.nextPermutation(nums)
print(nums)
```

Output:

```
[1, 3, 2]
```

Explanation:

- The next permutation after `[1, 2, 3]` is `[1, 3, 2]`.

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - We perform one pass to find the decreasing element, one pass to find the next larger element, and one pass to reverse.
2. **Space Complexity:** `O(1)`
    
    - No additional space used apart from in-place modifications.

---

## Edge Cases

1. If the array is sorted in descending order → Reverse to ascending order.
2. Single element → No change.

---

## Conclusion

This solution efficiently generates the next lexicographical permutation by identifying key positions and rearranging the array in-place.