# LeetCode Problem 139: Word Break

## Problem Description

Given a string `s` and a dictionary of strings `wordDict`, determine if `s` can be segmented into a space-separated sequence of one or more dictionary words.

**Note:**

- The same word in the dictionary may be reused multiple times in the segmentation.
- You may assume the dictionary does not contain duplicate words.

**Example 1:**

```
Input: s = "leetcode", wordDict = ["leet", "code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```

**Example 2:**

```
Input: s = "applepenapple", wordDict = ["apple", "pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
             Note that you are allowed to reuse a dictionary word.
```

**Example 3:**

```
Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
Output: false
```

## Solution

To solve this problem, we can use dynamic programming. We'll maintain a boolean array `dp` where `dp[i]` indicates whether the substring `s[0:i]` can be segmented into words present in the `wordDict`.

### Approach

1. **Initialization:**
    
    - Create a boolean array `dp` of size `n + 1` (where `n` is the length of `s`) initialized to `false`.
    - Set `dp[0]` to `true` because an empty string can always be segmented.
2. **Dynamic Programming Transition:**
    
    - Iterate over the string with index `i` from `1` to `n`.
    - For each `i`, iterate backwards from `i-1` to `0` with index `j`.
    - Check if `dp[j]` is `true` and the substring `s[j:i]` is in `wordDict`.
    - If both conditions are met, set `dp[i]` to `true` and break the inner loop.
3. **Result:**
    
    - The value of `dp[n]` will indicate whether the entire string can be segmented.

### Time Complexity

- The time complexity is O(n^3), where `n` is the length of the string `s`. This is because:
    - We have an outer loop running `n` times.
    - For each iteration of the outer loop, the inner loop runs up to `n` times.
    - The substring operation `s[j:i]` takes O(n) time in the worst case.

### Space Complexity

- The space complexity is O(n) due to the `dp` array of size `n + 1`.

## Python Implementation

```python
from typing import List

def wordBreak(s: str, wordDict: List[str]) -> bool:
    word_set = set(wordDict)
    n = len(s)
    dp = [False] * (n + 1)
    dp[0] = True

    for i in range(1, n + 1):
        for j in range(i):
            if dp[j] and s[j:i] in word_set:
                dp[i] = True
                break

    return dp[n]
```

## Explanation

- We convert `wordDict` to a set `word_set` for O(1) average-time complexity lookups.
- The `dp` array keeps track of whether substrings of `s` can be segmented.
- We iterate through each character position `i` in `s`.
- For each position `i`, we check all possible substrings ending at `i` by iterating backwards with index `j`.
- If the substring `s[j:i]` is in `word_set` and `dp[j]` is `true`, it means the substring `s[0:i]` can be segmented, so we set `dp[i]` to `true` and break out of the inner loop.
- Finally, we return `dp[n]`, which indicates whether the entire string `s` can be segmented into words from `wordDict`.

This approach ensures that we efficiently determine if the string can be segmented using the given dictionary words.

### Trie-Based Approach

Using a Trie can optimize the lookup process for word segmentation.

#### Trie Implementation

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end_of_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end_of_word = True

    def search(self, word: str) -> bool:
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end_of_word

def wordBreak(s: str, wordDict: list[str]) -> bool:
    trie = Trie()
    for word in wordDict:
        trie.insert(word)

    n = len(s)
    dp = [False] * (n + 1)
    dp[0] = True

    for i in range(1, n + 1):
        for j in range(i):
            if dp[j] and trie.search(s[j:i]):
                dp[i] = True
                break

    return dp[n]
```

#### Explanation

1. **Trie Construction:**
    
    - We insert each word from `wordDict` into the Trie for efficient lookups.
        
2. **Dynamic Programming:**
    
    - Similar to the previous DP approach, we iterate through the string `s`.
        
    - Instead of checking the substring directly against a set, we search for the substring in the Trie.
        

#### Time Complexity

- **Trie Construction:** O(m * k), where `m` is the number of words in `wordDict` and `k` is the average length of each word.
    
- **Word Break:** O(n^2), where `n` is the length of the string `s`.
    

#### Space Complexity

- O(m * k) for storing the Trie.