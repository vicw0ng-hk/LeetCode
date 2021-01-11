# 76. Minimum Window Substring

Given two strings `s` and `t`, return *the minimum window in `s` which will contain all the characters in `t`*. If there is no such window in `s` that covers all characters in `t`, return *the empty string `""`*.

**Note** that If there is such a window, it is guaranteed that there will always be only one unique minimum window in `s`.

## Example 1:
```
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
```

## Example 2:
```
Input: s = "a", t = "a"
Output: "a"
```

## Constraints:
- <code>1 <= s.length, t.length <= 10<sup>5</sup></code>
- `s` and `t` consist of English letters.

# Solution
```python
from collections import Counter

class Solution:
    def minWindow(self, s: str, t: str) -> str:
        target, target_length = Counter(t), len(t)
        start, finish = 0, -1
        start_tmp = 0
        for finish_tmp in range(len(s)):
            target_length -= 1 if target[s[finish_tmp]] > 0 else 0
            target[s[finish_tmp]] -= 1
            if target_length == 0:
                while target[s[start_tmp]] < 0:
                    target[s[start_tmp]] += 1
                    start_tmp += 1
                if finish == -1 or finish_tmp - start_tmp <= finish - start:
                    start, finish = start_tmp, finish_tmp
                target[s[start_tmp]] += 1
                start_tmp += 1
                target_length += 1
        return s[start:finish+1]
```
Use a sliding window, and keep a hash table of the remaining target.
