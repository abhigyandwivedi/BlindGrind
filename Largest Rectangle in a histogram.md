# Solution to "84. Largest Rectangle in Histogram"

## Problem Statement

Given an array of integers `heights` representing the histogram's bar heights, return the area of the largest rectangle that can be formed in the histogram.

Example:

```
Input: heights = [2,1,5,6,2,3]
Output: 10
```

---

## Approach: Stack

### Explanation

1. **Use a Stack:** Maintain a stack of indices representing the bars.
2. **Push indices:** Push the index if the current height is greater than or equal to the height at the stack's top.
3. **Pop and Calculate:** When a smaller height is encountered, pop from the stack and calculate the area using the popped height as the smallest bar.
4. **Final Pass:** Ensure all bars are processed by pushing a `0` height at the end.

---

## Implementation in Python

```python
def largestRectangleArea(heights):
    stack = []  # Stack to store indices
    max_area = 0
    heights.append(0)  # Sentinel value to clear the stack

    for i, h in enumerate(heights):
        while stack and heights[stack[-1]] > h:
            height = heights[stack.pop()]
            width = i if not stack else i - stack[-1] - 1
            max_area = max(max_area, height * width)
        stack.append(i)

    return max_area
```

---

## Example Run

Input:

```python
heights = [2, 1, 5, 6, 2, 3]
print(largestRectangleArea(heights))
```

Output:

```
10
```

Explanation:

- The largest rectangle has height `5` and width `2` (`5 x 2 = 10`).

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each bar is pushed and popped once.
2. **Space Complexity:** `O(n)`
    
    - Stack stores indices.

---

## Edge Cases

1. Empty array → `0`.
2. Single-bar histogram → Height of the single bar.
3. Increasing or decreasing heights → Stack ensures proper calculation.

---

## Conclusion

Using a stack efficiently finds the largest rectangle in a histogram in linear time.