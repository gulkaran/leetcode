# Last Stone Weight

[https://leetcode.com/problems/last-stone-weight/](https://leetcode.com/problems/last-stone-weight/)

Max heap problem!

```python
import heapq

class Solution:
    def lastStoneWeight(self, stones: List[int]) -> int:
        stones = [-i for i in stones]
        
        heapify(stones)

        while len(stones) >= 2:
            y = -heappop(stones)
            x = -heappop(stones)

            if x == y:
                continue

            heappush(stones, -(y-x))

        return -stones[0] if len(stones) == 1 else 0
```