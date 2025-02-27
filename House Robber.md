# Solution to "198. House Robber"

## Problem Statement

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, represented by an array `nums`. If you rob two adjacent houses, the alarm will be triggered.

Return the maximum amount of money you can rob without alerting the police.

---

## Approach: Dynamic Programming

### Explanation

1. **DP Array:** Define `dp[i]` as the maximum amount of money that can be robbed up to the `i`-th house.
    
2. **Recurrence Relation:**
    
    - For each house `i`, choose between:
        - Robbing the current house and adding it to the amount from `i-2`: `nums[i] + dp[i-2]`.
        - Skipping the current house and taking the amount from `i-1`: `dp[i-1]`.
    - Formula: `dp[i] = max(nums[i] + dp[i-2], dp[i-1])`
3. **Space Optimization:** Instead of an array, use two variables to track the last two results.
    

---

## Implementation in Python

```python
class Solution:
    def rob(self, nums: list[int]) -> int:
        if not nums:
            return 0
        if len(nums) == 1:
            return nums[0]

        prev2, prev1 = 0, 0

        for num in nums:
            current = max(num + prev2, prev1)
            prev2 = prev1
            prev1 = current

        return prev1
```

---

## Example Run

Input:

```python
nums = [2, 7, 9, 3, 1]
solution = Solution()
print(solution.rob(nums))
```

Output:

```
12
```

Explanation:

- Rob house 1 (`2`) + house 3 (`9`) + house 5 (`1`) = `2 + 9 + 1 = 12`

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - We iterate through the array once.
2. **Space Complexity:** `O(1)`
    
    - Only constant space is used.

---

## Edge Cases

1. No houses → `0`
2. One house → `nums[0]`
3. Two houses → `max(nums[0], nums[1])`

---

## Conclusion

Using dynamic programming with space optimization, we efficiently find the maximum amount that can be robbed without alerting the police.