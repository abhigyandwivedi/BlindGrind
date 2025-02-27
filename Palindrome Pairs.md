# 336. Palindrome Pairs

## Problem Statement

Given a list of unique words, return all the pairs of distinct indices `(i, j)` such that the concatenation of `words[i] + words[j]` is a palindrome.

## Example

```python
Input: words = ["abcd","dcba","lls","s","sssll"]
Output: [[0,1],[1,0],[3,2],[2,4]]
```

---

## Solution 1: Brute Force

### Approach

Check all possible pairs `(i, j)` and verify if `words[i] + words[j]` forms a palindrome.

### Implementation (Python)

```python
def palindrome_pairs(words):
    def is_palindrome(s):
        return s == s[::-1]

    res = []
    for i in range(len(words)):
        for j in range(len(words)):
            if i != j and is_palindrome(words[i] + words[j]):
                res.append([i, j])
    return res
```

### Complexity Analysis

- **Time Complexity:** O(n^2 * k), where `n` is the number of words and `k` is the maximum length of a word. Each pair takes O(k) to verify palindrome.
- **Space Complexity:** O(1), excluding the output list.

---

## Solution 2: Trie-based Approach

### Approach

Use a Trie to store words in reverse order. For each word, check valid prefixes and suffixes that can form palindromic pairs.

### Implementation (Python)

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.index = -1
        self.palindrome_suffixes = []

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word, index):
        node = self.root
        for i, char in enumerate(reversed(word)):
            if word[:len(word) - i] == word[:len(word) - i][::-1]:
                node.palindrome_suffixes.append(index)
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.index = index

    def search(self, word, index):
        node = self.root
        result = []
        while word:
            if node.index >= 0 and node.index != index and word == word[::-1]:
                result.append([index, node.index])
            if word[0] not in node.children:
                return result
            node = node.children[word[0]]
            word = word[1:]

        if node.index >= 0 and node.index != index:
            result.append([index, node.index])
        for pal_index in node.palindrome_suffixes:
            result.append([index, pal_index])
        return result


def palindrome_pairs(words):
    trie = Trie()
    for i, word in enumerate(words):
        trie.insert(word, i)

    result = []
    for i, word in enumerate(words):
        result.extend(trie.search(word, i))
    return result
```

### Complexity Analysis

- **Time Complexity:** O(n * k^2)
    - Insertion takes O(n * k).
    - Each search takes O(k^2) for checking palindromic prefixes.
- **Space Complexity:** O(n * k) for storing words in the Trie.

---

## Solution 3: Hash Map Approach

### Approach

Use a hash map to store word indices and check palindromic splits.

### Implementation (Python)

```python
def palindrome_pairs(words):
    word_dict = {word: i for i, word in enumerate(words)}
    res = []

    for index, word in enumerate(words):
        for j in range(len(word) + 1):
            prefix, suffix = word[:j], word[j:]
            if prefix == prefix[::-1] and suffix[::-1] in word_dict and word_dict[suffix[::-1]] != index:
                res.append([word_dict[suffix[::-1]], index])
            if j != len(word) and suffix == suffix[::-1] and prefix[::-1] in word_dict and word_dict[prefix[::-1]] != index:
                res.append([index, word_dict[prefix[::-1]]])
    return res
```

### Complexity Analysis

- **Time Complexity:** O(n * k^2), where `n` is the number of words and `k` is the maximum word length.
- **Space Complexity:** O(n * k), for storing words and reversed strings in the dictionary.

---

## Final Thoughts

- **Brute Force:** Simple but inefficient for large inputs.
- **Trie Approach:** Efficient for larger datasets but uses more space.
- **Hash Map Approach:** Balance between time and space complexity.

Choose the approach based on the problem constraints and input size.