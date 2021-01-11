# 80. Remove Duplicates from Sorted Array II

Given a sorted array *nums*, remove the duplicates [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) such that duplicates appeared at most *twice* and return the new length.

Do not allocate extra space for another array; you must do this by modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) with O(1) extra memory.

**Clarification**:

Confused why the returned value is an integer, but your answer is an array?

Note that the input array is passed in by **reference**, which means a modification to the input array will be known to the caller.

Internally you can think of this:

```
// nums is passed in by reference. (i.e., without making a copy)
int len = removeDuplicates(nums);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

## Example 1:
```
Input: nums = [1,1,1,2,2,3]
Output: 5, nums = [1,1,2,2,3]
Explanation: Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3 respectively. It doesn't matter what you leave beyond the returned length.
```

## Example 2:
```
Input: nums = [0,0,1,1,1,1,2,3,3]
Output: 7, nums = [0,0,1,1,2,3,3]
Explanation: Your function should return length = 7, with the first seven elements of nums being modified to 0, 0, 1, 1, 2, 3 and 3 respectively. It doesn't matter what values are set beyond the returned length.
```

## Constraints:
- <code>1 <= nums.length <= 3 * 10<sup>4</sup></code>
- <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
- `nums` is sorted in ascending order

# Solution
```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        previous, flag = nums[0], False
        i = 1
        for j in range(1, len(nums)):
            if nums[j] == previous:
                if not flag:
                    nums[i] = nums[j]
                    i += 1
                    flag = True
            else:
                nums[i] = nums[j]
                i += 1
                flag = False
                previous = nums[j]
        return i
```
Use two pointers, one for traversing the array, the other for filling in legal elements.
