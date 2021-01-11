# 74. Search a 2D Matrix

Write an efficient algorithm that searches for a value in an `m x n` matrix. This matrix has the following properties:
- Integers in each row are sorted from left to right.
- The first integer of each row is greater than the last integer of the previous row.

## Example 1:
```
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
```

## Example 2:
```
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
Output: false
```

## Constraints:
- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 100`
- <code>-10<sup>4</sup> <= matrix[i][j], target <= 10<sup>4</sup></code>

# Solution
```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        up, down = 0, len(matrix) - 1
        while up < down:
            mid = (up + down + 1) // 2
            if matrix[mid][0] == target:
                return True
            elif matrix[mid][0] < target:
                up = mid
            else:
                down = mid - 1
        left, right = 0, len(matrix[0]) - 1
        while left < right:
            mid = (left + right + 1) // 2
            if matrix[up][mid] == target:
                return True
            elif matrix[up][mid] < target:
                left = mid
            else:
                right = mid - 1
        return matrix[up][left] == target
```
Just a 2D Binary Search.
