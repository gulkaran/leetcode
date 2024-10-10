# Find Minimum in Rotated Sorted Array

[https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

Do binary search on the array and search the correct half. If the value at $mid$ is larger than the left $l$ pointer, we know the smallest element must be on the **right** half and vice versa.

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:

        l, r = 0, len(nums) - 1
        res = nums[0]

        while l <= r:
            if nums[l] < nums[r]:
                return min(res, nums[l])
            
            mid = (l + r) // 2
            res = min(res, nums[mid])
            
            if nums[mid] >= nums[l]:
                l = mid + 1
            else:
                r = mid - 1

        return res
```