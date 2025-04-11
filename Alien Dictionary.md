# LeetCode 269: Alien Dictionary

https://leetcode.com/problems/alien-dictionary/

Both solns listed down , prefere DFS over BFS as BFS involves kahns algo and gets complicated...
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





# DFS solution



## 📥 Example Input

words = ["wrt", "wrf", "er", "ett", "rftt"]


## 💡 Explanation

From the given words:

- "wrt" -> "wrf": `t` comes before `f`
    
- "wrf" -> "er": `w` comes before `e`
    
- "er" -> "ett": `r` comes before `t`
    
- "ett" -> "rftt": `e` comes before `r`
    

This gives the order: `w -> e -> r -> t -> f`

## 🚀 Approach (DFS Topological Sort)

We treat characters as nodes and build a directed graph (adjacency list). An edge from character `a` to `b` (i.e., `a -> b`) means `a` comes before `b`. We perform a **DFS-based topological sort** on the graph.

If a cycle is detected during DFS, it means the order is invalid.

---

## 🔢 Steps:

1. Build a graph of characters (adjacency list) by comparing adjacent words.
    
2. Initialize a visited state map:
    
    - `0`: unvisited
        
    - `1`: visiting
        
    - `2`: visited
        
3. Perform DFS on each unvisited node.
    
    - If during DFS we encounter a visiting node again, it's a cycle → return `""`.
        
4. Append nodes to a result list once fully visited.
    
5. Reverse the result list to get correct order.


```python
from collections import defaultdict
from typing import List


class Solution:
    def alienOrder(self, words: List[str]) -> str:
        graph = defaultdict(set)  # we use sets here so we dont have duplicates.
        visited = {}  # 0 = unvisited, 1 = visiting, 2 = visited
        result = []

        # Build graph
        for word in words:
            for char in word:
                graph[char]  # ensure every char appears in graph

        for i in range(len(words) - 1):
            w1, w2 = words[i], words[i + 1]
            minLen = min(len(w1), len(w2))
            if w1[:minLen] == w2[:minLen] and len(w1) > len(w2):
                return ""  # invalid case: prefix issue
            for j in range(minLen):
                if w1[j] != w2[j]:
                    graph[w1[j]].add(w2[j])
                    break

        print(graph)

        def dfs(char):
            if char in visited:
                print("Visited:", char)
                return visited[char] == 2  # true if already visited

            visited[char] = 1  # mark as visiting
            for neighbor in graph[char]:
                if visited.get(neighbor, 0) == 1:  # cycle detected
                    print("Cycle detected:", visited, neighbor)
                    return False
                if not dfs(neighbor):
                    print("NOT DFS:", neighbor)
                    return False
            print("Visiting char:", char)
            visited[char] = 2  # mark as visited
            result.append(char)
            return True

        for char in graph:
            if visited.get(char, 0) == 0:
                if not dfs(char):
                    return ""

        return "".join(reversed(result))


# Example usage
words = ["wrt", "wrf", "er", "ett", "rftt"]
sol = Solution()
order = sol.alienOrder(words)
print(order)  # Output should be a valid order like: "wertf"
```


## 🔍 Walkthrough

Given:

python


`words = ["wrt", "wrf", "er", "ett", "rftt"]`

### Graph Construction:

By comparing adjacent words:

- "wrt" vs "wrf": `t -> f`
    
- "wrf" vs "er": `w -> e`
    
- "er" vs "ett": `r -> t`
    
- "ett" vs "rftt": `e -> r`
    

So graph becomes:

python

{
    'w': {'e'},
    'e': {'r'},
    'r': {'t'},
    't': {'f'},
    'f': set()
}


### DFS Traversal:

- Start with unvisited node `'w'`
    
    - Visit `'e'`
        
        - Visit `'r'`
            
            - Visit `'t'`
                
                - Visit `'f'`
                    
            - Append `'f'`, then `'t'`, `'r'`, `'e'`, `'w'` to result in post-order
                

Reversed result: `'wertf'`
## ⏱️ Time and Space Complexity

### Time Complexity:

- **O(C + E)** where
    
    - `C` = number of unique characters in all words
        
    - `E` = number of edges (i.e., constraints from adjacent words)
        

### Space Complexity:

- **O(C + E)** for:
    
    - Graph storage
        
    - Visited dictionary
        
    - Call stack in DFS
        

---

## ✅ Edge Cases Handled

- Words list with a prefix issue like `["abc", "ab"]` → returns `""`
    
- Disconnected characters → still included in output
    
- Cycles → detected and return `""`
    

---

## 📌 Notes

- This problem is a classic application of **topological sorting** on a **directed graph**.
    
- It can also be solved using **BFS (Kahn's algorithm)**, but this version uses DFS.