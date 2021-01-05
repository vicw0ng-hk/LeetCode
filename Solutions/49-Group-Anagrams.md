# 49. Group Anagrams

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Example 1:
```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

## Example 2:
```
Input: strs = [""]
Output: [[""]]
```

## Example 3:
```
Input: strs = ["a"]
Output: [["a"]]
```

## Constraints:
- <code>1 <= strs.length <= 10<sup>4</sup></code>
- `0 <= strs[i].length <= 100`
- `strs[i]` consists of lower-case English letters.

# Solution
```python
from collections import defaultdict

class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        ans = defaultdict(list)
        for s in strs:
            tmp = [0 for _ in range(26)]
            for c in s:
                tmp[ord(c)-ord('a')] += 1
            ans[tuple(tmp)] += [s]
        return ans.values()
```
Categorize the strings by count of characters.
