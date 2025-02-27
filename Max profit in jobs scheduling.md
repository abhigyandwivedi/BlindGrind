# Solution to "1235. Maximum Profit in Job Scheduling"

## Problem Statement

You are given `startTime`, `endTime`, and `profit` arrays, each representing `n` jobs. The `i`-th job starts at `startTime[i]`, ends at `endTime[i]`, and earns `profit[i]`. Find the maximum profit achievable such that no two jobs overlap.

Example:

```
Input: startTime = [1,2,3,3], endTime = [3,4,5,6], profit = [50,10,40,70]
Output: 120
```

Explanation: Schedule jobs 1 and 4 for a total profit of `50 + 70 = 120`.

---

## Approach: Dynamic Programming with Binary Search

### Explanation

1. **Sort by End Time:** Sort jobs by `endTime`.
2. **Binary Search:** Use binary search to find the last non-conflicting job.
3. **DP Transition:** For each job, either:
    - Include the job and add its profit to the best non-conflicting job.
    - Skip the job and take the previous best profit.

---

## Implementation in Python

```python
from bisect import bisect_right

def jobScheduling(startTime, endTime, profit):
    jobs = sorted(zip(startTime, endTime, profit), key=lambda x: x[1])
    dp = [(0, 0)]  # (end_time, max_profit)

    for start, end, p in jobs:
        # Find last non-conflicting job
        i = bisect_right(dp, (start, float('inf'))) - 1
        curr_profit = dp[i][1] + p
        if curr_profit > dp[-1][1]:
            dp.append((end, curr_profit))

    return dp[-1][1]
```

---

## Example Run

Input:

```python
startTime = [1, 2, 3, 3]
endTime = [3, 4, 5, 6]
profit = [50, 10, 40, 70]

print(jobScheduling(startTime, endTime, profit))
```

Output:

```
120
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n log n)`
    
    - Sorting takes `O(n log n)`.
    - Each job insertion uses binary search, `O(log n)`.
2. **Space Complexity:** `O(n)`
    
    - DP array stores profits for `n` jobs.

---

## Edge Cases

1. Single job → Take the job's profit.
2. Completely overlapping jobs → Choose the most profitable.
3. Non-overlapping jobs → Take all profits.

---

## Conclusion

Dynamic programming with binary search efficiently finds the maximum profit in job scheduling with non-overlapping constraints.