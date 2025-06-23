# Python Dictionary Data Strucutre

Here’s a **clear explanation and example** for each important `dict` method in Python:

---

## ✅ 1. `get(key, default=None)`

Safely retrieve a value from a dictionary. Returns `None` (or a default) if the key is missing.

```python
d = {'name': 'Alice', 'age': 25}
print(d.get('name'))        # Alice
print(d.get('city'))        # None
print(d.get('city', 'NY'))  # NY
```

> 🔹 Useful for avoiding `KeyError` when accessing missing keys.

---

## ✅ 2. `pop(key, default)`

Removes and returns the value associated with the key. If key doesn’t exist and `default` is provided, returns the default.

```python
d = {'a': 10, 'b': 20}
val = d.pop('a')
print(val)  # 10
print(d)    # {'b': 20}

# With default:
print(d.pop('z', 'Not found'))  # Not found
```

> 🔹 Modifies the dict by removing the key.

---

## ✅ 3. `keys()`

Returns a **view** object of all keys.

```python
d = {'x': 1, 'y': 2}
print(list(d.keys()))  # ['x', 'y']
```

> 🔹 Often used in loops or to check if a key exists.

---

## ✅ 4. `values()`

Returns a **view** object of all values.

```python
d = {'x': 1, 'y': 2}
print(list(d.values()))  # [1, 2]
```

> 🔹 Can be used to search if a value exists.

---

## ✅ 5. `items()`

Returns a **view** object of (key, value) pairs as tuples.

```python
d = {'x': 1, 'y': 2}
for k, v in d.items():
    print(f"{k} => {v}")
# x => 1
# y => 2
```

> 🔹 Commonly used in `for` loops to iterate over dicts.

---

## ✅ 6. `update(other_dict)`

Merges another dictionary into the current one. Overwrites matching keys.

```python
d = {'a': 1, 'b': 2}
d.update({'b': 3, 'c': 4})
print(d)  # {'a': 1, 'b': 3, 'c': 4}
```

> 🔹 Equivalent to doing multiple assignments like `d['b'] = 3`

---

## ✅ 7. `setdefault(key, default)`

Returns the value if key exists, else sets it to `default` and returns that.

```python
d = {'a': 1}
val = d.setdefault('a', 100)
print(val)  # 1

val2 = d.setdefault('b', 200)
print(val2)  # 200
print(d)     # {'a': 1, 'b': 200}
```

> 🔹 Useful for initializing nested dictionaries.

---

## ✅ 8. `clear()`

Removes all items from the dictionary.

```python
d = {'x': 10, 'y': 20}
d.clear()
print(d)  # {}
```

> 🔹 Completely resets the dictionary in-place.

---

## 💡 Summary Table

| Method         | Purpose                                |
| -------------- | -------------------------------------- |
| `get()`        | Safe key access                        |
| `pop()`        | Remove and return key’s value          |
| `keys()`       | Return all keys                        |
| `values()`     | Return all values                      |
| `items()`      | Return key-value pairs                 |
| `update()`     | Merge with another dict                |
| `setdefault()` | Insert key with default if not present |
| `clear()`      | Remove all entries                     |

---

## Dict Keys Concept:

### Question: can we use list or set as a key for dict:
---

## 📌 Reason:

Dictionary keys must be **hashable** and **immutable** because they are stored in a **hash table**.

* ✅ **Immutable** types like `str`, `int`, `tuple` (with only immutable elements) are hashable.
* ❌ **Mutable** types like `list`, `set`, and `dict` are not hashable and thus cannot be keys.

---

## 🧪 Example: Trying to use list/set as dict key:

```python
d = {}
d[[1, 2]] = "value"   # ❌ TypeError
```

```
TypeError: unhashable type: 'list'
```

```python
d[{1, 2}] = "value"   # ❌ TypeError
```

```
TypeError: unhashable type: 'set'
```

---

## ✅ What You Can Use as Keys:

| Type         | Can be dict key?             | Reason                |
| ------------ | ---------------------------- | --------------------- |
| `int`, `str` | ✅                            | Immutable, hashable   |
| `tuple`      | ✅ (if elements are hashable) |                       |
| `list`       | ❌                            | Mutable, not hashable |
| `set`        | ❌                            | Mutable, not hashable |
| `frozenset`  | ✅                            | Immutable, hashable   |

---

## ✅ Correct Way (using `tuple` or `frozenset`):

```python
d = {}
d[(1, 2)] = "value"        # ✅ tuple is hashable
d[frozenset([1, 2])] = "v" # ✅ frozenset is hashable
```

---

Let me know if you want a deep dive into **hashability**, `__hash__()` & `__eq__()` mechanics or custom dict key design!


---

# Advance Dict Examples:

