# Decorators in Python
Decorators in Python are a **very powerful and expressive tool** that allows you to modify or enhance the behavior of functions or classes without changing their source code. They're commonly used for **logging, access control, caching, measuring performance, and more**.

---

## 📌 What is a Decorator?

A **decorator is a function** that takes another function as an argument, **adds some functionality**, and **returns a new function**.

This is possible because in Python:

* Functions are **first-class objects**.
* You can **pass functions as arguments**, **return them from other functions**, and **assign them to variables**.

---

## 🔧 Basic Syntax

```python
def my_decorator(func):
    def wrapper():
        print("Before the function runs")
        func()
        print("After the function runs")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
```

### Output:

```
Before the function runs
Hello!
After the function runs
```

Using `@my_decorator` is equivalent to:

```python
say_hello = my_decorator(say_hello)
```

---

## ⚙️ Decorators with Arguments

If your function takes arguments, the wrapper must accept them too.

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Arguments passed:", args, kwargs)
        return func(*args, **kwargs)
    return wrapper

@my_decorator
def greet(name):
    print(f"Hello, {name}")

greet("Alice")
```

---

## 🏗️ Writing Decorators with `functools.wraps`

When you decorate a function, it loses its original name and docstring unless you use `functools.wraps`.

```python
import functools

def my_decorator(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        print("Calling", func.__name__)
        return func(*args, **kwargs)
    return wrapper
```

---

## 🧠 Decorators with Parameters (Decorator Factory)

To pass arguments to a decorator itself, you must add one more level of function nesting.

```python
def repeat(n):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(n):
                func(*args, **kwargs)
        return wrapper
    return decorator

@repeat(3)
def greet(name):
    print(f"Hello, {name}")

greet("Bob")
```

---

## 💡 Common Use Cases

### ✅ Logging

```python
def logger(func):
    def wrapper(*args, **kwargs):
        print(f"Function {func.__name__} called with {args} {kwargs}")
        return func(*args, **kwargs)
    return wrapper
```

### ✅ Timing

```python
import time

def timer(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} took {end - start:.4f}s")
        return result
    return wrapper
```

### ✅ Access Control

```python
def requires_admin(func):
    def wrapper(user, *args, **kwargs):
        if not user.is_admin:
            raise Exception("Not authorized!")
        return func(user, *args, **kwargs)
    return wrapper
```

---

## 🔁 Stacking Multiple Decorators

They are applied **bottom-up** (the closest to the function runs first).

```python
@decorator1
@decorator2
def my_function():
    pass
```

Is equivalent to:

```python
my_function = decorator1(decorator2(my_function))
```

---

## 🧪 Class-Based Decorators

You can also create decorators using classes by defining `__call__`.

```python
class MyDecorator:
    def __init__(self, func):
        self.func = func
    
    def __call__(self, *args, **kwargs):
        print("Before call")
        result = self.func(*args, **kwargs)
        print("After call")
        return result

@MyDecorator
def say_hello():
    print("Hello!")
```

---

## 🔄 Real-World Example: Memoization

```python
def memoize(func):
    cache = {}
    def wrapper(n):
        if n not in cache:
            cache[n] = func(n)
        return cache[n]
    return wrapper

@memoize
def fib(n):
    if n < 2:
        return n
    return fib(n-1) + fib(n-2)
```

---

## 🧵 Summary

| Concept           | Explanation                                                           |
| ----------------- | --------------------------------------------------------------------- |
| Decorator         | Function that takes another function and adds functionality           |
| `@decorator`      | Shortcut for `function = decorator(function)`                         |
| `functools.wraps` | Preserves metadata of original function                               |
| Use cases         | Logging, timing, memoization, validation, permissions                 |
| Types             | Function decorators, parameterized decorators, class-based decorators |

---

# Types of Decorators

---

## 🔹 1. Function Decorators

A **function decorator** takes a function as input, adds or modifies its behavior, and returns a new function.

### ✅ Example: Logging Decorator

```python
def log_decorator(func):
    def wrapper(*args, **kwargs):
        print(f"Function {func.__name__} called with arguments {args}, {kwargs}")
        return func(*args, **kwargs)
    return wrapper

@log_decorator
def add(x, y):
    return x + y

print(add(3, 4))
```

### ✅ Output

```
Function add called with arguments (3, 4), {}
7
```

🧠 **Key Idea**: This wraps a function and logs before calling the original logic.

---

## 🔹 2. Method Decorators (Inside Classes)

A **method decorator** behaves just like a function decorator but is applied to **methods inside classes**. The only difference is: methods receive `self` (or `cls` in classmethods) as the first argument.

---

### ✅ Example: Timing a Method

```python
import time

def time_it(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} took {end - start:.4f} seconds")
        return result
    return wrapper

class Math:
    @time_it
    def factorial(self, n):
        if n == 0:
            return 1
        return n * self.factorial(n - 1)

m = Math()
print(m.factorial(5))
```

### ✅ Output

```
factorial took 0.0001 seconds
120
```

---

### 🔸 Decorators for `@classmethod` and `@staticmethod`

```python
class MyClass:
    @staticmethod
    @log_decorator
    def say_hello(name):
        print(f"Hello {name}")

    @classmethod
    @log_decorator
    def show_class(cls):
        print(f"Class name is {cls.__name__}")
```

💡 You can combine decorators, but decorator order matters!

---

## 🔹 3. Class Decorators

A **class decorator** takes a class as input, modifies or enhances it, and returns a modified version.

---

### ✅ Example: Register Class Automatically

Suppose we want to auto-register all plugin classes.

```python
registry = {}

def register(cls):
    registry[cls.__name__] = cls
    return cls

@register
class PluginA:
    pass

@register
class PluginB:
    pass

print(registry)
```

### ✅ Output

```python
{'PluginA': <class '__main__.PluginA'>, 'PluginB': <class '__main__.PluginB'>}
```

---

### ✅ Example: Adding a Method to Class Dynamically

```python
def add_greet_method(cls):
    def greet(self):
        return f"Hello from {self.__class__.__name__}"
    cls.greet = greet
    return cls

@add_greet_method
class Person:
    def __init__(self, name):
        self.name = name

p = Person("Alice")
print(p.greet())  # Hello from Person
```

---

### ✅ Class Decorator Using `__call__` (Advanced)

You can create a **class-based decorator** by defining `__call__`.

```python
class Decorator:
    def __init__(self, func):
        self.func = func

    def __call__(self, *args, **kwargs):
        print("Decorator before call")
        return self.func(*args, **kwargs)

@Decorator
def greet():
    print("Hello")

greet()
```

---

## 🔚 Summary Table

| Decorator Type     | Target              | Input Type               | Use Case                                     |
| ------------------ | ------------------- | ------------------------ | -------------------------------------------- |
| Function Decorator | Standalone function | `function`               | Logging, validation, memoization             |
| Method Decorator   | Class method        | `method (with self/cls)` | Auth checks, timing, logging                 |
| Class Decorator    | Whole class         | `class`                  | Register class, add methods, inject behavior |

---
# Nested decorators and chaining (multiple) decorators

These concepts are key to advanced decorator usage and are often seen in frameworks like Flask, Django, or FastAPI.

---

## ✅ 1. **What Are Nested and Chained Decorators?**

### ✅ Nested Decorators:

* A **decorator inside another decorator**.
* One decorator wraps another **before** it decorates the target function.
* Useful for building **configurable or layered decorators**.

### ✅ Chaining Decorators:

* Applying **multiple decorators** to the **same function or method**.
* They are executed **from bottom to top** (the closest to the function applies first).

---

## 🔁 2. Chaining (Multiple) Decorators – Explained

### 🔹 Syntax:

```python
@decorator1
@decorator2
def my_func():
    pass
```

This is equivalent to:

```python
my_func = decorator1(decorator2(my_func))
```

So, `decorator2` is applied first, and its result is passed to `decorator1`.

---

### ✅ Example: Logging + Timing

```python
import time
import functools

def log_decorator(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        print(f"[LOG] Calling {func.__name__} with args={args}, kwargs={kwargs}")
        return func(*args, **kwargs)
    return wrapper

def time_decorator(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"[TIME] {func.__name__} executed in {end - start:.4f} seconds")
        return result
    return wrapper

@log_decorator
@time_decorator
def compute(x):
    time.sleep(0.5)
    return x ** 2

print(compute(4))
```

### ✅ Output:

```
[LOG] Calling compute with args=(4,), kwargs={}
[TIME] compute executed in 0.5001 seconds
16
```

> ✅ `time_decorator` runs **first**, then `log_decorator` wraps the result.

---

## 🔁 3. Nested Decorators (Decorator Inside Decorator)

This is when a **decorator is defined inside another function**, usually to allow passing arguments to the decorator.

---

### ✅ Example: Nested Logging Based on Level

```python
def log(level):  # Outer function
    def decorator(func):  # Actual decorator
        def wrapper(*args, **kwargs):
            print(f"[{level}] {func.__name__} called")
            return func(*args, **kwargs)
        return wrapper
    return decorator

@log("DEBUG")
def say_hello():
    print("Hello!")

say_hello()
```

### ✅ Output:

```
[DEBUG] say_hello called
Hello!
```

> ✅ Here, `log("DEBUG")` returns `decorator`, which is then used to decorate `say_hello`.

---

### ✅ Real-World Example: Role-Based Access

```python
def requires_role(role):
    def decorator(func):
        def wrapper(user, *args, **kwargs):
            if user.get("role") != role:
                raise PermissionError("Access Denied")
            return func(user, *args, **kwargs)
        return wrapper
    return decorator

@requires_role("admin")
def delete_post(user, post_id):
    print(f"Post {post_id} deleted by {user['name']}")

user = {"name": "Alice", "role": "admin"}
delete_post(user, 42)  # Works

user = {"name": "Bob", "role": "guest"}
delete_post(user, 42)  # Raises PermissionError
```

---

## 🔗 4. Combining Nested + Chained Decorators

You can use both together:

```python
def tag(name):
    def decorator(func):
        def wrapper(*args, **kwargs):
            print(f"[{name}] Start")
            result = func(*args, **kwargs)
            print(f"[{name}] End")
            return result
        return wrapper
    return decorator

def timer(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"Time taken: {end - start:.4f}s")
        return result
    return wrapper

@tag("outer")
@timer
@tag("inner")
def process():
    print("Processing...")

process()
```

### ✅ Output:

```
[outer] Start
[inner] Start
Processing...
[inner] End
Time taken: 0.0000s
[outer] End
```

---

## 🧠 Summary

| Concept              | Description                                                                              |
| -------------------- | ---------------------------------------------------------------------------------------- |
| **Chaining**         | Applying multiple decorators on a single function. Bottom-up execution.                  |
| **Nested Decorator** | A decorator inside a function, usually used to pass arguments or for logic layering.     |
| **Order Matters**    | The decorator closest to the function runs first. Each wraps the result of the previous. |
| **Use Cases**        | Logging, timing, access control, input validation, error handling, caching.              |

---
# Commonly used built-in decorators:

* `@staticmethod`
* `@classmethod`
* `@property`

Each of these decorators is used **within classes** and modifies how a method or attribute behaves.

---

## ✅ 1. `@staticmethod`

### 🔹 What it does:

* Declares a method that **does not receive `self` or `cls`**.
* Behaves like a **normal function** but is **called using the class or instance**.
* It **cannot modify class or instance state**.

### 🔹 Use case:

Utility/helper methods that logically belong to the class but **don’t access or modify** the class or instance.

---

### ✅ Example:

```python
class MathUtils:
    @staticmethod
    def add(x, y):
        return x + y

# Can be called using class or instance
print(MathUtils.add(2, 3))       # 5
m = MathUtils()
print(m.add(4, 5))               # 9
```

> ✅ No `self` or `cls` is passed automatically. It's purely functional.

---

## ✅ 2. `@classmethod`

### 🔹 What it does:

* Declares a method that **receives the class (`cls`) as the first argument**.
* Can **access and modify class-level variables or create new instances**.

### 🔹 Use case:

* **Factory methods** that create instances using alternate constructors.
* **Modifying class variables**.

---

### ✅ Example:

```python
class Person:
    count = 0

    def __init__(self, name):
        self.name = name
        Person.count += 1

    @classmethod
    def get_count(cls):
        return cls.count

p1 = Person("Alice")
p2 = Person("Bob")
print(Person.get_count())  # 2
```

> ✅ `cls` refers to the class, so `cls.count` is the same as `Person.count`.

---

### ✅ Example: Alternate Constructor

```python
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author

    @classmethod
    def from_string(cls, book_str):
        title, author = book_str.split("-")
        return cls(title.strip(), author.strip())

b = Book.from_string("The Alchemist - Paulo Coelho")
print(b.title, b.author)
```

---

## ✅ 3. `@property`

### 🔹 What it does:

* Turns a **method into a read-only attribute**.
* Allows **getter, setter, and deleter** for attribute access while **preserving encapsulation**.
* Useful to **compute a value dynamically** while exposing it as an attribute.

---

### ✅ Simple Getter Example:

```python
class Circle:
    def __init__(self, radius):
        self._radius = radius

    @property
    def area(self):
        return 3.14 * self._radius ** 2

c = Circle(5)
print(c.area)  # 78.5 (no parentheses)
```

> ✅ `@property` allows calling a method **without parentheses** like an attribute.

---

### ✅ Full Example with Getter, Setter, Deleter:

```python
class Product:
    def __init__(self, price):
        self._price = price

    @property
    def price(self):
        print("Getting price")
        return self._price

    @price.setter
    def price(self, value):
        if value < 0:
            raise ValueError("Price cannot be negative")
        print("Setting price")
        self._price = value

    @price.deleter
    def price(self):
        print("Deleting price")
        del self._price

p = Product(100)
print(p.price)     # Getting price => 100
p.price = 150      # Setting price
del p.price        # Deleting price
```

---

## 🧠 Comparison Summary Table

| Decorator       | First Arg | Used for                         | Access to `self`/`cls` | Modifies?      |
| --------------- | --------- | -------------------------------- | ---------------------- | -------------- |
| `@staticmethod` | —         | Utility methods, pure functions  | ❌                      | No access      |
| `@classmethod`  | `cls`     | Factory methods, class-level ops | ✅ `cls`                | Class-level    |
| `@property`     | `self`    | Getter/setter-like access        | ✅ `self`               | Instance-level |




