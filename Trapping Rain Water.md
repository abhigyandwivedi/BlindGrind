# Solution to "42. Trapping Rain Water"

## Problem Statement

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

Example:

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

---

## Approach: Two-Pointer Technique

### Explanation

1. **Two Pointers:** Start with pointers at both ends of the array.
2. **Max Heights:** Keep track of the maximum height from the left and right.
3. **Water Calculation:** At each step, calculate trapped water based on the lower max height.

---

## Implementation in Python

```python
def trap(height):
    if not height:
        return 0

    left, right = 0, len(height) - 1
    left_max, right_max = height[left], height[right]
    water = 0

    while left < right:
        if left_max < right_max:
            left += 1
            left_max = max(left_max, height[left])
            water += max(0, left_max - height[left])
        else:
            right -= 1
            right_max = max(right_max, height[right])
            water += max(0, right_max - height[right])

    return water
```

---

## Example Run

Input:

```python
height = [0,1,0,2,1,0,1,3,2,1,2,1]
print(trap(height))
```

Output:

```
6
```

---

## Complexity Analysis

1. **Time Complexity:** `O(N)`
    
    - `N` is the length of `height`.
    - Each element is processed once.
2. **Space Complexity:** `O(1)`
    
    - Constant space used for pointers and counters.

---

## Edge Cases

1. Empty array → Output: 0.
2. No trapping possible → Output: 0.

---

## Conclusion

The two-pointer technique efficiently calculates trapped water with linear time complexity and constant space.