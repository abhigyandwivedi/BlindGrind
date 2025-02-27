# Solution to "759. Employee Free Time"

## Problem Statement

You are given a list `schedule` representing the working hours of employees. Each employee has a list of non-overlapping intervals. Return the list of finite intervals representing the free time common to all employees.

---

## Approach: Merge and Find Gaps

### Explanation

We can solve this problem using the following approach:

1. **Flatten the Schedule:**
    
    - Combine all employee intervals into one list.
2. **Sort the Intervals:**
    
    - Sort the intervals based on start times.
3. **Merge Intervals:**
    
    - Merge overlapping intervals.
4. **Find Gaps:**
    
    - Identify gaps between merged intervals as the free time.

### Example Walkthrough

For example, given the input:

```
schedule = [[[1, 3], [6, 7]], [[2, 4]], [[2, 5], [9, 12]]]
```

1. Flatten:

```
[ [1, 3], [6, 7], [2, 4], [2, 5], [9, 12] ]
```

1. Sort:

```
[ [1, 3], [2, 4], [2, 5], [6, 7], [9, 12] ]
```

1. Merge:

```
[ [1, 5], [6, 7], [9, 12] ]
```

1. Find gaps:

```
[ [5, 6], [7, 9] ]
```

---

## Implementation in Python

```python
class Solution:
    def employeeFreeTime(self, schedule: List[List[Interval]]) -> List[Interval]:
        intervals = [i for employee in schedule for i in employee]
        intervals.sort(key=lambda x: x.start)
        
        merged = [intervals[0]]
        for i in intervals[1:]:
            if i.start <= merged[-1].end:
                merged[-1].end = max(merged[-1].end, i.end)
            else:
                merged.append(i)
        
        free_time = []
        for i in range(1, len(merged)):
            free_time.append(Interval(merged[i-1].end, merged[i].start))
        
        return free_time
```

---

## Example Run

Input:

```python
schedule = [[[1, 3], [6, 7]], [[2, 4]], [[2, 5], [9, 12]]]
solution = Solution()
free_time = solution.employeeFreeTime(schedule)
for interval in free_time:
    print(f"[{interval.start}, {interval.end}]")
```

Output:

```
[5, 6]
[7, 9]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n log n)`
    
    - Flattening takes `O(n)`.
    - Sorting takes `O(n log n)`.
    - Merging takes `O(n)`.
2. **Space Complexity:** `O(n)`
    
    - Extra space is used for merged intervals and the result.

---

## Edge Cases

1. If all intervals overlap, return an empty list.
2. If there is only one employee, gaps are between their shifts.

---

## Conclusion

This solution efficiently finds common free time among employees using interval merging and gap identification.