# 3. Longest Substring Without Repeating Characters

Given a string `s`, find the length of the **longest substring** without repeating characters.

## Example 1:
```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

## Example 2:
```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

## Example 3:
```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

## Example 4:
```
Input: s = ""
Output: 0
```

## Constraints:
- <code>0 <= s.length <= 5 * 10<sup>4</sup></code>
- `s` consists of English letters, digits, symbols and spaces.

# Solution
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if len(s) < 2: return len(s)
        left, right = 0, 1
        current_length, max_length = 1, 1
        memo = [s[0]]
        while right != len(s):
            right += 1
            current_length += 1
            if s[right-1] in memo:
                while left < right:
                    left += 1
                    current_length -= 1
                    if s[left-1] == s[right-1]:
                        break
                    else:
                        memo.remove(s[left-1])
            else:
                memo.append(s[right-1])
            max_length = max(max_length, current_length)
        return max_length
```
Use a sliding window
