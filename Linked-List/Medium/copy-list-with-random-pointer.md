# Copy List With Random Pointer

[https://leetcode.com/problems/copy-list-with-random-pointer/](https://leetcode.com/problems/copy-list-with-random-pointer/)

Solution is quite straight forward, we do 2 passes through the list.

1. map the curr node to a copy node
2. connect the links between the copy nodes

```python
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random

class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        
        # edge case if curr.next is None (tail edge case)
        old_to_new = { None: None }

        curr = head
        while curr:
            new = Node(curr.val)
            old_to_new[curr] = new
            curr = curr.next

        curr = head
        while curr:
            new = old_to_new[curr]
            new.next = old_to_new[curr.next]
            new.random = old_to_new[curr.random]
            curr = curr.next

        return old_to_new[head]
        
```