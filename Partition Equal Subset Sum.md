# Solution to "416. Partition Equal Subset Sum"

## Problem Statement

Given an integer array `nums`, return `true` if you can partition the array into two subsets such that the sum of the elements in both subsets is equal.

Example:

```
Input: nums = [1, 5, 11, 5]
Output: true
Explanation: The array can be partitioned as [1, 5, 5] and [11].
```

---

## Approach: Dynamic Programming

### Explanation

1. **Total Sum Check:** Calculate the total sum of the array. If it's odd, return `false` (odd sums cannot be evenly partitioned).
2. **Subset Sum Problem:** Convert the problem into finding a subset with a sum equal to `total_sum // 2`.
3. **DP Array:** Use a boolean array `dp` where `dp[j]` indicates if a subset with sum `j` can be formed.
4. **Iterate through Elements:** For each number, update the `dp` array from the back to avoid overwriting values.

---

## Implementation in Python

```python
def canPartition(nums: list[int]) -> bool:
    total_sum = sum(nums)
    if total_sum % 2 != 0:
        return False

    target = total_sum // 2
    dp = [False] * (target + 1)
    dp[0] = True

    for num in nums:
        for j in range(target, num - 1, -1):
            dp[j] = dp[j] or dp[j - num]

    return dp[target]
```

---

## Example Run

Input:

```python
nums = [1, 5, 11, 5]
print(canPartition(nums))
```

Output:

```
True
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n * target)`
    
    - `n` is the number of elements, and `target` is `total_sum // 2`.
2. **Space Complexity:** `O(target)`
    
    - Only the `dp` array is used.

---

## Edge Cases

1. Empty array → Return `false`.
2. Single element array → Return `false`.
3. Odd total sum → Return `false`.

---

## Conclusion

This dynamic programming solution efficiently determines whether an array can be partitioned into two equal subsets.