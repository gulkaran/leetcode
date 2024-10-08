# Permutation in String

[https://leetcode.com/problems/permutation-in-string/](https://leetcode.com/problems/permutation-in-string/description/)

### Problem

Given two strings $s1, s2,$ return $true$ if one of $s1$'s permutations is the substring of $s2$.

### Solution

The brute force method is to compute the permutations of s1 and check if any of them are a substring in s2 but this will obviously result in a TLE.

The more optimized solution I found was comparing the frequency of characters in $s1$ and the window in $s2$. We iterate through $s2$ and compute the frequency of the substring created from the sliding window and comparing if the frequency dictionaries are the same.

```python
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:

        window_size = len(s1)
        l = 0
        freq_s1 = collections.defaultdict(int)
        
        for letter in s1:
            freq_s1[letter] += 1
        
        for r in range(window_size, len(s2) + 1):
            substring = s2[l:r]

            freq_s2 = collections.defaultdict(int)

            for letter in substring:
                freq_s2[letter] += 1
            
            if freq_s1 == freq_s2:
                return True
            
            l += 1
        
        return False
```

There is a more efficient solution with comparing the matches and not recomputing frequencies (instead just updating one $s2$ frequency dictionary). We can make this solution into a $O(n)$ solution by updating the frequency dictionary instead of recalculating it from scratch.