# Solution to "39. Combination Sum"

## Problem Statement

Given an array of distinct integers `candidates` and a target integer `target`, return a list of all unique combinations of `candidates` where the chosen numbers sum to `target`. You may use the same number multiple times.

Example:

```
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]

Input: candidates = [2,3,5], target = 8
Output: [[2,2,2,2],[2,3,3],[3,5]]
```

---

## Approach: Backtracking

### Explanation

1. **Backtracking:** Explore each candidate, either including it or skipping it, while reducing the target accordingly.
2. **Base Case:** When the target reaches `0`, add the current combination to the result.
3. **Recursive Case:** Continue exploring with the same element (for repetition) or move to the next element.

---

## Implementation in Python

```python
def combination_sum(nums, target):
    def backtrack(index, ds, target):
        tabs = "".join(["\t"] * (index))
        print(
            tabs,
            f"fn(index:{index},target:{target},ds:{ds},nums:{nums},result:{result})",
        )

        if target == 0:
            result.append(ds[:])
            return
        for i in range(index, len(nums)):
            print(tabs, f"Entering Loop i:{i} for fn(index:{index},target:{target},ds:{ds},nums:{nums},result:{result})")
            if nums[i] > target:
                print(
                    tabs,
                    f"Exiting Loop with bad {nums[i]} > {target} for i:{i} for fn(index:{index},target:{target},ds:{ds},nums:{nums},result:{result})",
                )
                continue  # Dont continue on this track of recursion
            ds.append(nums[i])
            backtrack(i, ds, target - nums[i])
            ds.pop()
            print(tabs, f"Exiting Loop with normal {nums[i]}<={target} for i:{i} fn(index:{index},target:{target},ds:{ds},nums:{nums},result:{result}) with ds appended")
    result = []
    candidates.sort()
    backtrack(0, [], target)
    return result


candidates = [7, 2, 3, 6]
target = 7
result = []
result = combination_sum(candidates, target)
print(result)

```

---

## Example Run

Input:

```python
candidates = [2, 3, 6, 7]
target = 7
result = combinationSum(candidates, target)
print(result)
```

Output:

```
[[2,2,3],[7]]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(2^T)`
    
    - T is the target value, and in the worst case, we explore all combinations.


- ## **Time Complexity Analysis**

- **Branching Factor:** Each number can be chosen multiple times.
- **Depth:** Maximum depth is **`target/min(candidates)`**.
- **Worst-case Complexity:** **O(2^T)** (exponential in terms of `target`).
- 
1. **Space Complexity:** `O(T)`
    
    - Recursion stack depth is proportional to the target.
    - 

---

## Edge Cases

1. No valid combinations: Return `[]`.
2. Single element equals target: Return `[[target]]`.
3. All candidates larger than target: Return `[]`.

---

## Conclusion

This solution efficiently finds all combinations that sum to the target using backtracking, ensuring correctness for all cases.


Recursion Tree and output textified:
```
 fn(index:0,target:7,ds:[],nums:[2, 3, 6, 7],result:[])
 fn(index:0,target:5,ds:[2],nums:[2, 3, 6, 7],result:[])
 fn(index:0,target:3,ds:[2, 2],nums:[2, 3, 6, 7],result:[])
 fn(index:0,target:1,ds:[2, 2, 2],nums:[2, 3, 6, 7],result:[])
	 fn(index:1,target:0,ds:[2, 2, 3],nums:[2, 3, 6, 7],result:[])
	 fn(index:1,target:2,ds:[2, 3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 fn(index:1,target:4,ds:[3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 fn(index:1,target:1,ds:[3, 3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
		 fn(index:2,target:1,ds:[6],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
			 fn(index:3,target:0,ds:[7],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
[[2, 2, 3], [7]]
```


0

