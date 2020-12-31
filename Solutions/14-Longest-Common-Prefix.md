# 14. Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

## Example 1:
```
Input: strs = ["flower","flow","flight"]
Output: "fl"
```

## Example 2:
```
Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

## Constraints:
- `0 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i]` consists of only lower-case English letters.

# Solution
```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        if len(strs) < 2:
            return strs[0] if strs else ''
        strs.sort()
        pair = tuple(zip(strs[0], strs[-1]))
        ans = ''
        for i in range(len(pair)):
            if pair[i][0] == pair[i][1]:
                ans += pair[i][0]
            else:
                break
        return ans
```
simple string sorting and comparing. 