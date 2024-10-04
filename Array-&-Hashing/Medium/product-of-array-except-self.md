# Product of Array Except Self

[https://leetcode.com/problems/product-of-array-except-self/](https://leetcode.com/problems/product-of-array-except-self/)

Requirements: $O(n)$ and no division

### Division Allowed

- find product of list, loop through each element and divide by that number

### Prefix/Postfix Inplace Array Method

- calculate the prefixes and postfixes and multiply them in place

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:

        # [1, 2, 3, 4]
        # [1, 1, 2, 6] <- prefix
        # [24, 12, 4, 1] <- postfix
        # [24, 12, 8, 6]

        results = [1 for i in range(len(nums))]

        for i in range(1, len(nums)):
            newPrefix = nums[i-1] * results[i-1]
            results[i] = newPrefix
        
        print(results)

				# better neetcode method (can do this above as well)
        postfix = 1
        for i in range(len(nums)-1, -1, -1):
            results[i] *= postfix
            postfix *= nums[i]
        
        return results
```