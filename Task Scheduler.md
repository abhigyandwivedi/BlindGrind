# Solution to "621. Task Scheduler"

## Problem Statement

Given a list of tasks represented by characters and an integer `n` representing the cooling period between the same tasks, find the minimum number of units of time required to complete all tasks.

Example:

```
Input: tasks = ['A', 'A', 'A', 'B', 'B', 'B'], n = 2
Output: 8
```

Explanation: A possible schedule is: `A -> B -> idle -> A -> B -> idle -> A -> B`

---

## Approach: Greedy with Priority Queue (Heap)

### Explanation

1. **Task Frequency:** Count the frequency of each task.
2. **Max Heap:** Use a max heap to prioritize the most frequent tasks.
3. **Cycle Processing:** In each cycle of `n + 1` units, process the most frequent tasks.
4. **Idle Handling:** If there are fewer tasks than the cycle length, idle time is added.
5. **End Condition:** Continue until all tasks are processed.

---

## Implementation in Python

```python
from collections import Counter
import heapq

def leastInterval(tasks, n):
    task_counts = Counter(tasks)
    max_heap = [-count for count in task_counts.values()]
    heapq.heapify(max_heap)

    time = 0

    while max_heap:
        temp = []
        cycle_time = 0

        # Process up to n + 1 tasks in each cycle
        for _ in range(n + 1):
            if max_heap:
                count = heapq.heappop(max_heap)
                if count < -1:
                    temp.append(count + 1)
                cycle_time += 1

        # Push remaining tasks back to the heap
        for count in temp:
            heapq.heappush(max_heap, count)

        # If tasks remain, complete full cycle; otherwise, only the time taken
        time += cycle_time if not max_heap else (n + 1)

    return time
```

---

## Example Run

Input:

```python
tasks = ['A', 'A', 'A', 'B', 'B', 'B']
n = 2
print(leastInterval(tasks, n))  # Output: 8
```

Output:

```
8
```

Explanation:

- The task schedule is `A -> B -> idle -> A -> B -> idle -> A -> B`.

---

## Complexity Analysis

1. **Time Complexity:** `O(N)`
    
    - `N` is the total number of tasks.
    - Each task is pushed and popped from the heap once.
2. **Space Complexity:** `O(1)`
    
    - Constant space for storing task frequencies.

---

## Edge Cases

1. If `n = 0`, tasks can be scheduled consecutively.
2. If all tasks are unique, no idle time is needed.

---

## Conclusion

This approach efficiently handles task scheduling using a priority queue, ensuring the minimum execution time while adhering to cooling periods.