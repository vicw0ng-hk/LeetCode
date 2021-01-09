# 65. Valid Number

Validate if a given string can be interpreted as a decimal number.

Some examples:

`"0"` => `true`<br>
`" 0.1 "` => `true`<br>
`"abc"` => `false`<br>
`"1 a"` => `false`<br>
`"2e10"` => `true`<br>
`" -90e3   "` => `true`<br>
`" 1e"` => `false`<br>
`"e3"` => `false`<br>
`" 6e-1"` => `true`<br>
`" 99e2.5 "` => `false`<br>
`"53.5e93"` => `true`<br>
`" --6 "` => `false`<br>
`"-+3"` => `false`<br>
`"95a54e53"` => `false`

**Note**: It is intended for the problem statement to be ambiguous. It would be best if you gathered all requirements up front before implementing one. However, here is a list of characters that can be in a valid decimal number:

- Numbers 0-9
- Exponent - "e"
- Positive/negative sign - "+"/"-"
- Decimal point - "."

Of course, the context of these characters also matters in the input.

## Example 1:
```
Input: s = "0"
Output: true
```

## Example 2:
```
Input: s = "3"
Output: true
```

## Constraints:
- `1 <= s.length <= 20`
- `s` consists of only English letters, digits, space `' '`, plus `'+'`, minus `'-'`, or dot `'.'`

# Solution
```python
class Solution:
    def isNumber(self, s: str) -> bool:
        s = s.strip()
        point = expo = digit = False
        for i in range(len(s)):
            if s[i] in ['+', '-']:
                if i > 0 and s[i-1] != 'e':
                    return False
            elif s[i] == '.':
                if point or expo:
                    return False
                point = True
            elif s[i] == 'e':
                if expo or not digit:
                    return False
                expo, digit = True, False
            elif s[i].isdigit():
                digit = True
            else:
                return False
        return digit
```
Theis is not difficult logic but extremely unfriendly with the conditions. Hated it. Python could do better:
```python
class Solution:
    def isNumber(self, s: str) -> bool:
        try:
            float(s)
            return True
        except :
            return False
```
