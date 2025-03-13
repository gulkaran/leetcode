# Meeting Rooms II

[https://neetcode.io/problems/meeting-schedule-ii](https://neetcode.io/problems/meeting-schedule-ii)

Use a min heap to track the end times. If a start time starts after the minimum ending time we’ve processed so far, it can reuse a room!

```python
import heapq

class Solution:
    def minMeetingRooms(self, intervals: List[Interval]) -> int:
        
        intervals.sort(key=lambda x: x.start)

        heap = []

        for i in intervals:
            
            # reusing a room
            if heap and heap[0] <= i.start:
                heapq.heappop(heap)

            heapq.heappush(heap, i.end)

        return len(heap)
```