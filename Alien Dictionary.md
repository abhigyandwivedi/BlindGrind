# LeetCode 269: Alien Dictionary

## Problem Statement

Given a list of strings `words` from an alien language dictionary, where the words are sorted lexicographically according to the alien language's unknown alphabet order, determine the order of characters in the alien alphabet.

### Example Input

```python
words = ["wrt", "wrf", "er", "ett", "rftt"]
```

### Example Output

```python
Output: "wertf"
```

### Explanation

From the order of words:

1. Compare `wrt` and `wrf` → `t` comes before `f`.
2. Compare `wrf` and `er` → `w` comes before `e`.
3. Compare `er` and `ett` → `r` comes before `t`.
4. Compare `ett` and `rftt` → `e` comes before `r`.

Thus, the correct order is `w`, `e`, `r`, `t`, `f` → "wertf".

---

## Approach

We can solve this problem using **Topological Sorting** of a Directed Acyclic Graph (DAG).

### Steps:

1. **Build Graph:**
    - Each character represents a node.
    - For each adjacent word pair, find the first differing character and create a directed edge.
2. **In-degree Calculation:**
    - Count incoming edges for each character.
3. **Topological Sort:**
    - Use Kahn's algorithm (BFS) to order characters with zero in-degree first.

---

## Solution (Python)

```python
from collections import defaultdict, deque

def alienOrder(words):
    # Step 1: Create graph and in-degree count
    graph = defaultdict(list)
    in_degree = {char: 0 for word in words for char in word}

    # Step 2: Build graph based on word comparisons
    for i in range(len(words) - 1):
        word1, word2 = words[i], words[i + 1]
        min_len = min(len(word1), len(word2))
        if word1[:min_len] == word2[:min_len] and len(word1) > len(word2):
            return ""
        for c1, c2 in zip(word1, word2):
            if c1 != c2:
                graph[c1].append(c2)
                in_degree[c2] += 1
                break

    # Step 3: Topological Sort using Kahn's Algorithm (BFS)
    queue = deque([char for char in in_degree if in_degree[char] == 0])
    order = []

    while queue:
        char = queue.popleft()
        order.append(char)
        for neighbor in graph[char]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)

    # If all characters are processed, return the order
    if len(order) == len(in_degree):
        return "".join(order)
    else:
        return ""

# Example usage
words = ["wrt", "wrf", "er", "ett", "rftt"]
print(alienOrder(words))  # Output: "wertf"
```

---

## Detailed Explanation

1. **Input:** `words = ["wrt", "wrf", "er", "ett", "rftt"]`
2. **Graph:** Build adjacency list:
    
    ```python
    {
      'w': ['e'],
      'e': ['r'],
      'r': ['t'],
      't': ['f']
    }
    ```
    
3. **In-degree:** Count of incoming edges:
    
    ```python
    {
      'w': 0,
      'e': 1,
      'r': 1,
      't': 1,
      'f': 1
    }
    ```
    
4. **Topological Sort:** Process nodes with `in-degree = 0`.

---

## Complexity Analysis

### Time Complexity: O(C)

- `C` is the total number of characters across all words.
- Building the graph takes linear time based on character comparisons.

### Space Complexity: O(1)

- The graph and in-degree storage depend on unique characters, which are limited to 26 for lowercase English letters.

---

## Edge Cases

1. **Single Word:** `words = ["abc"]` → Output: "abc".
2. **Inconsistent Order:** `words = ["abc", "ab"]` → Output: "" (invalid order).
3. **Empty Input:** `words = []` → Output: "".

---

## Conclusion

This solution efficiently determines the alien language order using graph-based topological sorting while ensuring correctness through cycle detection.

---

Let me know if you'd like further clarifications or alternative approaches!