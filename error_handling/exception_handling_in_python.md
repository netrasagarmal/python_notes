# ✅ Exception Handling in Python

## 🔹 What is an Exception?

An **exception** is an error that **interrupts the normal flow** of a program during execution.

Example:

```python
a = 5 / 0  # Raises ZeroDivisionError
```

If not handled, Python **stops execution** and shows a traceback.

---

## ✅ Why Handle Exceptions?

To:

* **Prevent crashes**
* **Provide meaningful error messages**
* **Gracefully recover** from unexpected events

---

## ✅ Basic Syntax

```python
try:
    # Code that might raise an exception
except ExceptionType:
    # Code to handle the exception
```

---

### ✅ Full Structure with `else` and `finally`

```python
try:
    # Risky code
except SomeError:
    # Handle error
else:
    # Executes if no error occurs
finally:
    # Always runs (cleanup code)
```

---

## 🔹 Example 1: Simple `try-except`

```python
try:
    x = int(input("Enter a number: "))
    print(10 / x)
except ZeroDivisionError:
    print("You cannot divide by zero.")
except ValueError:
    print("Invalid input. Please enter a number.")
```

---

## 🔹 Example 2: Using `else` and `finally`

```python
try:
    f = open("example.txt", "r")
    data = f.read()
except FileNotFoundError:
    print("File not found.")
else:
    print("File read successfully.")
finally:
    print("Execution finished.")
```

---

## ✅ Catching Multiple Exceptions Together

```python
try:
    result = int("abc") / 0
except (ValueError, ZeroDivisionError) as e:
    print("Caught an exception:", e)
```

---

## ✅ Raising Your Own Exception

```python
def set_age(age):
    if age < 0:
        raise ValueError("Age cannot be negative")
    print("Age set to", age)

set_age(-5)  # Raises ValueError
```

---

## ✅ Custom Exceptions (User-defined)

```python
class CustomError(Exception):
    pass

def risky_operation():
    raise CustomError("Something went wrong")

try:
    risky_operation()
except CustomError as e:
    print("Caught:", e)
```

---

# 🚨 Common Exception Types in Python

| Exception Type      | Description                                  | Example                          |
| ------------------- | -------------------------------------------- | -------------------------------- |
| `ZeroDivisionError` | Division or modulo by zero                   | `10 / 0`                         |
| `ValueError`        | Invalid value passed to a function           | `int("abc")`                     |
| `TypeError`         | Invalid operation between incompatible types | `1 + '2'`                        |
| `IndexError`        | Index out of bounds in a list                | `lst[10]`                        |
| `KeyError`          | Accessing missing dictionary key             | `dict['x']` when x not in dict   |
| `AttributeError`    | Object doesn't have the accessed attribute   | `'str'.fake_method()`            |
| `FileNotFoundError` | File or directory not found                  | `open("nofile.txt")`             |
| `NameError`         | Variable or name not defined                 | `print(x)` when `x` is undefined |
| `ImportError`       | Module can't be imported                     | `import non_existing_module`     |
| `StopIteration`     | Raised when no more elements in an iterator  | `next(iter([]))`                 |
| `RuntimeError`      | Unspecified errors at runtime                | General runtime failure          |
| `IndentationError`  | Incorrect indentation in code                | Misaligned code block            |
| `SyntaxError`       | Code syntax is incorrect                     | `print "hello"` (Python 3)       |
| `MemoryError`       | Operation runs out of memory                 | Extremely large data allocation  |
| `AssertionError`    | Raised by `assert` statement failure         | `assert 2 + 2 == 5`              |

---

## ✅ Best Practice: Catch Specific Exceptions First

```python
try:
    # risky code
except ValueError:
    # handle ValueError
except Exception:
    # catch any other
```

---

## 🧠 Tips for Exception Handling

| Tip                                       | Why it matters                        |
| ----------------------------------------- | ------------------------------------- |
| Use specific exceptions                   | Avoids catching unintended errors     |
| Use `finally` for cleanup                 | Ensures file/network/database cleanup |
| Don’t silently ignore (`except: pass`)    | Hides bugs                            |
| Raise custom exceptions for domain errors | Improves readability and control      |

