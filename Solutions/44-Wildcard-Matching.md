# 44. Wildcard Matching

Given an input string (`s`) and a pattern (`p`), implement wildcard pattern matching with support for `'?'` and `'*'` where:

- `'?'` Matches any single character.
- `'*'` Matches any sequence of characters (including the empty sequence).
The matching should cover the **entire** input string (not partial).

## Example 1:
```
Input: s = "aa", p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
```

## Example 2:
```
Input: s = "aa", p = "*"
Output: true
Explanation: '*' matches any sequence.
```

## Example 3:
```
Input: s = "cb", p = "?a"
Output: false
Explanation: '?' matches 'c', but the second letter is 'a', which does not match 'b'.
```

## Example 4:
```
Input: s = "adceb", p = "*a*b"
Output: true
Explanation: The first '*' matches the empty sequence, while the second '*' matches the substring "dce".
```

## Example 5:
```
Input: s = "acdcb", p = "a*c?b"
Output: false
```

## Constraints:
- `0 <= s.length, p.length <= 2000`
- `s` contains only lowercase English letters.
- `p` contains only lowercase English letters, `'?'` or `'*'`.

# Solution
```python
class Solution:
    def __init__(self):
        self.memo = {}
    def dp(self, s: str, p: str, i: int, j: int) -> bool:
        if (i, j) not in self.memo:
            if j == len(p):
                ans = (i == len(s))
            else:
                if j < len(p) and p[j] == '*':
                    ans = self.dp(s, p, i, j+1) or (i < len(s) and self.dp(s, p, i+1, j))
                else:
                    ans = i < len(s) and p[j] in [s[i], '?'] and self.dp(s, p, i+1, j+1)
            self.memo[i, j] = ans
        return self.memo[i, j]
    def isMatch(self, s: str, p: str) -> bool:
        return self.dp(s, p, 0 ,0)
```
A small modification of [10. Regular Expression Matching](/Solutions/10-Regular-Expression-Matching.md).
