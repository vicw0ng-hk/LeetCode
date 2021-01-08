# 60. Permutation Sequence

The set `[1, 2, 3, ..., n]` contains a total of `n!` unique permutations.

By listing and labeling all of the permutations in order, we get the following sequence for `n = 3`:

1. `"123"`
2. `"132"`
3. `"213"`
4. `"231"`
5. `"312"`
6. `"321"`

Given `n` and `k`, return the <code>k<sup>th</sup></code> permutation sequence.

## Example 1:
```
Input: n = 3, k = 3
Output: "213"
```

## Example 2:
```
Input: n = 4, k = 9
Output: "2314"
```

## Example 3:
```
Input: n = 3, k = 1
Output: "123"
```

## Constraints:
- `1 <= n <= 9`
- `1 <= k <= n!`

# Solution
```python
class Solution:
    def getPermutation(self, n: int, k: int) -> str:
        if n == 1:
            return "1"
        fact = {1: 1}
        for i in range(2, n):
            fact[i] = fact[i-1] * i
        mod = []
        k -= 1
        for i in range(n-1,0,-1):
            mod.append(k//fact[i])
            k %= fact[i]
        nums = list(range(1, n+1))
        ans = ""
        for m in mod:
            ans += str(nums[m])
            nums = nums[:m] + nums[m+1:]
        ans += str(nums[0])
        return ans
```
Notice the relation between the k<sup>th</sup> digit and the number of possible permutations after it. 