```
 fn(index:0,target:7,ds:[],nums:[2, 3, 6, 7],result:[])
 Entering Loop i:0
 fn(index:0,target:5,ds:[2],nums:[2, 3, 6, 7],result:[])
 Entering Loop i:0
 fn(index:0,target:3,ds:[2, 2],nums:[2, 3, 6, 7],result:[])
 Entering Loop i:0
 fn(index:0,target:1,ds:[2, 2, 2],nums:[2, 3, 6, 7],result:[])
 Entering Loop i:0
 Exiting Loop with bad 2 > 1 for i:0
 Entering Loop i:1
 Exiting Loop with bad 3 > 1 for i:1
 Entering Loop i:2
 Exiting Loop with bad 6 > 1 for i:2
 Entering Loop i:3
 Exiting Loop with bad 7 > 1 for i:3
 Exiting Loop with normal 2<=3 for i:0
 Entering Loop i:1
	 fn(index:1,target:0,ds:[2, 2, 3],nums:[2, 3, 6, 7],result:[])
 Exiting Loop with normal 3<=3 for i:1
 Entering Loop i:2
 Exiting Loop with bad 6 > 3 for i:2
 Entering Loop i:3
 Exiting Loop with bad 7 > 3 for i:3
 Exiting Loop with normal 2<=5 for i:0
 Entering Loop i:1
	 fn(index:1,target:2,ds:[2, 3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Entering Loop i:1
	 Exiting Loop with bad 3 > 2 for i:1
	 Entering Loop i:2
	 Exiting Loop with bad 6 > 2 for i:2
	 Entering Loop i:3
	 Exiting Loop with bad 7 > 2 for i:3
 Exiting Loop with normal 3<=5 for i:1
 Entering Loop i:2
 Exiting Loop with bad 6 > 5 for i:2
 Entering Loop i:3
 Exiting Loop with bad 7 > 5 for i:3
 Exiting Loop with normal 2<=7 for i:0
 Entering Loop i:1
	 fn(index:1,target:4,ds:[3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Entering Loop i:1
	 fn(index:1,target:1,ds:[3, 3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Entering Loop i:1
	 Exiting Loop with bad 3 > 1 for i:1
	 Entering Loop i:2
	 Exiting Loop with bad 6 > 1 for i:2
	 Entering Loop i:3
	 Exiting Loop with bad 7 > 1 for i:3
	 Exiting Loop with normal 3<=4 for i:1
	 Entering Loop i:2
	 Exiting Loop with bad 6 > 4 for i:2
	 Entering Loop i:3
	 Exiting Loop with bad 7 > 4 for i:3
 Exiting Loop with normal 3<=7 for i:1
 Entering Loop i:2
		 fn(index:2,target:1,ds:[6],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
		 Entering Loop i:2
		 Exiting Loop with bad 6 > 1 for i:2
		 Entering Loop i:3
		 Exiting Loop with bad 7 > 1 for i:3
 Exiting Loop with normal 6<=7 for i:2
 Entering Loop i:3
			 fn(index:3,target:0,ds:[7],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
 Exiting Loop with normal 7<=7 for i:3
[[2, 2, 3], [7]]
```

# Further Notes:
```python
fn(index:0, target:7, ds:[], nums:[2, 3, 6, 7])
    ├── Pick 2 → fn(index:0, target:5, ds:[2])
    │      ├── Pick 2 → fn(index:0, target:3, ds:[2,2])
    │      │      ├── Pick 2 → fn(index:0, target:1, ds:[2,2,2]) → Exceeds, backtrack
    │      │      ├── Pick 3 → fn(index:1, target:0, ds:[2,2,3]) → **Valid**
    │      │      ├── Pick 6 → Exceeds, backtrack
    │      │      ├── Pick 7 → Exceeds, backtrack
    │      ├── Pick 3 → fn(index:1, target=2, ds:[2,3])
    │      │      ├── Pick 3 → Exceeds, backtrack
    │      │      ├── Pick 6 → Exceeds, backtrack
    │      │      ├── Pick 7 → Exceeds, backtrack
    │      ├── Pick 6 → fn(index:2, target=1, ds:[2,6]) → Exceeds, backtrack
    │      ├── Pick 7 → fn(index:3, target=0, ds:[7]) → **Valid**
    ├── Pick 3 → fn(index:1, target=4, ds:[3])
    ├── Pick 6 → fn(index:2, target=1, ds:[6]) → Exceeds, backtrack
    ├── Pick 7 → fn(index:3, target=0, ds:[7]) → **Valid**

```

