# Python Data Types
---

## 🔢 1. Numeric Types

| Type      | Description                      | Example      |
| --------- | -------------------------------- | ------------ |
| `int`     | Integer numbers                  | `x = 10`     |
| `float`   | Decimal (floating-point) numbers | `pi = 3.14`  |
| `complex` | Complex numbers (a + bj)         | `z = 2 + 3j` |

```python
a = 10        # int
b = 3.14      # float
c = 1 + 2j    # complex
```

---

## 🔤 2. Text Type

| Type  | Description               | Example       |
| ----- | ------------------------- | ------------- |
| `str` | Unicode character strings | `s = "Hello"` |

```python
s = "Python"
print(s.upper())   # PYTHON
```

---

## 📦 3. Sequence Types

| Type    | Description                   | Mutable? |
| ------- | ----------------------------- | -------- |
| `list`  | Ordered, mutable collection   | ✅        |
| `tuple` | Ordered, immutable collection | ❌        |
| `range` | Immutable sequence of numbers | ❌        |

### List

```python
l = [1, 2, 3]
l.append(4)
```

### Tuple

```python
t = (1, 2, 3)
# t[0] = 9 ❌ Error: immutable
```

### Range

```python
r = range(1, 5)
print(list(r))  # [1, 2, 3, 4]
```

---

## 🗃️ 4. Set Types

| Type        | Description              | Mutable? |
| ----------- | ------------------------ | -------- |
| `set`       | Unordered, unique items  | ✅        |
| `frozenset` | Immutable version of set | ❌        |

### Set

```python
s = {1, 2, 3}
s.add(4)
```

### Frozenset

```python
fs = frozenset([1, 2, 3])
# fs.add(4) ❌ Error
```

---

## 🗂️ 5. Mapping Type

| Type   | Description                | Mutable? |
| ------ | -------------------------- | -------- |
| `dict` | Key-value pairs, unordered | ✅        |

```python
d = {"name": "Alice", "age": 25}
d["age"] = 26
```

---

## ⚙️ 6. Boolean Type

| Type   | Description          | Example         |
| ------ | -------------------- | --------------- |
| `bool` | Logical value: `T/F` | `True`, `False` |

```python
is_active = True
```

---

## 🧵 7. Binary Types

| Type         | Description                 | Mutable? |
| ------------ | --------------------------- | -------- |
| `bytes`      | Immutable sequence of bytes | ❌        |
| `bytearray`  | Mutable version of bytes    | ✅        |
| `memoryview` | Access internal byte data   | ✅        |

```python
b = b"hello"            # bytes
ba = bytearray(b)       # bytearray
mv = memoryview(b)      # memoryview
```

---

## ⛔ 8. None Type

| Type       | Description                 |
| ---------- | --------------------------- |
| `NoneType` | Represents null/empty value |

```python
x = None
```

---

## ✅ Summary Table

| Category | Types                              |
| -------- | ---------------------------------- |
| Numeric  | `int`, `float`, `complex`          |
| Text     | `str`                              |
| Sequence | `list`, `tuple`, `range`           |
| Set      | `set`, `frozenset`                 |
| Mapping  | `dict`                             |
| Boolean  | `bool`                             |
| Binary   | `bytes`, `bytearray`, `memoryview` |
| Special  | `NoneType`                         |

---

## 🔄 Mutable vs Immutable – Quick Summary

| Type        | Can Change After Creation? | Examples                                                     |
| ----------- | -------------------------- | ------------------------------------------------------------ |
| ✅ Mutable   | Yes                        | `list`, `dict`, `set`, `bytearray`                           |
| ❌ Immutable | No                         | `int`, `float`, `str`, `tuple`, `frozenset`, `bool`, `bytes` |

---

## ✅ Mutable Data Types

Mutable objects **can be modified in place**.

### 1. `list`

```python
a = [1, 2, 3]
a[0] = 100        # Modify element
a.append(4)       # Add new element
print(a)          # [100, 2, 3, 4]
```

### 2. `dict`

```python
d = {"x": 10, "y": 20}
d["x"] = 99       # Change value
d["z"] = 30       # Add new key-value
print(d)          # {'x': 99, 'y': 20, 'z': 30}
```

### 3. `set`

