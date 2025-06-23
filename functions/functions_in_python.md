## 📘 1. Functions in Python

Functions are reusable blocks of code that perform a specific task. They help in:

- **Code reusability**
- **Modularity**
- **Cleaner and maintainable code**

### 🔹 Syntax:

```python
def greet(name):
    return f"Hello, {name}!"
print(greet("Alice"))  # Output: Hello, Alice!

```

## 📘 2. Function Arguments

### 🔹 a) **Positional Arguments**

- Passed in order.

```python
def add(a, b):
    return a + b

print(add(2, 3))  # Output: 5

```

### 🔹 b) **Keyword Arguments**

- Specify parameter names explicitly.

```python
def greet(name, msg):
    print(f"{msg}, {name}!")

greet(name="Alice", msg="Hi")  # Output: Hi, Alice!

```

### 🔹 c) **Default Arguments**

- Provide a default value if not passed.

```python
def greet(name, msg="Hello"):
    print(f"{msg}, {name}!")

greet("Bob")  # Output: Hello, Bob!

```

### 🔹 d) `args` – Variable-Length Positional Arguments

- Collects extra positional arguments as a **tuple**.

```python
def sum_all(*args):
    return sum(args)

print(sum_all(1, 2, 3, 4))  # Output: 10

```

### 🔹 e) `*kwargs` – Variable-Length Keyword Arguments

- Collects extra keyword arguments as a **dictionary**.

```python
def show_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key} = {value}")

show_info(name="Alice", age=30)
# Output:
# name = Alice
# age = 3
```

```python
def example_function(*args, **kwargs):
    print("Args:")
    for arg in args:
        print(arg)

    print("\nKwargs:")
    for key, value in kwargs.items():
        print(f"{key}: {value}")

# Calling the function with different arguments
example_function(1, 2, 3, name="Alice", age=30)
```

## 📘 1. First-Class Functions

### ✅ Definition:

Python treats **functions as first-class citizens**, meaning:

- Functions can be **passed as arguments** to other functions
- Functions can be **returned from other functions**
- Functions can be **assigned to variables**
- Functions can be **stored in data structures**

This allows **functional programming** patterns in Python.

### ✅ Example:

```python
def greet(name):
    return f"Hello, {name}"

# Assign to variable
say_hello = greet
print(say_hello("Alice"))  # Hello, Alice

# Pass function as argument
def call_func(func, value):
    return func(value)

print(call_func(greet, "Bob"))  # Hello, Bob

# Return a function
def outer():
    def inner():
        return "Inner function called"
    return inner

f = outer()
print(f())  # Inner function called

```

## 📘 2. Closures

### ✅ Definition:

A **closure** is a function that **remembers the variables from its enclosing lexical scope**, even if the outer function has finished executing.

Closures enable **data hiding and encapsulation** in Python.

### ✅ Structure:

- An outer function defines a local variable
- An inner function uses that variable
- The outer function returns the inner function

### ✅ Example:

```python
def outer(msg):
    def inner():
        print(f"Message: {msg}")  # msg is remembered!
    return inner

closure_fn = outer("Hi there!")
closure_fn()  # Output: Message: Hi there!

```

Even after `outer()` has finished, `inner()` retains access to `msg`.