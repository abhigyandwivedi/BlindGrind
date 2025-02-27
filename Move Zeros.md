# Solution to "283. Move Zeros"

## Problem Statement

Given an integer array `nums`, move all `0`s to the end of it while maintaining the relative order of the non-zero elements.

- You must do this in-place without making a copy of the array.

---

## Approach: Two-Pointer Technique

### Explanation

We can solve this problem using the **Two-Pointer** approach:

1. **Two Pointers:**
    
    - Use one pointer `non_zero` to track the position where the next non-zero element should be placed.
    - Use another pointer `i` to iterate through the array.
2. **Move Non-Zeros:**
    
    - For each non-zero element `nums[i]`, place it at `nums[non_zero]` and increment `non_zero`.
3. **Fill Zeros:**
    
    - After placing all non-zero elements, fill the remaining positions with zeros.

### Example Walkthrough

For example, given the input:

```
nums = [0, 1, 0, 3, 12]
```

1. Move non-zero elements to the front:

```
nums = [1, 3, 12, 0, 0]
```

---

## Implementation in Python

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        non_zero = 0
        
        # Move non-zero elements to the front
        for i in range(len(nums)):
            if nums[i] != 0:
                nums[non_zero] = nums[i]
                non_zero += 1
        
        # Fill the rest with zeros
        for i in range(non_zero, len(nums)):
            nums[i] = 0
```

---

## Example Run

Input:

```python
nums = [0, 1, 0, 3, 12]
solution = Solution()
solution.moveZeroes(nums)
print(nums)
```

Output:

```
[1, 3, 12, 0, 0]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - We traverse the array twice: first to move non-zero elements and second to fill zeros.
2. **Space Complexity:** `O(1)`
    
    - In-place manipulation requires constant extra space.

---

## Edge Cases

1. If the array is empty, return as-is.
2. If all elements are zero, return an array of zeros.
3. If no zero exists, the array remains unchanged.

---

## Conclusion

This efficient two-pointer approach moves all zeros to the end while preserving the order of non-zero elements in-place.