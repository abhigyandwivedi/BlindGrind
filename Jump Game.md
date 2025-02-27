# Solution to "55. Jump Game"

## Problem Statement

Given an array of non-negative integers `nums`, you are initially positioned at the first index of the array. Each element in the array represents the maximum jump length from that position.

Return `true` if you can reach the last index, or `false` otherwise.

---

## Approach: Greedy Algorithm

### Explanation

We use a greedy approach by tracking the farthest position reachable as we iterate through the array.

### Algorithm Steps

1. **Initialize:** Set `farthest = 0`.
2. **Iterate:** For each index `i`, update `farthest` as `max(farthest, i + nums[i])`.
3. **Check:** If at any point `i > farthest`, return `false`.
4. **Return:** If `farthest` reaches or exceeds the last index, return `true`.

---

## Implementation in Python

```python
class Solution:
    def canJump(self, nums: list[int]) -> bool:
        farthest = 0
        for i in range(len(nums)):
            if i > farthest:
                return False
            farthest = max(farthest, i + nums[i])
        return True
```

---

## Example Run

Input:

```python
nums = [2, 3, 1, 1, 4]
solution = Solution()
print(solution.canJump(nums))
```

Output:

```
True
```

Input:

```python
nums = [3, 2, 1, 0, 4]
print(solution.canJump(nums))
```

Output:

```
False
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - We traverse the array once.
2. **Space Complexity:** `O(1)`
    
    - Only a few variables are used.

---

## Edge Cases

1. Single element → Output: `True`.
2. All zeros except the first → Output depends on reachability.

---

## Conclusion

This solution efficiently determines whether the last index is reachable using a greedy strategy.