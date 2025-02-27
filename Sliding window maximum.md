# 239. Sliding Window Maximum

## Problem Statement

Given an integer array `nums` and a sliding window of size `k`, find the maximum value in each window as it moves from left to right.

### Example

**Input:**

```
nums = [1,3,-1,-3,5,3,6,7], k = 3
```

**Output:**

```
[3, 3, 5, 5, 6, 7]
```

**Explanation:**

- Window `[1,3,-1]` → Max = `3`
- Window `[3,-1,-3]` → Max = `3`
- Window `[-1,-3,5]` → Max = `5`
- Window `[-3,5,3]` → Max = `5`
- Window `[5,3,6]` → Max = `6`
- Window `[3,6,7]` → Max = `7`

---

## Approach: Deque (Double-Ended Queue)

### Idea

1. Use a deque to store indices of array elements.
2. The deque maintains indices of elements in decreasing order.
3. The front of the deque always holds the index of the maximum element in the current window.
4. Slide the window:
    - Remove indices of elements outside the current window.
    - Remove smaller elements as they can't be maximum in the current window.
    - Add the current index to the deque.
    - Append the front element to the result as the current maximum.

---

## Implementation (Python)

```python
from collections import deque

def maxSlidingWindow(nums, k):
    if not nums:
        return []

    result = []
    deque_window = deque()

    for i in range(len(nums)):
        # Remove indices outside the current window
        if deque_window and deque_window[0] < i - k + 1:
            deque_window.popleft()

        # Remove smaller elements from the deque
        while deque_window and nums[deque_window[-1]] < nums[i]:
            deque_window.pop()

        # Add current index to the deque
        deque_window.append(i)

        # Append max for the current window
        if i >= k - 1:
            result.append(nums[deque_window[0]])

    return result
```

---

## Example Run

For `nums = [1,3,-1,-3,5,3,6,7]` and `k = 3`:

1. `Window [1,3,-1]` → Max = `3`
2. `Window [3,-1,-3]` → Max = `3`
3. `Window [-1,-3,5]` → Max = `5`
4. `Window [-3,5,3]` → Max = `5`
5. `Window [5,3,6]` → Max = `6`
6. `Window [3,6,7]` → Max = `7`

Output: `[3, 3, 5, 5, 6, 7]`

---

## Complexity Analysis

### Time Complexity

- **O(n):** Each element is added to and removed from the deque once.

### Space Complexity

- **O(k):** Deque stores indices of elements within the current window.

---

## Edge Cases

1. `nums = []` → Output: `[]` (Empty array)
2. `k = 1` → Output: `nums` (Each element is its own maximum)
3. `nums = [1,3,1,2,0,5]`, `k = 3` → Output: `[3, 3, 2, 5]`

---

## Conclusion

This solution efficiently finds the maximum value in each sliding window using a deque, ensuring linear time complexity while maintaining the current window's potential maximums.