```python
s = {1, 2, 3}
s.add(4)          # Add element
s.remove(2)       # Remove element
print(s)          # {1, 3, 4}
```

---

## ❌ Immutable Data Types

Immutable objects **cannot be modified**. If you try to change them, a **new object is created**.

### 1. `int`

```python
x = 10
y = x
x = x + 5
print(x, y)       # 15 10
# x points to new object; y still points to old one
```

### 2. `str`

```python
s = "hello"
s2 = s
s = s + " world"
print(s, s2)      # 'hello world' 'hello'
```

### 3. `tuple`

```python
t = (1, 2, 3)
# t[0] = 9       ❌ Error: tuple does not support item assignment
```

---

## 🔍 Behind the Scenes: `id()` Demo

```python
x = 100
print(id(x))
x += 1
print(id(x))  # Different ID => new object created (immutable)

lst = [1, 2]
print(id(lst))
lst.append(3)
print(id(lst))  # Same ID => modified in place (mutable)
```

---

## 🧠 Why It Matters

* **Mutable types** can change unexpectedly when passed to functions.
* **Immutable types** are safer for shared/global variables, keys in dictionaries, and hash-based collections.

---

## 📘 3. Type Casting (Type Conversion)

### 🔹 Implicit Type Casting

Python automatically converts compatible types:

```python
x = 5       # int
y = 2.0     # float
z = x + y   # float
print(z)    # Output: 7.0

```

### 🔹 Explicit Type Casting

Manually converting data types:

```python
# str to int
a = int("10")      # 10
# float to int (truncates decimal)
b = int(5.9)       # 5
# int to float
c = float(3)       # 3.0
# int to str
d = str(123)       # "123"
# list to set
e = set([1, 2, 2]) # {1, 2}

```

---

## 🔤 1. Unicode Strings (`str` in Python 3)

A **Unicode string** represents **text** — human-readable characters.

### ✅ Characteristics:

* Type: `str`
* Each character is a Unicode code point (e.g., `'a'`, `'ñ'`, `'你'`)
* Default string type in **Python 3**

### Example:

```python
s = "hello"
print(type(s))  # <class 'str'>
```

### Use case:

* Text processing
* User-visible strings
* Anything intended to be read or displayed

---

## 🧱 2. Byte Strings (`bytes`)

A **byte string** is a sequence of **bytes** — i.e., raw 8-bit values.

### ✅ Characteristics:

* Type: `bytes`
* Immutable
* Each element is an integer between 0 and 255
* Not meant for direct human readability

### Example:

```python
b = b"hello"
print(type(b))  # <class 'bytes'>
```

### Use case:

* File reading in binary mode
* Networking
* Encryption or compression
* Encoding/decoding data

---

## 🔁 3. Encoding and Decoding

To convert between `str` and `bytes`, you use:

### 🔄 Encode (str → bytes):

```python
s = "café"
b = s.encode("utf-8")
print(b)  # b'caf\xc3\xa9'
```

### 🔄 Decode (bytes → str):

```python
s2 = b.decode("utf-8")
print(s2)  # 'café'
```

You **must specify an encoding** like `"utf-8"`, `"ascii"`, or `"latin1"` when converting.

---

## ⚠️ Key Differences Summary:

| Feature            | `str` (Unicode)           | `bytes` (Byte String)      |
| ------------------ | ------------------------- | -------------------------- |
| Meaning            | Human-readable characters | Raw binary data            |
| Type               | `str`                     | `bytes`                    |
| Default in Python3 | ✅ Yes                     | ❌ No                       |
| Mutable?           | No                        | No                         |
| Uses               | UI text, file content     | Network, files, encryption |
| Example            | `"hello"`                 | `b"hello"`                 |
| Operations         | Character-wise            | Byte-wise                  |

---

## 🧪 Common Errors

Trying to mix them directly:

```python
s = "hello"
b = b"world"
print(s + b)  # ❌ TypeError: can't concat str to bytes
```

**Fix**:

```python
print(s.encode() + b)  # works
```

---

## ✅ Best Practice:

* Keep **`str` for all internal text processing**.
* Use `bytes` **only** at the input/output boundary (e.g., reading files, APIs).
* Always **encode/decode explicitly** when crossing that boundary.
