# 54. Spiral Matrix

Given an `m x n` `matrix`, return *all elements of the* `matrix` *in spiral order*.

## Example 1:

```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```

## Example 2:

```
Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

## Constraints:
- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 10`
- `-100 <= matrix[i][j] <= 100`

# Solution
```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        ans, move = [], [(n, 0)]
        m, n, i, j, flag = len(matrix), len(matrix[0]), 0, -1, (m - 1 > 0)
        if flag:
            move += [(m-1, 1)]
        flag = (flag and n - 1 > 0)
        if flag:
            move += [(n-1, 2)]
        flag = (flag and m - 2 > 0)
        if flag:
            move += [(m-2, 3)]
        n, m = n - 1, m - 2
        while move:
            if move[0][1] == 0:
                ans += [matrix[i][j+_] for _ in range(1, move[0][0]+1)]
                j += move[0][0]
                move = move[1:]
                flag = (flag and n - 1 > 0)
                if flag:
                    n -= 1
                    move += [(n, 0)]
            elif move[0][1] == 1:
                ans += [matrix[i+_][j] for _ in range(1, move[0][0]+1)]
                i += move[0][0]
                move = move[1:]
                flag = (flag and m - 1 > 0)
                if flag:
                    m -= 1
                    move += [(m, 1)]
            elif move[0][1] == 2:
                ans += [matrix[i][j-_] for _ in range(1, move[0][0]+1)]
                j -= move[0][0]
                move = move[1:]
                flag = (flag and n - 1 > 0)
                if flag:
                    n -= 1
                    move += [(n, 2)]
            else:
                ans += [matrix[i-_][j] for _ in range(1, move[0][0]+1)]
                i -= move[0][0]
                move = move[1:]
                flag = (flag and m - 1 > 0)
                if flag:
                    m -= 1
                    move += [(m, 3)]
        return ans
```
Simulate the spiral path.
