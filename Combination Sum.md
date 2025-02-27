# Solution to "39. Combination Sum"

## Problem Statement

Given an array of distinct integers `candidates` and a target integer `target`, return a list of all unique combinations of `candidates` where the chosen numbers sum to `target`. You may use the same number multiple times.

Example:

```
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]

Input: candidates = [2,3,5], target = 8
Output: [[2,2,2,2],[2,3,3],[3,5]]
```

---

## Approach: Backtracking

### Explanation

1. **Backtracking:** Explore each candidate, either including it or skipping it, while reducing the target accordingly.
2. **Base Case:** When the target reaches `0`, add the current combination to the result.
3. **Recursive Case:** Continue exploring with the same element (for repetition) or move to the next element.

---

## Implementation in Python

```python
def combinationSum(candidates, target):
    def backtrack(start, path, remaining):
        if remaining == 0:
            result.append(path[:])
            return
        for i in range(start, len(candidates)):
            if candidates[i] > remaining:
                continue
            path.append(candidates[i])
            backtrack(i, path, remaining - candidates[i])
            path.pop()

    result = []
    candidates.sort()
    backtrack(0, [], target)
    return result

# Example usage
candidates = [2, 3, 6, 7]
target = 7
result = combinationSum(candidates, target)
print(result)
```

---

## Example Run

Input:

```python
candidates = [2, 3, 6, 7]
target = 7
result = combinationSum(candidates, target)
print(result)
```

Output:

```
[[2,2,3],[7]]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(2^T)`
    
    - T is the target value, and in the worst case, we explore all combinations.
2. **Space Complexity:** `O(T)`
    
    - Recursion stack depth is proportional to the target.

---

## Edge Cases

1. No valid combinations: Return `[]`.
2. Single element equals target: Return `[[target]]`.
3. All candidates larger than target: Return `[]`.

---

## Conclusion

This solution efficiently finds all combinations that sum to the target using backtracking, ensuring correctness for all cases.