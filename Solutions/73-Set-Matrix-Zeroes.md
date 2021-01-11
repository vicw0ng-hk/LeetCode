# 73. Set Matrix Zeroes

Given an *`m x n`* matrix. If an element is **0**, set its entire row and column to **0**. Do it [in-place](https://en.wikipedia.org/wiki/In-place_algorithm).

**Follow up**:
- A straight forward solution using O(*mn*) space is probably a bad idea.
- A simple improvement uses O(*m + n*) space, but still not the best solution.
- Could you devise a constant space solution?

## Example 1:
![mat3.jpg](/src/mat3.jpg)
```
Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
```

## Example 2:
![mat4.jpg](/src/mat4.jpg)
```
Input: matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
Output: [[0,0,0,0],[0,4,5,0],[0,3,1,0]]
```

## Constraints:
- `m == matrix.length`
- `n == matrix[0].length`
- `1 <= m, n <= 200`
- <code>-2<sup>31</sup> <= matrix[i][j] <= 2<sup>31</sup> - 1</code>

# Solution
```python
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        a, b = 0, 0
        for i in range(len(matrix)):
            if matrix[i][0] == 0:
                a = 1
        for j in range(len(matrix[0])):
            if matrix[0][j] == 0:
                b = 1
        for i in range(1, len(matrix)):
            for j in range(1, len(matrix[0])):
                if matrix[i][j] == 0:
                    matrix[i][0] = matrix[0][j] = 0
        for i in range(1, len(matrix)):
            if matrix[i][0] == 0:
                for j in range(1, len(matrix[0])):
                    matrix[i][j] = 0
        for j in range(1, len(matrix[0])):
            if matrix[0][j] == 0:
                for i in range(1, len(matrix)):
                    matrix[i][j] = 0
        if a:
            for i in range(len(matrix)):
                matrix[i][0] = 0
        if b:
            for j in range(len(matrix[0])):
                matrix[0][j] = 0
```
Use the array itself to record.
