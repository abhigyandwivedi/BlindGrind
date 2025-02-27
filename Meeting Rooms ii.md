# LeetCode 253: Meeting Rooms II

## Problem Statement

Given an array of meeting time intervals `intervals` where `intervals[i] = [start_i, end_i]`, return the minimum number of conference rooms required.

---

## Example

### Example Input

```
Input: intervals = [[0, 30], [5, 10], [15, 20]]
```

### Example Output

```
Output: 2
```

### Explanation

- At time `0-30`, one meeting room is occupied.
- At time `5-10`, a second meeting room is needed.
- After time `10`, one room becomes free, and at `15-20`, it is occupied again.

Hence, two rooms are required.

---

## Approach

We can solve this problem using a **priority queue (min-heap)**. The approach involves the following steps:

### Steps:

1. **Sort Intervals:** Sort the meetings by start times.
2. **Min-Heap for End Times:** Use a priority queue (min-heap) to track the end times of meetings currently using rooms.
3. **Allocate or Free Room:**
    - If a meeting starts after or when another ends, reuse the room (remove from heap).
    - Otherwise, allocate a new room (add to heap).
4. **Result:** The size of the heap at any point represents the number of rooms required.

---

## Solution (Python)

```python
import heapq

def minMeetingRooms(intervals):
    if not intervals:
        return 0

    # Step 1: Sort intervals by start time
    intervals.sort(key=lambda x: x[0])

    # Step 2: Min-heap to track end times
    heap = []

    # Step 3: Process each meeting
    for interval in intervals:
        start, end = interval

        # If the room is free, reuse it (remove ended meetings)
        if heap and heap[0] <= start:
            heapq.heappop(heap)

        # Allocate a new room (add the current meeting's end time)
        heapq.heappush(heap, end)

    # Step 4: The size of the heap represents the required room count
    return len(heap)

# Example usage
intervals = [[0, 30], [5, 10], [15, 20]]
print(minMeetingRooms(intervals))  # Output: 2
```

---

## Detailed Explanation

1. **Sorting:**
    
    - Sort the meetings by start time: `[[0, 30], [5, 10], [15, 20]]`.
2. **Min-Heap:**
    
    - Use a min-heap to store the end times of meetings currently occupying rooms.
3. **Processing Meetings:**
    
    - For `[0, 30]`, add `30` to the heap.
    - For `[5, 10]`, add `10` (overlap, need second room).
    - For `[15, 20]`, remove `10` (free room), add `20`.
4. **Final Heap:**
    
    - The heap contains `[20, 30]`, meaning two rooms are required.

---

## Complexity Analysis

### Time Complexity: O(N log N)

1. **Sorting:** `O(N log N)` for sorting the intervals.
2. **Heap Operations:** For each interval, `O(log N)` for insertion and deletion.

Thus, the overall complexity is `O(N log N)`.

### Space Complexity: O(N)

- The heap stores end times for ongoing meetings, at most `N` elements in worst case.

---

## Edge Cases

1. **No Meetings:** `intervals = []` → Output: `0`
2. **One Meeting:** `intervals = [[5, 10]]` → Output: `1`
3. **All Meetings Overlap:** `intervals = [[0, 10], [1, 5], [2, 7]]` → Output: `3`
4. **No Overlap:** `intervals = [[0, 5], [6, 10], [11, 15]]` → Output: `1`

---

## Example Run

For the input example `[[0, 30], [5, 10], [15, 20]]`, the output will be:

```
2
```

---

## Conclusion

This optimized solution efficiently determines the minimum number of rooms required using a priority queue. It ensures minimal complexity while accurately handling overlapping intervals.

---

Let me know if you'd like further clarifications or optimizations!