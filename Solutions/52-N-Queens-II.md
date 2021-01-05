# 52. N-Queens II

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer n, return *the number of distinct solutions to the **n-queens puzzle***.

## Example 1:
![queens.jpg](/src/queens.jpg)
```
Input: n = 4
Output: 2
Explanation: There are two distinct solutions to the 4-queens puzzle as shown.
```

## Example 2:
```
Input: n = 1
Output: 1
```

## Constraints:
- `1 <= n <= 9`

# Solution
```python
class Solution:
    def __init__(self):
        self.ans = 0
        self.column = []
        self.diag1 = []
        self.diag2 = []
    def find(self, y: int, n: int):
        if y == n:
            self.ans += 1
        for x in range(n):
            if self.column[x] or self.diag1[x+y] or self.diag2[x-y+n-1]:
                continue
            self.column[x] = self.diag1[x+y] = self.diag2[x-y+n-1] = 1
            self.find(y+1, n)
            self.column[x] = self.diag1[x+y] = self.diag2[x-y+n-1] = 0
    def totalNQueens(self, n: int) -> int:
        self.column, self.diag1, self.diag2 = [0 for _ in range(n)], [0 for _ in range(2*n-1)], [0 for _ in range(2*n-1)]
        self.find(0, n)
        return self.ans
```
Typical Backtracking problem. Pay attention to the conditions:
```
column:
0 1 2 3
0 1 2 3
0 1 2 3
0 1 2 3

diag1:
0 1 2 3
1 2 3 4
2 3 4 5
3 4 5 6

diag2:
3 4 5 6
2 3 4 5
1 2 3 4
0 1 2 3
```
