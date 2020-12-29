# 5. Longest Palindromic Substring

Given a string `s`, return the *longest palindromic substring* in `s`.

## Example 1:
```
Input: s = "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

## Example 2:
```
Input: s = "cbbd"
Output: "bb"
```

## Example 3:
```
Input: s = "a"
Output: "a"
```

## Example 4:
```
Input: s = "ac"
Output: "a"
```

## Constraints:
- `1 <= s.length <= 1000`
- `s` consist of only digits and English letters (lower-case and/or upper-case)

# Solution
Using Brute force or even dynamic programming for Python 3 will result in **Time Limit Exceeded**. 
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        ss = '|'
        for c in s: ss += c + '|'
        P = [0 for _ in range(len(ss))]
        C, R = 0, -1
        for i in range(len(ss)):
            rad = min(P[2*C-i], R-i) if i <= R else 0
            while i + rad < len(ss) and i >= rad and ss[i-rad] == ss[i+rad]:
                rad += 1
            P[i] = rad
            if i + rad - 1 > R:
                C, R = i, i + rad - 1
        ii = P.index(max(P))
        return ss[ii+1-max(P): ii+max(P)].replace('|', '')
```
[Manacher's Algorithm](https://en.wikipedia.org/wiki/Longest_palindromic_substring#Manacher's_algorithm): O(n).
