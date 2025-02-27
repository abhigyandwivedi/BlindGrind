```python
class ListNode:
	def __init__(self,val=0,Next=None):
		self.val=val
		self.Next=None
	
	def __str__(self):
		result=[]
		current=self
		while current:
			result.append(str(self.val))
			current=current.Next
		return result	
	
```