# 435. Non-overlapping Intervals

## Problem Statement

Given an array of intervals where `intervals[i] = [start_i, end_i]`, find the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.

### Example

```python
Input: intervals = [[1,2],[2,3],[3,4],[1,3]]
Output: 1
Explanation: Remove [1,3] to make the rest non-overlapping.
```

## Solution Explanation

The problem can be efficiently solved using a greedy algorithm. The idea is to:

1. **Sort** the intervals based on their ending times.
2. **Iterate** through the intervals and keep track of the end time of the last non-overlapping interval.
3. **Count** the number of intervals that overlap and need to be removed.

### Python Code

```python
def eraseOverlapIntervals(intervals):
    if not intervals:
        return 0

    # Sort by ending time
    intervals.sort(key=lambda x: x[1])

    non_overlapping_count = 0
    last_end = float('-inf')

    for interval in intervals:
        if interval[0] >= last_end:
            # No overlap, update last_end
            last_end = interval[1]
            non_overlapping_count += 1

    # Total intervals - non-overlapping gives the count to remove
    return len(intervals) - non_overlapping_count
```

## Complexity Analysis

### Time Complexity

1. **Sorting**: `O(n log n)` - Sorting the intervals based on their ending times.
2. **Iteration**: `O(n)` - Iterating through the sorted intervals.

Thus, the overall time complexity is:

O(nlog⁡n)+O(n)=O(nlog⁡n)O(n \log n) + O(n) = O(n \log n)

### Space Complexity

1. **Input storage**: `O(n)` - Storing the input intervals.
2. **Additional variables**: `O(1)` - For tracking `last_end` and `non_overlapping_count`.

Thus, the overall space complexity is:

O(n)O(n)

## Detailed Explanation

1. **Sorting by end time** ensures that we always consider the interval that ends the earliest, maximizing the room for subsequent intervals.
2. **Tracking last_end** helps identify overlapping intervals efficiently.
3. **Counting non-overlapping intervals** allows us to deduce the number of intervals to remove by subtraction.

This greedy approach ensures optimal performance while maintaining clarity and efficiency.