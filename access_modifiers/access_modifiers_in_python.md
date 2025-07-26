## 🔐 What Are Access Modifiers?

Access modifiers **control access** to **class members (variables and methods)** from outside the class. Python doesn’t enforce strict access control like C++ or Java, but uses **naming conventions** to signal intent.

---

## 🧩 1. **Public Access Modifier**

### ✅ Definition:

- Public members are **accessible from anywhere** (inside or outside the class).
- **Default behavior** in Python.

### 🧪 Example:

```python
class MyClass:
    def __init__(self):
        self.name = "Public Variable"

    def show(self):
        print("Public Method")

obj = MyClass()
print(obj.name)  # ✅ Accessed from outside
obj.show()       # ✅ Called from outside

```

---

## 🔐 2. **Protected Access Modifier**

### ✅ Definition:

- Prefixed with a **single underscore** `_var`.
- Meant to be **used only within the class or its subclasses**.
- It’s still accessible from outside — this is a **convention**, not enforcement.

### 🧪 Example:

```python
class MyClass:
    def __init__(self):
        self._data = "Protected Variable"

    def _helper(self):
        print("Protected Method")

class SubClass(MyClass):
    def access_protected(self):
        print(self._data)      # ✅ Accessed in subclass
        self._helper()

obj = MyClass()
print(obj._data)  # ⚠️ Can be accessed (not recommended)
obj._helper()     # ⚠️ Can be called

```

---

## 🔒 3. **Private Access Modifier**

### ✅ Definition:

- Prefixed with **double underscore** `__var`.
- Python **name-mangles** private members to prevent access from outside (`_ClassName__var`).
- Enforces stronger encapsulation.

### 🧪 Example:

```python
class MyClass:
    def __init__(self):
        self.__secret = "Private Variable"

    def __hidden(self):
        print("Private Method")

    def reveal(self):
        self.__hidden()

obj = MyClass()
# print(obj.__secret)   ❌ AttributeError
# obj.__hidden()        ❌ AttributeError

# ✅ Access via name mangling (not recommended)
print(obj._MyClass__secret)
obj._MyClass__hidden()

```

---

## 📚 Summary Table:

| Access Modifier | Syntax | Accessible from outside? | Used in Subclasses? | Enforced? | Purpose |
| --- | --- | --- | --- | --- | --- |
| **Public** | `var` | ✅ Yes | ✅ Yes | No | General use |
| **Protected** | `_var` | ⚠️ Yes (by convention) | ✅ Yes | No | For internal/inherited use |
| **Private** | `__var` | ❌ No (name mangled) | ❌ Not directly | Yes | Enforce encapsulation |

---

## 🎯 Why Use Access Modifiers?

| Need | Benefit |
| --- | --- |
| **Encapsulation** | Hide internal data from external misuse |
| **Abstraction** | Expose only necessary details |
| **Maintainability** | Reduce dependency on internal implementation |
| **Inheritance Control** | Control what gets inherited or overridden |
| **Security & Robustness** | Prevent accidental modification of sensitive data |

---

## 🧠 Best Practices:

- Use `public` for all external APIs or interfaces.
- Use `_protected` for internal methods meant for inheritance but not public use.
- Use `__private` for sensitive logic/data you want to encapsulate tightly.