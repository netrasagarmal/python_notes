## 🔁 1. **Method Overriding** (Supported in Python)

### ✅ Definition:

**Overriding** means **redefining a method in a subclass** that already exists in the parent class. It allows **runtime polymorphism** — the method that gets called is based on the **object type**, not the reference type.

### 🧪 Example: Method Overriding

```python
class Animal:
    def speak(self):
        print("Animal speaks")

class Dog(Animal):
    def speak(self):  # Overrides parent method
        print("Dog barks")

a = Animal()
d = Dog()

a.speak()  # Animal speaks
d.speak()  # Dog barks (overridden method)

```

> 🔹 The child class overrides the parent class method with its own implementation.
> 

## ➕ 2. **Method Overloading** (Not directly supported in Python)

### ✅ Definition:

**Overloading** refers to defining **multiple methods with the same name** but **different arguments** (by type or number). Common in languages like Java or C++.

### ❗ In Python:

Python **doesn't support traditional method overloading**. If you define the same method multiple times, only the **last definition is retained**.

### 🧪 Example: Not true overloading

```python
class Demo:
    def show(self, a=None):
        if a is not None:
            print(f"Argument: {a}")
        else:
            print("No argument")

d = Demo()
d.show()      # No argument
d.show(5)     # Argument: 5

```

> 🔹 You manually simulate overloading by using default arguments, *args, or **kwargs.
> 

## 🔍 Difference Table: Overriding vs Overloading

| Feature | **Overriding** | **Overloading (Python)** |
| --- | --- | --- |
| **Definition** | Redefining a method in a child class | Multiple methods with same name, different args |
| **Polymorphism** | Runtime polymorphism | Compile-time in other languages (simulated in Python) |
| **Inheritance** | Requires inheritance | Doesn't require inheritance |
| **Arguments** | Must match base method's signature | Varies (simulated via default/`*args`) |
| **Support in Python** | ✅ Yes | ❌ Not directly, simulated using tricks |
| **Use Case** | Modify parent behavior | Same method name for different use cases |

### ✅ Overriding Example in Practice:

```python
class Shape:
    def area(self):
        raise NotImplementedError

class Circle(Shape):
    def area(self):
        return 3.14 * 5 * 5  # Overrides base

print(Circle().area())  # 78.5

```

### ✅ Overloading Simulation in Python:

```python
class Calculator:
    def add(self, *args):
        return sum(args)

c = Calculator()
print(c.add(1, 2))         # 3
print(c.add(1, 2, 3, 4))   # 10

```

## 🎯 Summary

- **Overriding** is fully supported and a key part of OOP in Python.
- **Overloading** must be simulated using default parameters or `args/**kwargs` due to Python's dynamic typing.