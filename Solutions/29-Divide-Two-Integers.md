# 29. Divide Two Integers

Given two integers `dividend` and `divisor`, divide two integers without using multiplication, division, and mod operator.

Return the quotient after dividing `dividend` by `divisor`.

The integer division should truncate toward zero, which means losing its fractional part. For example, `truncate(8.345) = 8` and `truncate(-2.7335) = -2`.

**Note**:

- Assume we are dealing with an environment that could only store integers within the 32-bit signed integer range: [−2<sup>31</sup>,  2<sup>31</sup> − 1]. For this problem, assume that your function **returns 2<sup>31</sup> − 1 when the division result overflows**. 

## Example 1:
```
Input: dividend = 10, divisor = 3
Output: 3
Explanation: 10/3 = truncate(3.33333..) = 3.
```

## Example 2:
```
Input: dividend = 7, divisor = -3
Output: -2
Explanation: 7/-3 = truncate(-2.33333..) = -2.
```

## Example 3:
```
Input: dividend = 0, divisor = 1
Output: 0
```

## Example 4:
```
Input: dividend = 1, divisor = 1
Output: 1
```

## Constraints:
- <code>-2<sup>31</sup> <= dividend, divisor <= 2<sup>31</sup> - 1</code>
- `divisor != 0`

# Solution
```python
class Solution:
    def divide_by_hand(self, dividend: int, divisor: int) -> (int, int):
        i = 0
        total = 0
        while True:
            if total + divisor > dividend:
                break
            i += 1
            total += divisor
        return (i, dividend - total)
    def divide(self, dividend: int, divisor: int) -> int:
        _overflow = (1<<31) - 1
        if abs(dividend) < abs(divisor):
            return 0
        neg = (dividend < 0 < divisor or divisor < 0 < dividend)
        dividend, divisor = abs(dividend), abs(divisor)
        ans = ''
        str_dividend, str_divisor = str(dividend), str(divisor)
        carry = str(str_dividend[0:len(str_divisor)-1])
        for i in range(len(str_dividend) - len(str_divisor) + 1):
            carry += str_dividend[i+len(str_divisor)-1]
            tmp = self.divide_by_hand(int(carry), divisor)
            ans += str(tmp[0])
            carry = str(tmp[1])
        ans = 0 - int(ans) if neg else int(ans)
        return ans if 0 - (1<<31) <= ans < (1<<31) else _overflow
```
Go back to when you were in primary school: [Long Division](https://en.wikipedia.org/wiki/Long_division).