---

## 🔁 **1. How do you merge two dictionaries without modifying either?**

```python
d1 = {'a': 1}
d2 = {'b': 2}
merged = {**d1, **d2}
print(merged)  # {'a': 1, 'b': 2}
```

> ✅ `**dict` unpacking is clean and preserves immutability.

---

## 🧠 **2. How to merge multiple dictionaries in one line (Python 3.9+)?**

```python
d1 = {'a': 1}
d2 = {'b': 2}
d3 = {'c': 3}
merged = d1 | d2 | d3
print(merged)  # {'a': 1, 'b': 2, 'c': 3}
```

> ✅ Use `|` operator (introduced in Python 3.9).

---

## 🕳️ **3. How to safely access a deeply nested key?**

```python
data = {'a': {'b': {'c': 10}}}
value = data.get('a', {}).get('b', {}).get('c')
print(value)  # 10
```

---

## 🧹 **4. Remove all keys with falsy values from a dictionary**

```python
d = {'a': 0, 'b': False, 'c': 5, 'd': ''}
cleaned = {k: v for k, v in d.items() if v}
print(cleaned)  # {'c': 5}
```

---

## 🧾 **5. Count frequency of elements in a list using `dict`**

```python
lst = ['a', 'b', 'a', 'c']
freq = {}
for item in lst:
    freq[item] = freq.get(item, 0) + 1
print(freq)  # {'a': 2, 'b': 1, 'c': 1}
```

---

## 🧠 **6. What are `dict_keys`, `dict_values`, and `dict_items`?**

They are **view objects** – dynamic, memory-efficient references to keys/values/pairs.

```python
d = {'x': 1}
keys = d.keys()
print(list(keys))  # ['x']
```

---

## 📐 **7. How to invert a dictionary (swap keys and values)?**

```python
d = {'a': 1, 'b': 2}
inv = {v: k for k, v in d.items()}
print(inv)  # {1: 'a', 2: 'b'}
```

---

## 🧑‍💻 **8. How to sort a dictionary by its values (descending)?**

```python
d = {'a': 5, 'b': 1, 'c': 3}
sorted_dict = dict(sorted(d.items(), key=lambda x: x[1], reverse=True))
# {'a': 5, 'c': 3, 'b': 1}
```

---

## 🧱 **9. How to group a list of tuples by their first element?**

```python
pairs = [('a', 1), ('b', 2), ('a', 3)]
grouped = {}
for k, v in pairs:
    grouped.setdefault(k, []).append(v)
print(grouped)  # {'a': [1, 3], 'b': [2]}
```

---

## 🧪 **10. How to filter dictionary keys based on condition?**

```python
d = {'a': 1, 'b': 2, 'c': 3}
filtered = {k: v for k, v in d.items() if v > 1}
print(filtered)  # {'b': 2, 'c': 3}
```

---

## 🧮 **11. Use dictionary comprehension to map squares**

```python
squares = {x: x**2 for x in range(1, 6)}
print(squares)  # {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
```

---

## 🧠 **12. What's the difference between `get()` and `[]`?**

* `get()` returns `None` or default, safe.
* `[]` raises `KeyError` if key is missing.

```python
d = {'x': 1}
print(d.get('y', 0))  # 0
# print(d['y'])  # KeyError
```

---

## ⚠️ **13. What happens if you mutate a key?**

You can't – `dict` keys must be **hashable and immutable**.

```python
# d = {[1,2]: "list"} ❌ TypeError: unhashable type: 'list'
```

---

## ⛓️ **14. Use a tuple as a dict key**

```python
d = {(1, 2): 'point'}
print(d[(1, 2)])  # point
```

> ✅ Tuples are immutable and hashable → valid keys.

---

## 📊 **15. Create a frequency counter using `collections.defaultdict`**

```python
from collections import defaultdict

freq = defaultdict(int)
for char in 'banana':
    freq[char] += 1

print(dict(freq))  # {'b': 1, 'a': 3, 'n': 2}
```

---

## 🏗️ **16. Create nested dictionary from list of keys**

```python
keys = ['a', 'b', 'c']
nested = current = {}
for k in keys:
    current[k] = {}
    current = current[k]
print(nested)  # {'a': {'b': {'c': {}}}}
```

---

## 🔍 **17. Find common keys between two dictionaries**

```python
d1 = {'a': 1, 'b': 2}
d2 = {'b': 3, 'c': 4}
common = d1.keys() & d2.keys()
print(common)  # {'b'}
```

---

## ⛔ **18. How to remove a key safely if it may not exist?**

```python
d = {'x': 1}
d.pop('y', None)  # Does nothing if 'y' doesn't exist
```

---

## 🧠 **19. How to initialize a dictionary with same value for multiple keys?**

