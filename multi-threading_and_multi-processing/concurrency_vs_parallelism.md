## Concurrency vs  Parallelism

### **1. Concurrency**

Concurrency is the ability of a program to handle multiple tasks at once by switching between them. 

It is not compulsory to execute all tasks at same moment but can be executed in overlapping periods of time. 

The main goal of concurrency is to handle multiple user inputs, manage several I/O tasks, or process multiple independent tasks.

### Types

- **Thread-Based Concurrency:** Threading is a technique for producing lightweight threads (sometimes known as "worker threads") in a single step. Because these threads share the same memory region, they are ideal for I/O-bound activities.
- **Process-Based Concurrency:** [**Multiprocessing**](https://www.geeksforgeeks.org/multiprocessing-python-set-1/) entails the execution of several processes, each with its own memory space. Because it can use several CPU cores, this is appropriate for CPU-bound activities.
- **Coroutine-Based Concurrency**: Asynchronous programming, with [**'asyncio'**](https://www.geeksforgeeks.org/asyncio-in-python/) , 'async', and 'await' keywords, is ideal for efficiently managing I/O-bound processes. It enables tasks to pause and hand over control to other tasks during I/O operations without causing the entire program to crash.

**In Python:**

Concurrency is commonly achieved using:

- **`threading` module** (threads run concurrently but due to GIL, only one runs at a time per process in CPython)
- **`asyncio` module** (single-threaded cooperative multitasking using coroutines)

**Example using `asyncio`:**

```python
import asyncio

async def task1():
    await asyncio.sleep(1)
    print("Task 1 completed")

async def task2():
    await asyncio.sleep(1)
    print("Task 2 completed")

async def main():
    await asyncio.gather(task1(), task2())

asyncio.run(main())
```

### **2. Parallelism**

Parallelism is the simultaneous execution of multiple tasks using multiple processors or CPU cores. Tasks truly run at the same time.

**In Python:**

Parallelism is achieved using:

- **`multiprocessing` module** (bypasses GIL by creating separate processes)
- **Joblib**, **Dask**, **concurrent.futures.ProcessPoolExecutor**

**Example using `multiprocessing`:**

```python
from multiprocessing import Process
import time

def task(name):
    time.sleep(1)
    print(f"Task {name} completed")

if __name__ == "__main__":
    p1 = Process(target=task, args=("A",))
    p2 = Process(target=task, args=("B",))
    p1.start()
    p2.start()
    p1.join()
    p2.join()
```

---

### **Key Differences**

| Feature | Concurrency | Parallelism |
| --- | --- | --- |
| Definition | Tasks are managed at the same time | Tasks are executed at the same time |
| Execution Model | Time-sliced switching (interleaved) | True simultaneous execution |
| CPU Utilization | Single-core (often) | Multi-core (uses multiple CPUs) |
| Libraries Used | `asyncio`, `threading` | `multiprocessing`, `joblib`, `Dask` |
| GIL Limitation | Affected (threads share GIL) | Not affected (separate processes) |
| Suitable For | I/O-bound tasks | CPU-bound tasks |

---

### **Summary**

- Use **concurrency** for **I/O-bound tasks** (like web scraping, file/network I/O).
- Use **parallelism** for **CPU-bound tasks** (like data processing, computation-heavy operations).