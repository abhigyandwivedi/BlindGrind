# Solution to "733. Flood Fill"

## Problem Statement

Given an `m x n` image represented by a 2D integer grid `image`, where `image[i][j]` represents the pixel value of the image, implement a function to perform a flood fill. Given a starting pixel `(sr, sc)` and a new color, fill all connected pixels with the same original color as `(sr, sc)` with the new color.

Example:

```
Input: image = [[1,1,1],[1,1,0],[1,0,1]], sr = 1, sc = 1, newColor = 2
Output: [[2,2,2],[2,2,0],[2,0,1]]
```

---

## Approach: Depth-First Search (DFS)

### Explanation

1. **Base Condition:** If the starting pixel already has the new color, return the image as-is.
2. **DFS Traversal:**
    - Start from `(sr, sc)`.
    - If the current pixel matches the original color, change it to the new color.
    - Recursively visit its 4-connected neighbors (up, down, left, right).

---

## Implementation in Python

```python
def floodFill(image, sr, sc, newColor):
    originalColor = image[sr][sc]
    if originalColor == newColor:
        return image

    def dfs(r, c):
        if r < 0 or r >= len(image) or c < 0 or c >= len(image[0]) or image[r][c] != originalColor:
            return
        image[r][c] = newColor
        dfs(r + 1, c)
        dfs(r - 1, c)
        dfs(r, c + 1)
        dfs(r, c - 1)

    dfs(sr, sc)
    return image

# Example usage
image = [[1,1,1],[1,1,0],[1,0,1]]
sr, sc, newColor = 1, 1, 2
result = floodFill(image, sr, sc, newColor)
print(result)
```

---

## Complexity Analysis

1. **Time Complexity:** `O(m * n)` - In the worst case, all pixels might be visited once.
2. **Space Complexity:** `O(m * n)` - Recursive stack depth in the worst case.

---

## Example Run

Input:

```
image = [[1,1,1],[1,1,0],[1,0,1]], sr = 1, sc = 1, newColor = 2
```

Output:

```
[[2,2,2],[2,2,0],[2,0,1]]
```

---

## Edge Cases

1. If the new color is the same as the original, no change is needed.
2. Handle boundary conditions to avoid index errors.

---

## Conclusion

Flood fill is efficiently implemented using DFS, ensuring connected regions are updated correctly.