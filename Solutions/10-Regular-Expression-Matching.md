# 10. Regular Expression Matching

Given an input string (`s`) and a pattern (`p`), implement regular expression matching with support for `'.'` and `'*'` where: 

- `'.'` Matches any single character.
- `'*'` Matches zero or more of the preceding element.

The matching should cover the **entire** input string (not partial).

## Example 1:
```
Input: s = "aa", p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
```

## Example 2:
```
Input: s = "aa", p = "a*"
Output: true
Explanation: '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
```

## Example 3:
```
Input: s = "ab", p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
```

## Example 4:
```
Input: s = "aab", p = "c*a*b"
Output: true
Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore, it matches "aab".
```

## Example 5:
```
Input: s = "mississippi", p = "mis*is*p*."
Output: false
```

## Constraints:
- `0 <= s.length <= 20`
- `0 <= p.length <= 30`
- `s` contains only lowercase English letters.
- `p` contains only lowercase English letters, `'.'`, and `'*'`.
- It is guaranteed for each appearance of the character `'*'`, there will be a previous valid character to match.

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
                flag = i < len(s) and p[j] in [s[i], '.']
                if j + 1 < len(p) and p[j+1] == '*':
                    ans = self.dp(s, p, i, j+2) or (flag and self.dp(s, p, i+1, j))
                else:
                    ans = flag and self.dp(s, p, i+1, j+1)
            self.memo[i, j] = ans
        return self.memo[i, j]
    def isMatch(self, s: str, p: str) -> bool:
        return self.dp(s, p, 0 ,0)
```

Use a top-down dynamic programming approach.

This will also work, but it defeats the purpose of this problem:
```python
import re

class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        return (re.fullmatch(p, s) is not None)
```
