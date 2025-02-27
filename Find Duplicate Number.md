# Solution to "287. Find the Duplicate Number"

## Problem Statement

Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive, there is only one repeated number in `nums`. Return the duplicate number.

**Note:** You must solve the problem without modifying the array and use only constant extra space.

---

## Approach: Floyd's Tortoise and Hare (Cycle Detection)

### Explanation

This problem can be transformed into a cycle detection problem:

1. Treat the array as a linked list where `nums[i]` points to the next index.
2. There will be a cycle because one number appears twice.
3. Use Floyd's Tortoise and Hare algorithm to detect the cycle.

### Algorithm Steps

1. **Phase 1: Detect cycle:**
    
    - Use two pointers: `slow` and `fast`.
    - Move `slow` by one step and `fast` by two steps until they meet.
2. **Phase 2: Find the start of the cycle (duplicate number):**
    
    - Reset one pointer to the start of the array.
    - Move both pointers one step at a time until they meet again.

The meeting point is the duplicate number.

---

## Implementation in Python

```python
class Solution:
    def findDuplicate(self, nums: list[int]) -> int:
        # Phase 1: Detect cycle
        slow, fast = nums[0], nums[0]
        while True:
            slow = nums[slow]
            fast = nums[nums[fast]]
            if slow == fast:
                break

        # Phase 2: Find start of cycle
        slow = nums[0]
        while slow != fast:
            slow = nums[slow]
            fast = nums[fast]

        return slow
```

---

## Example Run

Input:

```python
nums = [3, 1, 3, 4, 2]
solution = Solution()
print(solution.findDuplicate(nums))
```

Output:

```
3
```

Explanation:

- The number `3` appears twice in the array.

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Both phases run in linear time.
2. **Space Complexity:** `O(1)`
    
    - Only constant extra space is used.

---

## Edge Cases

1. Minimum array size → `[1, 1]` → Output: `1`
2. Multiple duplicates → Only one guaranteed duplicate.

---

## Conclusion

This solution efficiently finds the duplicate number using cycle detection while maintaining constant space complexity.