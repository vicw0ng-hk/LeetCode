# 37. Sudoku Solver

Write a program to solve a Sudoku puzzle by filling the empty cells.

A sudoku solution must satisfy **all of the following rules**:

Each of the digits `1-9` must occur exactly once in each row.
Each of the digits `1-9` must occur exactly once in each column.
Each of the digits `1-9` must occur exactly once in each of the 9 `3x3` sub-boxes of the grid.
The `'.'` character indicates empty cells.

## Example 1:
![250px-Sudoku-by-L2G-20050714.svg.png](/src/250px-Sudoku-by-L2G-20050714.svg.png)
```
Input: board = [["5","3",".",".","7",".",".",".","."],["6",".",".","1","9","5",".",".","."],[".","9","8",".",".",".",".","6","."],["8",".",".",".","6",".",".",".","3"],["4",".",".","8",".","3",".",".","1"],["7",".",".",".","2",".",".",".","6"],[".","6",".",".",".",".","2","8","."],[".",".",".","4","1","9",".",".","5"],[".",".",".",".","8",".",".","7","9"]]
Output: [["5","3","4","6","7","8","9","1","2"],["6","7","2","1","9","5","3","4","8"],["1","9","8","3","4","2","5","6","7"],["8","5","9","7","6","1","4","2","3"],["4","2","6","8","5","3","7","9","1"],["7","1","3","9","2","4","8","5","6"],["9","6","1","5","3","7","2","8","4"],["2","8","7","4","1","9","6","3","5"],["3","4","5","2","8","6","1","7","9"]]
Explanation: The input board is shown above and the only valid solution is shown below:
![250px-Sudoku-by-L2G-20050714_solution.svg.png](/src/250px-Sudoku-by-L2G-20050714_solution.svg.png)
```

## Constraints:
- `board.length == 9`
- `board[i].length == 9`
- `board[i][j]` is a digit or `'.'`.
- It is **guaranteed** that the input board has only one solution.

# Solution
```python
from collections import defaultdict

class Solution:
    def checkBlock(self, m: int, n: int, board: List[List[str]]) -> bool:
        tmp = defaultdict(int)
        for i in range(3):
            for j in range(3):
                tmp[board[i+3*m][j+3*n]] += 1
        tmp['.'] = 0
        if max(tmp.values()) > 1:
            return False
        return True
    def checkRow(self, i: int, board: List[List[str]]) -> bool:
        tmp = defaultdict(int)
        for j in range(9):
            tmp[board[i][j]] += 1
        tmp['.'] = 0
        if max(tmp.values()) > 1:
            return False
        return True
    def checkColumn(self, j: int, board: List[List[str]]) -> bool:
        tmp = defaultdict(int)
        for i in range(9):
            tmp[board[i][j]] += 1
        tmp['.'] = 0
        if max(tmp.values()) > 1:
            return False
        return True
    def solve(self, board: List[List[str]], i: int, j: int) -> bool:
        if i == 9:
            return True
        elif board[i][j] == '.':
            for k in range(9):
                board[i][j] = str(k+1)
                if self.checkBlock(i//3, j//3, board) and self.checkRow(i, board) and self.checkColumn(j, board):
                    if (j == 8 and self.solve(board, i+1, 0)) or (j != 8 and self.solve(board, i, j+1)):
                        return True
            board[i][j] = '.'
        else:
            return self.solve(board, i+1, 0) if j == 8 else self.solve(board, i, j+1)
    def solveSudoku(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        self.solve(board, 0, 0)
```
Somewhat complicated backtracking. 
