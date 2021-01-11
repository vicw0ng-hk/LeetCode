# 75. Sort Colors

Given an array `nums` with `n` objects colored red, white, or blue, sort them [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

Here, we will use the integers `0`, `1`, and `2` to represent the color red, white, and blue respectively.

**Follow up**:
- Could you solve this problem without using the library's sort function?
- Could you come up with a one-pass algorithm using only `O(1)` constant space?

## Example 1:
```
Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

## Example 2:
```
Input: nums = [2,0,1]
Output: [0,1,2]
```

## Example 3:
```
Input: nums = [0]
Output: [0]
```

## Example 4:
```
Input: nums = [1]
Output: [1]
```

## Constraints:
- `n == nums.length`
- `1 <= n <= 300`
- `nums[i]` is `0`, `1`, or `2`

# Solution
```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        counter = [0, 0, 0]
        for n in nums:
            counter[n] += 1
        i = 0
        for c in range(counter[0]):
            nums[i] = 0
            i += 1
        for c in range(counter[1]):
            nums[i] = 1
            i += 1
        for c in range(counter[2]):
            nums[i] = 2
            i += 1
```
Simple [counting sort](https://en.wikipedia.org/wiki/Counting_sort).
