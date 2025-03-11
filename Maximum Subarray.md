# Solution to "53. Maximum Subarray"

## Problem Statement

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Example:

```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

---
![[Pasted image 20250305024019.png]]
## Approach: Kadane's Algorithm

### Explanation

1. **Dynamic Programming Insight:** We iterate through the array while maintaining two variables:
    
    - `current_sum`: Maximum subarray sum ending at the current index.
    - `max_sum`: The global maximum subarray sum found so far.
2. **Transition:** For each element `nums[i]`, decide whether to extend the current subarray or start fresh:
    
    - `current_sum = max(nums[i], current_sum + nums[i])`
3. **Update Maximum:**
    
    - `max_sum = max(max_sum, current_sum)`

---

## Implementation in Python

```python
def maxSubArray(nums):
    current_sum = nums[0]
    max_sum = nums[0]

    for num in nums[1:]:
        current_sum = max(num, current_sum + num)
        max_sum = max(max_sum, current_sum)

    return max_sum

# Example usage
nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
result = maxSubArray(nums)
print(result)  # Output: 6
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)` - We traverse the array once.
2. **Space Complexity:** `O(1)` - Only constant extra space is used.

---

## Example Run

Input:

```
nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
```

Output:

```
6
```

---

## Edge Cases

1. Single element → That element is the result.
2. All negative numbers → Pick the least negative.

---

## Conclusion

Kadane's algorithm provides an optimal solution for the maximum subarray problem with linear time complexity.