# Longest Consecutive Sequence

[https://leetcode.com/problems/longest-consecutive-sequence/](https://leetcode.com/problems/longest-consecutive-sequence/)

### Brute Force Method

- sort the list, and find the largest sequence from there - $O(n\log n)$ to sort

### Optimized HashSet Way

- convert the array to a hashset
- find if the number we are on is the first in the ‘sequence’
    - how do we know if a number is the first? if the number *before* it is **NOT** in the set
- then we continue adding 1 to the number and checking whether its in the hashset or not
    - from here, we can keep track of the largest count
    

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        # [100,1,200,4,3,2] -> hashset

        # [1, 2, 3, 4], [100], [200]

        nums = set(nums)
        maxCount = 0

        for num in nums:
            count = 0

            # find sequence starting nums, and calculate length of seq after them
            if (num - 1) not in nums:
                count += 1

                while num + 1 in nums:
                    count += 1
                    num += 1
            
                maxCount = max(maxCount, count)

        return maxCount
```

### Small Optimization

If the maxCount we found is larger than the remaining number of elements we have left to search, we can return maxCount there

```python
# small premature optimization
if maxCount >= len(nums) - i+1: # use enumeration then
    return maxCount
```

e.g. [100,1,200,4,3,2]

- at $i=1,num=1$, we would’ve found a maxCount of 4. Even if we progress, we will never find a maxCount larger than that, because 1 was our starting number for the sequence. Small, case specific optimizations.