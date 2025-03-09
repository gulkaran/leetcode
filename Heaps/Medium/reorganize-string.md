# Reorganize String

[https://leetcode.com/problems/reorganize-string](https://leetcode.com/problems/reorganize-string)

Use a greedy approach to select the most frequent elements first and use a heap to get those most frequent items efficiently!

```python
import heapq 
from collections import Counter

class Solution:
    def reorganizeString(self, s: str) -> str:
        c = Counter(s)

        heap = [(-count, char) for char, count in c.items()]

        heapify(heap)

        result = ""

        while len(heap) >= 2:
            count1, char1 = heappop(heap)
            count2, char2 = heappop(heap)

            result += char1 + char2 

            if count1 + 1 != 0:
                heappush(heap, (count1 + 1, char1))

            if count2 + 1 != 0:
                heappush(heap, (count2 + 1, char2))
        
        if heap:
            count, char = heappop(heap)

            # we can use the letter more than once or its the same as the prev letter we used
            if count < -1 or (char == result[-1] if result else False):
                result = ""
       
            else:
                result += char
        
        return result
```