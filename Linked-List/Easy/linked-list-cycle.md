# Linked List Cycle

[https://leetcode.com/problems/linked-list-cycle/](https://leetcode.com/problems/linked-list-cycle/)

Intuitively, we would approach this problem with a set and just check if the node we are visiting are in the set, however, that would be $O(n)$ time and $O(n)$ space complexity. 

We can optimize our approach by utilizing slow and fast pointers where the logic relies on the concept that if the slow pointer somehow caught up to the fast one, there **must** be a cycle within the linked list!

```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        if not head:
            return False
        
        slow, fast = head, head.next

        while fast and fast.next:
            if slow == fast:
                return True
            
            slow = slow.next
            fast = fast.next.next
        
        return False
```