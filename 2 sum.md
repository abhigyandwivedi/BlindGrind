
#python2sum #2sum #2sumpython 

using hashmaps I found the index of other element required to be equal to target element.
I use a hashmap to store values like so{"key":arr_value,"value":index}
so say for the given arr [8,3,2,4] the map would be {8:0,3:1,2:2,4:3}
once map is prepped do a enumerated for over the array to identify the index of the other element which could be found by map[target-arr[i]] say j and i!= j

Time complexity : O(n)
space complexity : O(n)
```python

class Solution:
    def twoSum(self, nums, target: int):
       list_set= {x:y for y,x in enumerate(nums)}
    
       for i,v in enumerate(nums):      
           if (target-v) in list_set and i!=list_set[target-v]:
                return [i,list_set[target-v]]       



n=Solution()
print(n.twoSum([8,3,2,4],6))
```


# 2 sum ii

https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/

#python2sumii #2sumii #2sumiipython 
```python
class Solution:
	def twoSum(self, numbers: List[int], target: int) -> List[int]:
		l=0
		r=len(numbers)-1
		while l<r:
			if numbers[l]+numbers[r]==target:
				return [l+1,r+ 1]
			elif numbers[l]+numbers[r]<target:
				l+=1
			else:
				r-=1
		return [-1,-1]
```

Time Complexity : O(n)  
Space Complexity: O(1)