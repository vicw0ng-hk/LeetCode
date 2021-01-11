# 77. Combinations

Given two integers *n* and *k*, return all possible combinations of *k* numbers out of 1 ... *n*.

You may return the answer in **any order**.

## Example 1:
```
Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

## Example 2:
```
Input: n = 1, k = 1
Output: [[1]]
```

## Constraints:
- `1 <= n <= 20`
- `1 <= k <= n`

# Solution
```python
class Solution:
    def __init__(self):
        self.ans = []
    def solve(self, candidate: List[int], bucket: List[int], k: int) -> None:
        if k == 0:
            self.ans.append(bucket.copy())
            return
        for i in range(len(candidate)-k+1):
            bucket.append(candidate[i])
            self.solve(candidate[i+1:], bucket, k-1)
            bucket.pop()
    def combine(self, n: int, k: int) -> List[List[int]]:
        candidate = [_ for _ in range(1, n+1)]
        self.solve(candidate, [], k)
        return self.ans
```
Simple backtracking.
