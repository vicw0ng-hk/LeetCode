# 78. Subsets

Given an integer array `nums`, return *all possible subsets (the power set)*.

The solution set must not contain duplicate subsets.

 

Example 1:
```
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

## Example 2:
```
Input: nums = [0]
Output: [[],[0]]
```

## Constraints:
- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`
- All the numbers of `nums` are **unique**

# Solution
```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        ans = []
        for i in range(1<<len(nums)):
            tmp = []
            for j in range(len(nums)):
                if i & (1<<j):
                    tmp.append(nums[j])
            ans.append(tmp)
        return ans
```
Simple bit manipulation.
