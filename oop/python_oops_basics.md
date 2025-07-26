## 📘 **Classes & Objects**

### ✅ Class:

A **class** is a blueprint for creating **objects**. It defines **attributes** (variables) and **methods** (functions) shared by all objects of that type.

```python
class Person:
    def speak(self):
        print("Hello, I am a person")

```

### ✅ Object:

An **object** is an **instance** of a class — it has real values assigned to the attributes and can use the methods.

```python
p1 = Person()  # Object creation
p1.speak()     # Output: Hello, I am a person

```

---

## ⚙️ `__init__`, `self`, instance vs class variables

### ✅ `__init__` Method:

- The **constructor** in Python
- Automatically called when a new object is created
- Used to initialize instance variables

```python
class Car:
    def __init__(self, brand):
        self.brand = brand  # instance variable

car1 = Car("Tesla")
print(car1.brand)  # Output: Tesla

```

---

### ✅ `self` Keyword:

- Refers to the **current object**
- Must be the **first parameter** of every instance method
- Used to access **attributes and methods** of the class

---

### ✅ Instance vs Class Variables:

| Feature | Instance Variable | Class Variable |
| --- | --- | --- |
| Defined in | `__init__` or methods with `self` | Inside class, outside methods |
| Scope | Specific to each object | Shared by all instances |
| Accessed via | `self.var` | `ClassName.var` or `self.var` |

```python
class Dog:
    species = "Canine"  # class variable

    def __init__(self, name):
        self.name = name  # instance variable

d1 = Dog("Max")
d2 = Dog("Buddy")

print(d1.name)       # Max
print(d2.name)       # Buddy
print(d1.species)    # Canine

```

## 🧱 OOP Pillars

### 🛡️ A. **Encapsulation**

- Binding data (variables) and methods into a single unit (class)
- **Hides internal state** and requires all interaction to go through methods

```python
class BankAccount:
    def __init__(self):
        self.__balance = 0  # private variable

    def deposit(self, amount):
        self.__balance += amount

    def get_balance(self):
        return self.__balance

acc = BankAccount()
acc.deposit(100)
print(acc.get_balance())  # 100

```

🔒 `__balance` is private (not directly accessible from outside).

### 🧩 B. **Abstraction**

- Hiding **complex implementation** and showing only the **essential features**
- Achieved using **abstract base classes (ABC)** or **method hiding**

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Circle(Shape):
    def __init__(self, r):
        self.r = r

    def area(self):
        return 3.14 * self.r * self.r

c = Circle(3)
print(c.area())  # 28.26

```

### 👪 C. **Inheritance**

- Allows a class (**child**) to inherit attributes and methods from another class (**parent**)
- Promotes **code reuse**

```python
class Animal:
    def speak(self):
        print("Animal speaks")

class Dog(Animal):
    def bark(self):
        print("Dog barks")

d = Dog()
d.speak()  # Inherited method
d.bark()   # Child method

```

### ✅ **Benefits of Inheritance in Python (and OOP in general)**

Inheritance is a core concept in object-oriented programming that allows a **child class to reuse the code from a parent class**. It promotes **code reusability**, **extensibility**, and **clean architecture**.

## 🎯 **Key Benefits of Inheritance**

### 1. ✅ **Code Reusability**

- You don’t need to rewrite code that is already present in the parent class.
- Common functionality can be abstracted to a base class.

```python
class Animal:
    def breathe(self):
        print("Breathing...")

class Dog(Animal):
    pass

d = Dog()
d.breathe()  # Inherited from Animal

```

### 2. ✅ **Extensibility**

- You can extend the functionality of an existing class without modifying it.
- Child classes can override or add new behavior.

```python
class Animal:
    def sound(self):
        print("Some sound")

class Cat(Animal):
    def sound(self):
        print("Meow")  # Overrides parent

Cat().sound()  # Meow

```

### 3. ✅ **Maintainability**

- Changes in the base class automatically propagate to all derived classes.
- Makes code easier to manage and refactor.

### 4. ✅ **Polymorphism**

- You can treat different subclasses as instances of the base class, enabling flexible and dynamic behavior at runtime.

```python
def animal_sound(animal):
    animal.sound()

animal_sound(Cat())  # Meow
animal_sound(Dog())  # Bark

