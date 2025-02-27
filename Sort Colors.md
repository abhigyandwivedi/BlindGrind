# Solution to "75. Sort Colors"

## Problem Statement

Given an array `nums` with `n` objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use integers to represent the colors:

- `0` for red
- `1` for white
- `2` for blue

Example:

```
Input: nums = [2, 0, 2, 1, 1, 0]
Output: [0, 0, 1, 1, 2, 2]
```

---

## Approach: Dutch National Flag Algorithm

### Explanation

1. **Three Pointers:** Use three pointers:
    - `low` to place `0`s.
    - `mid` to traverse the array.
    - `high` to place `2`s.
2. **Traversal:**
    - If `nums[mid] == 0`, swap `nums[low]` and `nums[mid]`, then increment both `low` and `mid`.
    - If `nums[mid] == 1`, increment `mid`.
    - If `nums[mid] == 2`, swap `nums[mid]` and `nums[high]`, then decrement `high`.

---

## Implementation in Python

```python
def sortColors(nums: list[int]) -> None:
    low, mid, high = 0, 0, len(nums) - 1

    while mid <= high:
        if nums[mid] == 0:
            nums[low], nums[mid] = nums[mid], nums[low]
            low += 1
            mid += 1
        elif nums[mid] == 1:
            mid += 1
        else:
            nums[mid], nums[high] = nums[high], nums[mid]
            high -= 1
```

---

## Example Run

Input:

```python
nums = [2, 0, 2, 1, 1, 0]
sortColors(nums)
print(nums)
```

Output:

```
[0, 0, 1, 1, 2, 2]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each element is processed once.
2. **Space Complexity:** `O(1)`
    
    - Sorting is done in-place.

---

## Edge Cases

1. Empty array → No change.
2. All elements are the same → Already sorted.
3. Random order → Sorted correctly.

---

## Conclusion

The Dutch National Flag algorithm efficiently sorts an array of colors in-place using three pointers.