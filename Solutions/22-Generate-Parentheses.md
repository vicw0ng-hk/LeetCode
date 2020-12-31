# 22. Generate Parentheses

Given `n` pairs of parentheses, write a function to *generate all combinations of well-formed parentheses*.

## Example 1:
```
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
```

## Example 2:
```
Input: n = 1
Output: ["()"]
```

## Constraints:
- `1 <= n <= 8`

# Solution
```python
class Solution:
    def __init__(self):
        self.ans = []
    def backtrack(self, s: str, n: int, m: int):
        if n == m == 0:
            self.ans.append(s)
        if m < n or n < 0 or m < 0:
            return
        self.backtrack(s+'(', n-1, m)
        self.backtrack(s+')', n, m-1)
    def generateParenthesis(self, n: int) -> List[str]:
        self.backtrack("", n, n)
        return self.ans
```
Simple recursion. 
