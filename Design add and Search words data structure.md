# Solution to "211. Design Add and Search Words Data Structure"

## Problem Statement

Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the `WordDictionary` class:

1. `WordDictionary()` initializes the object.
2. `addWord(word)` adds `word` to the data structure.
3. `search(word)` returns `true` if `word` exists, where `.` can match any letter.

---

## Approach: Trie with Backtracking

### Explanation

We use a Trie (prefix tree) for efficient word storage and searching. Each node represents a character, and `.` allows exploring all child nodes.

### Algorithm Steps

1. **Add Word:**
    
    - Traverse the Trie, inserting characters.
    - Mark the end of the word.
2. **Search Word:**
    
    - Traverse normally for letters.
    - If `.` appears, recursively search all children.

---

## Implementation in Python

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end_of_word = False

class WordDictionary:
    def __init__(self):
        self.root = TrieNode()

    def addWord(self, word: str) -> None:
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end_of_word = True

    def search(self, word: str) -> bool:
        def dfs(index, node):
            if index == len(word):
                return node.is_end_of_word

            char = word[index]
            if char == '.':
                for child in node.children.values():
                    if dfs(index + 1, child):
                        return True
                return False
            elif char in node.children:
                return dfs(index + 1, node.children[char])
            else:
                return False

        return dfs(0, self.root)
```

---

## Example Run

Input:

```python
wordDictionary = WordDictionary()
wordDictionary.addWord("bad")
wordDictionary.addWord("dad")
wordDictionary.addWord("mad")
print(wordDictionary.search("pad"))  # False
print(wordDictionary.search("bad"))  # True
print(wordDictionary.search(".ad"))  # True
print(wordDictionary.search("b.."))  # True
```

Output:

```
False
True
True
True
```

---

## Complexity Analysis

1. **Add Word:**
    
    - Time Complexity: `O(n)` → `n` is the word length.
    - Space Complexity: `O(n)` → New nodes for each unique character.
2. **Search Word:**
    
    - Time Complexity: `O(n)` without `.` and `O(26^m)` with multiple `.`.
    - Space Complexity: `O(1)` without recursion, `O(m)` with recursion.

---

## Edge Cases

1. Search empty word → Return `False` unless added.
2. Multiple dots → Explore all branches.

---

## Conclusion

This solution efficiently supports word addition and search using Trie while handling wildcard characters effectively.