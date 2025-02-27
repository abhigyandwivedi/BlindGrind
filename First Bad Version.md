# Solution to "278. First Bad Version"

## Problem Statement

You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check.

Given `n` versions [1, 2, ..., n], you need to find the first bad one, causing all the following ones to be bad.

You have an API `bool isBadVersion(version)` which returns whether a version is bad. Implement a function to find the first bad version.

Example:

```
Input: n = 5, first bad version = 4
Output: 4
```

---

## Approach: Binary Search

### Explanation

1. **Binary Search:** Use binary search to efficiently find the first bad version.
2. **Midpoint Check:** If `isBadVersion(mid)` returns true, the first bad version must be at `mid` or before it.
3. **Narrow the Range:** If false, move the search to the right half.

---

## Implementation in Python

```python
def firstBadVersion(n):
    left, right = 1, n
    while left < right:
        mid = (left + right) // 2
        if isBadVersion(mid):
            right = mid
        else:
            left = mid + 1
    return left

# Example usage
# Suppose version 4 is the first bad version
# print(firstBadVersion(5))  # Output: 4
```

---

## Complexity Analysis

1. **Time Complexity:** `O(log n)`
    - The search space is halved in each step, leading to logarithmic time complexity.
2. **Space Complexity:** `O(1)`
    - Only constant space is used for the left, right, and mid pointers.

---

## Example Run

Input:

```
n = 5, first bad version = 4
```

Output:

```
4
```

---

## Edge Cases

1. Single version and bad: `n = 1, firstBadVersion = 1` → Output: `1`
2. All versions good: Not possible as per the problem constraint.
3. First version bad: `n = 5, firstBadVersion = 1` → Output: `1`

---

## Conclusion

This solution efficiently finds the first bad version using binary search, minimizing API calls and ensuring optimal performance.