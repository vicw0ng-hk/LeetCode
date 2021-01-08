# 58. Length of Last Word

Given a string `s` consists of some words separated by spaces, return *the length of the last word in the string. If the last word does not exist, return* `0`.

A **word** is a maximal substring consisting of non-space characters only.

## Example 1:
```
Input: s = "Hello World"
Output: 5
```

## Example 2:
```
Input: s = " "
Output: 0
```

## Constraints:
- <code>1 <= s.length <= 10<sup>4</sup></code>
- `s` consists of only English letters and spaces `' '`

# Solution
```python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        s = s.split()
        return len(s[-1]) if s else 0
```
Simple Python string operation.
