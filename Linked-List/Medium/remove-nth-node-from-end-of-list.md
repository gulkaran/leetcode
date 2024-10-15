# Remove nth Node From End of List

[https://leetcode.com/problems/remove-nth-node-from-end-of-list](https://leetcode.com/problems/remove-nth-node-from-end-of-list)

Keep a gap of $n$ nodes so we can reach the previous node of the one we want to delete in just one pass. If our left pointer started at the head, we would reach the node we want to delete, so we create a dummy node that we insert in front of head so we reach the node previous to the $n$th from the end one we want to delete.

- move our $r$ pointer $n$ times from head to create that gap between $l$ and $r$
- iterate until $r$ becomes **null**
- $l$ is now at the previous node so delete the next node

```python
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:

        if not head:
            return

        dummy = ListNode(0, head)
        l = dummy
        r = head
				
				# move our r pointer n times from head to create that gap between l and r
        while n > 0 and r:
            r = r.next
            n -= 1
           
        # iterate until r becomes **null**
        while r:
            l = l.next
            r = r.next
        
        # deletion of the next node
        l.next = l.next.next
				
				# return head
        return dummy.next
```