# Add Two Numbers

[https://leetcode.com/problems/add-two-numbers/](https://leetcode.com/problems/add-two-numbers/)

Keep track of the carry and the edge case with carry == 1 after the algorithm is done. Other than that, its a simple linked list problem.

```python
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:

        head = ListNode(0) # dummy node to avoid insertion errors
        curr = head

        carry = 0
        while l1 or l2:
            d1 = l1.val if l1 else 0
            d2 = l2.val if l2 else 0

            val = d1 + d2 + carry
            carry = 1 if val >= 10 else 0

            # val % 10 gets the ones place digit if theres a carry
            new_node = ListNode(val % 10)
            curr.next = new_node

            # update pointers
            curr = curr.next
            l1 = l1.next if l1 else None
            l2 = l2.next if l2 else None

        # edge case, e.g. 8 + 7 = 5 with carry 1, need to add extra 1 node, 5 -> 1
        if carry == 1:
            curr.next = ListNode(1)

        return head.next
```
