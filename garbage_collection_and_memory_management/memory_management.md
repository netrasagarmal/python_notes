## Memory Management in Python

## 📦 1. **Memory Management in Python**

Python manages memory automatically using a **combination of techniques**:

### ✅ Key Concepts:

- **Reference Counting**
- **Garbage Collection (GC)**
- **Heap Allocation**
- **Object-specific memory pools**

---

### 🧮 A. **Reference Counting**

- Every object in Python maintains a **reference count** — the number of references pointing to it.
- When the reference count drops to **zero**, Python automatically frees the memory.

```python
import sys

a = [1, 2, 3]
b = a
print(sys.getrefcount(a))  # e.g., 3 (includes temporary ref from getrefcount)

```

- If you `del a` and `del b`, the object is no longer referenced and can be deleted.

---

### 🧹 B. **Garbage Collection (GC)**

Python uses a **cyclic garbage collector** in addition to reference counting to detect and clean up **reference cycles**.

### 📌 What is a reference cycle?

When two or more objects reference each other, but are no longer used in the program.

```python
class A:
    def __init__(self):
        self.b = None

class B:
    def __init__(self):
        self.a = None

a = A()
b = B()
a.b = b
b.a = a

```

- Even after `a` and `b` go out of scope, the objects might not be deleted **unless** the **garbage collector** detects the cycle.

### 🔧 Forcing GC:

```python
import gc
gc.collect()  # Manually trigger garbage collection

```

---

## 🧭 2. **Shallow Copy vs Deep Copy**

Python provides ways to **copy objects**, but it’s crucial to know how the object is copied:

### ✅ A. Shallow Copy

- Creates a **new outer object**, but **references the same inner objects**.
- Changes to **mutable nested objects** affect both copies.

```python
import copy

original = [[1, 2], [3, 4]]
shallow = copy.copy(original)

shallow[0][0] = 99
print(original)  # [[99, 2], [3, 4]] → inner object modified

```

---

### ✅ B. Deep Copy

- Creates a **completely independent copy**, including all nested objects.
- Changes to deep-copied object **do not affect** the original.

```python
deep = copy.deepcopy(original)

deep[0][0] = 42
print(original)  # Unchanged

```

---

### ⚖️ Comparison Table:

| Feature | Shallow Copy | Deep Copy |
| --- | --- | --- |
| Method | `copy.copy(obj)` | `copy.deepcopy(obj)` |
| Outer object | New copy | New copy |
| Inner objects | References (shared) | Copied (independent) |
| Performance | Faster | Slower |
| Use Case | When nested objects don't change | When complete independence needed |

---

## 🧠 Summary:

### 🔹 Memory Management:

- **Reference Counting**: Tracks number of references to an object.
- **Garbage Collector**: Handles unreachable cyclic references.
- **Manual GC**: `gc.collect()`.

### 🔹 Object Copying:

- **Shallow Copy**: One level copy — inner objects are shared.
- **Deep Copy**: Fully independent copy of entire object graph.

---

Would you like a visual diagram showing how shallow and deep copies differ in memory references?