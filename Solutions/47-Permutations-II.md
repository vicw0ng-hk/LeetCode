# 47. Permutations II

Given a collection of numbers, `nums`, that might contain duplicates, return *all possible unique permutations **in any order***.

## Example 1:
```
Input: nums = [1,1,2]
Output:
[[1,1,2],
 [1,2,1],
 [2,1,1]]
```

## Example 2:
```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

## Constraints:
- `1 <= nums.length <= 8`
- `-10 <= nums[i] <= 10`

# Solution
```python
class Solution:
    def find(self, nums: List[int], i: int, ans: List[List[int]]):
        if i == len(nums):
            ans.append(nums.copy())
            return
        for j in range(i, len(nums)):
            if j > i and nums[j] == nums[i]:
                continue
            nums[i], nums[j] = nums[j], nums[i]
            self.find(nums, i+1, ans)
        for j in range(len(nums)-1, i, -1):
            nums[i], nums[j] = nums[j], nums[i]
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        ans = []
        self.find(nums, 0, ans)
        return ans
```
DFS but skipping some cases with the same values.
