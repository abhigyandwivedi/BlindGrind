# 787. Cheapest Flights Within K Stops

## Problem Statement

Given `n` cities numbered from `0` to `n-1`, an array `flights` where `flights[i] = [from_i, to_i, price_i]` represents a flight from city `from_i` to city `to_i` with cost `price_i`, and three integers `src`, `dst`, and `k`, return the cheapest price from `src` to `dst` with at most `k` stops. If there is no such route, return `-1`.

### Example

**Input:**

```
n = 4
flights = [[0,1,100],[1,2,100],[2,0,100],[1,3,600],[2,3,200]]
src = 0, dst = 3, k = 1
```

**Output:**

```
700
```

**Explanation:** The cheapest route is `0 -> 1 -> 3` with cost `100 + 600 = 700`.

---

## Approach: Bellman-Ford Algorithm

### Idea

1. Use the Bellman-Ford algorithm with an additional constraint of `k` stops.
2. Maintain an array `cost` where `cost[i]` represents the cheapest price to reach city `i`.
3. Perform `k+1` iterations (0 stops to k stops).
4. In each iteration, update the costs based on the available flights.

---

## Implementation (Python)

```python
def findCheapestPrice(n, flights, src, dst, k):
    # Initialize cost array with infinity
    cost = [float('inf')] * n
    cost[src] = 0

    # Iterate k+1 times
    for _ in range(k + 1):
        temp = cost.copy()
        for u, v, w in flights:
            if cost[u] != float('inf') and cost[u] + w < temp[v]:
                temp[v] = cost[u] + w
        cost = temp

    return cost[dst] if cost[dst] != float('inf') else -1
```

---

## Example Run

For `n = 4`, `flights = [[0,1,100],[1,2,100],[2,0,100],[1,3,600],[2,3,200]]`, `src = 0`, `dst = 3`, and `k = 1`:

1. Initialize `cost = [0, inf, inf, inf]`.
2. After first iteration (0 stops): `cost = [0, 100, inf, inf]`
3. After second iteration (1 stop): `cost = [0, 100, 200, 700]`

Output: `700`

---

## Complexity Analysis

### Time Complexity

- **O(E * k):** `E` is the number of flights. For each stop, all flights are processed.

### Space Complexity

- **O(n):** Array to store the minimum cost for each city.

---

## Edge Cases

1. No route exists → Output: `-1`.
2. `src == dst` → Output: `0`.
3. `k = 0` and no direct flight → Output: `-1`.

---

## Conclusion

This solution efficiently finds the cheapest flight with at most `k` stops using a modified Bellman-Ford algorithm, ensuring linear complexity relative to the number of flights and stops.