# Data Strucutres in Python

## 1. **Arrays** (`array` module)

Used when you need efficient, fixed-type numeric arrays (not common for general use).

```python
import array

arr = array.array('i', [1, 2, 3, 4])  # 'i' = int
arr.append(5)
arr.remove(2)
print(arr[2])  # 3
```

### Key Methods:

* `append()`, `insert()`, `remove()`, `pop()`
* `index()`, `reverse()`, `buffer_info()`

---

## 2. **List** (built-in)

A dynamic array. Most commonly used collection in Python.

```python
lst = [10, 20, 30]
lst.append(40)
lst.insert(1, 15)
lst.pop()
lst.remove(20)
print(lst)  # [10, 15, 30]
```

### Key Methods:

* `append()`, `insert()`, `remove()`, `pop()`, `sort()`, `reverse()`
* `extend()`, `index()`, `count()`, slicing `lst[start:end:step]`

---

## 3. **Tuple** (built-in)

Immutable list — fast and hashable (can be used as dict keys).

```python
t = (1, 2, 3)
print(t[0])  # 1
```

### Key Operations:

* Indexing, slicing
* `count()`, `index()`
* Can't modify (`t[0] = 5` ❌)

---

## 4. **Dict** (Dictionary)

Key-value pairs, unordered but indexed from Python 3.7+.

```python
d = {'a': 1, 'b': 2}
d['c'] = 3
del d['a']
print(d.get('b'))  # 2
```

### Key Methods:

* `get()`, `pop()`, `keys()`, `values()`, `items()`
* `update()`, `setdefault()`, `clear()`

---

## 5. **Set**

Unordered, unique items. Fast membership testing.

```python
s = {1, 2, 3}
s.add(4)
s.remove(2)
print(3 in s)  # True
```

### Key Methods:

* `add()`, `remove()`, `discard()`, `pop()`
* `union()`, `intersection()`, `difference()`, `issubset()`

---

## 6. **Stack**

LIFO (Last In First Out). Python lists can be used.

```python
stack = []
stack.append(10)
stack.append(20)
print(stack.pop())  # 20
```

✅ For thread-safe: use `collections.deque`

---

## 7. **Queue**

FIFO (First In First Out)

```python
from collections import deque

queue = deque()
queue.append(1)
queue.append(2)
print(queue.popleft())  # 1
```

✅ Use `queue.Queue` for multi-threading

---

## 8. **Linked List** (Custom Implementation)

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def append(self, val):
        if not self.head:
            self.head = Node(val)
            return
        curr = self.head
        while curr.next:
            curr = curr.next
        curr.next = Node(val)

    def display(self):
        curr = self.head
        while curr:
            print(curr.data, end=' -> ')
            curr = curr.next
        print('None')

ll = LinkedList()
ll.append(10)
ll.append(20)
ll.display()  # 10 -> 20 -> None
```

---

## 9. **Trees** (Binary Tree Example)

```python
class TreeNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def inorder(root):
    if root:
        inorder(root.left)
        print(root.data, end=' ')
        inorder(root.right)

# Example
root = TreeNode(1)
root.left = TreeNode(2)
root.right = TreeNode(3)
inorder(root)  # 2 1 3
```

### Traversals:

* Inorder (LNR)
* Preorder (NLR)
* Postorder (LRN)
* Level-order (use queue)

---

## 10. **Graph** (Adjacency List Example)

```python
graph = {
    'A': ['B', 'C'],
    'B': ['D'],
    'C': ['E'],
    'D': [],
    'E': []
}

def dfs(node, visited=set()):
    if node not in visited:
        print(node, end=' ')
        visited.add(node)
        for neighbor in graph[node]:
            dfs(neighbor, visited)

dfs('A')  # A B D C E
```

### Representation Options:

* Adjacency List (dict)
* Adjacency Matrix (2D list)
* Edge List

---

## 🔚 Summary Table

| Data Structure | Python Support    | Mutable | Notes                              |
| -------------- | ----------------- | ------- | ---------------------------------- |
| Array          | `array` module    | ✅       | Fixed type, rare in high-level use |
| List           | Built-in          | ✅       | Most flexible                      |
| Tuple          | Built-in          | ❌       | Immutable                          |
| Dict           | Built-in          | ✅       | Key-value store                    |
| Set            | Built-in          | ✅       | Unique values                      |
| Stack          | `list` / `deque`  | ✅       | LIFO behavior                      |
| Queue          | `deque` / `queue` | ✅       | FIFO                               |
| Linked List    | Manual            | ✅       | Requires class                     |
| Tree           | Manual            | ✅       | For structured data                |
| Graph          | Manual (`dict`)   | ✅       | DFS/BFS, traversal, shortest path  |

---

