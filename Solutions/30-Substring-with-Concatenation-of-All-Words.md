# 30. Substring with Concatenation of All Words

You are given a string `s` and an array of strings `words` of **the same length**. Return all starting indices of substring(s) in `s` that is a concatenation of each word in `words` **exactly once**, **in any order**, and **without any intervening characters**.

You can return the answer in **any order**.

## Example 1:
```
Input: s = "barfoothefoobarman", words = ["foo","bar"]
Output: [0,9]
Explanation: Substrings starting at index 0 and 9 are "barfoo" and "foobar" respectively.
The output order does not matter, returning [9,0] is fine too.
```

## Example 2:
```
Input: s = "wordgoodgoodgoodbestword", words = ["word","good","best","word"]
Output: []
```

## Example 3:
```
Input: s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]
Output: [6,9,12]
```

## Constraints:
- <code>1 <= s.length <= 10<sup>4</sup></code>
- `s` consists of lower-case English letters.
- `1 <= words.length <= 5000`
- `1 <= words[i].length <= 30`
- `words[i]` consists of lower-case English letters.

# Solution
```python
from collections import Counter

class Solution:
    def findSubstring(self, s: str, words: List[str]) -> List[int]:
        s_length, words_count = len(s), len(words)
        word_length = len(words[0])
        total_length = word_length * words_count
        words_map = dict(Counter(words))
        ans = []
        for i in range(s_length-total_length+1):
            tmp = {}
            for j in range(i, i+total_length, word_length):
                current_word = s[j:j+word_length]
                if current_word in words_map:
                    if current_word in tmp: 
                        tmp[current_word] += 1
                    else:
                        tmp[current_word] = 1
                    if tmp[current_word] > words_map[current_word]:
                        break
                else:
                    break
            if tmp == words_map: 
                ans.append(i)
        return ans
```
I don't like the idea of this problem. It is very basic in logic, but a bit more complicated in implementation. Use 2 maps (dictionaries) would do the trick. 
