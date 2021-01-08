# 57. Insert Interval

Given a set of *non-overlapping* intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.

## Example 1:
```
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
```

## Example 2:
```
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
```

## Example 3:
```
Input: intervals = [], newInterval = [5,7]
Output: [[5,7]]
```

## Example 4:
```
Input: intervals = [[1,5]], newInterval = [2,3]
Output: [[1,5]]
```

## Example 5:
```
Input: intervals = [[1,5]], newInterval = [2,7]
Output: [[1,7]]
```

## Constraints:
- <code>0 <= intervals.length <= 10<sup>4</sup></code>
- `intervals[i].length == 2`
- <code>0 <= intervals[i][0] <= intervals[i][1] <= 10<sup>5</sup></code>
- `intervals` is sorted by `intervals[i][0]` in **ascending** order.
- `newInterval.length == 2`
- <code>0 <= newInterval[0] <= newInterval[1] <= 10<sup>5</sup></code>

# Solution
```python
class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        if not intervals:
            return [newInterval]
        left, right = 0, len(intervals)-1
        while left < right:
            mid = (left + right) // 2
            if intervals[mid][1] < newInterval[0]:
                left = mid + 1
            else:
                right = mid
        if intervals[left][1] >= newInterval[0]:
            pos_1 = left
        else:
            return intervals + [newInterval]
        left, right = 0, len(intervals)-1
        while left < right:
            mid = (left + right + 1) // 2
            if intervals[mid][0] > newInterval[1]:
                right = mid - 1
            else:
                left = mid
        if intervals[left][0] <= newInterval[1]:
            pos_2 = right
        else:
            return [newInterval] + intervals
        return intervals[:pos_1] + [[min(newInterval[0], intervals[pos_1][0]), max(newInterval[1],intervals[pos_2][1])]] + intervals[pos_2+1:]
```
Search for position and reconstruct. 