# What is the Purpose of the For Loop?

The for loop iterates through the numbers starting from the current index (`index`) and explores all possible ways to sum up to `target` by recursively including numbers and backtracking.

## Step-by-Step Explanation of the Loop

### Loop Starts from Index:

- It ensures that the same number can be picked multiple times, but we do not go backwards (avoiding duplicate work).
- We only look forward to maintain order.

### Checks if `nums[i] > target`:

- If the number at index `i` is greater than `target`, it is skipped (pruning unnecessary calculations).

### Adds `nums[i]` to `ds` (current combination).

### Calls `backtrack(i, ds, target - nums[i])`:

- The function is called recursively with `i` (not `i + 1`), allowing repeated usage of the same number.
- `target` is reduced accordingly.

### Backtracks:

- Once recursion returns, we remove the last added number (undo the choice) to explore other possibilities.


```
 fn(index:0,target:7,ds:[],nums:[2, 3, 6, 7],result:[])
 Entering Loop i:0 for fn(index:0,target:7,ds:[],nums:[2, 3, 6, 7],result:[])
 fn(index:0,target:5,ds:[2],nums:[2, 3, 6, 7],result:[])
 Entering Loop i:0 for fn(index:0,target:5,ds:[2],nums:[2, 3, 6, 7],result:[])
 fn(index:0,target:3,ds:[2, 2],nums:[2, 3, 6, 7],result:[])
 Entering Loop i:0 for fn(index:0,target:3,ds:[2, 2],nums:[2, 3, 6, 7],result:[])
 fn(index:0,target:1,ds:[2, 2, 2],nums:[2, 3, 6, 7],result:[])
 Entering Loop i:0 for fn(index:0,target:1,ds:[2, 2, 2],nums:[2, 3, 6, 7],result:[])
 Exiting Loop with bad 2 > 1 for i:0 for fn(index:0,target:1,ds:[2, 2, 2],nums:[2, 3, 6, 7],result:[])
 Entering Loop i:1 for fn(index:0,target:1,ds:[2, 2, 2],nums:[2, 3, 6, 7],result:[])
 Exiting Loop with bad 3 > 1 for i:1 for fn(index:0,target:1,ds:[2, 2, 2],nums:[2, 3, 6, 7],result:[])
 Entering Loop i:2 for fn(index:0,target:1,ds:[2, 2, 2],nums:[2, 3, 6, 7],result:[])
 Exiting Loop with bad 6 > 1 for i:2 for fn(index:0,target:1,ds:[2, 2, 2],nums:[2, 3, 6, 7],result:[])
 Entering Loop i:3 for fn(index:0,target:1,ds:[2, 2, 2],nums:[2, 3, 6, 7],result:[])
 Exiting Loop with bad 7 > 1 for i:3 for fn(index:0,target:1,ds:[2, 2, 2],nums:[2, 3, 6, 7],result:[])
 Exiting Loop with normal 2<=3 for i:0 fn(index:0,target:3,ds:[2, 2],nums:[2, 3, 6, 7],result:[]) with ds appended
 Entering Loop i:1 for fn(index:0,target:3,ds:[2, 2],nums:[2, 3, 6, 7],result:[])
	 fn(index:1,target:0,ds:[2, 2, 3],nums:[2, 3, 6, 7],result:[])
 Exiting Loop with normal 3<=3 for i:1 fn(index:0,target:3,ds:[2, 2],nums:[2, 3, 6, 7],result:[[2, 2, 3]]) with ds appended
 Entering Loop i:2 for fn(index:0,target:3,ds:[2, 2],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
 Exiting Loop with bad 6 > 3 for i:2 for fn(index:0,target:3,ds:[2, 2],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
 Entering Loop i:3 for fn(index:0,target:3,ds:[2, 2],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
 Exiting Loop with bad 7 > 3 for i:3 for fn(index:0,target:3,ds:[2, 2],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
 Exiting Loop with normal 2<=5 for i:0 fn(index:0,target:5,ds:[2],nums:[2, 3, 6, 7],result:[[2, 2, 3]]) with ds appended
 Entering Loop i:1 for fn(index:0,target:5,ds:[2],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 fn(index:1,target:2,ds:[2, 3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Entering Loop i:1 for fn(index:1,target:2,ds:[2, 3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Exiting Loop with bad 3 > 2 for i:1 for fn(index:1,target:2,ds:[2, 3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Entering Loop i:2 for fn(index:1,target:2,ds:[2, 3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Exiting Loop with bad 6 > 2 for i:2 for fn(index:1,target:2,ds:[2, 3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Entering Loop i:3 for fn(index:1,target:2,ds:[2, 3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Exiting Loop with bad 7 > 2 for i:3 for fn(index:1,target:2,ds:[2, 3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
 Exiting Loop with normal 3<=5 for i:1 fn(index:0,target:5,ds:[2],nums:[2, 3, 6, 7],result:[[2, 2, 3]]) with ds appended
 Entering Loop i:2 for fn(index:0,target:5,ds:[2],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
 Exiting Loop with bad 6 > 5 for i:2 for fn(index:0,target:5,ds:[2],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
 Entering Loop i:3 for fn(index:0,target:5,ds:[2],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
 Exiting Loop with bad 7 > 5 for i:3 for fn(index:0,target:5,ds:[2],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
 Exiting Loop with normal 2<=7 for i:0 fn(index:0,target:7,ds:[],nums:[2, 3, 6, 7],result:[[2, 2, 3]]) with ds appended
 Entering Loop i:1 for fn(index:0,target:7,ds:[],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 fn(index:1,target:4,ds:[3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Entering Loop i:1 for fn(index:1,target:4,ds:[3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 fn(index:1,target:1,ds:[3, 3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Entering Loop i:1 for fn(index:1,target:1,ds:[3, 3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Exiting Loop with bad 3 > 1 for i:1 for fn(index:1,target:1,ds:[3, 3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Entering Loop i:2 for fn(index:1,target:1,ds:[3, 3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Exiting Loop with bad 6 > 1 for i:2 for fn(index:1,target:1,ds:[3, 3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Entering Loop i:3 for fn(index:1,target:1,ds:[3, 3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Exiting Loop with bad 7 > 1 for i:3 for fn(index:1,target:1,ds:[3, 3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Exiting Loop with normal 3<=4 for i:1 fn(index:1,target:4,ds:[3],nums:[2, 3, 6, 7],result:[[2, 2, 3]]) with ds appended
	 Entering Loop i:2 for fn(index:1,target:4,ds:[3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Exiting Loop with bad 6 > 4 for i:2 for fn(index:1,target:4,ds:[3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Entering Loop i:3 for fn(index:1,target:4,ds:[3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
	 Exiting Loop with bad 7 > 4 for i:3 for fn(index:1,target:4,ds:[3],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
 Exiting Loop with normal 3<=7 for i:1 fn(index:0,target:7,ds:[],nums:[2, 3, 6, 7],result:[[2, 2, 3]]) with ds appended
 Entering Loop i:2 for fn(index:0,target:7,ds:[],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
		 fn(index:2,target:1,ds:[6],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
		 Entering Loop i:2 for fn(index:2,target:1,ds:[6],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
		 Exiting Loop with bad 6 > 1 for i:2 for fn(index:2,target:1,ds:[6],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
		 Entering Loop i:3 for fn(index:2,target:1,ds:[6],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
		 Exiting Loop with bad 7 > 1 for i:3 for fn(index:2,target:1,ds:[6],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
 Exiting Loop with normal 6<=7 for i:2 fn(index:0,target:7,ds:[],nums:[2, 3, 6, 7],result:[[2, 2, 3]]) with ds appended
 Entering Loop i:3 for fn(index:0,target:7,ds:[],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
			 fn(index:3,target:0,ds:[7],nums:[2, 3, 6, 7],result:[[2, 2, 3]])
 Exiting Loop with normal 7<=7 for i:3 fn(index:0,target:7,ds:[],nums:[2, 3, 6, 7],result:[[2, 2, 3], [7]]) with ds appended
[[2, 2, 3], [7]]
```


