# Kth Largest Element in a Stream

[https://leetcode.com/problems/kth-largest-element-in-a-stream/](https://leetcode.com/problems/kth-largest-element-in-a-stream/)

We use a ***min*** heap of length $k$ to do complete this problem optimally. 

**Constructor**

- we heapify the nums array and pop $n-k$ times to have a heap of length $k$
- $O((n-k)\log n)$ time complexity

**Add Function**

- We add the element into the heap, remove one, then return the min element
    - why do we remove twice? for example if $k=3$, we add the element which *reheapify’s* the heap (reorder’s the heap based on the heap ordering property).
    - the heap is now $k + 1$ length, so we pop once (maintain $k$ length heap) and we can **peek** into the min element without removing by simply accessing it at 0-index

```python
import heapq

class KthLargest:

    def __init__(self, k: int, nums: List[int]):
        self.heap = nums
        self.k = k

        heapify(self.heap)

        # n - k log n
        for i in range(len(nums) - k):
            heappop(self.heap)

    def add(self, val: int) -> int:
        heappush(self.heap, val)

        if len(self.heap) > self.k:
            heappop(self.heap)
        
        return self.heap[0]
```