# 50. Pow(x, n)

Implement [pow(x, n)](https://www.cplusplus.com/reference/valarray/pow/), which calculates *x* raised to the power *n* (i.e. x<sup>n</sup>).

## Example 1:
```
Input: x = 2.00000, n = 10
Output: 1024.00000
```

## Example 2:
```
Input: x = 2.10000, n = 3
Output: 9.26100
```

## Example 3:
<pre><code>Input: x = 2.00000, n = -2
Output: 0.25000
Explanation: 2<sup>-2</sup> = 1/2<sup>2</sup> = 1/4 = 0.25
</pre></code>

## Constraints:
- `-100.0 < x < 100.0`
- <code>-2<sup>31</sup> <= n <= 2<sup>31</sup>-1</code>
- <code>-10<sup>4</sup> <= xn <= 10<sup>4</sup></code>

# Solution
```python
class Solution:
    def __init__(self):
        self.memo = {0: 1.0}
    def myPow(self, x: float, n: int) -> float:
        if n < 0:
            return 1 / self.myPow(x, 0-n)
        if n not in self.memo:
            if n == 1:
                self.memo[n] = x
            elif n & 1:
                self.memo[n] = self.myPow(x, n>>1) * self.myPow(x, n>>1) * x
            else:
                self.memo[n] = self.myPow(x, n>>1) * self.myPow(x, n>>1)
        return self.memo[n]
```
Typical [exponentiation by squaring](https://en.wikipedia.org/wiki/Exponentiation_by_squaring)
