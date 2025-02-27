# Solution to "56. Merge Intervals"

## Problem Statement

Given an array of intervals where `intervals[i] = [start_i, end_i]`, merge all overlapping intervals and return an array of the non-overlapping intervals that cover all the intervals in the input.

Example:

```
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]

Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
```

---

## Approach: Sorting and Merging

### Explanation

1. **Sort the Intervals:** Sort the array based on the start of each interval.
2. **Merge Intervals:** Iterate through the sorted intervals and merge overlapping intervals by comparing the end of the current interval with the start of the next.

---

## Implementation in Python

```python
def merge(intervals):
    if not intervals:
        return []

    # Sort intervals by start time
    intervals.sort(key=lambda x: x[0])
    merged = [intervals[0]]

    for current in intervals[1:]:
        last = merged[-1]
        if current[0] <= last[1]:
            # Merge overlapping intervals
            last[1] = max(last[1], current[1])
        else:
            merged.append(current)

    return merged

# Example usage
intervals = [[1,3],[2,6],[8,10],[15,18]]
result = merge(intervals)
print(result)  # Output: [[1,6],[8,10],[15,18]]
```

---

## Example Run

Input:

```python
intervals = [[1,3],[2,6],[8,10],[15,18]]
result = merge(intervals)
print(result)
```

Output:

```
[[1,6],[8,10],[15,18]]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(N log N)`
    
    - Sorting takes `O(N log N)` and merging takes `O(N)`.
2. **Space Complexity:** `O(N)`
    
    - Extra space for the merged intervals.

---

## Edge Cases

1. Single interval: Return the interval as is.
2. Fully overlapping intervals: Merge into one.
3. Non-overlapping intervals: Return all as separate.

---

## Conclusion

This solution efficiently merges overlapping intervals using sorting and a single pass, ensuring correctness for all cases.