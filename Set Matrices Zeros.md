# LeetCode 73: Set Matrix Zeroes

## Problem Statement

Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`'s.

You must do it **in-place** without using extra space for another matrix.

---

## Example

### Example 1

```
Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
```

### Example 2

```
Input: matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
Output: [[0,0,0,0],[0,4,5,0],[0,3,1,0]]
```

---

## Approach

We can achieve the solution in-place using the first row and first column as markers.

### Steps:

1. **Mark rows and columns:**
    - Use the first row to mark columns that should be zero.
    - Use the first column to mark rows that should be zero.
2. **Mark zeroes:**
    - Iterate through the matrix, marking corresponding first-row and first-column cells if a zero is found.
3. **Set zeroes:**
    - Iterate again and set cells to zero if their corresponding markers are zero.
4. **Handle first row and column:**
    - Zero out the first row and column if they originally contained any zero.

---

## Solution (Python)

```python
def setZeroes(matrix):
    ROWS, COLS = len(matrix), len(matrix[0])
    first_row_zero = any(matrix[0][j] == 0 for j in range(COLS))
    first_col_zero = any(matrix[i][0] == 0 for i in range(ROWS))

    # Mark zeroes using first row and column
    for i in range(1, ROWS):
        for j in range(1, COLS):
            if matrix[i][j] == 0:
                matrix[i][0] = 0
                matrix[0][j] = 0

    # Set matrix cells to zero based on markers
    for i in range(1, ROWS):
        for j in range(1, COLS):
            if matrix[i][0] == 0 or matrix[0][j] == 0:
                matrix[i][j] = 0

    # Zero out first row if needed
    if first_row_zero:
        for j in range(COLS):
            matrix[0][j] = 0

    # Zero out first column if needed
    if first_col_zero:
        for i in range(ROWS):
            matrix[i][0] = 0
```

---

## Detailed Explanation

### Step 1: Identify Zero Rows and Columns

- Use the first row and first column as markers.
- If any cell `matrix[i][j]` is zero, set `matrix[i][0]` and `matrix[0][j]` to zero.

Example after marking:

```
Input: [[1,1,1],[1,0,1],[1,1,1]]
Marked: [[1,0,1],[1,0,1],[1,1,1]]
```

### Step 2: Update the Matrix

- Use the markers to set cells to zero.

Example after update:

```
Output: [[1,0,1],[0,0,0],[1,0,1]]
```

### Step 3: Handle First Row and Column

- If the first row or column originally contained zero, set them to zero.

---

## Complexity Analysis

### Time Complexity: O(M * N)

- We traverse the matrix twice:
    - First pass to mark rows and columns.
    - Second pass to set zeroes. Thus, the time complexity is **O(M * N)**.

### Space Complexity: O(1)

- No extra space is used apart from the input matrix.
- We only use the first row and column as markers.

---

## Edge Cases

1. **Empty Matrix:** If the matrix is empty, nothing changes.
2. **Single Row/Column:** Properly handles single row or column matrices.
3. **Multiple Zeroes:** Properly propagates zeroes across rows and columns.

---

## Example Run

For the input `[[0,1,2,0],[3,4,5,2],[1,3,1,5]]`, the output will be:

```
[[0,0,0,0],[0,4,5,0],[0,3,1,0]]
```

---

## Conclusion

This solution efficiently sets matrix zeroes in-place with linear time complexity and constant space complexity, ensuring efficient memory usage.