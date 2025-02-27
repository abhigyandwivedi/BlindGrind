# 🟢 Squares of a Sorted Array (LeetCode 977)

## 🚀 Problem Statement

Given an integer array `nums` sorted in **non-decreasing order**, return an array of the **squares of each number** sorted in non-decreasing order.

### 🔑 Example:

```python
Input: nums = [-4, -1, 0, 3, 10]
Output: [0, 1, 9, 16, 100]
```

---

## 📝 **O(n) Solution: Two-Pointer Approach**

```python
from typing import List

def sortedSquares(nums: List[int]) -> List[int]:
    left, right = 0, len(nums) - 1
    result = [0] * len(nums)
    index = len(nums) - 1

    while left <= right:
        left_square = nums[left] ** 2
        right_square = nums[right] ** 2

        if left_square > right_square:
            result[index] = left_square
            left += 1
        else:
            result[index] = right_square
            right -= 1
        index -= 1

    return result

# Example usage
nums = [-4, -1, 0, 3, 10]
print(sortedSquares(nums))  # Output: [0, 1, 9, 16, 100]
```

---

## ⏱️ **Time Complexity Analysis**

- **Two-pointer traversal:** We traverse the array once using `left` and `right` pointers.
- **Each element processed once:** Every element is squared and placed in the result array.

Thus, the time complexity is:

O(n)O(n)

Where `n` is the number of elements in the array.

---

## 💾 **Space Complexity Analysis**

- **Output array:** We use an extra array `result` of size `n` to store the squares.
- **No additional data structures:** Apart from the output array, constant space is used for variables.

Thus, the space complexity is:

O(n)O(n)

---

## ✅ **Key Insights:**

1. Squaring flips the order of negative numbers, requiring sorting.
2. The two-pointer approach compares absolute values from both ends.
3. Efficient O(n)O(n) complexity avoids the O(nlog⁡n)O(n \log n) of naive sorting.