# Combination Sum Variants

## 1. Combination Sum (LeetCode 39)

### Problem Statement

Given an array of distinct integers `candidates` and a target integer `target`, return all unique combinations of `candidates` where the chosen numbers sum to `target`. Each number may be used **unlimited** times.

### Example

```python
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3], [7]]
```

### Approach

- Use **backtracking** to explore all possible combinations.
- Avoid duplicates by considering only elements at or after the current index.

### Python Code

```python
def combinationSum(candidates, target):
    res = []
    
    def backtrack(start, path, remaining):
        if remaining == 0:
            res.append(path[:])
            return
        for i in range(start, len(candidates)):
            if candidates[i] > remaining:
                continue
            path.append(candidates[i])
            backtrack(i, path, remaining - candidates[i])
            path.pop()
    
    backtrack(0, [], target)
    return res
```

---

## 2. Combination Sum II (LeetCode 40)

### Problem Statement

Given a collection of integers `candidates` (which may contain duplicates) and a target `target`, find all unique combinations where the numbers sum to `target`. Each number may be used **only once**.

### Example

```python
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: [[1,1,6], [1,2,5], [1,7], [2,6]]
```

### Approach

- **Sort** the array to handle duplicates.
- Use **backtracking** but do **not reuse** elements from the same index.
- **Skip duplicate elements** in the recursion loop.

