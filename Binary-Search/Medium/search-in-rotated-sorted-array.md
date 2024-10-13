# Search in Rotated Sorted Array

[https://leetcode.com/problems/search-in-rotated-sorted-array/](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)

This question is like a proof by cases — tedious and exhausting. We know we have two portions of the array which meet at the rotation index. We will call these the left sorted portion and right sorted portion.

We compute $mid$, the midpoint between our $l$ and $r$ pointers. We will determine what to do if our $mid$ falls within our left sorted portion versus our right sorted portion.

We can check which sorted portion we are in by computing $nums[mid] \geq nums[l]$. This means from $l \rightarrow mid$, the numbers are in ascending order. Take this example:

- $nums=[4,5,6,7,0,1,2]$

From here, we can make an educated guess on where to search based on what information our $target$ provides. 

- $target > 7$, **** search in the right sorted portion. (if target > nums[mid])
    - We know the numbers before $mid$ are smaller than 7 and increase in ascending order so there may be a number larger than 7 in the right portion.
    - for example if $nums=[4,5,6,7,8,9,1]$
- $target < 4$, search in the right sorted portion. (if target < nums[l])
    - We know numbers are ascending from $l \rightarrow mid$, so we would want to search in the right sorted portion for potentially smaller values
- Note these are mutually exclusive conditions
- If neither of these conditions are true, we know $nums[l] \leq target \leq nums[mid]$, and we can search the left sorted portion. This was where my intuition led as well.

For the other case where $nums[mid] \leq nums[r]$, when we are in the right sorted portion, we can use similar logic to devise the conditions of which half to search. 

For example: $nums=[4,5,6,-1,0,1,2]$

- $target > 2$, search the left portion
- $target < -1$, search the left portion
- $-1 \leq target \leq 2$, search the right portion

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l, r = 0, len(nums) - 1

        while l <= r:
            mid = (l + r) // 2

            if nums[mid] == target:
                return mid

            # left sorted portion, e.g. [4,5,6,7,0,1,2]
            if nums[mid] >= nums[l]:
                if target > nums[mid] or target < nums[l]:
                    l = mid + 1
                else:               # 4 <= target <= 7
                    r = mid - 1
            
            # right sorted portion, e.g. [4,5,6,-1,0,1,2]
            else:
                if target < nums[mid] or target > nums[r]:
                    r = mid - 1
                else:               # -1 <= target <= 2
                    l = mid + 1

        return -1 
```