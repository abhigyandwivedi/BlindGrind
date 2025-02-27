# Solution to "134. Gas Station"

## Problem Statement

There are `n` gas stations along a circular route, where the amount of gas at the `i`-th station is `gas[i]`.

You have a car with an unlimited gas tank, and it costs `cost[i]` of gas to travel from the `i`-th station to its next station `(i + 1)`. You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return `-1`.

---

## Approach: Greedy Strategy

### Explanation

1. **Check Total Balance:** If the total gas available is less than the total cost required, it's impossible to complete the circuit. Return `-1`.
2. **Find Starting Point:** Traverse the stations while keeping track of the current tank balance. If the tank becomes negative, reset the start station to the next station and reset the tank.

### Algorithm Steps

1. Calculate the total `gas - cost` for all stations.
2. If the total is negative, return `-1`.
3. Traverse the stations:
    - Maintain a `current_tank`.
    - If `current_tank` falls below `0`, reset the start index to the next station and reset `current_tank`.
4. Return the start index if the circuit is possible.

---

## Implementation in Python

```python
class Solution:
    def canCompleteCircuit(self, gas: list[int], cost: list[int]) -> int:
        total_tank, current_tank, start_index = 0, 0, 0

        for i in range(len(gas)):
            balance = gas[i] - cost[i]
            total_tank += balance
            current_tank += balance

            # If current tank is negative, reset the start station
            if current_tank < 0:
                start_index = i + 1
                current_tank = 0

        return start_index if total_tank >= 0 else -1
```

---

## Example Run

Input:

```python
gas = [1, 2, 3, 4, 5]
cost = [3, 4, 5, 1, 2]
solution = Solution()
print(solution.canCompleteCircuit(gas, cost))
```

Output:

```
3
```

Explanation:

- Starting at station `3`, the car can complete the circuit.

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - We traverse the gas stations once.
2. **Space Complexity:** `O(1)`
    
    - Only constant extra space is used.

---

## Edge Cases

1. If total gas is less than total cost → Return `-1`.
2. If only one station and gas >= cost → Return `0`.

---

## Conclusion

This greedy approach efficiently finds the valid start station if a complete circuit is possible.