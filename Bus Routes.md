# LeetCode 815: Bus Routes

## Problem Statement

You are given an array `routes` representing bus routes where `routes[i]` is a bus route that the `i-th` bus repeats forever.

- If `routes[i] = [1, 2, 7]`, it means that the `i-th` bus travels in the sequence `1 -> 2 -> 7 -> 1 -> 2 -> 7 -> ...`.

You are also given `source` and `target` bus stops. Return the minimum number of buses you must take to travel from the `source` to the `target`. If it is not possible to reach the `target`, return `-1`.

### Example Input

```python
routes = [[1, 2, 7], [3, 6, 7]]
source = 1
target = 6
```

### Example Output

```python
Output: 2
```

### Explanation

- Take the first bus from stop `1` to stop `7`.
- Then take the second bus from stop `7` to stop `6`.

---

## Approach

We can solve this problem using **Breadth-First Search (BFS)**. The idea is to treat each bus route as a node and find the shortest path between the source and target stops.

### Steps:

1. **Build a Graph:** Create a mapping from each bus stop to the buses that visit that stop.
2. **BFS Traversal:**
    - Start from the `source` stop and traverse through all reachable bus routes.
    - Track visited buses and stops to avoid cycles.
    - If the `target` stop is reached, return the number of buses taken.
3. If the target is unreachable, return `-1`.

---

## Solution (Python)

```python
from collections import deque, defaultdict

def numBusesToDestination(routes, source, target):
    if source == target:
        return 0

    # Map each stop to the buses that pass through it
    stop_to_buses = defaultdict(list)
    for i, route in enumerate(routes):
        for stop in route:
            stop_to_buses[stop].append(i)

    # Queue for BFS: (current_stop, buses_taken)
    queue = deque([(source, 0)])
    visited_stops = set([source])
    visited_buses = set()

    while queue:
        stop, buses_taken = queue.popleft()

        for bus in stop_to_buses[stop]:
            if bus in visited_buses:
                continue

            visited_buses.add(bus)

            # Check all stops on this bus route
            for next_stop in routes[bus]:
                if next_stop == target:
                    return buses_taken + 1
                if next_stop not in visited_stops:
                    visited_stops.add(next_stop)
                    queue.append((next_stop, buses_taken + 1))

    return -1

# Example usage
routes = [[1, 2, 7], [3, 6, 7]]
source = 1
target = 6
print(numBusesToDestination(routes, source, target))  # Output: 2
```

---

## Detailed Explanation

1. **Input:** `routes = [[1, 2, 7], [3, 6, 7]], source = 1, target = 6`
2. **Stop to Buses Mapping:**
    
    ```python
    {
      1: [0],
      2: [0],
      7: [0, 1],
      3: [1],
      6: [1]
    }
    ```
    
3. **BFS Traversal:**
    - Start from `1` → Bus `0` → Reach `7`
    - From `7` → Bus `1` → Reach `6`

---

## Complexity Analysis

### Time Complexity: O(N + E)

- `N` is the total number of bus stops.
- `E` is the total number of routes and connections.

### Space Complexity: O(N + E)

- We store the graph and visited sets for stops and buses.

---

## Edge Cases

1. **Source equals Target:** `source = 1, target = 1` → Output: `0`
2. **Unreachable Target:** `routes = [[1, 2, 3]], source = 1, target = 5` → Output: `-1`
3. **Direct Route:** `routes = [[1, 2, 3]], source = 1, target = 3` → Output: `1`

---

## Conclusion

This solution efficiently finds the shortest path between bus stops using a graph-based BFS approach, ensuring optimal time and space complexity.

---

Let me know if you'd like further clarifications or alternative solutions!