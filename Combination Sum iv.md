# LeetCode 377: Combination Sum IV

## Problem Statement

Given an array of distinct integers `nums` and a target integer `target`, return the number of possible combinations that add up to `target`.

### Example

```python
Input: nums = [1, 2, 3], target = 4
Output: 7
Explanation:
The possible combinations are:
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)
```

## Approach: Dynamic Programming

We can solve this problem using dynamic programming. The idea is to use an array `dp` where `dp[i]` represents the number of possible combinations to get the sum `i` using the given numbers in `nums`.

### Steps

1. Initialize a `dp` array of size `target + 1` with all zeros.
2. Set `dp[0] = 1` because there is one way to get a sum of zero: by choosing no elements.
3. Iterate through each value from `1` to `target`.
4. For each value `i`, iterate through `nums` and add `dp[i - num]` to `dp[i]` if `i - num >= 0`.
5. Finally, return `dp[target]`.

### Code Implementation

```python
class Solution:
    def combinationSum4(self, nums: List[int], target: int) -> int:
        # DP array to store the number of combinations for each sum
        dp = [0] * (target + 1)
        dp[0] = 1  # One way to get sum 0 (empty set)

        # Iterate through all possible sums
        for i in range(1, target + 1):
            for num in nums:
                if i - num >= 0:
                    dp[i] += dp[i - num]

        return dp[target]
```

### Dry Run

For `nums = [1, 2, 3]` and `target = 4`:

- `dp[0] = 1` (base case)
- `dp[1] = dp[0]` (using 1) → `1`
- `dp[2] = dp[1] + dp[0]` (using 1 and 2) → `2`
- `dp[3] = dp[2] + dp[1] + dp[0]` (using 1, 2, 3) → `4`
- `dp[4] = dp[3] + dp[2] + dp[1]` (using 1, 2, 3) → `7`

Final answer: `dp[4] = 7`

### Complexity Analysis

#### Time Complexity: `O(target * n)`

- For each target value from `1` to `target`, we iterate through `nums`.
- Hence, the time complexity is `O(target * n)` where `n` is the length of `nums`.

#### Space Complexity: `O(target)`

- We use an array `dp` of size `target + 1` to store results.

## Edge Cases

1. If `nums` is empty, return `0`.
2. If `target` is `0`, return `1` (empty combination).
3. If all numbers in `nums` are greater than `target`, return `0`.