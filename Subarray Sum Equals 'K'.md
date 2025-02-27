#hashmap  #prefixsum #rangesum
# Solution to "560. Subarray Sum Equals K"

## Problem Statement

Given an array of integers `nums` and an integer `k`, find the total number of continuous subarrays whose sum equals `k`.

---

## Approach: Prefix Sum with Hash Map

### Explanation

We can efficiently solve this problem using the prefix sum approach with a hash map.

### Algorithm Steps

1. **Prefix Sum:**
    
    - Maintain a cumulative sum while iterating through the array.
2. **Hash Map:**
    
    - Store the count of prefix sums encountered.
3. **Count Subarrays:**
    
    - For each `prefix_sum`, check if `(prefix_sum - k)` exists in the hash map.

### Example Walkthrough

For example, given the input:

```
nums = [1, 2, 3]
k = 3
```

1. `prefix_sum` starts at `0`.
2. Iterate through `nums`:
    - `1`: `prefix_sum = 1`, `1 - 3` not found.
    - `2`: `prefix_sum = 3`, `3 - 3 = 0` found → 1 subarray.
    - `3`: `prefix_sum = 6`, `6 - 3 = 3` found → 1 more subarray.

Output:

```
2
```

---

## Implementation in Python

```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        prefix_sum = 0
        count = 0
        prefix_map = {0: 1}

        for num in nums:
            prefix_sum += num
            if prefix_sum - k in prefix_map:
                count += prefix_map[prefix_sum - k]
            prefix_map[prefix_sum] = prefix_map.get(prefix_sum, 0) + 1

        return count
```

---

## Example Run

Input:

```python
nums = [1, 2, 3]
k = 3
solution = Solution()
print(solution.subarraySum(nums, k))
```

Output:

```
2
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - We traverse the array once.
2. **Space Complexity:** `O(n)`
    
    - Extra space for the prefix sum hash map.

---

## Edge Cases

1. Single-element array → Check if it equals `k`.
2. Negative numbers → Properly handled by the prefix sum approach.
3. Zero `k` → Count subarrays with sum `0`.

---

## Conclusion

This solution efficiently finds subarrays summing to `k` using the prefix sum technique and hash map, achieving an optimal `O(n)` time complexity.