```python
keys = ['a', 'b', 'c']
d = dict.fromkeys(keys, 0)
print(d)  # {'a': 0, 'b': 0, 'c': 0}
```

---

## 🚀 **20. Dictionary with function as value (dispatch table)**

```python
def add(x, y): return x + y
def sub(x, y): return x - y

ops = {'+': add, '-': sub}
print(ops['+'](10, 5))  # 15
```

---

## 🔚 Summary of Concepts Covered:

* ✅ Merging, updating, filtering
* ✅ Comprehensions, nested dicts
* ✅ `get()`, `pop()`, `setdefault()`, view objects
* ✅ Custom structures, counting, grouping, sorting
* ✅ Advanced key/value types

---

## Interview-Style `dict` Use Cases

---

### ✅ **1. Count character frequency in a string**

**Problem:** Count how many times each character appears in `"engineering"`.

```python
from collections import defaultdict

s = "engineering"
freq = defaultdict(int)

for char in s:
    freq[char] += 1

print(dict(freq))  
# {'e': 3, 'n': 3, 'g': 2, 'i': 2, 'r': 1}
```

> 🔹 Replace `defaultdict(int)` with `Counter(s)` if allowed.

---

### ✅ **2. Group words by their first letter**

```python
words = ["apple", "apricot", "banana", "blueberry", "avocado"]
grouped = defaultdict(list)

for word in words:
    grouped[word[0]].append(word)

print(dict(grouped))
# {'a': ['apple', 'apricot', 'avocado'], 'b': ['banana', 'blueberry']}
```

---

### ✅ **3. Count frequency of elements in a list without using `collections`**

```python
nums = [1, 2, 2, 3, 3, 3]
freq = {}

for num in nums:
    freq[num] = freq.get(num, 0) + 1

print(freq)  # {1: 1, 2: 2, 3: 3}
```

---

### ✅ **4. Group anagram words together**

```python
words = ["bat", "tab", "cat", "act", "tac", "dog"]

anagrams = defaultdict(list)

for word in words:
    key = ''.join(sorted(word))
    anagrams[key].append(word)

print(list(anagrams.values()))
# [['bat', 'tab'], ['cat', 'act', 'tac'], ['dog']]
```

---

### ✅ **5. Build an index of positions of words in a sentence**

```python
sentence = "to be or not to be"
word_positions = defaultdict(list)

for i, word in enumerate(sentence.split()):
    word_positions[word].append(i)

print(dict(word_positions))
# {'to': [0, 4], 'be': [1, 5], 'or': [2], 'not': [3]}
```

---

### ✅ **6. Implement a `defaultdict` manually**

```python
class MyDefaultDict(dict):
    def __init__(self, default_factory):
        super().__init__()
        self.default_factory = default_factory

    def __getitem__(self, key):
        if key not in self:
            self[key] = self.default_factory()
        return super().__getitem__(key)

d = MyDefaultDict(list)
d['x'].append(1)
print(d)  # {'x': [1]}
```

---

### ✅ **7. Group students by department from list of tuples**

```python
students = [
    ("Alice", "CS"),
    ("Bob", "Math"),
    ("Charlie", "CS"),
    ("David", "Math"),
]

groups = defaultdict(list)
for name, dept in students:
    groups[dept].append(name)

print(dict(groups))
# {'CS': ['Alice', 'Charlie'], 'Math': ['Bob', 'David']}
```

---

### ✅ **8. Create nested dictionaries dynamically**

```python
nested = lambda: defaultdict(nested)
data = nested()
data['user']['preferences']['theme'] = 'dark'
print(data['user']['preferences']['theme'])  # dark
```

> ⚠️ Use carefully — it creates infinite-depth structures.

---

### ✅ **9. Find the word with max frequency in a sentence**

```python
sentence = "apple banana apple orange banana apple"
words = sentence.split()
freq = {}

for word in words:
    freq[word] = freq.get(word, 0) + 1

max_word = max(freq, key=freq.get)
print(max_word)  # apple
```

---

### ✅ **10. Group scores by student and calculate average**

```python
records = [
    ("Alice", 85),
    ("Bob", 78),
    ("Alice", 95),
    ("Bob", 88),
]

scores = defaultdict(list)
for name, score in records:
    scores[name].append(score)

averages = {name: sum(marks)/len(marks) for name, marks in scores.items()}
print(averages)  # {'Alice': 90.0, 'Bob': 83.0}
```

---

## 🧠 Tips for Interviews:

* Use `get()` when unsure if a key exists.
* Prefer `defaultdict` or `setdefault()` for grouping.
* Avoid mutating dicts during iteration.
* Understand `dict` time complexity (O(1) avg for get/set).

---
