# Top K Frequent Elements

[https://leetcode.com/problems/top-k-frequent-elements/](https://leetcode.com/problems/top-k-frequent-elements/)

## Naive Approach

- count the frequency of each element - $O(n)$
- sort the dictionary in descending order - $O(n\log n)$
- loop through dict, k times - $O(k)$

```python
class Solution(object):
    def topKFrequent(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        freq = {}
        for i in nums:
            if i in freq:
                freq[i] += 1
            else:
                freq[i] = 1
        
        freq = sorted(freq.items(), key=lambda x: x[1], reverse=True)

        result = []
        for i in range(k):
            result.append(freq[i][0])

        return result
```

## Better Approach

- count the frequency
- instead of sorting the dictionary, add these kvp into an **array** where the index is the count (max the length of the nums array) and the value is the number
    - since the indexes are already sorted, we can iterate from the end of the array and append k times to a result array

```python
class Solution(object):
    def topKFrequent(self, nums, k):
        count = {}
        
        for n in nums:
            count[n] = 1 + count.get(n, 0) # default 0 if key not found

				# [] if multiple n-freq nums, e.g. [2, 3]
				freq = [[] for i in range(len(nums)+1)]
				
				# key = num, val = freq/count
        for num, c in count.items():
            freq[c].append(num)
				
        result = []

				# iterates in reverse
        for i in range(len(freq)-1, 0, -1):

            for n in freq[i]:
                result.append(n)

                if len(result) == k:
                    return result
```