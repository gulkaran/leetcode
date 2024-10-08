# Binary Search

[https://leetcode.com/problems/binary-search/](https://leetcode.com/problems/binary-search/)

Not much to say about this other than its a simple binary search! Calculate the midpoint and check whether the target is on the larger or smaller half (only works on sorted arrays or BSTs)

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        
        l, r = 0, len(nums) - 1

        while l <= r:
            mid = (r + l) // 2
            if target == nums[mid]:
                return mid
            elif target > nums[mid]:
                l = mid + 1
            else:
                r = mid - 1
                
        return -1
```