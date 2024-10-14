# Merge Two Sorted Lists

[https://leetcode.com/problems/merge-two-sorted-lists/](https://leetcode.com/problems/merge-two-sorted-lists/)

The concept is to create a third result Linked List, and keep track of a tail node. Using the same logic as the merge function in merge sort, we assign the smaller value to the tail. Don’t forget to increment the tail. 

Once we reach the end of one of the lists, we can simply copy the rest of the other list.

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
 
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:

        c1 = list1
        c2 = list2
        res = ListNode()
        tail = res
        
        # base case
        if c1 is None:
            return c2
        elif c2 is None:
            return c1

        # similar to merge sort
        while c1 is not None and c2 is not None:
            if c1.val > c2.val:
                tail.next = c2
                c2 = c2.next

            else:
                tail.next = c1
                c1 = c1.next

            tail = tail.next

        # copy over the rest since one list reached its end
        if c1 is None:
            tail.next = c2
            
        elif c2 is None:
            tail.next = c1
        
        return res.next
```