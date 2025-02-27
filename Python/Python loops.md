#pythonimportant #pythonloops #python #loops #reduce  #pythonreduce
## 1. `for` Loop
### Example: Iterating over a List
```python
numbers = [1, 2, 3, 4, 5]
for num in numbers:
    print(num)
```

### Example: Using `range()`
```python
for i in range(5):  # 0 to 4
    print(i)
```

---

## 2. `while` Loop
### Example: Basic `while` Loop
```python
count = 0
while count < 5:
    print(count)
    count += 1
```

### Example: Using `while` with `break`
```python
x = 0
while True:
    print(x)
    x += 1
    if x == 5:
        break
```

---

## 3. Nested Loops
### Example: Nested `for` Loops
```python
for i in range(3):
    for j in range(3):
        print(f"i={i}, j={j}")
```

### Example: Nested `while` Loops
```python
i = 0
while i < 3:
    j = 0
    while j < 3:
        print(f"i={i}, j={j}")
        j += 1
    i += 1
```

---

## 4. Loop with `else`
### Example: `for-else`
```python
for i in range(3):
    print(i)
else:
    print("Loop completed!")
```

### Example: `while-else`
```python
x = 0
while x < 3:
    print(x)
    x += 1
else:
    print("While loop ended!")
```

---

## 5. Looping with `break` and `continue`
### Example: Using `break`
```python
for i in range(5):
    if i == 3:
        break
    print(i)  # Stops at 3
```

### Example: Using `continue`
```python
for i in range(5):
    if i == 2:
        continue  # Skips 2
    print(i)
```

---

## 6. Looping with `pass`
### Example: `pass` in a Loop
```python
for i in range(5):
    if i == 2:
        pass  # Placeholder, does nothing
    print(i)
```

---

## 7. List Comprehensions (Loop in One Line)
### Example: Creating a List
```python
squares = [x**2 for x in range(5)]
print(squares)  # Output: [0, 1, 4, 9, 16]
```

### Example: List Comprehension with `if` Condition
```python
even_numbers = [x for x in range(10) if x % 2 == 0]
print(even_numbers)  # Output: [0, 2, 4, 6, 8]
```

---

## 8. Dictionary & Set Comprehensions
### Example: Dictionary Comprehension
```python
squared_dict = {x: x**2 for x in range(5)}
print(squared_dict)  # Output: {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

### Example: Set Comprehension
```python
squared_set = {x**2 for x in range(5)}
print(squared_set)  # Output: {0, 1, 4, 9, 16}
```

---

## 9. Using `map()` with Lambda (Functional Loop)
### Example: Using `map()`
```python
numbers = [1, 2, 3, 4]
squared = list(map(lambda x: x**2, numbers))
print(squared)  # Output: [1, 4, 9, 16]
```

---

## 10. Using `filter()` with Lambda (Conditional Loop)
### Example: Using `filter()`
```python
numbers = [1, 2, 3, 4, 5, 6]
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
print(even_numbers)  # Output: [2, 4, 6]
```

---

## 11. Using `reduce()` with Lambda (Cumulative Loop)
```python
from functools import reduce
numbers = [1, 2, 3, 4]
product = reduce(lambda x, y: x * y, numbers)
print(product)  # Output: 24 (1*2*3*4)
```

---

## 12. Using `zip()` in a Loop
### Example: Iterating Over Two Lists Simultaneously
```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
for name, age in zip(names, ages):
    print(f"{name} is {age} years old")
```

---

## 13. Using `enumerate()` in a Loop
### Example: Getting Index While Iterating
```python
fruits = ["apple", "banana", "cherry"]
for index, fruit in enumerate(fruits):
    print(f"Index {index}: {fruit}")
```

---

## 14. Generator Loops (`yield`)
### Example: Generator Function
```python
def countdown(n):
    while n > 0:
        yield n
        n -= 1

for num in countdown(5):
    print(num)  # Output: 5, 4, 3, 2, 1
```

---

## 15. Infinite Loop (Use with Caution)
### Example: Infinite `while` Loop
```python
while True:
    print("This will run forever!")  # Stop with Ctrl+C
```

---

## 16. Using `itertools` for Advanced Looping
### Example: Infinite Counter
```python
from itertools import count

for num in count(1):  # Starts at 1, goes forever
    print(num)
    if num == 5:
        break  # Stop at 5
```


