# Solution to "57. Insert Interval"

## Problem Statement

Given a list of non-overlapping intervals sorted by their start times, insert a new interval into the list while ensuring the list remains non-overlapping and sorted.

Example:

```
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
```

---

## Approach: Merge Intervals

### Explanation

1. **Initialization:** Traverse the list of intervals.
2. **Merge:**
    - If the current interval ends before the new interval starts, add it to the result.
    - If the current interval starts after the new interval ends, add the new interval and remaining intervals.
    - If they overlap, merge them by updating the start and end.
3. **Result:** Ensure all intervals are processed.

---

## Implementation in Python

```python
def insert(intervals, newInterval):
    result = []
    i = 0
    start, end = newInterval

    # Add intervals before newInterval
    while i < len(intervals) and intervals[i][1] < start:
        result.append(intervals[i])
        i += 1

    # Merge overlapping intervals
    while i < len(intervals) and intervals[i][0] <= end:
        start = min(start, intervals[i][0])
        end = max(end, intervals[i][1])
        i += 1
    result.append([start, end])

    # Add remaining intervals
    result.extend(intervals[i:])

    return result

# Example usage
intervals = [[1,3],[6,9]]
newInterval = [2,5]
print(insert(intervals, newInterval))
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)` - Each interval is processed once.
2. **Space Complexity:** `O(n)` - Storage for the result list.

---

## Example Run

Input:

```
intervals = [[1,3],[6,9]]
newInterval = [2,5]
```

Output:

```
[[1,5],[6,9]]
```

---

## Edge Cases

1. New interval before all → Add at the start.
2. New interval after all → Add at the end.
3. Full overlap → Merge all intersecting intervals.

---

## Conclusion

This solution efficiently inserts a new interval while maintaining the sorted, non-overlapping properties.