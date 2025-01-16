# Split Array Largest Sum

[https://leetcode.com/problems/split-array-largest-sum/description/](https://leetcode.com/problems/split-array-largest-sum/description/)

Backtracking with finding all possibilities is too slow, we can optimize this to a binary search solution.  Our $l,r$ pointers will be the possible ***range*** of values the return value can take. 

For example, if $nums=[7,2,5,10,8], m=2$

- the $l$ pointer will be the ***max*** integer of the array
    - the minimum the sum could possibly be is the largest value of the array currently
    - $l = 10$ in this example
- the $r$ pointer will be the ***sum*** of the array
    - the maximum value isn’t necessarily the sum, however, it is more efficient to compute it as that instead of trying to consider finding the real maximum value within the $m$ subarrays
    - $r=32$ in this example

### Intuition Behind Computing Mid Value

Now in typical binary search fashion, we can compute the mid point, from here. Following our example, $mid = 21$. 

The best solution we can find so far is $r$, but we can use $mid$ to see if we *greedily* take our nums array, split into $m$ groups, and find a maximum sum which is $\leq mid$, then we can search that half of the possible range of answers. 

### Greedy Portion

We can start at the beginning of the array, adding elements to the subarray sum as long as its less than or equal to our $mid$ value. Once it is larger than $mid$, we create another subarray and continue the same process.

**Question:** What if we made less than **$m$** subarrays? 

**Answer:** That’s perfectly fine! If we made less than $m$ subarrays, then we know we could split any of those subarrays and get a smaller maximum sum which holds valid. 

```python
class Solution:
    def splitArray(self, nums: List[int], k: int) -> int:
        lo = max(nums)
        hi = sum(nums)
        result = hi

        def can_split(largest_sum):
            subarrays = 1
            curr_sum = 0

            for n in nums:
                curr_sum += n
                if curr_sum > largest_sum:
                    subarrays += 1
                    curr_sum = n
            
            return subarrays <= k

        while lo <= hi:
            mid = lo + ((hi - lo) // 2)

            if can_split(mid):
                result = mid
                hi = mid - 1
            else:
                lo = mid + 1

        return result
```