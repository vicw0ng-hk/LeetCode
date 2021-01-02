# 32. Longest Valid Parentheses

Given a string containing just the characters `'('` and `')'`, find the length of the longest valid (well-formed) parentheses substring.

## Example 1:
```
Input: s = "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()".
```

## Example 2:
```
Input: s = ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()".
```

## Example 3:
```
Input: s = ""
Output: 0
```

## Constraints:
- <code>0 <= s.length <= 3 * 10<sup>4</sup></code>
- `s[i]` is `'('`, or `')'`.

# Solution
```python
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        left_bracket_1, right_bracket_1 = 0, 0
        left_bracket_2, right_bracket_2 = 0, 0
        current_length_1, current_length_2 = 0, 0
        max_length = 0
        for i in range(len(s)):
            if s[i] == '(':           left_bracket_1 += 1
            else:                    right_bracket_1 += 1
            if s[len(s)-i-1] == ')': right_bracket_2 += 1
            else:                     left_bracket_2 += 1
            if left_bracket_1 == right_bracket_1:
                max_length = max(max_length, 2*left_bracket_1)
            elif left_bracket_1 <= right_bracket_1:
                left_bracket_1 = right_bracket_1 = 0
            if left_bracket_2 == right_bracket_2:
                max_length = max(max_length, 2*right_bracket_2)
            elif left_bracket_2 >= right_bracket_2:
                left_bracket_2 = right_bracket_2 = 0
        return max_length
```
Use two pointers from both ends of the string. 
