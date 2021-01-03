# 36. Valid Sudoku

Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated **according to the following rules**:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the nine `3 x 3` sub-boxes of the grid must contain the digits `1-9` without repetition.

**Note**:

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.

## Example 1:
![250px-Sudoku-by-L2G-20050714.svg.png](/src/250px-Sudoku-by-L2G-20050714.svg.png)
```
Input: board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
```

## Example 2:
```
Input: board = 
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

## Constraints:
- `board.length == 9`
- `board[i].length == 9`
- `board[i][j]` is a digit or `'.'`

# Solution
```python
from collections import defaultdict

class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        for i in range(3):
            for j in range(3):
                tmp = defaultdict(int)
                tmp[board[0+3*i][0+3*j]] += 1
                tmp[board[0+3*i][1+3*j]] += 1
                tmp[board[0+3*i][2+3*j]] += 1
                tmp[board[1+3*i][0+3*j]] += 1
                tmp[board[1+3*i][1+3*j]] += 1
                tmp[board[1+3*i][2+3*j]] += 1
                tmp[board[2+3*i][0+3*j]] += 1
                tmp[board[2+3*i][1+3*j]] += 1
                tmp[board[2+3*i][2+3*j]] += 1
                tmp['.'] = 0
                if max(tmp.values()) > 1:
                    return False
        for i in range(9):
            tmp1, tmp2 = defaultdict(int), defaultdict(int)
            for j in range(9):
                tmp1[board[i][j]] += 1
                tmp2[board[j][i]] += 1
            tmp1['.'] = tmp2['.'] = 0
            if max(tmp1.values()) > 1 or max(tmp2.values()) > 1:
                return False
        return True
```
Use Python dict to record each block, column and row.
