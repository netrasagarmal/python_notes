# Built-in Functions

---

## ✅ 1. `any()`

### 🔹 Purpose:

Returns `True` if **any one element** in the iterable is truthy (`True`), otherwise returns `False`.

### ✅ Syntax:

```python
any(iterable)
```

---

### ✅ Example 1: With list of booleans

```python
flags = [False, False, True]
print(any(flags))  # Output: True
```

### ✅ Example 2: With conditions

```python
nums = [0, 0, 0, 5]
print(any(x > 0 for x in nums))  # Output: True
```

---

## ✅ 2. `all()`

### 🔹 Purpose:

Returns `True` if **all elements** in the iterable are truthy (`True`), else returns `False`.

### ✅ Syntax:

```python
all(iterable)
```

---

### ✅ Example 1: With all True values

```python
flags = [True, True, True]
print(all(flags))  # Output: True
```

### ✅ Example 2: With list condition

```python
nums = [2, 4, 6, 8]
print(all(x % 2 == 0 for x in nums))  # Output: True
```

---

## ✅ 3. `map()`

### 🔹 Purpose:

Applies a **function to each item** of an iterable and returns a map object (like a generator).

### ✅ Syntax:

```python
map(function, iterable)
```

---

### ✅ Example 1: Square each number

```python
nums = [1, 2, 3]
squares = list(map(lambda x: x ** 2, nums))
print(squares)  # [1, 4, 9]
```

### ✅ Example 2: Convert strings to integers

```python
str_nums = ['1', '2', '3']
nums = list(map(int, str_nums))
print(nums)  # [1, 2, 3]
```

---

## ✅ 4. `reduce()` (from `functools`)

### 🔹 Purpose:

**Reduces** an iterable to a single value by applying a function cumulatively.

### ✅ Syntax:

```python
from functools import reduce
reduce(function, iterable)
```

---

### ✅ Example 1: Sum of all elements

```python
from functools import reduce
nums = [1, 2, 3, 4]
total = reduce(lambda x, y: x + y, nums)
print(total)  # 10
```

### ✅ Example 2: Find the maximum value

```python
from functools import reduce
nums = [4, 1, 7, 3]
maximum = reduce(lambda x, y: x if x > y else y, nums)
print(maximum)  # 7
```

---

## ✅ 5. `filter()`

### 🔹 Purpose:

Filters the elements of an iterable based on a function that returns `True` or `False`.

### ✅ Syntax:

```python
filter(function, iterable)
```

---

### ✅ Example 1: Keep even numbers

```python
nums = [1, 2, 3, 4, 5]
evens = list(filter(lambda x: x % 2 == 0, nums))
print(evens)  # [2, 4]
```

### ✅ Example 2: Remove empty strings

```python
words = ["apple", "", "banana", "", "cherry"]
non_empty = list(filter(None, words))
print(non_empty)  # ['apple', 'banana', 'cherry']
```

---

## ✅ 6. `zip()`

### 🔹 Purpose:

Combines elements from multiple iterables into tuples, **element-wise**.

### ✅ Syntax:

```python
zip(iter1, iter2, ...)
```

---

### ✅ Example 1: Combine names and scores

```python
names = ['Alice', 'Bob']
scores = [90, 85]
combined = list(zip(names, scores))
print(combined)  # [('Alice', 90), ('Bob', 85)]
```

### ✅ Example 2: Unzipping

```python
pairs = [('a', 1), ('b', 2)]
letters, numbers = zip(*pairs)
print(letters)  # ('a', 'b')
print(numbers)  # (1, 2)
```

---

## ✅ 7. `enumerate()`

### 🔹 What it does:

* The `enumerate()` function **adds a counter** to an iterable.
* Returns an **enumerate object**: pairs of `(index, value)`.

### ✅ Syntax:

```python
enumerate(iterable, start=0)
```

---

### ✅ Example 1: Loop with index

