# Koko Eating Bananas

[https://leetcode.com/problems/koko-eating-bananas/](https://leetcode.com/problems/koko-eating-bananas/)

### Problem

- $piles[]$ array where the $i$th element in the array has $pile[i]$ bananas.
- Guards come back in $h$ hours
- Koko has a eating banana speed of $k$, find the minimum $k$ where she can eat all the bananas in the pile before the guards return.
    - Conditions
        - each hour Koko chooses some pile to eat and will eat $k$ bananas from that pile
        - if it has less than $k$ bananas, she eats all of them and won’t eat any more bananas

### Solution

We can notice that if we choose the max element in the $piles$ array, we guarantee that Koko will finish eating all the bananas. This is off the restriction that $len(piles) \leq h$. If this restriction didn’t exist, there would be cases with no solutions.

So now we can easily think of a brute force solution where we attempt $[1, \cdots, \text{max}(piles)]$ and accept the first $k$ value as the minimum. This would be $O(\text{max}(piles) \cdot n)$ time complexity, but we can transition this into something slightly more efficient by using binary search!

Say $k = [1, \cdots, 11]$, we can try the $k$ values using a binary search approach to cut down the number of total integers we try. We would try $k=6$ first, see that it works, then since we want to minimize $k$, we can search the values $1, \cdots, 5$. 

```python
import math

class Solution:
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        
        l, r = 1, max(piles)

        min_k = r

        while l <= r:
            k = (r + l) // 2
					
						# piles[i] = 7, k = 6
						# ceil(7/6) -> 2 hours to finish eating the bananas
            hours = 0
            for i in range(len(piles)):
                hours += math.ceil(piles[i] / k)

            if hours <= h:
                r = k - 1
                min_k = k
            else:
                l = k + 1

        return min_k
```