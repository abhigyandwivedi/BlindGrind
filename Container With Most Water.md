# Solution to "11. Container With Most Water"

## Problem Statement

Given `n` non-negative integers `height[i]` representing the height of vertical lines drawn at each index, find two lines that, together with the x-axis, form a container that holds the most water.

Example:

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
```

---

## Approach: Two-Pointer Technique

### Explanation

1. **Two Pointers:** Start with one pointer at the beginning and another at the end of the array.
2. **Area Calculation:** Calculate the area formed by the heights at the two pointers and the distance between them.
3. **Move Pointers:** Move the pointer pointing to the shorter height inward, as moving the taller one won’t increase the area.
4. **Repeat:** Continue until the pointers meet.

---

## Implementation in Python

```python
def maxArea(height):
    left, right = 0, len(height) - 1
    max_water = 0

    while left < right:
        # Calculate the area
        width = right - left
        h = min(height[left], height[right])
        max_water = max(max_water, width * h)

        # Move the pointers
        if height[left] < height[right]:
            left += 1
        else:
            right -= 1

    return max_water
```

---

## Example Run

Input:

```python
height = [1,8,6,2,5,4,8,3,7]
print(maxArea(height))
```

Output:

```
49
```

Explanation:

- The container formed by `height[1]` (8) and `height[8]` (7) gives the maximum area of `49` units.

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each element is processed once as the two pointers move toward each other.
2. **Space Complexity:** `O(1)`
    
    - Constant extra space used for variables.

---

## Edge Cases

1. If `height` has less than two elements, return `0`.
2. If all heights are the same, the area depends on the widest distance.

---

## Conclusion

This two-pointer approach efficiently finds the container with the most water in linear time.