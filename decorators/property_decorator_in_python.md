# `@property` Decorator

## 🔍 What is `@property`?

The `@property` decorator is used to **define getter methods** that are accessed like attributes.

It enables:

* **Read-only attributes**.
* Encapsulation (e.g., adding validation when setting a value).
* Computed properties.

---

## ✅ Basic Syntax

```python
class MyClass:
    def __init__(self, value):
        self._value = value

    @property
    def value(self):
        return self._value
```

```python
obj = MyClass(10)
print(obj.value)  # calls value() method without parentheses
```

You can also define:

* `@value.setter` — for setting the attribute
* `@value.deleter` — for deleting the attribute

---

## ✅ Anatomy of a Full `@property`

```python
class Example:
    def __init__(self):
        self._x = 0

    @property
    def x(self):             # Getter
        return self._x

    @x.setter
    def x(self, value):      # Setter
        if value < 0:
            raise ValueError("x must be non-negative")
        self._x = value

    @x.deleter
    def x(self):             # Deleter
        del self._x
```

---

# ✅ 3 Real-World Examples of `@property`

---

## 🧮 **1. Bank Account – Balance with Validation**

### 🎯 Scenario:

You want to make sure users cannot **set a negative balance** and expose balance as a **simple attribute**.

```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self._balance = balance

    @property
    def balance(self):
        return self._balance

    @balance.setter
    def balance(self, amount):
        if amount < 0:
            raise ValueError("Balance cannot be negative")
        self._balance = amount

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        if amount > self.balance:
            raise ValueError("Insufficient funds")
        self.balance -= amount

# ✅ Usage
acc = BankAccount("Alice", 1000)
print(acc.balance)       # 1000
acc.deposit(500)
print(acc.balance)       # 1500
acc.withdraw(200)
print(acc.balance)       # 1300
acc.balance = -500       # ❌ Raises ValueError
```

---

## 🧱 **2. Rectangle – Area as a Read-only Computed Property**

### 🎯 Scenario:

The area of a rectangle should be **computed from length and width**, but **not directly set**.

```python
class Rectangle:
    def __init__(self, length, width):
        self.length = length
        self.width = width

    @property
    def area(self):
        return self.length * self.width

# ✅ Usage
r = Rectangle(10, 5)
print(r.area)         # 50
r.length = 20
print(r.area)         # 100
r.area = 200          # ❌ AttributeError: can't set attribute
```

---

## 🚗 **3. Car – Speed with Unit Conversion**

### 🎯 Scenario:

Expose **speed in km/h**, but allow user to **set it in m/s**. Let’s manage this smartly using `@property`.

```python
class Car:
    def __init__(self, speed_mps):
        self._speed_mps = speed_mps  # meters per second

    @property
    def speed_kmph(self):
        return self._speed_mps * 3.6

    @speed_kmph.setter
    def speed_kmph(self, kmph):
        self._speed_mps = kmph / 3.6

# ✅ Usage
car = Car(20)  # 20 m/s
print(car.speed_kmph)  # 72.0 km/h
car.speed_kmph = 108   # Set speed in km/h
print(car._speed_mps)  # 30.0 m/s
```

---

## 🧠 Why Use `@property`?

| Feature            | Traditional Getter/Setter | `@property`             |
| ------------------ | ------------------------- | ----------------------- |
| Call style         | `obj.get_x()`             | `obj.x`                 |
| Readability        | ❌ Less Pythonic           | ✅ Cleaner               |
| Compatibility      | ❌ Breaks on change        | ✅ Encapsulates behavior |
| Validation support | ✅ Yes                     | ✅ Yes                   |

---

## 🧪 Bonus: Read-only Property

```python
class Circle:
    def __init__(self, radius):
        self.radius = radius

    @property
    def diameter(self):
        return self.radius * 2

c = Circle(5)
print(c.diameter)  # 10
c.diameter = 20    # ❌ AttributeError
```

---

## ✅ Summary

| Decorator    | Purpose                                          |
| ------------ | ------------------------------------------------ |
| `@property`  | Makes a method behave like a read-only attribute |
| `@x.setter`  | Defines logic when setting the attribute         |
| `@x.deleter` | Logic for deleting the attribute                 |


