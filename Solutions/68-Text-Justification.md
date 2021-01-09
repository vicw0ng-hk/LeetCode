# 68. Text Justification

Given an array of words and a width *maxWidth*, format the text such that each line has exactly *maxWidth* characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces `' '` when necessary so that each line has exactly *maxWidth* characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line do not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left justified and no **extra** space is inserted between words.

**Note**:
- A word is defined as a character sequence consisting of non-space characters only.
- Each word's length is guaranteed to be greater than 0 and not exceed *maxWidth*.
- The input array `words` contains at least one word.

## Example 1:
```
Input: words = ["This", "is", "an", "example", "of", "text", "justification."], maxWidth = 16
Output:
[
   "This    is    an",
   "example  of text",
   "justification.  "
]
```

## Example 2:
```
Input: words = ["What","must","be","acknowledgment","shall","be"], maxWidth = 16
Output:
[
  "What   must   be",
  "acknowledgment  ",
  "shall be        "
]
Explanation: Note that the last line is "shall be    " instead of "shall     be", because the last line must be left-justified instead of fully-justified.
Note that the second line is also left-justified becase it contains only one word.
```

## Example 3:
```
Input: words = ["Science","is","what","we","understand","well","enough","to","explain","to","a","computer.","Art","is","everything","else","we","do"], maxWidth = 20
Output:
[
  "Science  is  what we",
  "understand      well",
  "enough to explain to",
  "a  computer.  Art is",
  "everything  else  we",
  "do                  "
]
```

## Constraints:
- `1 <= words.length <= 300`
- `1 <= words[i].length <= 20`
- `words[i]` consists of only English letters and symbols.
- `1 <= maxWidth <= 100`
- `words[i].length <= maxWidth`

# Solution
```python
class Solution:
    def fullJustify(self, words: List[str], maxWidth: int) -> List[str]:
        ans = []
        ptr = 0
        while ptr < len(words):
            count_words, count_words_length = 1, len(words[ptr])
            tmp_ptr = ptr
            while tmp_ptr + 1 < len(words) and count_words_length + count_words + len(words[tmp_ptr+1]) <= maxWidth:
                tmp_ptr += 1
                count_words += 1
                count_words_length += len(words[tmp_ptr])
            tmp = ""
            if tmp_ptr + 1 == len(words):
                for i in range(0, tmp_ptr-ptr+1):
                    tmp += words[i+ptr]
                    if i != tmp_ptr - ptr:
                        tmp += " "
                tmp += " " * (maxWidth - len(tmp))
            elif count_words == 1:
                tmp += words[tmp_ptr] + " " * (maxWidth - count_words_length)
            else:
                avg_space = (maxWidth - count_words_length) // (count_words - 1)
                special_space = (maxWidth - count_words_length) % (count_words - 1)
                for i in range(0, tmp_ptr-ptr+1):
                    tmp += words[i+ptr]
                    if i != tmp_ptr - ptr:
                        tmp += " " * avg_space
                        if i < special_space:
                            tmp += " "
            ans.append(tmp)
            ptr = tmp_ptr + 1
        return ans
```
Just be greedy and be careful with string operations. 
