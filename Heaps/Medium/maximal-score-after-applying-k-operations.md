# Maximal Score After Applying K Operations

[https://leetcode.com/problems/maximal-score-after-applying-k-operations/](https://leetcode.com/problems/maximal-score-after-applying-k-operations/description/)

### Brute Force Greedy Algorithm

First intuition is a greedy algorithm which takes the **max** element of the array and finds that index and we can compute the answer pretty straight forward from there. However, this results in TLE. 

```python
class Solution:
    def maxKelements(self, nums: List[int], k: int) -> int:
        score = 0
        for _ in range(k):
            i = nums.index(max(nums))

            score += nums[i]
            nums[i] = ceil(nums[i] / 3)
        
        return score
```

### Heap Algorithm

We can use a **max heap** to get the max element in $O(\log n)$ time. Since we are also given the *nums* array, we can use the built-in heapify algorithm to convert *nums* into a max heap in $O(n)$ time instead of traditional $O(n\log n)$ methods.

```python
import heapq

class Solution:
    def maxKelements(self, nums: List[int], k: int) -> int:
        
        score = 0

        for i in range(len(nums)):
            nums[i] *= -1

        heapq.heapify(nums)

        for _ in range(k):
            x = -heapq.heappop(nums)
            score += x
            heapq.heappush(nums, -ceil(x / 3))

        return score
```

Note in Python there is only a min heap variant given by heapq, so we simply just negate the values.