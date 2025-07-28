## **Multithreading & Multiprocessing**

### ✅ Overview Table

| Feature | Multithreading | Multiprocessing |
| --- | --- | --- |
| Execution Model | Multiple threads in a single process | Multiple separate Python processes |
| Memory | Shared memory | Separate memory spaces |
| Suitable For | I/O-bound tasks | CPU-bound tasks |
| Concurrency | Yes | Yes |
| Parallelism | Not real due to GIL | Real parallelism |
| Uses | `threading` module | `multiprocessing` module |

## 🔐 2. **Global Interpreter Lock (GIL)**

### 🔸 What is GIL?

- GIL (Global Interpreter Lock) is a mutex that **allows only one thread to execute Python bytecode at a time**.
- It affects **CPython** (the standard Python implementation).
- This means **CPU-bound multithreading is limited**, because threads can't run truly in parallel.

### 🔸 When does GIL matter?

- **Does not affect I/O-bound** tasks (e.g., file/network I/O).
- **Does affect CPU-bound** tasks (e.g., math-heavy computation).

## 🔍 1. What is a **CPU-bound** Task?

### ✅ Definition:

A **CPU-bound** task is one that primarily uses the **CPU for computations**. These tasks are intensive in terms of processing power and require a lot of calculations.

### 💡 Examples:

- Complex mathematical computations
- Image/video processing
- Machine learning model training
- Data encryption/decryption
- Simulation and modeling

### 🧠 Characteristics:

- Uses a lot of CPU cycles
- Little or no waiting for I/O
- Runs faster on **multiple processors/cores**

### 🔧 Suitable for:

- **Multiprocessing** (bypasses GIL and uses multiple CPU cores)

### 🧪 Example:

```python
# CPU-bound: Calculate factorial
def factorial(n):
    return 1 if n == 0 else n * factorial(n-1)

for i in range(1, 10000):
    factorial(100)

```

---

## 🔌 2. What is an **I/O-bound** Task?

### ✅ Definition:

An **I/O-bound** task is one that spends most of its time **waiting for input/output operations** to complete, rather than performing computations.

### 💡 Examples:

- Reading/writing to disk
- Fetching data from an API
- Database queries
- File uploads/downloads
- User input or network latency

### 🧠 Characteristics:

- Less CPU usage, more time waiting
- Can benefit from concurrency to utilize wait time
- Often limited by speed of hardware or external systems

### 🔧 Suitable for:

- **Multithreading** or **AsyncIO** (does not need parallelism, only concurrency)

### 🧪 Example:

```python
# I/O-bound: Simulate file download
import time

def download_file():
    time.sleep(2)  # Simulate waiting for I/O
    print("Downloaded")

download_file()

```

---

## ⚖️ Summary Table

| Feature | CPU-bound Task | I/O-bound Task |
| --- | --- | --- |
| Main bottleneck | CPU performance | I/O wait time (disk/network) |
| Example | Image processing, encryption | API calls, file reads |
| Best suited for | `multiprocessing` | `threading` / `asyncio` |
| GIL impact | GIL limits multithreading | GIL is less of a concern |
| Parallelism needed | Yes (use multiple cores) | No (concurrent threads are enough) |

---

## 🚦 Rule of Thumb:

- Use **threading/asyncio** for I/O-bound tasks to keep your app responsive while waiting.
- Use **multiprocessing** for CPU-bound tasks to split the workload across cores.

---

Would you like a benchmark comparison showing how threading vs multiprocessing performs on both task types?

## 🧵 3. **Multithreading (using `threading` module)**

### ✅ Best for:

- I/O-bound tasks (like downloading files, reading from sockets)

### 🧪 Example:

```python
import threading
import time

def print_numbers():
    for i in range(5):
        print(f"Number: {i}")
        time.sleep(1)

thread1 = threading.Thread(target=print_numbers)
thread2 = threading.Thread(target=print_numbers)

thread1.start()
thread2.start()

thread1.join()
thread2.join()

print("Done")

```

Even though both threads run concurrently, due to the GIL, **only one executes Python code at a time**.

## ⚙️ 4. **Multiprocessing (using `multiprocessing` module)**

### ✅ Best for:

- CPU-bound tasks (e.g., image processing, scientific calculations)

### 🧪 Example:

```python
import multiprocessing
import time

def print_numbers():
    for i in range(5):
        print(f"Number: {i}")
        time.sleep(1)

process1 = multiprocessing.Process(target=print_numbers)
process2 = multiprocessing.Process(target=print_numbers)

process1.start()
process2.start()

process1.join()
process2.join()

print("Done")

```

Here, **each process has its own Python interpreter and memory space**, so GIL is not a limitation.

---

### 📌 Key Differences Between `threading` and `multiprocessing`

| Aspect | `threading` | `multiprocessing` |
| --- | --- | --- |
| Concurrency Type | Concurrent (not parallel) | True parallel execution |
| GIL Impact | Affected | Not affected |
| Performance (CPU-bound) | Poor | Excellent |
| Overhead | Low | Higher (new process creation, IPC) |
| Memory | Shared memory | Separate memory |

---

## 🧠 Summary

- **Use `threading`** for **I/O-bound** tasks (e.g., network requests, file I/O).
- **Use `multiprocessing`** for **CPU-bound** tasks (e.g., image processing, simulations).
- **GIL** is the main reason CPU-bound multithreading is ineffective in CPython.