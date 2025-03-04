# Make Array Zero by Subtracting Equal Amounts

[https://leetcode.com/problems/make-array-zero-by-subtracting-equal-amounts](https://leetcode.com/problems/make-array-zero-by-subtracting-equal-amounts)

$nums =[1,5,0,3,5] \to \{1,5,3\} \to \text{return } 3$

- we greedily choose the minimum element 3 times

```python
class Solution:
    def minimumOperations(self, nums: List[int]) -> int:
        return len(set([i for i in nums if i > 0]))
```