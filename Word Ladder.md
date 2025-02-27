# Solution to "127. Word Ladder"

## Problem Statement

Given two words, `beginWord` and `endWord`, and a list of `wordList`, find the shortest transformation sequence from `beginWord` to `endWord` such that:

1. Only one letter can be changed at a time.
2. Each transformed word must exist in `wordList`.

Return the length of the shortest transformation sequence, or `0` if no such sequence exists.

Example:

```
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
Output: 5
Explanation: "hit" → "hot" → "dot" → "dog" → "cog"
```

---

## Approach: Breadth-First Search (BFS)

### Explanation

1. **Use a Queue:** Perform level-order traversal using a queue.
2. **Transform Words:** Change one letter at a time and check if it's in `wordList`.
3. **Track Levels:** Each level represents one transformation step.

---

## Implementation in Python

```python
from collections import deque

def ladderLength(beginWord: str, endWord: str, wordList: list[str]) -> int:
    wordSet = set(wordList)
    if endWord not in wordSet:
        return 0

    queue = deque([(beginWord, 1)])

    while queue:
        word, level = queue.popleft()
        if word == endWord:
            return level

        for i in range(len(word)):
            for char in 'abcdefghijklmnopqrstuvwxyz':
                next_word = word[:i] + char + word[i+1:]
                if next_word in wordSet:
                    wordSet.remove(next_word)
                    queue.append((next_word, level + 1))

    return 0
```

---

## Example Run

Input:

```python
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log","cog"]
print(ladderLength(beginWord, endWord, wordList))
```

Output:

```
5
```

---

## Complexity Analysis

1. **Time Complexity:** `O(M * N)`
    
    - `M` is the word length.
    - `N` is the number of words in `wordList`.
2. **Space Complexity:** `O(N)`
    
    - Queue and word set storage.

---

## Edge Cases

1. No transformation possible → Return `0`.
2. Begin and end word are the same → Return `1`.
3. Empty word list → Return `0`.

---

## Conclusion

Breadth-First Search ensures the shortest path is found efficiently by exploring all possible transformations level by level.