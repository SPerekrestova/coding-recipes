
# Matrix Rotation

## Problem Description

Rotate a given 2D matrix 90 degrees clockwise **in place**.

### Understanding the Rotation

- Each element in the matrix moves to its corresponding position in the next layer.
- The element at position `(i, j)` moves to `(j, n-1-i)`.

**Example:**

**Input:**
```
[
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
```

**Output (rotated 90° clockwise):**
```
[
    [7, 4, 1],
    [8, 5, 2],
    [9, 6, 3]
]
```

---

## Approach

We can achieve the rotation in two steps:

### Step 1: Transpose the Matrix

- Swap the element at `(i, j)` with the element at `(j, i)` for all `i < j`.
- This flips the matrix along its main diagonal.

**Example (after transposing):**
```
[
    [1, 4, 7],
    [2, 5, 8],
    [3, 6, 9]
]
```

### Step 2: Reverse Each Row

- Reverse the elements in each row to complete the 90-degree rotation.

**Example (after reversing rows):**
```
[
    [7, 4, 1],
    [8, 5, 2],
    [9, 6, 3]
]
```

---

## Algorithm

1. **Transpose the Matrix:** Iterate over the upper triangle of the matrix (excluding the diagonal), and swap elements.
2. **Reverse Each Row:** Iterate through each row and reverse its elements.

---

## Code Implementation

### Java Code:
```java
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;

        // Step 1: Transpose the matrix
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        // Step 2: Reverse each row
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n / 2; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[i][n - 1 - j];
                matrix[i][n - 1 - j] = temp;
            }
        }
    }
}
```

---

## Complexity Analysis

### Time Complexity

- **Transposing:** Requires \(O(n^2)\) swaps.
- **Reversing Rows:** Requires \(O(n^2)\) operations.
- **Overall:** \(O(n^2)\).

### Space Complexity

- All operations are performed **in place**, so the space complexity is \(O(1)\).

---

## Edge Cases

1. **Single Element Matrix:** e.g., `[[1]]`.
2. **Matrix with All Identical Elements:** e.g., `[[5, 5], [5, 5]]`.
3. **Large \(n 	imes n\) Matrix:** e.g., \(n = 1000\).

---

## Related Problems

- Rotate 90° counterclockwise.
- Rotate 180° (clockwise or counterclockwise).
- Mirror a matrix along its diagonal or anti-diagonal.

---

### Counterclockwise Rotation

For a **90° counterclockwise rotation**, follow these steps:

1. Transpose the matrix.
2. Reverse each column instead of rows.


# Additional Matrix Rotations

## Rotating 180° (Clockwise or Counterclockwise)

To rotate a matrix 180°, you need to:

1. **Reverse Rows:**
    - Reverse the order of rows in the matrix.
    - This flips the matrix upside-down.

2. **Reverse Columns:**
    - Reverse the order of elements within each column.
    - This mirrors the matrix horizontally.

### Explanation

Rotating 180° is equivalent to flipping the matrix upside down and then left-to-right (or vice versa).

### Code Snippet (Java)
```java
class Solution {
    public void rotate180(int[][] matrix) {
        int n = matrix.length;

        // Reverse rows
        for (int i = 0; i < n / 2; i++) {
            int[] temp = matrix[i];
            matrix[i] = matrix[n - 1 - i];
            matrix[n - 1 - i] = temp;
        }

        // Reverse columns
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n / 2; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[i][n - 1 - j];
                matrix[i][n - 1 - j] = temp;
            }
        }
    }
}
```

---

## Rotating 270° (Clockwise)

To rotate a matrix 270° clockwise (or 90° counterclockwise), you need to:

1. **Transpose the Matrix:**
    - Swap the element at `(i, j)` with the element at `(j, i)` for all `i < j`.
    - This converts rows into columns.

2. **Reverse Columns:**
    - Reverse the elements in each column of the transposed matrix.
    - This aligns the columns in the correct rotated order.

### Explanation

Rotating 270° clockwise is equivalent to rotating 90° counterclockwise, and involves flipping the matrix diagonally (transpose) and then vertically (reverse columns).

### Code Snippet (Java)
```java
class Solution {
    public void rotate270(int[][] matrix) {
        int n = matrix.length;

        // Step 1: Transpose the matrix
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        // Step 2: Reverse columns
        for (int j = 0; j < n; j++) {
            for (int i = 0; i < n / 2; i++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[n - 1 - i][j];
                matrix[n - 1 - i][j] = temp;
            }
        }
    }
}
```

---

## Summary of Matrix Rotation Techniques

| Rotation            | Steps                           | Key Operations                           |
|---------------------|---------------------------------|------------------------------------------|
| **90° Clockwise**   | Transpose + Reverse Rows        | Flip diagonal + Mirror horizontally      |
| **90° Counterclockwise** | Transpose + Reverse Columns     | Flip diagonal + Mirror vertically        |
| **180°**            | Reverse Rows + Reverse Columns  | Flip upside-down + Mirror horizontally   |
| **270° Clockwise**  | Transpose + Reverse Columns     | Flip diagonal + Mirror vertically        |

---
