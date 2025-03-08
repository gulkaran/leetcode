# k Closest Points to Origin

[https://leetcode.com/problems/k-closest-points-to-origin/](https://leetcode.com/problems/k-closest-points-to-origin/)

simple heap!

```python
import heapq

class Solution:
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
        
        heap = []

        for x, y in points:
            d = math.sqrt(x**2 + y**2)
            heappush(heap, [d, [x,y]])
        
        output = []
        
        for i in range(k):
            d, [x,y] = heappop(heap)
            output.append([x,y])

        return output
```