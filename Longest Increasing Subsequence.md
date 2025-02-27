# Solution to "300. Longest Increasing Subsequence"

## Problem Statement

Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

---

## Approach: Dynamic Programming

### Explanation

We use a dynamic programming approach where:

1. Define `dp[i]` as the length of the longest increasing subsequence ending at index `i`.
2. For each `i`, iterate through all previous indices `j` (`0 <= j < i`).
3. If `nums[j] < nums[i]`, update `dp[i]` as `dp[i] = max(dp[i], dp[j] + 1)`.
4. Finally, return the maximum value in `dp`.

---

## Implementation in Python

```python
class Solution:
    def lengthOfLIS(self, nums: list[int]) -> int:
        if not nums:
            return 0

        n = len(nums)
        dp = [1] * n

        for i in range(n):
            for j in range(i):
                if nums[j] < nums[i]:
                    dp[i] = max(dp[i], dp[j] + 1)

        return max(dp)
```

---

## Example Run

Input:

```python
nums = [10, 9, 2, 5, 3, 7, 101, 18]
solution = Solution()
print(solution.lengthOfLIS(nums))
```

Output:

```
4
```

Explanation: The longest increasing subsequence is `[2, 3, 7, 101]`.

---

## Complexity Analysis

1. **Time Complexity:** `O(n^2)`
    
    - Two nested loops iterate through the array.
2. **Space Complexity:** `O(n)`
    
    - `dp` array stores the LIS length for each index.

---

## Edge Cases

1. Empty array → `0`.
2. Single element → `1`.
3. Already increasing array → Length of array.

---

## Conclusion

This solution efficiently finds the longest increasing subsequence using dynamic programming with a quadratic time complexity.