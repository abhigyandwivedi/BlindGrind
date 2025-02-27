# Solution to "78. Subsets"

## Problem Statement

Given an integer array `nums` of unique elements, return all possible subsets (the power set).

Example:

```
Input: nums = [1,2,3]
Output: [
  [],
  [1],
  [2],
  [3],
  [1,2],
  [1,3],
  [2,3],
  [1,2,3]
]
```

---

## Approach: Backtracking

### Explanation

1. **Recursive Exploration:** For each number, decide whether to include it in the current subset.
2. **Base Case:** Once all numbers are considered, add the current subset to the result.

---

## Implementation in Python

```python
def subsets(nums: list[int]) -> list[list[int]]:
    result = []

    def backtrack(start=0, current=[]):
        result.append(current[:])
        for i in range(start, len(nums)):
            current.append(nums[i])
            backtrack(i + 1, current)
            current.pop()

    backtrack()
    return result
```

---

## Example Run

Input:

```python
nums = [1, 2, 3]
print(subsets(nums))
```

Output:

```
[[], [1], [2], [3], [1,2], [1,3], [2,3], [1,2,3]]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(2^n)`
    
    - Each element has two choices: include or exclude.
2. **Space Complexity:** `O(n)`
    
    - Depth of recursion stack.

---

## Edge Cases

1. Empty array → Return `[[]]`.
2. Single element → Return `[[], [element]]`.

---

## Conclusion

Backtracking efficiently generates all subsets by exploring all inclusion possibilities recursively.# Solution to "78. Subsets"

## Problem Statement

Given an integer array `nums` of unique elements, return all possible subsets (the power set).

Example:

```
Input: nums = [1,2,3]
Output: [
  [],
  [1],
  [2],
  [3],
  [1,2],
  [1,3],
  [2,3],
  [1,2,3]
]
```

---

## Approach: Backtracking

### Explanation

1. **Recursive Exploration:** For each number, decide whether to include it in the current subset.
2. **Base Case:** Once all numbers are considered, add the current subset to the result.

---

## Implementation in Python

```python
def subsets(nums: list[int]) -> list[list[int]]:
    result = []

    def backtrack(start=0, current=[]):
        result.append(current[:])
        for i in range(start, len(nums)):
            current.append(nums[i])
            backtrack(i + 1, current)
            current.pop()

    backtrack()
    return result
```

---

## Example Run

Input:

```python
nums = [1, 2, 3]
print(subsets(nums))
```

Output:

```
[[], [1], [2], [3], [1,2], [1,3], [2,3], [1,2,3]]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(2^n)`
    
    - Each element has two choices: include or exclude.
2. **Space Complexity:** `O(n)`
    
    - Depth of recursion stack.

---

## Edge Cases

1. Empty array → Return `[[]]`.
2. Single element → Return `[[], [element]]`.

---

## Conclusion

Backtracking efficiently generates all subsets by exploring all inclusion possibilities recursively.