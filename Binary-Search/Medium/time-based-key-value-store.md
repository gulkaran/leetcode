# Time Based Key-Value Store

[https://leetcode.com/problems/time-based-key-value-store/](https://leetcode.com/problems/time-based-key-value-store/description/)

### Problem

Creating a key-value data structure where the same key can have multiple values based on a differing timestamp. 

- set(key, value, timestamp)
- get(key, timestamp)
    - attempt to find the value with the exact match, if no exact timestamp match is found, we return the value with the closest **previous** timestamp.
    - e.g. $map = \{ \ key → [ (foo, 1), (bar, 2), (baz, 4) ] \ \}$
    - if we run $map.get(key, 3)$, we would return **bar** instead of baz since we always return the closest previous timestamp.

### Solution

Store the values as an array of tuples so $key \rightarrow [(val, timestamp), (val2, timestamp2)]$

- this way we can utilize binary search to find the resulting value in $O(\log n)$ time.
- we change the algorithm a little since we also need to account for the closest previous match which is easy enough. we can update this when the get timestamp (provided in parameter) is greater than the middle binary search timestamp.
- so when we need to search the right half (update the left pointer), we can store that best value

```python
class TimeMap:

    def __init__(self):
        self.map = {}

    def set(self, key: str, value: str, timestamp: int) -> None:
        if key not in self.map:
            self.map[key] = []
        
        self.map[key].append((value, timestamp))

    def get(self, key: str, timestamp: int) -> str:
        arr = self.map.get(key, [])

        l, r = 0, len(arr) - 1
        result = ""

        while l <= r:
            mid = (l + r) // 2
        
            if timestamp >= arr[mid][1]:
                result = arr[mid][0]
                l = mid + 1
            else:
                r = mid - 1

        return result
```