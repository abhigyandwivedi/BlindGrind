# Solution to "207. Course Schedule"

## Problem Statement

Given `numCourses` and a list of prerequisites where `prerequisites[i] = [a, b]` indicates that you must complete course `b` before taking course `a`, determine if it is possible to finish all courses.

Example:

```
Input: numCourses = 2, prerequisites = [[1, 0]]
Output: true

Input: numCourses = 2, prerequisites = [[1, 0], [0, 1]]
Output: false
```

---

## Approach: Topological Sort using Kahn's Algorithm

### Explanation

1. **Graph Representation:** Use an adjacency list where each course points to the courses dependent on it.
2. **Indegree Calculation:** Count incoming edges for each course.
3. **Queue Processing:** Start with courses having `0` indegree and process them.
4. **Topological Order:** If all courses are processed, return `True`; otherwise, return `False`.

---

## Implementation in Python

```python
from collections import deque

def canFinish(numCourses, prerequisites):
    # Graph and indegree initialization
    graph = {i: [] for i in range(numCourses)}
    indegree = [0] * numCourses

    # Build graph and calculate indegree
    for course, prereq in prerequisites:
        graph[prereq].append(course)
        indegree[course] += 1

    # Queue of courses with zero indegree
    queue = deque([i for i in range(numCourses) if indegree[i] == 0])

    # Process queue
    processed_courses = 0
    while queue:
        course = queue.popleft()
        processed_courses += 1
        for neighbor in graph[course]:
            indegree[neighbor] -= 1
            if indegree[neighbor] == 0:
                queue.append(neighbor)

    # Check if all courses were processed
    return processed_courses == numCourses

# Example usage
print(canFinish(2, [[1, 0]]))     # Output: True
print(canFinish(2, [[1, 0], [0, 1]]))  # Output: False
```

---

## Complexity Analysis

1. **Time Complexity:** `O(V + E)` where `V` is the number of courses and `E` is the number of prerequisites.
2. **Space Complexity:** `O(V + E)` for storing the graph and indegree array.

---

## Example Run

Input:

```python
print(canFinish(2, [[1, 0]]))     # Output: True
print(canFinish(2, [[1, 0], [0, 1]]))  # Output: False
```

---

## Edge Cases

1. No prerequisites: `numCourses = 3, prerequisites = []` → Output: `True`
2. Self-dependency: `[[1, 1]]` → Output: `False`
3. Multiple independent chains: `[[1, 0], [2, 3]]` → Output: `True`

---

## Conclusion

This solution uses topological sorting via Kahn's algorithm to efficiently determine if a valid course schedule exists, ensuring `O(V + E)` complexity for processing dependencies.