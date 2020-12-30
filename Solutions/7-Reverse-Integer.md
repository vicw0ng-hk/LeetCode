# 7. Reverse Integer

Given a 32-bit signed integer, reverse digits of an integer.

**Note**:

Assume we are dealing with an environment that could only store integers within the 32-bit signed integer range: [−2<sup>31</sup>,  2<sup>31</sup> − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

## Example 1:
```
Input: x = 123
Output: 321
```

## Example 2:
```
Input: x = -123
Output: -321
```

## Example 3:
```
Input: x = 120
Output: 21
```

## Example 4:
```
Input: x = 0
Output: 0
```

## Constraints:
- `-231 <= x <= 231 - 1`

# Solution
```python
class Solution:
    def reverse(self, x: int) -> int:
        ans = int(str(x)[::-1]) if x >= 0 else (-1) * int(str(x)[-1:0:-1])
        return ans if -2**31 <= ans < 2**31 else 0
```
Python 3's convenient string operation.
