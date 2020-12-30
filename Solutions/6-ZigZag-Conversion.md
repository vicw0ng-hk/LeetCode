# 6. ZigZag Conversion

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string s, int numRows);
```

## Example 1:
```
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
```

## Example 2:
```
Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:
P     I    N
A   L S  I G
Y A   H R
P     I
```

## Example 3:
```
Input: s = "A", numRows = 1
Output: "A"
```

## Constraints:
- `1 <= s.length <= 1000`
- `s` consists of English letters (lower-case and upper-case), `','` and `'.'`.
- `1 <= numRows <= 1000`

# Solution
```python
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if numRows == 1:
            return s
        length = len(s)
        i = []
        x = 0
        while 2*(numRows-1)*x < length:
            i.append(2*(numRows-1)*x)
            x += 1
        for y in range(1, (numRows-2)+1):
            x = 0
            while True:
                if 2*(numRows-1)*x+y >= length:
                    break
                else:
                    i.append(2*(numRows-1)*x+y)
                if 2*(numRows-1)*x+y+2*(numRows-1-y) >= length:
                    break
                else:
                    i.append(2*(numRows-1)*x+y+2*(numRows-1-y))
                x += 1
        x = 0
        while 2*(numRows-1)*x+(numRows-1) < length:
            i.append(2*(numRows-1)*x+(numRows-1))
            x += 1
        for _i in range(len(i)):
            i[_i] = s[i[_i]]
        return "".join(i)
```

Notice the mathematical relationship of the transformation of indices:

```
0 1 2 3 4 5 6 7 8 9

0 2 4 6 8
1 3 5 7 9

0   4   8
1 3 5 7 9
2   6

0     6
1   5 7
2 4   8
3     9

0       8
1     7 9
2   6
3 5
4

...
```
