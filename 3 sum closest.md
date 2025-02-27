# 🔷 3Sum Closest (LeetCode 16)

## 🚀 Problem Statement

Given an integer array `nums` of length `n` and an integer `target`, find the sum of three integers in `nums` such that the sum is **closest** to `target`. Return the sum of the three integers.

### 🔑 Example:

```python
Input: nums = [-1, 2, 1, -4], target = 1
Output: 2
Explanation: The sum that is closest to 1 is 2 (-1 + 2 + 1 = 2).
```

---

## 📝 **Optimized O(n²) Solution: Two-Pointer Approach**

```python
from typing import List

def threeSumClosest(nums: List[int], target: int) -> int:
    nums.sort()  # Sort the array first
    closest_sum = float('inf')

    for i in range(len(nums) - 2):
        # Skip duplicate elements to avoid redundant calculations
        if i > 0 and nums[i] == nums[i - 1]:
            continue

        left, right = i + 1, len(nums) - 1

        while left < right:
            current_sum = nums[i] + nums[left] + nums[right]

            # Update closest sum if the current one is closer
            if abs(current_sum - target) < abs(closest_sum - target):
                closest_sum = current_sum

            # If exact match found, return immediately
            if current_sum == target:
                return current_sum

            # Move pointers based on sum comparison
            if current_sum < target:
                left += 1
            else:
                right -= 1

    return closest_sum

# Example usage
nums = [-1, 2, 1, -4]
target = 1
print(threeSumClosest(nums, target))  # Output: 2
```

---

## ⏱️ **Time Complexity Analysis**

- **Sorting:** O(nlog⁡n)O(n \log n)
- **Two-pointer traversal:** For each element, the inner `while` loop runs in O(n)O(n).
- **Duplicate Skip:** Reduces redundant calculations.

Thus, the overall time complexity remains:

O(n2)O(n^2)

Where `n` is the length of the input array.

---

## 💾 **Space Complexity Analysis**

- **Sorting:** O(1)O(1) extra space for in-place sorting.
- **Auxiliary Variables:** Constant space used for `closest_sum` and pointers.

Thus, the overall space complexity remains:

O(1)O(1)

---

## ✅ **Key Insights:**

1. Sorting simplifies the problem by allowing two-pointer traversal.
2. Skipping duplicates improves efficiency without affecting correctness.
3. Adjusting pointers based on the current sum efficiently narrows down the closest sum.
4. O(n2)O(n^2) complexity is optimal for typical input constraints.