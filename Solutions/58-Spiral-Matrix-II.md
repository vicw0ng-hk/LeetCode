# 58. Spiral Matrix II

Given a positive integer `n`, generate an `n x n` `matrix` filled with elements from `1` to <code>n<sup>2</sup></code> in spiral order.

## Example 1:

```
Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]
```

## Example 2:
```
Input: n = 1
Output: [[1]]
```

## Constraints:
- `1 <= n <= 20`

# Solution
```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        ans = [[_+1 for _ in range(n)]]
        for i in range(n-1):
            ans.append([0 for _ in range(n)])
        count, direction, position = n, 1, [0, n-1]
        while count < n * n:
            count += 1
            if direction == 0:
                if position[1] + 1 >= n or ans[position[0]][position[1]+1] != 0:
                    direction = 1
                    position[0] += 1
                else:
                    position[1] += 1
            elif direction == 1:
                if position[0] + 1 >= n or ans[position[0]+1][position[1]] != 0:
                    direction = 2
                    position[1] -= 1
                else:
                    position[0] += 1
            elif direction == 2:
                if position[1] - 1 < 0 or ans[position[0]][position[1]-1] != 0:
                    direction = 3
                    position[0] -= 1
                else:
                    position[1] -= 1
            elif direction == 3:
                if position[0] - 1 < 0 or ans[position[0]-1][position[1]] != 0:
                    direction = 0
                    position[1] += 1
                else:
                    position[0] -= 1
            ans[position[0]][position[1]] = count
        return ans
```
Simulation of spiral path.
