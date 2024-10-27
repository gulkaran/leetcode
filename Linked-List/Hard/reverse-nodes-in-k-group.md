# Reverse Nodes in k-Group

[https://leetcode.com/problems/reverse-nodes-in-k-group](https://leetcode.com/problems/reverse-nodes-in-k-group/description/)

We want to keep track of a node **before and after** the group we want to reverse. The main ideas are

- get the $k$th_node
- when we normally reverse, the first node will now point to **null** which in our case would split our linked list. Instead, we have it point to the $k$th.next node.
- update the previous node to the **tail** of the reversed LL. We can do this by storing the previous.next in a temporary variable and reassign it after step 2.

```python
class Solution:
    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        
        dummy = ListNode(0, head)
        prev = dummy # node before group
        while True:
            kth_node = self.kth(prev, k)

            if not kth_node:
                break

            # node after the group
            kth_next = kth_node.next

            # instead of splitting it, let prevN connect to the next group
            prevN, curr = kth_node.next, prev.next
            
            while curr != kth_next:
                tmp = curr.next
                curr.next = prevN
                prevN = curr
                curr = tmp
    
            # want the node before the group to point to the new head
            tmp = prev.next # this node was first, now its last after reversal
            prev.next = prevN
            prev = tmp
        
        return dummy.next
        
    def kth(self, head, k):
        while head and k > 0:
            head = head.next
            k -= 1
        return head
```