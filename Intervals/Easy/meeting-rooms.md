# Meeting Rooms

[https://neetcode.io/problems/meeting-schedule](https://neetcode.io/problems/meeting-schedule)

Sort the intervals!

```python
class Solution:
    def canAttendMeetings(self, intervals: List[Interval]) -> bool:

        intervals.sort(key=lambda x: x.start)

        for i in range(len(intervals) - 1):
            if intervals[i].end > intervals[i + 1].start:
                return False

        
        return True
```