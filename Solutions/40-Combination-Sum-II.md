# 40. Combination Sum II

Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sum to `target`.

Each number in `candidates` may only be used **once** in the combination.

**Note**: The solution set must not contain duplicate combinations.

## Example 1:
```
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
```

## Example 2:
```
Input: candidates = [2,5,2,1,2], target = 5
Output: 
[
[1,2,2],
[5]
]
```

## Constraints:
- `1 <= candidates.length <= 100`
- `1 <= candidates[i] <= 50`
- `1 <= target <= 30`

# Solution
```python
class Solution:
    def solve(self, candidates: List[int], target: int, bucket: List[int], ans: List[List[int]]) -> None:
        if target < 0:
            return
        if target == 0:
            ans.append(bucket)
        i = 0
        while i < len(candidates):
            if candidates[i] > target:
                break
            k = 0
            while True:
                if i + k == len(candidates) - 1 or candidates[i+k] != candidates[i+k+1]:
                    break
                k += 1
            k += 1
            for j in range(1, k+1):
                self.solve(candidates[i+k:], target-candidates[i]*j, bucket+[candidates[i] for _ in range(j)], ans)
            i += k
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        candidates.sort()
        ans = []
        self.solve(candidates, target, [], ans)
        return ans
```
Backtracking but with some notice on the repeating values.
