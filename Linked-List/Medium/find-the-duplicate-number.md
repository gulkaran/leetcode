# Find the Duplicate Number

This question is quite ridiculous if you don’t know Floyd’s Cycle Detection algorithm. It boils down to that we can model the array as a linked list by looking at its indexes

- nums = [1, 3, 4, 2, 2] can be modelled as a linked list
- LL: $0 \to 3 \to 2 \leftrightarrow 4$ (2 and 4 create a cycle)

We see that 2 is the start of the cycle and the node we want to return. We can get to the next link by using the value of the node as the index in the array. But how do we get the starting node of the cycle? FLOYD’S CYCLE ALGORITHM!!!!

**Phase 1**

- slow and fast pointers
- when they meet up, break out of that while loop

**Phase 2**

- have a secondary slow pointer start at the head of the LL
- increment both slow pointers until they meet
- they meet at the starting node of the cycle!

There is a mathy proof of why this algorithm works, it boils down to the distance between the head node and the cycle-starting node being the same as the length between cycle-starting node and the node the fast and slow pointer meet at. 

```python
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        # there must be a cycle, we want to find the starting node of the cycle
        # can use slow and fast pointers for this (floyd's cycle detection)

        # phase 1: reach a point where slow and fast ptrs meet
        slow, fast = 0, 0
        while True:
            slow = nums[slow]
            fast = nums[nums[fast]]

            if slow == fast:
                break
        
        # phase 2: increment slow ptr and ptr at head 
        # to reach the node that starts the cycle
        slow2 = 0
        while slow2 != slow:
            slow2 = nums[slow2]
            slow = nums[slow]

        return slow
```