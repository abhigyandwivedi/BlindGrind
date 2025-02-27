# Solution to "128. Longest Consecutive Sequence"

## Problem Statement

Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.

**Note:** The sequence must be consecutive numbers, but the order in the array does not matter.

---

## Approach: Using Hash Set

### Explanation

1. Convert the array into a set to allow `O(1)` lookups.
2. Iterate through each number in the set.
3. For each number, check if it's the start of a sequence (i.e., `num - 1` does not exist in the set).
4. If it is, iterate through the sequence and count its length.
5. Keep track of the maximum length found.

### Algorithm Steps

1. Add all numbers to a set.
2. For each number in the set:
    - If `num - 1` is not in the set, start counting the sequence from `num`.
    - Increment the count while `num + 1` exists in the set.
3. Update the maximum length for each sequence found.

---

## Implementation in Python

```python
class Solution:
    def longestConsecutive(self, nums: list[int]) -> int:
        if not nums:
            return 0

        num_set = set(nums)
        max_length = 0

        for num in num_set:
            if num - 1 not in num_set:
                current_num = num
                current_length = 1

                while current_num + 1 in num_set:
                    current_num += 1
                    current_length += 1

                max_length = max(max_length, current_length)

        return max_length
```

---

## Example Run

Input:

```python
nums = [100, 4, 200, 1, 3, 2]
solution = Solution()
print(solution.longestConsecutive(nums))
```

Output:

```
4
```

Explanation: The longest consecutive sequence is `[1, 2, 3, 4]`.

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each number is processed once, and lookups in a set take `O(1)` time.
2. **Space Complexity:** `O(n)`
    
    - The set stores all unique numbers.

---

## Edge Cases

1. Empty array → Result is `0`.
2. Single element → Result is `1`.
3. All unique consecutive numbers → Result is the length of the array.

---

## Conclusion

This solution efficiently finds the longest consecutive sequence in an array using a hash set for `O(n)` time complexity.