# Reorder List

[https://leetcode.com/problems/reorder-list](https://leetcode.com/problems/reorder-list)

The intuition of this algorithm comes from the question structure itself — its an easy problem to solve if we were using arrays instead of linked lists. If this was an array problem, we would simply take a $right$ pointer and decrement it so why not do that for the LL as well.

We start with the intuition of reversing the linked list, but how much of the LL do we reverse? Going halfway makes the most sense so we can use a **slow-fast pointer** approach to find the middle node of the LL.

From there we merge the two LL’s by using temp variables to store the head and tails .next node.

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:
        slow, fast = head, head.next

        # slow reaches the middle of the LL
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        
        second_half = slow.next
        slow.next = None    # cuts first half off to make 2 seperate lists

        second_half = self.reverse(second_half)

        curr = head

        # merge algorithm
        while second_half:
            t1, t2 = curr.next, second_half.next
            
            curr.next = second_half
            second_half.next = t1

            # iterate to the next node in both lists
            curr, second_half = t1, t2
        
    def reverse(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None
        curr = head
        next = head

        while next != None:
            next = curr.next
            curr.next = prev
            prev = curr
            curr = next
        
        return prev
```