



| Tree BFS - Level Order Traversal<br> | Problems                                      |
| ------------------------------------ | --------------------------------------------- |
|                                      | 102. Binary Tree Level Order Traversal        |
|                                      | 103. Binary Tree Zigzag Level Order Traversal |
|                                      | 199. Binary Tree Right Side View              |
|                                      | 515. Find Largest Value in Each Tree Row      |
|                                      | 1161. Maximum Level Sum of a Binary Tree      |

| Tree DFS - Recursive Preorder Traversal | Problems                                                       |
| --------------------------------------- | -------------------------------------------------------------- |
|                                         | 100. Same Tree                                                 |
|                                         | 101. Symmetric Tree                                            |
|                                         | 105. Construct Binary Tree from Preorder and Inorder Traversal |
|                                         | 114. Flatten Binary Tree to Linked List                        |
|                                         | 226. Invert Binary Tree                                        |
|                                         | 257. Binary Tree Paths                                         |
|                                         | 988. Smallest String Starting From Leaf                        |



| Tree DFS - Recursive Inorder Traversal | Problems                                |
| -------------------------------------- | --------------------------------------- |
|                                        | 94. Binary Tree Inorder Traversal       |
|                                        | 98. Validate Binary Search Tree         |
|                                        | 173. Binary Search Tree Iterator        |
|                                        | 230. Kth Smallest Element in a BST      |
|                                        | 501. Find Mode in Binary Search Tree    |
|                                        | 530. Minimum Absolute Difference in BST |


| Tree DFS - Recursive Postorder Traversal | Problems                                                  |
| ---------------------------------------- | --------------------------------------------------------- |
|                                          | 104. Maximum Depth of Binary Tree                         |
|                                          | 110. Balanced Binary Tree                                 |
|                                          | 124. Binary Tree Maximum Path Sum                         |
|                                          | 145. Binary Tree Postorder Traversal                      |
|                                          | 337. House Robber III                                     |
|                                          | 366. Find Leaves of Binary Tree                           |
|                                          | 543. Diameter of Binary Tree                              |
|                                          | 863. All Nodes Distance K in Binary Tree                  |
|                                          | 1110. Delete Nodes And Return Forest                      |
|                                          | 2458. Height of Binary Tree After Subtree Removal Queries |

| Tree - Lowest Common Ancestor (LCA) Finding | Problems                                            |
| ------------------------------------------- | --------------------------------------------------- |
|                                             | 235. Lowest Common Ancestor of a Binary Search Tree |
|                                             | 236. Lowest Common Ancestor of a Binary Tree        |

| Tree - Serialization and Deserialization | Problems                                   |
| ---------------------------------------- | ------------------------------------------ |
|                                          | 297. Serialize and Deserialize Binary Tree |
|                                          | 572. Subtree of Another Tree               |
|                                          | 652. Find Duplicate Subtrees               |


| Graph DFS - Connected Components / Island Counting | Problems                         |
| -------------------------------------------------- | -------------------------------- |
|                                                    | 130. Surrounded Regions          |
|                                                    | 200. Number of Islands           |
|                                                    | 417. Pacific Atlantic Water Flow |
|                                                    | 547. Number of Provinces         |
|                                                    | 695. Max Area of Island          |
|                                                    | 733. Flood Fill                  |
|                                                    | 841. Keys and Rooms              |
|                                                    | 1020. Number of Enclaves         |
|                                                    | 1254. Number of Closed Islands   |
|                                                    | 1905. Count Sub Islands          |
|                                                    | 2101. Detonate the Maximum Bombs |


| Graph BFS - Connected Components / Island Counting | Problems                             |
| -------------------------------------------------- | ------------------------------------ |
|                                                    | 127. Word Ladder                     |
|                                                    | 542. 01 Matrix                       |
|                                                    | 994. Rotting Oranges                 |
|                                                    | 1091. Shortest Path in Binary Matrix |





| Graph DFS - Cycle Detection (Directed Graph) | Problems                                        |
| -------------------------------------------- | ----------------------------------------------- |
|                                              | 207. Course Schedule                            |
|                                              | 210. Course Schedule II                         |
|                                              | 802. Find Eventual Safe States                  |
|                                              | 1059. All Paths from Source Lead to Destination |


| Graph BFS - Topological Sort (Kahn's Algorithm) | Problems                                            |
| ----------------------------------------------- | --------------------------------------------------- |
|                                                 | 207. Course Schedule                                |
|                                                 | 210. Course Schedule II                             |
|                                                 | 269. Alien Dictionary                               |
|                                                 | 310. Minimum Height Trees                           |
|                                                 | 444. Sequence Reconstruction                        |
|                                                 | 1136. Parallel Courses                              |
|                                                 | 1857. Largest Color Value in a Directed Graph       |
|                                                 | 2050. Parallel Courses III                          |
|                                                 | 2115. Find All Possible Recipes from Given Supplies |
|                                                 | 2392. Build a Matrix With Conditions                |

| Graph - Deep Copy / Cloning  | Problems         |
| ---------------------------- | ---------------- |
| #dfs #bfs #graph  #hashtable | 133. Clone Graph |


| Graph - Shortest Path (Bellman-Ford / BFS + K) | Problems                             |
| ---------------------------------------------- | ------------------------------------ |
|                                                | 787. Cheapest Flights Within K Stops |



| Graph - Union-Find (Disjoint Set Union - DSU) | Problems                                                   |
| --------------------------------------------- | ---------------------------------------------------------- |
|                                               | 200. Number of Islands                                     |
|                                               | 261. Graph Valid Tree                                      |
|                                               | 305. Number of Islands II                                  |
|                                               | 323. Number of Connected Components in an Undirected Graph |
|                                               | 547. Number of Provinces                                   |
|                                               | 684. Redundant Connection                                  |
|                                               | 721. Accounts Merge                                        |
|                                               | 737. Sentence Similarity II                                |
|                                               | 947. Most Stones Removed with Same Row or Column           |
|                                               | 952. Largest Component Size by Common Factor               |
|                                               | 959. Regions Cut By Slashes                                |
|                                               | 1101. The Earliest Moment When Everyone Become Friends     |



# Topological Sort

| Problem                                            | Difficulty | Notes                                                       |
| -------------------------------------------------- | ---------- | ----------------------------------------------------------- |
| 207. Course Schedule                               | Medium     | Cycle detection in a DAG                                    |
| 210. Course Schedule II                            | Medium     | Return one valid topological order                          |
| 269. Alien Dictionary                              | Hard       | Topo sort with character graph                              |
| 444. Sequence Reconstruction                       | Medium     | Detect **unique** topological order                         |
| 1203. Sort Items by Groups Respecting Dependencies | Hard       | Multi-level topological sort (group + item)                 |
| 1857. Largest Color Value in a Directed Graph      | Hard       | Max color path in a DAG (cycle detection + tracking paths)  |
| 329. Longest Increasing Path in a Matrix           | Hard       | Treat as DAG and apply DFS-based topological sorting        |
| 2050. Parallel Courses III                         | Hard       | Topo sort + DP for time scheduling                          |
| 1128. Number of Equivalent Domino Pairs            | Easy       | Not topo sort – don’t be tricked by similar sounding titles |