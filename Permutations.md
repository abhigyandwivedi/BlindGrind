# Solution to "46. Permutations"

## Problem Statement

Given an array `nums` of distinct integers, return all possible permutations in any order.

Example:

```
Input: nums = [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

---

## Approach: Backtracking

### Explanation

1. **Backtracking:** We explore all possible orderings by recursively swapping and exploring choices.
2. **Base Case:** Once the current permutation reaches the length of `nums`, add it to the result.
3. **Recursive Case:** For each element, place it in the current position and recurse.

---

## Implementation in Python

```python
def permute(nums):
    def backtrack(start):
        if start == len(nums):
            result.append(nums[:])
            return
        for i in range(start, len(nums)):
            nums[start], nums[i] = nums[i], nums[start]
            backtrack(start + 1)
            nums[start], nums[i] = nums[i], nums[start]

    result = []
    backtrack(0)
    return result

# Example usage
nums = [1, 2, 3]
result = permute(nums)
print(result)
```

---

## Example Run

Input:

```python
nums = [1, 2, 3]
result = permute(nums)
print(result)
```

Output:

```
[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(N!)`
    
    - There are `N!` permutations and each takes `O(N)` to build.
2. **Space Complexity:** `O(N)`
    
    - Recursion stack depth is `N`.

---

## Edge Cases

1. Empty input: Return `[]`.
2. Single element: Return `[[element]]`.

---

## Conclusion

This solution efficiently generates all permutations using backtracking, ensuring correctness for all cases.