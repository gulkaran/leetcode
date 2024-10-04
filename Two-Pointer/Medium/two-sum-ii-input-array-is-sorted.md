# Two Sum 2 - Input Array Is Sorted

[https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)

Use two pointers, one at the start and one at the end, if the sum is larger than our target, decrement the right pointer and vise versa.

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:

        i, j = 0, len(numbers) - 1

        while numbers[i] + numbers[j] != target:

            if numbers[i] + numbers[j] > target:
                j -= 1
            else:
                i += 1

        return [i + 1, j + 1]
```