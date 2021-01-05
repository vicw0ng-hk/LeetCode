# 51. N-Queens

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer n, return *all distinct solutions to the **n-queens puzzle***.

Each solution contains a distinct board configuration of the n-queens' placement, where `'Q'` and `'.'` both indicate a queen and an empty space, respectively.

## Example 1:
![queens.jpg](/src/queens.jpg)
```
Input: n = 4
Output: [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
Explanation: There exist two distinct solutions to the 4-queens puzzle as shown above
```

## Example 2:
```
Input: n = 1
Output: [["Q"]]
```

## Constraints:
- `1 <= n <= 9`

# Solution
```python
class Solution:
    def __init__(self):
        self.ans = []
        self.column = []
        self.diag1 = []
        self.diag2 = []
        self.board = []
    def find(self, y: int, n: int):
        if y == n:
            self.ans.append(self.board.copy())
        for x in range(n):
            if self.column[x] or self.diag1[x+y] or self.diag2[x-y+n-1]:
                continue
            self.column[x] = self.diag1[x+y] = self.diag2[x-y+n-1] = 1
            self.board[y] = self.board[y][:x] + 'Q' + self.board[y][x+1:]
            self.find(y+1, n)
            self.column[x] = self.diag1[x+y] = self.diag2[x-y+n-1] = 0
            self.board[y] = self.board[y][:x] + '.' + self.board[y][x+1:]
    def solveNQueens(self, n: int) -> List[List[str]]:
        self.column, self.diag1, self.diag2 = [0 for _ in range(n)], [0 for _ in range(2*n-1)], [0 for _ in range(2*n-1)]
        self.board = ['.'*n for _ in range(n)]
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
