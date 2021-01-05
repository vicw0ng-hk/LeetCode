# 46. Permutations

Given an array `nums` of distinct integers, return *all the possible permutations*. You can return the answer in **any order**.

## Example 1:
```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

## Example 2:
```
Input: nums = [0,1]
Output: [[0,1],[1,0]]
```

## Example 3:
```
Input: nums = [1]
Output: [[1]]
```

## Constraints:
- `1 <= nums.length <= 6`
- `-10 <= nums[i] <= 10`
- All the integers of `nums` are **unique**.

# Solution
```python
class Solution:
    def find(self, nums: List[int], bucket: List[int], ans: List[List[int]]):
        if not nums:
            ans.append(bucket)
        for i in range(len(nums)):
            self.find(nums[:i]+nums[i+1:], bucket+[nums[i]], ans)
    def permute(self, nums: List[int]) -> List[List[int]]:
        ans = []
        self.find(nums, [], ans)
        return ans
```
Simple DFS.
