# Search Insert Position

[https://leetcode.com/problems/search-insert-position](https://leetcode.com/problems/search-insert-position/description/)

Classic binary search, return left pointer

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        lo = 0
        hi = len(nums) - 1

        while lo <= hi:
            mid = lo + (hi - lo // 2)

            if target == nums[mid]:
                return mid
            elif target > nums[mid]:
                lo = mid + 1
            else:
                hi = mid - 1
        
        return lo
```