---

## ✅ Real-World Example: Safe Division

```python
def safe_divide(a, b):
    try:
        return a / b
    except ZeroDivisionError:
        return "Cannot divide by zero"

print(safe_divide(10, 2))  # 5.0
print(safe_divide(5, 0))   # Cannot divide by zero
```

---

## ✅ Summary

| Keyword   | Purpose                               |
| --------- | ------------------------------------- |
| `try`     | Block of code to test for errors      |
| `except`  | Handles the error                     |
| `else`    | Runs if no exception was raised       |
| `finally` | Always runs (use for cleanup)         |
| `raise`   | Used to raise an exception explicitly |

---

# ✅ What Are Custom Exceptions?

Custom exceptions are **user-defined error types** that allow you to:

* Represent **domain-specific or application-specific errors**
* Improve **code readability**
* Enable **fine-grained exception handling**

They are created by **subclassing** the built-in `Exception` class (or one of its subclasses).

---

## 🧱 Why Use Custom Exceptions?

### 🔹 Problems with generic exceptions:

```python
raise Exception("Invalid user input")
```

* Doesn't clearly describe the error type.
* Harder to catch specific errors.
* Violates principle of clear code design.

### ✅ Better:

```python
raise InvalidUserInput("Email format is wrong")
```

* Clear error semantics.
* Enables targeted `except InvalidUserInput`.

---

## ✅ How to Define a Custom Exception

### 🔹 Basic Syntax:

```python
class MyCustomError(Exception):
    pass
```

This creates a new exception type `MyCustomError` that behaves like a regular exception.

---

### ✅ Example 1: Basic Custom Exception

```python
class NegativeAgeError(Exception):
    """Raised when age is negative"""
    pass

def set_age(age):
    if age < 0:
        raise NegativeAgeError("Age cannot be negative")
    print("Age set to:", age)

try:
    set_age(-5)
except NegativeAgeError as e:
    print("Error:", e)
```

---

### ✅ Output:

```
Error: Age cannot be negative
```

---

## ✅ Custom Exception with `__init__` and `__str__`

```python
class SalaryTooLowError(Exception):
    def __init__(self, salary, message="Salary below threshold"):
        self.salary = salary
        self.message = message
        super().__init__(self.message)

    def __str__(self):
        return f"{self.message}: {self.salary}"
```

### ✅ Example 2: Usage

```python
def check_salary(salary):
    if salary < 3000:
        raise SalaryTooLowError(salary)
    print("Salary accepted.")

try:
    check_salary(2500)
except SalaryTooLowError as e:
    print(e)
```

### ✅ Output:

```
Salary below threshold: 2500
```

---

## ✅ Inheriting from Other Exception Types

You can subclass other types like `ValueError`, `IOError`, etc.

```python
class InvalidEmailError(ValueError):
    pass
```

This helps integrate your custom exceptions into existing exception hierarchies.

---

## ✅ Catching Custom Exceptions

You can catch them specifically:

```python
try:
    # something risky
except InvalidEmailError:
    print("Please enter a valid email.")
```

Or handle multiple:

```python
try:
    # ...
except (InvalidEmailError, PasswordTooShortError) as e:
    print(e)
```

---

## ✅ Real-World Example: Login System

```python
class LoginError(Exception): pass
class UserNotFound(LoginError): pass
class InvalidPassword(LoginError): pass

def login(username, password):
    users = {"alice": "pass123"}
    if username not in users:
        raise UserNotFound("User not found.")
    if users[username] != password:
        raise InvalidPassword("Password is incorrect.")
    return "Login successful"

try:
    print(login("bob", "1234"))
except UserNotFound as e:
    print("Login failed:", e)
except InvalidPassword as e:
    print("Login failed:", e)
```

---

## ✅ Best Practices for Custom Exceptions

| Rule                                           | Why                                            |
| ---------------------------------------------- | ---------------------------------------------- |
| Subclass `Exception`, not `BaseException`      | `BaseException` is for system-level exceptions |
| Name classes ending with `Error`               | Conveys intent clearly                         |
| Add docstrings/messages                        | Helps debugging                                |
| Use them to **model domain-specific problems** | Improves clarity and abstraction               |

