# Merge k Sorted Lists

[https://leetcode.com/problems/merge-k-sorted-lists/](https://leetcode.com/problems/merge-k-sorted-lists/)

This question builds off the LC easy Merge 2 Sorted Lists. We use that as a helper function for this problem as well. 

The main optimization we do here is merge pair of 2 LL’s at a time (similar to the merge operation in merge sort) which costs us $O(\log k)$ merges instead of an inefficient $O(k)$ time complexity if we merge one by one (e.g. merge list $i=1,2$ and merge that result with $i=3$ and so on).

```python
class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        
        # base case
        if not lists or len(lists) == 0:
            return None

        while len(lists) > 1:
            merged = []
            
            # skip by 2 to get pairs of lists
            # e.g. len(lists) = 9 so i in [0, 2, 4, 6, 8]
            for i in range(0, len(lists), 2):
                l1 = lists[i]
                l2 = lists[i + 1] if (i + 1) < len(lists) else None
                merged.append(self.mergeLists(l1, l2))
            
            lists = merged
        
        return lists[0]

    def mergeLists(self, l1, l2):
        dummy = ListNode()
        tail = dummy

        while l1 and l2:
            if l1.val > l2.val:
                tail.next = l2
                l2 = l2.next
            
            else:
                tail.next = l1
                l1 = l1.next 

            tail = tail.next
        
        if l1:
            tail.next = l1
        else:
            tail.next = l2
        
        return dummy.next
```