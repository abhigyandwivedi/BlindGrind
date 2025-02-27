# Solution to "208. Implement Trie (Prefix Tree)"

## Problem Statement

Design a `Trie` (pronounced as "try") data structure that supports the following operations:

1. `insert(word)` - Inserts the word into the trie.
2. `search(word)` - Returns `true` if the word is in the trie.
3. `startsWith(prefix)` - Returns `true` if there is any word in the trie that starts with the given prefix.

Example:

```
Input:
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");   // true
trie.search("app");     // false
trie.startsWith("app"); // true
trie.insert("app");
trie.search("app");     // true
```

---

## Approach: Trie Node Implementation

### Explanation

1. Each `TrieNode` contains:
    - A `children` dictionary to store the next characters.
    - A `isEnd` boolean indicating if the current node marks the end of a word.
2. For `insert(word)`, traverse through the characters and add nodes as needed.
3. For `search(word)`, traverse and check if the word exists, ensuring `isEnd` is `True`.
4. For `startsWith(prefix)`, traverse and check if the prefix path exists.

---

## Implementation in Python

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.isEnd = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.isEnd = True

    def search(self, word: str) -> bool:
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.isEnd

    def startsWith(self, prefix: str) -> bool:
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
        return True

# Example usage
trie = Trie()
trie.insert("apple")
print(trie.search("apple"))    # Output: True
print(trie.search("app"))      # Output: False
print(trie.startsWith("app"))  # Output: True
trie.insert("app")
print(trie.search("app"))      # Output: True
```

---

## Complexity Analysis

1. **Insert Operation:** `O(n)` where `n` is the length of the word. Each character is processed once.
2. **Search Operation:** `O(n)` where `n` is the length of the word.
3. **Prefix Search:** `O(n)` where `n` is the length of the prefix.
4. **Space Complexity:** `O(N * M)` where `N` is the number of words inserted and `M` is the average word length.

---

## Example Run

Input:

```python
trie = Trie()
trie.insert("apple")
print(trie.search("apple"))    # Output: True
print(trie.search("app"))      # Output: False
print(trie.startsWith("app"))  # Output: True
trie.insert("app")
print(trie.search("app"))      # Output: True
```

---

## Edge Cases

1. Empty string: Inserting and searching for `""` should return `True` after insertion.
2. Prefix as a word: Inserting `"apple"` and searching `"app"` should return `False`.
3. Overlapping words: Inserting `"app"` and `"apple"` should handle both independently.

---

## Conclusion

This solution efficiently implements a prefix tree with `O(n)` time complexity for insertion, search, and prefix checking, ensuring fast lookups and insertions in a dictionary-like structure.