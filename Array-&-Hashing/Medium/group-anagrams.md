# Group Anagrams

[https://leetcode.com/problems/group-anagrams/description/](https://leetcode.com/problems/group-anagrams/description/)

### Naive Approach

- sort each word in the list - $O(m \log m)$  where $m$ is avg length of word
- group together the words

### Better Approach

- Have an array (length 26) represents the count of each letter (0→26 indexes), values is the count of each letter
    - use ascii representation (ord(letter))
- Have a hash map where they key is the **array** and value are the word**s** that fit that key.
    - ** lists can’t be keys, but tuples can **
- return hash map values
- this solution is $O(n\cdot m)$
    - $n$ is the length of the input array
    - $m$ is the average length of the strings

```python
class Solution(object):
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """

        # key -> arr[26] : index -> letter, val -> count
        # value -> arr of anagrams
        hashmap = {}
        
        for word in strs:
            arr = [0 for i in range(26)]

            for letter in word:
                arr[ord(letter) - ord("a")] += 1

            # lists cannot be keys, tuples are immutable
            hashmap[tuple(arr)] = [word] + (hashmap.get(tuple(arr), []))
        
        return hashmap.values()
```