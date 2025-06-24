# 🧪 Exception Handling: Interview-Style Questions & Exercises

---

## ✅ Beginner Level

### 🔹 Q1. Handle Division by Zero

**Task:** Write a function that takes two numbers and divides them, handling division by zero.

```python
def safe_divide(a, b):
    # Your code here
    pass

print(safe_divide(10, 2))   # Output: 5.0
print(safe_divide(10, 0))   # Output: "Cannot divide by zero"
```

---

### 🔹 Q2. Handle Invalid Input

**Task:** Ask user for an integer and print its square. Handle invalid input (non-numeric).

```python
def input_and_square():
    # Your code here
    pass

# Example: input → "abc" → Output: "Invalid input"
```

---

### 🔹 Q3. Read a File

**Task:** Write a function that reads a file. If it doesn’t exist, return `"File not found"`.

```python
def read_file(filename):
    # Your code here
    pass

print(read_file("sample.txt"))
```

---

## ✅ Intermediate Level

### 🔹 Q4. Validate Age with Custom Exception

**Task:** Raise a custom exception if the user enters a negative age.

```python
class NegativeAgeError(Exception):
    pass

def set_age(age):
    # Raise exception if age < 0
    pass

# Test case:
# set_age(-1) → Raises NegativeAgeError
```

---

### 🔹 Q5. Catch Multiple Exceptions

**Task:** Given a function, catch and identify both `TypeError` and `ZeroDivisionError`.

```python
def risky(a, b):
    return a / b

try:
    print(risky("5", 0))
except TypeError:
    print("Caught TypeError")
except ZeroDivisionError:
    print("Caught ZeroDivisionError")
```

---

### 🔹 Q6. Use `else` and `finally`

**Task:** Simulate opening and reading a file using `try-except-else-finally`.

```python
def read_and_log():
    # Use try, else and finally
    pass

# Output:
# - File read successfully.
# - File closed (even if not found).
```

---

## ✅ Advanced Level

### 🔹 Q7. Raise Custom Salary Exception

**Task:** Create a `LowSalaryError` and raise it if salary < 3000.

```python
class LowSalaryError(Exception):
    def __init__(self, salary):
        super().__init__(f"Salary {salary} is too low!")

def process_salary(salary):
    # Raise LowSalaryError if needed
    pass

# Test:
# process_salary(2500) → Raises LowSalaryError
```

---

### 🔹 Q8. Nested Exception Blocks

**Task:** Handle nested try-except blocks for two operations: converting a string to int and dividing.

```python
def process(x, y):
    try:
        a = int(x)
        try:
            return a / y
        except ZeroDivisionError:
            return "Division by zero"
    except ValueError:
        return "Invalid number"

print(process("10", 2))    # 5.0
print(process("abc", 2))   # Invalid number
print(process("10", 0))    # Division by zero
```

---

### 🔹 Q9. Iterator StopIteration Handling

**Task:** Iterate manually and handle `StopIteration` gracefully.

```python
def iterate_list(lst):
    it = iter(lst)
    while True:
        try:
            print(next(it))
        except StopIteration:
            print("Done iterating.")
            break
```

---

### 🔹 Q10. Login Exception System

**Task:** Raise exceptions for:

* `UserNotFoundError`
* `IncorrectPasswordError`

```python
class UserNotFoundError(Exception): pass
class IncorrectPasswordError(Exception): pass

users = {"alice": "123"}

def login(username, password):
    # Your code here
    pass

# Test:
# login("bob", "123") → UserNotFoundError
# login("alice", "wrong") → IncorrectPasswordError
# login("alice", "123") → "Login successful"
```

---

## 🧠 Bonus: Debug the Bug

### 🔹 Q11. What's wrong with this code?

```python
try:
    num = int(input("Enter number: "))
    print("Result:", 100 / num)
except:
    print("Something went wrong")
finally
    print("Done")
```

🟡 Identify and fix all issues.

---