```

### 5. ✅ **Hierarchical Organization**

- Logical grouping of common behaviors promotes a clean architecture (e.g., `Vehicle` → `Car`, `Bike`).

### 6. ✅ **DRY Principle (Don't Repeat Yourself)**

- Avoid duplicating code across multiple classes by putting shared behavior in a base class.

## ⚠️ When Not to Use Inheritance

- Overusing inheritance can lead to tight coupling.
- Consider **composition over inheritance** when you just need functionality reuse without hierarchical relationships.

### 🔀 D. **Polymorphism**

- Same method name behaves differently in **different classes**
- Achieved via **method overriding**

```python
class Bird:
    def sound(self):
        print("Chirp")

class Dog:
    def sound(self):
        print("Bark")

def make_sound(animal):
    animal.sound()

make_sound(Bird())  # Chirp
make_sound(Dog())   # Bark

```

✔️ Function `make_sound()` works for different types — this is **polymorphism**.

## ✅ Summary Table

| Concept | Description | Example Keyword/Mechanism |
| --- | --- | --- |
| Class & Object | Blueprint and its instance | `class`, instantiation |
| `__init__`, `self` | Constructor and object reference | `__init__`, `self` |
| Encapsulation | Restrict access to internal state | Private vars, getters/setters |
| Abstraction | Hiding internal complexity | `ABC`, `@abstractmethod` |
| Inheritance | Derive class from another | `class Child(Parent)` |
| Polymorphism | One interface, multiple behaviors | Method overriding |

## 🔹 Special / Dunder Methods (a.k.a. Magic Methods)

Dunder (double underscore) methods are **special methods** that Python uses to perform built-in operations (like printing, comparing, or adding objects).

These methods **begin and end** with double underscores, e.g., `__init__`, `__str__`, etc.

### ✅ Common Dunder Methods:

| Method | Purpose | Example Usage |
| --- | --- | --- |
| `__init__` | Constructor | `obj = MyClass()` |
| `__str__` | Readable string for users | `print(obj)` |
| `__repr__` | Official string for developers | `repr(obj)` |
| `__eq__` | Equality (`==`) comparison | `obj1 == obj2` |
| `__lt__` | Less than (`<`) comparison | `obj1 < obj2` |
| `__len__` | Length of object | `len(obj)` |

### 🧪 Example:

```python
class Book:
    def __init__(self, title, pages):
        self.title = title
        self.pages = pages

    def __str__(self):
        return f"{self.title} with {self.pages} pages"

    def __repr__(self):
        return f"Book('{self.title}', {self.pages})"

    def __eq__(self, other):
        return self.pages == other.pages

    def __lt__(self, other):
        return self.pages < other.pages

    def __len__(self):
        return self.pages

b1 = Book("Python 101", 300)
b2 = Book("Learn Python", 400)

print(str(b1))       # Python 101 with 300 pages
print(repr(b2))      # Book('Learn Python', 400)
print(b1 == b2)      # False
print(b1 < b2)       # True
print(len(b1))       # 300

```

## 🔹 Class methods and static methods

### ✅ `@classmethod`

A `@classmethod` is a method that is bound to the **class** and not the instance. It takes the **class itself (`cls`) as the first argument** instead of `self`. It can **access and modify class state**, such as class variables. It’s commonly used for **factory methods** or to create methods that work at the class level.

- Takes `cls` (not `self`) as the first argument
- Can **access and modify class state**
- Used for **alternative constructors**

```python
class Employee:
    raise_amount = 1.1

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    @classmethod
    def from_string(cls, emp_str):
        name, salary = emp_str.split("-")
        return cls(name, int(salary))

emp = Employee.from_string("Alice-50000")
print(emp.name)  # Alice

```

### ✅ `@staticmethod`

A `@staticmethod` is a method that **does not take `self` or `cls` as its first parameter**. It behaves like a regular function but resides inside the class's namespace. It is used when the method logic is related to the class but doesn’t need to access or modify the class or instance state.

- No access to `self` or `cls`
- Behaves like a normal function but lives in the class's namespace
- Used for **utility/helper methods**

```python
class Math:
    @staticmethod
    def add(x, y):
        return x + y

print(Math.add(5, 3))  # 8

```

### ✅ Use Cases:

- Use **`@classmethod`** when the method needs to work with **class-level data** or create instances in a controlled way.
- Use **`@staticmethod`** when the method is **utility-like** and doesn’t depend on instance or class state.

### 🆚 Difference Table

| Feature | Instance Method | Class Method | Static Method |
| --- | --- | --- | --- |
| First param | `self` | `cls` | None |
| Access `self` | ✅ | ❌ | ❌ |
| Access `cls` | ❌ | ✅ | ❌ |
| Use-case | Operate on object | Alternative constructors | Utility functions |