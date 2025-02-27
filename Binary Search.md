# Solution to "704. Binary Search"

## Problem Statement

Given an array of integers `nums` sorted in ascending order and an integer `target`, write a function to search for `target` in `nums`. If `target` exists, return its index. Otherwise, return `-1`.

Example:

```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
```

---

## Approach: Binary Search

### Explanation

1. **Initialize Pointers:** Set `left` to `0` and `right` to `len(nums) - 1`.
2. **Binary Search Loop:**
    - Calculate `mid` as the middle index between `left` and `right`.
    - If `nums[mid]` equals `target`, return `mid`.
    - If `nums[mid]` is less than `target`, search the right half by updating `left = mid + 1`.
    - If `nums[mid]` is greater than `target`, search the left half by updating `right = mid - 1`.
3. **Return -1** if the target is not found.

---

## Implementation in Python

```python
def binarySearch(nums, target):
    left, right = 0, len(nums) - 1

    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1

# Example usage
nums = [-1, 0, 3, 5, 9, 12]
target = 9
result = binarySearch(nums, target)
print(result)
```

---

## Complexity Analysis

1. **Time Complexity:** `O(log n)` - Each iteration cuts the search space in half.
2. **Space Complexity:** `O(1)` - Constant space used.

---

## Example Run

Input:

```
nums = [-1,0,3,5,9,12], target = 9
```

Output:

```
4
```

---

## Edge Cases

1. If the array is empty, return `-1`.
2. If the target is smaller than the first element or larger than the last, return `-1`.

---

## Conclusion

Binary search efficiently finds an element in a sorted array using logarithmic time complexity.