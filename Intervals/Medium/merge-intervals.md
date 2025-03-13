# Merge Intervals

[https://leetcode.com/problems/merge-intervals/](https://leetcode.com/problems/merge-intervals/)

Lowkey stack problem

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        
        intervals.sort(key=lambda x : x[0])

        merged = [intervals[0]]

        # main algorithm
        for i in range(1, len(intervals)):

            if intervals[i][0] <= merged[-1][1]:
                new_interval = [merged[-1][0], max(intervals[i][1], merged[-1][1])]
                merged.pop()
                merged.append(new_interval)
            
            else:
                merged.append(intervals[i])

        return merged

```