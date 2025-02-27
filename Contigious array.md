# Solution to "525. Contiguous Array"

## Problem Statement

Given a binary array `nums`, find the maximum length of a contiguous subarray with an equal number of `0`s and `1`s.

---

## Approach: Hash Map

### Explanation

1. Treat `0` as `-1` and `1` as `+1`.
2. Maintain a running sum (`count`).
3. Use a hash map to store the first occurrence of each count.
4. If the count reappears, the subarray between the two indices has equal `0`s and `1`s.

### Algorithm Steps

1. Initialize `count = 0` and `count_map = {0: -1}`.
2. Traverse the array:
    - Increment `count` by `+1` for `1` and `-1` for `0`.
    - If `count` exists in `count_map`, calculate the subarray length.
    - Otherwise, store the first occurrence of `count`.
3. Track the maximum subarray length.

---

## Implementation in Python

```python
class Solution:
    def findMaxLength(self, nums: list[int]) -> int:
        count = 0
        count_map = {0: -1}
        max_length = 0

        for i, num in enumerate(nums):
            count += 1 if num == 1 else -1

            if count in count_map:
                max_length = max(max_length, i - count_map[count])
            else:
                count_map[count] = i

        return max_length
```

---

## Example Run

Input:

```python
nums = [0, 1, 0, 1, 1, 0, 0]
solution = Solution()
print(solution.findMaxLength(nums))
```

Output:

```
6
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Single pass through the array.
2. **Space Complexity:** `O(n)`
    
    - Hash map stores counts and indices.

---

## Edge Cases

1. All `0`s or all `1`s → Result is `0`.
2. Alternating `0`s and `1`s → Maximum length.
3. Empty array → Result is `0`.

---

## Conclusion

This solution efficiently finds the maximum length of a contiguous subarray with equal `0`s and `1`s using a hash map approach.