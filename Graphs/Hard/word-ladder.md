# Word Ladder

[https://leetcode.com/problems/word-ladder/](https://leetcode.com/problems/word-ladder/)

Simple BFS with creating adjacent words in $O(26\cdot m)$ time. The total time complexity is $O(n^2 \cdot m)$ where $n$ is the number of words and $m$ is the length of the word.

```python
from collections import defaultdict, deque

class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        
        adj = defaultdict(list)
        wordList.append(beginWord)

        wordSet = set(wordList)

        queue = deque()
        seen = set()

        queue.append((beginWord, 0))
        seen.add(beginWord)

        while queue:
            word, dist = queue.popleft()

            if word == endWord:
                return dist + 1

            for i in range(len(word)):
                for c in 'abcdefghijklmnopqrstuvwxyz':
                    adj_word = word[:i] + c + word[i + 1:]
                    if adj_word in wordSet and adj_word not in seen:
                        queue.append((adj_word, dist + 1))
                        seen.add(adj_word)
        
        return 0
```