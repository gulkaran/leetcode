# Reverse Linked List

[https://leetcode.com/problems/reverse-linked-list](https://leetcode.com/problems/reverse-linked-list)

Simple problem, we have a previous and next node. We set the current node’s next pointer to the previous node but since we need a way to iterate to the following node (since we just reassigned its next pointer), we use a **next** node.

```python
class ListNode:
		def __init__(self, val=0, next=None):
		    self.val = val
		    self.next = next

class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        
        # empty LL
        if not head:
            return
        
        prev = None
        curr = head
        next = curr
				
        while next != None:
            next = curr.next
            curr.next = prev
            prev = curr
            curr = next
        
        # at the end of the algorithm, curr = next which becomes None
        # so prev is at the tail of the LL
        head = prev

        return head
```