```python
fruits = ['apple', 'banana', 'cherry']
for index, fruit in enumerate(fruits):
    print(index, fruit)
```

#### Output:

```
0 apple
1 banana
2 cherry
```

---

### ✅ Example 2: Custom start index

```python
colors = ['red', 'green', 'blue']
for i, color in enumerate(colors, start=1):
    print(f"Color {i}: {color}")
```

#### Output:

```
Color 1: red
Color 2: green
Color 3: blue
```

---

## ✅ 8. `iter()`

### 🔹 What it does:

* Converts an **iterable** (like a list or string) into an **iterator**.
* Returns an **iterator object** that can be used with `next()`.

### ✅ Syntax:

```python
iter(iterable)
```

---

### ✅ Example 1: Manual iteration with `next()`

```python
nums = [10, 20, 30]
it = iter(nums)
print(next(it))  # 10
print(next(it))  # 20
print(next(it))  # 30
# print(next(it))  # Raises StopIteration
```

---

### ✅ Example 2: Iterating a string

```python
s = "ABC"
it = iter(s)
for _ in range(len(s)):
    print(next(it))
```

#### Output:

```
A
B
C
```

---

## ✅ 9. Iterator

### 🔹 What is an Iterator?

An **iterator** is:

* An object with a `__next__()` method (in Python 3) or `next()` (in Python 2).
* Returned by `iter()` on any **iterable** (like list, tuple, set, etc.).

### ✅ Iterator must implement:

* `__iter__()` — returns the iterator object itself
* `__next__()` — returns the next item or raises `StopIteration`

---

### ✅ Example 1: Custom Iterator Class

```python
class Counter:
    def __init__(self, start, end):
        self.current = start
        self.end = end

    def __iter__(self):
        return self

    def __next__(self):
        if self.current > self.end:
            raise StopIteration
        self.current += 1
        return self.current - 1

for num in Counter(1, 5):
    print(num)
```

#### Output:

```
1
2
3
4
5
```

---

### ✅ Example 2: Using `iter()` on iterable gives iterator

```python
lst = [1, 2, 3]
it = iter(lst)

print(hasattr(it, '__next__'))  # True
print(hasattr(it, '__iter__'))  # True
```

> ✅ This shows `it` is an **iterator**, not just an iterable.

---

## 🧠 Key Differences

| Feature  | `enumerate()`               | `iter()`                       | Iterator                               |
| -------- | --------------------------- | ------------------------------ | -------------------------------------- |
| Purpose  | Add index to iterable       | Convert iterable to iterator   | Object that returns data on `next()`   |
| Returns  | Enumerate object (iterator) | Iterator object                | Must implement `__next__` + `__iter__` |
| Use Case | Indexed loop                | Manual iteration with `next()` | Custom looping logic                   |



# Other Built-in Functions
---

## ➗ `divmod(a, b)`

- Returns a **tuple** `(a // b, a % b)` — quotient and remainder.

```python
print(divmod(10, 3))  # (3, 1)

```

---

## 🔤 `chr(i)`

- Converts an **integer to its Unicode character**.

```python
print(chr(65))  # 'A'

```

---

## 🔢 `bin(x)`

- Converts an integer to a **binary string**.

```python
print(bin(10))  # '0b1010'

```

---

## 🔣 `bytes()`

- Returns a **bytes object**, often used for binary data.

```python
b = bytes([65, 66, 67])
print(b)  # b'ABC'

```

---

## 🔡 `ascii(obj)`

- Returns a **printable ASCII-only string** of an object, escaping non-ASCII characters.

```python
print(ascii("Héllo"))  # 'H\xe9llo'

```

---

## 🧮 `oct(x)`

- Converts an integer to an **octal string**.

```python
print(oct(8))  # '0o10'

```

---

## 🔢 `hex(x)`

- Converts an integer to a **hexadecimal string**.

```python
print(hex(255))  # '0xff'

```