# Solution to "739. Daily Temperatures"

## Problem Statement

Given an array of integers `temperatures` representing the daily temperatures, return an array `answer` such that `answer[i]` is the number of days you have to wait after the `i`-th day to get a warmer temperature. If there is no future day for which this is possible, put `0` instead.

---

## Approach: Monotonic Stack

### Explanation

1. **Use a Stack:** Maintain a stack where each element is an index of the `temperatures` array.
2. **Processing:**
    - For each temperature, check if it's warmer than the temperature at the top index of the stack.
    - If it is, calculate the difference in indices and update the `answer` array.
    - Push the current index onto the stack.

---

## Implementation in Python

```python
class Solution:
    def dailyTemperatures(self, temperatures: list[int]) -> list[int]:
        stack = []  # Stores indices of temperatures
        answer = [0] * len(temperatures)

        for i, temp in enumerate(temperatures):
            while stack and temperatures[stack[-1]] < temp:
                prev_index = stack.pop()
                answer[prev_index] = i - prev_index
            stack.append(i)

        return answer
```

---

## Example Run

Input:

```python
temperatures = [73, 74, 75, 71, 69, 72, 76, 73]
solution = Solution()
print(solution.dailyTemperatures(temperatures))
```

Output:

```
[1, 1, 4, 2, 1, 1, 0, 0]
```

Explanation:

- On day 0 (73°F), the next warmer day is day 1 (74°F).
- On day 1 (74°F), the next warmer day is day 2 (75°F).
- On day 2 (75°F), the next warmer day is day 6 (76°F).
- For days 6 and 7, there are no warmer days.

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each temperature is pushed and popped from the stack once.
2. **Space Complexity:** `O(n)`
    
    - Stack space for indices.

---

## Edge Cases

1. All decreasing temperatures → `[0, 0, 0, ..., 0]`
2. All increasing temperatures → `[1, 1, 1, ..., 0]`
3. Single day → `[0]`

---

## Conclusion

This stack-based approach efficiently finds the number of days to wait for a warmer temperature for each day.