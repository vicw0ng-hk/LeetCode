# 69. Sqrt(x)

Given a non-negative integer `x`, compute and return *the square root of* `x`.

Since the return type is an integer, the decimal digits are **truncated**, and only **the integer part** of the result is returned.

## Example 1:
```
Input: x = 4
Output: 2
```

## Example 2:
```
Input: x = 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since the decimal part is truncated, 2 is returned.
```

## Constraints:
- <code>0 <= x <= 2<sup>31</sup> - 1</code>

# Solution
```python
class Solution:
    def mySqrt(self, x: int) -> int:
        left, right = 0, (x + 1) // 2
        while left < right:
            mid = (left + right + 1) // 2
            if mid * mid <= x:
                left = mid
            else:
                right = mid - 1
        return left
```
Use binary search.
