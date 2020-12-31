# 17. Letter Combinations of a Phone Number

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.



## Example 1:
```
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

## Example 2:
```
Input: digits = ""
Output: []
```

## Example 3:
```
Input: digits = "2"
Output: ["a","b","c"]
```

## Constraints:
- `0 <= digits.length <= 4`
- `digits[i]` is a digit in the range `['2', '9']`.

# Solution
```python
class Solution:
    def __init__(self):
        self.ans = []
        self.n2l = ['', '', 'abc', 'def', 'ghi', 'jkl', 'mno', 'pqrs', 'tuv', 'wxyz']
    def backtrack(self, res: str, digits: str):
        if len(digits) == 0:
            self.ans.append(res)
        else:
            for l in self.n2l[int(digits[0])]:
                self.backtrack(res+l, digits[1:])
    def letterCombinations(self, digits: str) -> List[str]:
        if digits:
            self.backtrack("", digits)
        return self.ans
```
Use backtrack to traverse all the possibilities. 

Powerful as Python 3, there must be a solution that requires a lot less effort but defeats the purpose of this problem:
```python
from itertools import product

class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        n2l = ['', '', 'abc', 'def', 'ghi', 'jkl', 'mno', 'pqrs', 'tuv', 'wxyz']
        possibles = [n2l[int(i)] for i in digits]
        return [''.join(x) for x in product(*possibles) if x]
```
