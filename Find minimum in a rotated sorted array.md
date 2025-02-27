# 🔍 Find Minimum in Rotated Sorted Array (LeetCode 153)

## 🚀 Problem Statement

Given a rotated sorted array of unique integers, find the minimum element. The array was originally sorted in ascending order and then rotated at an unknown pivot.

### 🔑 Example:

```python
Input: nums = [3, 4, 5, 1, 2]
Output: 1
Explanation: The minimum element is 1.
```

---

## 📝 **Optimized O(log n) Solution: Binary Search Approach**

```python
from typing import List

def findMin(nums: List[int]) -> int:
    left, right = 0, len(nums) - 1

    while left < right:
        mid = (left + right) // 2

        # If middle element is greater than the rightmost element,
        # the minimum must be in the right half.
        if nums[mid] > nums[right]:
            left = mid + 1
        else:
            right = mid

    # When the loop ends, left == right and points to the minimum element
    return nums[left]

# Example usage
nums = [3, 4, 5, 1, 2]
print(findMin(nums))  # Output: 1
```

---

## ⏱️ **Time Complexity Analysis**

1. **Binary Search:** In each iteration, the search space is halved.
2. **Logarithmic Reduction:** Since the array size reduces by half each time, the complexity is:

O(log⁡n)O(\log n)

Where `n` is the length of the array.

---

## 💾 **Space Complexity Analysis**

- **In-place Search:** No extra space is used aside from a few variables.
- **Constant Space:** Only `left`, `right`, and `mid` pointers are maintained.

Thus, the overall space complexity is:

O(1)O(1)

---

## ✅ **Key Insights:**

1. A rotated sorted array has two sorted halves.
2. The minimum lies in the unsorted half.
3. Efficient binary search achieves logarithmic time complexity.
4. O(log⁡n)O(\log n) time and O(1)O(1) space are optimal for this problem.