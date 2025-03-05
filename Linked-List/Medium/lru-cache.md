# LRU Cache

[https://leetcode.com/problems/lru-cache](https://leetcode.com/problems/lru-cache)

Defining two helper functions $remove$ and $add$ makes this question a lot easier. We use a hashmap to store $key\to node$ to have the $get()$ function be $O(1)$ time. The $put()$ can be done in $O(1)$ by making the tail represent our MRU and head be the LRU.  

```python
class Node:
    def __init__(self, key, val):
        self.key = key
        self.val = val
        self.prev = None
        self.next = None

class LRUCache:

    def __init__(self, capacity: int):
        self.capacity = capacity
        self.node_map = {}

        self.head = Node(-1, -1) # LRU
        self.tail = Node(-1, -1) # MRU

        self.head.next = self.tail
        self.tail.prev = self.head

    def _add(self, node):
        tail = self.tail.prev

        tail.next = node
        node.prev = tail

        node.next = self.tail
        self.tail.prev = node
    
    def _remove(self, node):
        node.prev.next = node.next
        node.next.prev = node.prev
        

    def get(self, key: int) -> int:
        if key not in self.node_map:
            return -1
        
        # move the found key to the tail of DLL
        node = self.node_map[key]

        self._remove(node)
        self._add(node)

        return node.val

    def put(self, key: int, value: int) -> None:
        if key in self.node_map:
            old = self.node_map[key]
            self._remove(old)

        node = Node(key, value)
        self.node_map[key] = node
        self._add(node)

        if len(self.node_map) > self.capacity:
            head = self.head.next
            self._remove(head)
            del self.node_map[head.key]
```