---

## ✅ Summary

| Concept          | Description                                             |
| ---------------- | ------------------------------------------------------- |
| Custom Exception | User-defined error class                                |
| Inherits from    | `Exception` or its subclasses                           |
| Benefits         | Cleaner code, specific error handling, better debugging |
| Use Cases        | Domain errors, validation, workflow constraints         |

---

## ✅ Custom Exception Template

```python
class MyCustomError(Exception):
    """Custom error with message"""
    def __init__(self, message="Something went wrong"):
        self.message = message
        super().__init__(self.message)
```

---

## In-depth working of exception handling:

**Raise an Exception inside a `try` block** and **handle it in the `except` block**.

---

### ✅ Example:

```python
try:
    print("Trying to do something risky...")
    raise ValueError("Something went wrong!")  # Manually raise an exception
except ValueError as e:
    print(f"Caught an exception: {e}")
```

---

### 🔍 Output:

```
Trying to do something risky...
Caught an exception: Something went wrong!
```

---

### 🧠 Explanation:

* `raise ValueError("Something went wrong!")`: You **manually trigger** a `ValueError`.
* Python immediately jumps to the `except ValueError as e:` block.
* `e` holds the actual exception object (`ValueError("Something went wrong!")`), and you can print it or log it.

---

### ✅ Try It Yourself:

You can replace `ValueError` with other types of exceptions, like `TypeError`, `RuntimeError`, or even a **custom exception** like this:

```python
class MyCustomError(Exception):
    pass

try:
    raise MyCustomError("This is a custom error")
except MyCustomError as e:
    print(f"Caught custom error: {e}")
```

## Let’s walk through this line by line and understand **how the message** `"This is a custom error"` is printed — including how **exception classes** work in Python and what gets inherited under the hood.`

---

### ✅ Code:

```python
class MyCustomError(Exception):
    pass

try:
    raise MyCustomError("This is a custom error")
except MyCustomError as e:
    print(f"Caught custom error: {e}")
```

---

### 🔍 Output:

```
Caught custom error: This is a custom error
```

---

## ✅ STEP-BY-STEP EXECUTION

---

### 1. `class MyCustomError(Exception):`

* You are **defining a custom exception class**.
* It **inherits** from Python’s built-in `Exception` class.
* The `Exception` class is part of Python’s exception hierarchy and provides all the base functionality like holding a message and traceback.

---

### 2. `raise MyCustomError("This is a custom error")`

* This line **raises** an instance of `MyCustomError` with the message `"This is a custom error"`.

* Internally, this is like calling:

  ```python
  e = MyCustomError("This is a custom error")
  raise e
  ```

* Because `MyCustomError` inherits from `Exception`, it accepts a message in its constructor via `__init__` and stores it.

---

### 3. `except MyCustomError as e:`

* Python matches the raised exception type (`MyCustomError`) to this handler.
* The raised exception object is assigned to variable `e`.

---

### 4. `print(f"Caught custom error: {e}")`

* This prints the exception object.
* So what does `str(e)` do?

---

## 🔍 How `"This is a custom error"` gets printed

### Internally:

When you do:

```python
str(e)
```

You're calling:

```python
e.__str__()
```

Now since you **did not override `__str__` in `MyCustomError`**, Python uses the `__str__` method from the base class `Exception`.

### Python’s `Exception` class:

```python
class Exception(BaseException):
    def __init__(self, *args):
        self.args = args

    def __str__(self):
        if len(self.args) == 1:
            return str(self.args[0])
        return str(self.args)
```

So:

* `self.args` becomes `("This is a custom error",)`
* `str(self.args[0])` → `"This is a custom error"`
* Hence `print(e)` prints: `"This is a custom error"`

---

## ✅ Summary

| Part                             | What it does                                 |
| -------------------------------- | -------------------------------------------- |
| `class MyCustomError(Exception)` | Inherits base exception behavior             |
| `raise MyCustomError("...")`     | Creates and raises an exception instance     |
| `except MyCustomError as e`      | Catches the raised custom exception          |
| `print(e)` or `str(e)`           | Calls `Exception.__str__()`, returns message |

---
