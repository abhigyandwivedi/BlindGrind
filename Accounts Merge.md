# Solution to "721. Accounts Merge"

## Problem Statement

Given a list of accounts where each account has a name followed by a list of emails, merge accounts that share common emails. Each account belongs to one person.

Example:

```
Input: accounts = [
    ["John", "johnsmith@mail.com", "john_newyork@mail.com"],
    ["John", "johnsmith@mail.com", "john00@mail.com"],
    ["Mary", "mary@mail.com"],
    ["John", "johnnybravo@mail.com"]
]

Output: [
    ["John", "john00@mail.com", "john_newyork@mail.com", "johnsmith@mail.com"],
    ["Mary", "mary@mail.com"],
    ["John", "johnnybravo@mail.com"]
]
```

---

## Approach: Disjoint Set Union (DSU)

### Explanation

1. **Union-Find:** Use DSU to group emails belonging to the same user.
2. **Map Emails to IDs:** Map each email to a unique ID and name.
3. **Merge Sets:** Use the DSU to find the root of each email and group them accordingly.
4. **Sort and Build Result:** Collect emails by root and output sorted lists.

---

## Implementation in Python

```python
from collections import defaultdict

class DSU:
    def __init__(self):
        self.parent = {}

    def find(self, x):
        if x != self.parent.setdefault(x, x):
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]

    def union(self, x, y):
        self.parent[self.find(x)] = self.find(y)

def accountsMerge(accounts: list[list[str]]) -> list[list[str]]:
    dsu = DSU()
    email_to_name = {}

    for account in accounts:
        name = account[0]
        first_email = account[1]
        for email in account[1:]:
            dsu.union(first_email, email)
            email_to_name[email] = name

    email_groups = defaultdict(list)
    for email in email_to_name:
        root = dsu.find(email)
        email_groups[root].append(email)

    result = []
    for root, emails in email_groups.items():
        result.append([email_to_name[root]] + sorted(emails))

    return result
```

---

## Example Run

Input:

```python
accounts = [
    ["John", "johnsmith@mail.com", "john_newyork@mail.com"],
    ["John", "johnsmith@mail.com", "john00@mail.com"],
    ["Mary", "mary@mail.com"],
    ["John", "johnnybravo@mail.com"]
]

print(accountsMerge(accounts))
```

Output:

```
[
    ["John", "john00@mail.com", "john_newyork@mail.com", "johnsmith@mail.com"],
    ["Mary", "mary@mail.com"],
    ["John", "johnnybravo@mail.com"]
]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(NlogN)`
    
    - `N` is the total number of emails. Sorting each group takes `O(NlogN)`.
2. **Space Complexity:** `O(N)`
    
    - Store parent relationships and email mappings.

---

## Edge Cases

1. Single account → Return as-is.
2. Completely disjoint accounts → No merging required.
3. Multiple accounts sharing common emails → Merged into one.

---

## Conclusion

This DSU-based solution efficiently merges accounts by connecting shared emails and outputting sorted results.