# Solution to "252. Meeting Rooms"

## Problem Statement

Given an array of meeting time intervals `intervals` where `intervals[i] = [start_i, end_i]`, determine if a person can attend all meetings.

---

## Approach: Sorting and Interval Check

### Explanation

1. **Sort Intervals:** Sort the intervals based on their start times.
2. **Check for Overlaps:** Iterate through the sorted intervals and check if the end time of one interval exceeds the start time of the next interval.

---

## Implementation in Python

```python
class Solution:
    def canAttendMeetings(self, intervals: list[list[int]]) -> bool:
        # Sort intervals by start time
        intervals.sort(key=lambda x: x[0])

        # Check for overlap
        for i in range(1, len(intervals)):
            if intervals[i][0] < intervals[i - 1][1]:
                return False

        return True
```

---

## Example Run

Input:

```python
intervals = [[0, 30], [5, 10], [15, 20]]
solution = Solution()
print(solution.canAttendMeetings(intervals))
```

Output:

```
False
```

Explanation:

- The meetings `[0, 30]` and `[5, 10]` overlap.

---

## Complexity Analysis

1. **Time Complexity:** `O(n log n)`
    
    - Sorting takes `O(n log n)` and checking overlaps takes `O(n)`.
2. **Space Complexity:** `O(1)`
    
    - Constant space used for variables.

---

## Edge Cases

1. No meetings → `True`
2. Single meeting → `True`
3. Overlapping meetings → `False`

---

## Conclusion

By sorting the intervals and checking for overlaps, we can efficiently determine if all meetings can be attended.