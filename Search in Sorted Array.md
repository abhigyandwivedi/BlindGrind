# Solution to "33. Search in Rotated Sorted Array"

## Problem Statement

Given a rotated sorted array `nums` and an integer `target`, return the index of `target` if it exists, otherwise return `-1`.

Example:

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4

Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

---

## Approach: Modified Binary Search

### Explanation

1. **Binary Search:** Perform binary search while handling the rotation.
2. **Identify Sorted Half:** At each step, determine which half is sorted.
3. **Target Comparison:** Decide whether to search in the left or right half based on `target`.

---

## Implementation in Python

```python
def search(nums, target):
    left, right = 0, len(nums) - 1

    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            return mid

        # Determine the sorted half
        if nums[left] <= nums[mid]:
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        else:
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1

    return -1

# Example usage
nums = [4, 5, 6, 7, 0, 1, 2]
target = 0
result = search(nums, target)
print(result)
```

---

## Example Run

Input:

```python
nums = [4, 5, 6, 7, 0, 1, 2]
target = 0
result = search(nums, target)
print(result)
```

Output:

```
4
```

---

## Complexity Analysis

1. **Time Complexity:** `O(log N)`
    
    - Binary search reduces the search space by half.
2. **Space Complexity:** `O(1)`
    
    - Constant space used for pointers.

---

## Edge Cases

1. Empty array: Return `-1`.
2. Single element equals target: Return `0`.
3. Target not found: Return `-1`.

---

## Conclusion

This solution efficiently searches for the target in a rotated sorted array using modified binary search.