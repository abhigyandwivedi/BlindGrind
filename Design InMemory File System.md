# Solution to "588. Design In-Memory File System"

## Problem Statement

Design an in-memory file system that supports the following operations:

1. `ls(path)`: List files and directories in the given path.
2. `mkdir(path)`: Create a directory if it does not exist.
3. `addContentToFile(filePath, content)`: Append content to a file. Create the file if it does not exist.
4. `readContentFromFile(filePath)`: Read the content of a file.

---

## Approach: Trie-like Directory Structure

### Explanation

We can represent the file system using a tree-like structure (Trie). Each node represents either a directory or a file.

### Design:

1. **Directory Node:** Each directory contains:
    
    - `children`: Dictionary mapping names to child nodes (directories or files).
    - `is_file`: Boolean indicating if the node is a file.
    - `content`: String to store file content.
2. **Operations:**
    
    - `ls(path)`: Traverse the path and list contents.
    - `mkdir(path)`: Create directories along the path.
    - `addContentToFile(path, content)`: Create or append content to a file.
    - `readContentFromFile(path)`: Retrieve content of a file.

### Example Walkthrough

For example:

```python
fs = FileSystem()
fs.mkdir("/a/b/c")
fs.addContentToFile("/a/b/c/file.txt", "Hello")
print(fs.ls("/a/b/c"))  # Output: ['file.txt']
print(fs.readContentFromFile("/a/b/c/file.txt"))  # Output: "Hello"
```

---

## Implementation in Python

```python
class FileSystem:
    class Node:
        def __init__(self):
            self.children = {}
            self.is_file = False
            self.content = ""

    def __init__(self):
        self.root = self.Node()

    def ls(self, path: str):
        node = self._traverse(path)
        if node.is_file:
            return [path.split('/')[-1]]
        return sorted(node.children.keys())

    def mkdir(self, path: str):
        self._traverse(path, create=True)

    def addContentToFile(self, filePath: str, content: str):
        node = self._traverse(filePath, create=True)
        node.is_file = True
        node.content += content

    def readContentFromFile(self, filePath: str) -> str:
        node = self._traverse(filePath)
        if node.is_file:
            return node.content
        return ""

    def _traverse(self, path: str, create=False):
        node = self.root
        if path == "/":
            return node
        parts = path.split("/")[1:]
        for part in parts:
            if part not in node.children:
                if create:
                    node.children[part] = self.Node()
                else:
                    return None
            node = node.children[part]
        return node
```

---

## Example Run

Input:

```python
fs = FileSystem()
fs.mkdir("/a/b/c")
fs.addContentToFile("/a/b/c/file.txt", "Hello")
print(fs.ls("/a/b/c"))
print(fs.readContentFromFile("/a/b/c/file.txt"))
```

Output:

```
['file.txt']
Hello
```

---

## Complexity Analysis

1. **Time Complexity:**
    
    - `ls(path)`: `O(m + n)` where `m` is path length and `n` is the number of items in the directory.
    - `mkdir(path)`: `O(m)` to traverse and create directories.
    - `addContentToFile(filePath, content)`: `O(m + c)` where `c` is content length.
    - `readContentFromFile(filePath)`: `O(m + c)` where `c` is content length.
2. **Space Complexity:** `O(m + c)`
    
    - `m` for directory structure and `c` for file content.

---

## Edge Cases

1. Path does not exist.
2. Empty directory.
3. Appending content multiple times.

---

## Conclusion

This solution efficiently implements an in-memory file system using a Trie-like structure to manage directories and files.