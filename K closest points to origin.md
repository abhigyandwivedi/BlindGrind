# Solution to "973. K Closest Points to Origin"

## Problem Statement

Given an array of `points` where `points[i] = [xi, yi]` represents a point on the X-Y plane and an integer `k`, return the `k` closest points to the origin `(0, 0)`.

Example:

```
Input: points = [[3,3],[5,-1],[-2,4]], k = 2
Output: [[3,3],[-2,4]]
Explanation: The distance from (0,0) to (3,3) and (-2,4) is smaller than to (5,-1).
```

---

## Approach: Min-Heap

### Explanation

1. **Distance Calculation:** Calculate the squared Euclidean distance for each point: `distance = x^2 + y^2`.
2. **Heap Storage:** Use a min-heap to efficiently retrieve the `k` closest points.
3. **Result:** Extract the top `k` points from the heap.

---

## Implementation in Python

```python
import heapq

def kClosest(points, k):
    # Create a min-heap based on squared distance
    heap = [(x**2 + y**2, [x, y]) for x, y in points]
    heapq.heapify(heap)

    # Extract k closest points
    return [heapq.heappop(heap)[1] for _ in range(k)]

# Example usage
points = [[3,3],[5,-1],[-2,4]]
k = 2
print(kClosest(points, k))  # Output: [[3,3], [-2,4]]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n log k)` - Inserting `n` elements into the heap and extracting `k` elements.
2. **Space Complexity:** `O(k)` - Heap storage for `k` closest points.

---

## Example Run

Input:

```
points = [[3,3],[5,-1],[-2,4]], k = 2
```

Output:

```
[[3,3], [-2,4]]
```

---

## Edge Cases

1. `k` equals the number of points → Return all points.
2. Single point → Return the point itself.
3. Multiple points with equal distances → Any valid set of `k` points.

---

## Conclusion

This solution efficiently finds the `k` closest points to the origin using a min-heap, ensuring optimal time and space complexity.