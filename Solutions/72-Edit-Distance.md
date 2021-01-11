# 72. Edit Distance

Given two strings `word1` and `word2`, return *the minimum number of operations required to convert `word1` to `word2`*.

You have the following three operations permitted on a word:
- Insert a character
- Delete a character
- Replace a character


## Example 1:
```
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation: 
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')
```

## Example 2:
```
Input: word1 = "intention", word2 = "execution"
Output: 5
Explanation: 
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')
```

## Constraints:
- `0 <= word1.length, word2.length <= 500`
- `word1` and `word2` consist of lowercase English letters.

# Solution
```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        memo = {(0,0): 0}
        a, b = len(word1), len(word2)
        for i in range(1, a+1):
            memo[(i,0)] = i
        for j in range(1, b+1):
            memo[(0,j)] = j
        for i in range(1, a+1):
            for j in range(1, b+1):
                cost = 0 if word1[i-1] == word2[j-1] else 1
                memo[(i,j)] = min(memo[(i-1,j)]+1, memo[(i,j-1)]+1, memo[(i-1,j-1)]+cost)
        return memo[(a,b)]
```
Classic dynamic programming for edit distance. 
