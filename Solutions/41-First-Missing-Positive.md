# 41. First Missing Positive

Given an unsorted integer array `nums`, find the smallest missing positive integer.

**Follow up**: Could you implement an algorithm that runs in `O(n)` time and uses constant extra space?

## Example 1:
```
Input: nums = [1,2,0]
Output: 3
```

## Example 2:
```
Input: nums = [3,4,-1,1]
Output: 2
```

## Example 3:
```
Input: nums = [7,8,9,11,12]
Output: 1
```

## Constraints:
- `0 <= nums.length <= 300`
- <code>-2<sup>31</sup> <= nums[i] <= 2<sup>31</sup> - 1</code>

# Solution
```python
class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        nums.append(0)
        n_plus_one = len(nums)
        for i in range(n_plus_one):
            if not 0 <= nums[i] < n_plus_one:
                nums[i] = 0
        for i in range(n_plus_one):
            nums[nums[i]%n_plus_one] += n_plus_one
        for i in range(1, n_plus_one):
            if nums[i] // n_plus_one < 1:
                return i
        return n_plus_one
```
With an array of length `n`, the answer could only be in `[1, 2, ..., n+1]`. So first we could get rid of all other values that are outside of `[1, 2, ..., n]`. Then normally we would use a hash table to record the occurence of the values, but we could use a little trick here to record it in the original array. 