### Python Code

```python
def combinationSum2(candidates, target):
    res = []
    candidates.sort()
    
    def backtrack(start, path, remaining):
        if remaining == 0:
            res.append(path[:])
            return
        for i in range(start, len(candidates)):
            if i > start and candidates[i] == candidates[i - 1]:  # Skip duplicates
                continue
            if candidates[i] > remaining:
                break
            path.append(candidates[i])
            backtrack(i + 1, path, remaining - candidates[i])
            path.pop()
    
    backtrack(0, [], target)
    return res
```

---

## 3. Combination Sum III (LeetCode 216)

### Problem Statement

Find all valid combinations of `k` numbers that sum to `n`. Each number must be from **1 to 9**, and each number can be used **only once**.

### Example

```python
Input: k = 3, n = 7
Output: [[1,2,4]]
```

### Approach

- Use **backtracking**.
- Consider numbers **only from 1 to 9**.
- Each number can be used **once**.

### Python Code

```python
def combinationSum3(k, n):
    res = []
    
    def backtrack(start, path, remaining):
        if len(path) == k and remaining == 0:
            res.append(path[:])
            return
        for i in range(start, 10):  # 1 to 9
            if remaining < i:
                break
            path.append(i)
            backtrack(i + 1, path, remaining - i)
            path.pop()
    
    backtrack(1, [], n)
    return res
```

---

## 4. Combination Sum IV (LeetCode 377)

### Problem Statement

Find the **total number** of unique ways to sum up to `target`, where elements can be used **unlimited** times. The order of elements **matters**.

### Example

```python
Input: nums = [1,2,3], target = 4
Output: 7
Explanation: The possible combinations are:
(1,1,1,1), (1,1,2), (1,2,1), (1,3), (2,1,1), (2,2), (3,1)
```

### Approach

- Use **dynamic programming** (`dp` array).
- **Permutation matters** → Different from previous problems.

### Python Code

```python
def combinationSum4(nums, target):
    dp = [0] * (target + 1)
    dp[0] = 1  # One way to get sum = 0 (by choosing nothing)
    
    for t in range(1, target + 1):
        for num in nums:
            if num <= t:
                dp[t] += dp[t - num]
    
    return dp[target]
```

---

## Comparison of Variants

|Variant|Unique Combinations?|Reuse Same Element?|Handles Duplicates?|Order Matters?|Uses DP?|
|---|---|---|---|---|---|
|**Combination Sum**|✅|✅|❌|❌|❌|
|**Combination Sum II**|✅|❌|✅|❌|❌|
|**Combination Sum III**|✅|❌|✅ (1-9 only)|❌|❌|
|**Combination Sum IV**|❌ (Counts ways)|✅|❌|✅|✅|

---

Which variant do you need help with? 🚀