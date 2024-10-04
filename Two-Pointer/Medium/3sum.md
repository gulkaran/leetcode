# 3Sum

[https://leetcode.com/problems/3sum/description/](https://leetcode.com/problems/3sum/description/)

### Optimal Solution

- start with sorting the array
- then its just two sum for the remaining one

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        
        results = []
        nums.sort() # e.g. [-4,-1,-1,0,1,2]

        for i in range(len(nums)):
            
            # ensures no duplicate triplets
            if i > 0 and nums[i - 1] == nums[i]:
                continue

            # now its just two sum for the remaining subarray
            j, k = i + 1, len(nums) - 1

            while j < k:
                threeSum = nums[i] + nums[j] + nums[k]

                if threeSum > 0:
                    k -= 1
                elif threeSum < 0:
                    j += 1
                else:
                    results.append([nums[i], nums[j], nums[k]])
                    
                    # [-4,-1,-1,0,1,2]
                    #      i  j     k
                    # there is still one more pair to be found,
                    # we can update the j pointer as the k pointer gets
                    # updated in the above twoSum logic

                    j += 1
                    # checking if its not a duplicate!!
                    while nums[j] == nums[j - 1] and j < k:
                        j += 1

        return results

```