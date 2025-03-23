```python
def fn(index, ds, nums, n):
    tabs = "".join(["\t"] * (index))
    print(tabs, f"fn(index:{index},ds:{ds},nums:{nums},n:{n})")
    if index == n:
        print(tabs, "\t", ds)
        return
    # Take one on index
    ds.append(nums[index])
    fn(index + 1, ds, nums, n)
    # remove one from last
    ds.pop()
    fn(index + 1, ds, nums, n)


nums = [9, 4, 8, 7]
n = len(nums)
ds = []
fn(0, ds, nums, n)

```

******************************

 ```output
 fn(index:0,ds:[],nums:[9, 4, 8, 7],n:4)
	 fn(index:1,ds:[9],nums:[9, 4, 8, 7],n:4)
		 fn(index:2,ds:[9, 4],nums:[9, 4, 8, 7],n:4)
			 fn(index:3,ds:[9, 4, 8],nums:[9, 4, 8, 7],n:4)
				 fn(index:4,ds:[9, 4, 8, 7],nums:[9, 4, 8, 7],n:4)
				 	 [9, 4, 8, 7]
				 fn(index:4,ds:[9, 4, 8],nums:[9, 4, 8, 7],n:4)
				 	 [9, 4, 8]
			 fn(index:3,ds:[9, 4],nums:[9, 4, 8, 7],n:4)
				 fn(index:4,ds:[9, 4, 7],nums:[9, 4, 8, 7],n:4)
				 	 [9, 4, 7]
				 fn(index:4,ds:[9, 4],nums:[9, 4, 8, 7],n:4)
				 	 [9, 4]
		 fn(index:2,ds:[9],nums:[9, 4, 8, 7],n:4)
			 fn(index:3,ds:[9, 8],nums:[9, 4, 8, 7],n:4)
				 fn(index:4,ds:[9, 8, 7],nums:[9, 4, 8, 7],n:4)
				 	 [9, 8, 7]
				 fn(index:4,ds:[9, 8],nums:[9, 4, 8, 7],n:4)
				 	 [9, 8]
			 fn(index:3,ds:[9],nums:[9, 4, 8, 7],n:4)
				 fn(index:4,ds:[9, 7],nums:[9, 4, 8, 7],n:4)
				 	 [9, 7]
				 fn(index:4,ds:[9],nums:[9, 4, 8, 7],n:4)
				 	 [9]
	 fn(index:1,ds:[],nums:[9, 4, 8, 7],n:4)
		 fn(index:2,ds:[4],nums:[9, 4, 8, 7],n:4)
			 fn(index:3,ds:[4, 8],nums:[9, 4, 8, 7],n:4)
				 fn(index:4,ds:[4, 8, 7],nums:[9, 4, 8, 7],n:4)
				 	 [4, 8, 7]
				 fn(index:4,ds:[4, 8],nums:[9, 4, 8, 7],n:4)
				 	 [4, 8]
			 fn(index:3,ds:[4],nums:[9, 4, 8, 7],n:4)
				 fn(index:4,ds:[4, 7],nums:[9, 4, 8, 7],n:4)
				 	 [4, 7]
				 fn(index:4,ds:[4],nums:[9, 4, 8, 7],n:4)
				 	 [4]
		 fn(index:2,ds:[],nums:[9, 4, 8, 7],n:4)
			 fn(index:3,ds:[8],nums:[9, 4, 8, 7],n:4)
				 fn(index:4,ds:[8, 7],nums:[9, 4, 8, 7],n:4)
				 	 [8, 7]
				 fn(index:4,ds:[8],nums:[9, 4, 8, 7],n:4)
				 	 [8]
			 fn(index:3,ds:[],nums:[9, 4, 8, 7],n:4)
				 fn(index:4,ds:[7],nums:[9, 4, 8, 7],n:4)
				 	 [7]
				 fn(index:4,ds:[],nums:[9, 4, 8, 7],n:4)
				 	 []
```				 	 

