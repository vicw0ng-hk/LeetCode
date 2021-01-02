# 31. Next Permutation

Implement **next permutation**, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such an arrangement is not possible, it must rearrange it as the lowest possible order (i.e., sorted in ascending order).

The replacement must be [in place](https://en.wikipedia.org/wiki/In-place_algorithm) and use only constant extra memory.

## Example 1:
```
Input: nums = [1,2,3]
Output: [1,3,2]
```

## Example 2:
```
Input: nums = [3,2,1]
Output: [1,2,3]
```

## Example 3:
```
Input: nums = [1,1,5]
Output: [1,5,1]
```

## Example 4:
```
Input: nums = [1]
Output: [1]
```

## Constraints:
- 1 <= nums.length <= 100
- 0 <= nums[i] <= 100

# Solution
```python
class Solution:
    def reverse(self, nums: List[int], i: int, j: int) -> None:
        k = 0
        while i + k < j - k:
            nums[i+k], nums[j-k] = nums[j-k], nums[i+k]
            k += 1
    def nextPermutation(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        i, flag = len(nums) - 1, 0
        while i > 0:
            i -= 1
            if nums[i] < nums[i+1]:
                flag = 1
                break
        if i == 0 and not flag: 
            self.reverse(nums, 0, len(nums)-1)
        else:
            j = i + 1
            target = j
            while j + 1 < len(nums):
                j += 1
                if nums[i] < nums[j] <= nums[target]:
                    target = j
            nums[i], nums[target] = nums[target], nums[i]
            self.reverse(nums, i+1, len(nums)-1)
```
First find the find the first descending node from the right side, then start there to the right side to find the smallest node that's larger than the found node, swap their values and then reverse the whole section on the right side of the first found node.
