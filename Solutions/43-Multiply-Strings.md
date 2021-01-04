# 43. Multiply Strings

Given two non-negative integers `num1` and `num2` represented as strings, return the product of `num1` and `num2`, also represented as a string.

**Note**: You must not use any built-in BigInteger library or convert the inputs to integer directly.

## Example 1:
```
Input: num1 = "2", num2 = "3"
Output: "6"
```

## Example 2:
```
Input: num1 = "123", num2 = "456"
Output: "56088"
```

## Constraints:
- `1 <= num1.length, num2.length <= 200`
- `num1` and `num2` consist of digits only.
- Both `num1` and `num2` do not contain any leading zero, except the number `0` itself.

# Solution
```python
class Solution:
    def multiply(self, num1: str, num2: str) -> str:
        if num1 == "0" or num2 == "0":
            return "0"
        ans = [-1 for _ in range(len(num1)+len(num2))]
        for i in range(len(num1)-1, -1, -1):
            for j in range(len(num2)-1, -1, -1):
                if ans[i+j+1] == -1:
                    ans[i+j+1] = 0
                tmp = (ord(num1[i]) - ord('0')) * (ord(num2[j]) - ord('0')) + ans[i+j+1]
                ans[i+j+1] = tmp % 10
                if tmp // 10 > 0:
                    if ans[i+j] == -1:
                        ans[i+j] = tmp // 10
                    else:
                        ans[i+j] += tmp // 10
        ans_str = ""
        for i in range(len(num1)+len(num2)-1, -1, -1):
            if ans[i] == -1:
                break
            ans_str = str(ans[i]) + ans_str
        return ans_str
```
Primary School stuff: [Long Multiplication](https://en.wikipedia.org/wiki/Multiplication_algorithm#Long_multiplication)
