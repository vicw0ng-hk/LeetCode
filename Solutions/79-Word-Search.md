# 79. Word Search

Given an `m x n` `board` and a `word`, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cells, where "adjacent" cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

## Example 1:
![word1.jpg](/src/word1.jpg)
```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
```

## Example 2:
![word2.jpg](/src/word2.jpg)
```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
Output: true
```

## Example 3:
![word3.jpg](/src/word3.jpg)
```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
Output: false
```

## Constraints:
- `m == board.length`
- `n = board[i].length`
- `1 <= m, n <= 200`
- <code>1 <= word.length <= 10<sup>3</sup></code>
- `board` and `word` consists only of lowercase and uppercase English letters

# Solution
```python
class Solution:
    def __init__(self):
        self.ans = False
    def solve(self, board: List[List[str]], i: int, j: int, word: str, s: str) -> None:
        if word == s:
            self.ans = True
            return
        if self.ans:
            return
        up = (i != 0 and board[i-1][j] != '.')
        down = (i != len(board)-1 and board[i+1][j] != '.')
        left = (j != 0 and board[i][j-1] != '.')
        right = (j != len(board[0])-1 and board[i][j+1] != '.')
        if up and board[i-1][j] == word[len(s)]:
            tmp, board[i-1][j] = board[i-1][j], '.'
            self.solve(board, i-1, j, word, s+tmp)
            board[i-1][j] = tmp
        if down and board[i+1][j] == word[len(s)]:
            tmp, board[i+1][j] = board[i+1][j], '.'
            self.solve(board, i+1, j, word, s+tmp)
            board[i+1][j] = tmp
        if left and board[i][j-1] == word[len(s)]:
            tmp, board[i][j-1] = board[i][j-1], '.'
            self.solve(board, i, j-1, word, s+tmp)
            board[i][j-1] = tmp
        if right and board[i][j+1] == word[len(s)]:
            tmp, board[i][j+1] = board[i][j+1], '.'
            self.solve(board, i, j+1, word, s+tmp)
            board[i][j+1] = tmp
    def exist(self, board: List[List[str]], word: str) -> bool:
        start = []
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] == word[0]:
                    start.append((i,j))
        for i in range(len(start)):
            if self.ans:
                return self.ans
            else:
                tmp, board[start[i][0]][start[i][1]] = board[start[i][0]][start[i][1]], '.'
                self.solve(board, start[i][0], start[i][1], word, word[0])
                board[start[i][0]][start[i][1]] = tmp
        return self.ans
```
First find the first letter, and then backtrack. Just like what a human would do in a puzzle like this.
