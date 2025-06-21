# Python List Data Strucutre

## In-Built Methods
---

### ✅ 1. `append()`

Adds an element to the **end** of the list.

```python
lst = [1, 2, 3]
lst.append(4)
print(lst)  # [1, 2, 3, 4]
```

---

### ✅ 2. `insert(index, value)`

Inserts an element at a **specific index**.

```python
lst = [10, 20, 30]
lst.insert(1, 15)  # Insert 15 at index 1
print(lst)  # [10, 15, 20, 30]
```

---

### ✅ 3. `remove(value)`

Removes the **first occurrence** of a value.

```python
lst = [1, 2, 3, 2]
lst.remove(2)
print(lst)  # [1, 3, 2]
```

---

### ✅ 4. `pop([index])`

Removes and returns the item at the **given index**. Defaults to the last item.

```python
lst = [10, 20, 30]
x = lst.pop()
print(x)    # 30
print(lst)  # [10, 20]

y = lst.pop(0)
print(y)    # 10
print(lst)  # [20]
```

---

### ✅ 5. `sort()`

Sorts the list **in place**, ascending by default.

```python
lst = [3, 1, 4, 2]
lst.sort()
print(lst)  # [1, 2, 3, 4]
```

### Sort descending:

```python
lst.sort(reverse=True)
print(lst)  # [4, 3, 2, 1]
```

---

### ✅ 6. `reverse()`

Reverses the list **in place**.

```python
lst = [1, 2, 3]
lst.reverse()
print(lst)  # [3, 2, 1]
```

---

### ✅ 7. `extend(iterable)`

Appends elements of another iterable (like list) to the end.

```python
lst = [1, 2]
lst.extend([3, 4])
print(lst)  # [1, 2, 3, 4]
```

---

### ✅ 8. `index(value)`

Returns the **index of first occurrence** of a value.

```python
lst = ['a', 'b', 'c', 'b']
print(lst.index('b'))  # 1
```

---

### ✅ 9. `count(value)`

Returns the **number of occurrences** of a value.

```python
lst = [1, 2, 2, 3, 2]
print(lst.count(2))  # 3
```

---

### ✅ 10. Slicing: `lst[start:end:step]`

```python
lst = [0, 1, 2, 3, 4, 5, 6]

print(lst[1:5])        # [1, 2, 3, 4]
print(lst[::2])        # [0, 2, 4, 6]
print(lst[::-1])       # [6, 5, 4, 3, 2, 1, 0] (reverse)
print(lst[2:6:2])      # [2, 4]
```

---

## Advance Practical Questions
---

### ✅ **1. What is the time complexity of `list.append()` and `list.insert(0, x)`?**

* `list.append(x)` is **amortized O(1)**.
* `list.insert(0, x)` is **O(n)** because it shifts all elements.

---

### ✅ **2. How do you flatten a nested list (1 level) using a one-liner?**

```python
nested = [[1, 2], [3, 4], [5]]
flat = [x for sub in nested for x in sub]
print(flat)  # [1, 2, 3, 4, 5]
```

---

### ✅ **3. What is the difference between `list.remove(x)` and `del list[i]`?**

* `remove(x)` deletes **first occurrence** of value `x`.
* `del list[i]` deletes the **element at index `i`**.

```python
lst = [1, 2, 3, 2]
lst.remove(2)  # removes first 2 → [1, 3, 2]
del lst[1]     # removes 3 → [1, 2]
```

---

### ✅ **4. How do you efficiently rotate a list by `k` elements to the right?**

```python
def rotate(lst, k):
    k %= len(lst)
    return lst[-k:] + lst[:-k]

rotate([1, 2, 3, 4, 5], 2)  # [4, 5, 1, 2, 3]
```

---

### ✅ **5. How do you remove duplicates from a list while preserving order?**

```python
def dedup(lst):
    seen = set()
    return [x for x in lst if not (x in seen or seen.add(x))]

dedup([1, 2, 2, 3, 1])  # [1, 2, 3]
```

---

### ✅ **6. Why is `list += other_list` faster than `list.extend(other_list)` in some cases?**

* `list +=` may call the **in-place `__iadd__()`** method, which can be optimized.
* In CPython, the performance difference is negligible, but idiomatic code prefers `extend()` for clarity.

---

### ✅ **7. What's the output of `[[[]]*3]*2` and why?**

```python
matrix = [[[]]*3]*2
matrix[0][0].append(1)
print(matrix)  # [[[1], [1], [1]], [[1], [1], [1]]]
```

➡️ All inner lists reference the same `[]` object — use deep copies to avoid this.

---

### ✅ **8. How do you sort a list of tuples by the second element, descending?**

```python
lst = [(1, 'a'), (2, 'c'), (3, 'b')]
sorted_lst = sorted(lst, key=lambda x: x[1], reverse=True)
# [(2, 'c'), (3, 'b'), (1, 'a')]
```

---

### ✅ **9. What is the difference between `sort()` and `sorted()`?**

* `sort()` modifies the list **in-place**.
* `sorted()` returns a **new list**, works on any iterable.

---

### ✅ **10. How do you find the second largest unique element in a list?**

```python
def second_largest(lst):
    return sorted(set(lst))[-2]

second_largest([4, 1, 2, 4, 3])  # 3
```

---

### ✅ **11. How do you use `bisect` to insert in a sorted list?**

```python
import bisect

lst = [1, 3, 5, 7]
bisect.insort(lst, 4)
# [1, 3, 4, 5, 7]
```

---

### ✅ **12. How do you split a list into chunks of size `n`?**

```python
def chunk(lst, n):
    return [lst[i:i+n] for i in range(0, len(lst), n)]

chunk([1,2,3,4,5,6], 2)  # [[1, 2], [3, 4], [5, 6]]
```

---

### ✅ **13. Explain the difference: `a = b[:]` vs `a = b.copy()` vs `a = list(b)`**

All create shallow copies:

* `[:]` is fastest
* `.copy()` is readable and idiomatic
* `list(b)` is generic (useful for other iterables)

---

### ✅ **14. How do you find common elements between two lists?**

```python
a = [1, 2, 3]
b = [2, 3, 4]
common = list(set(a) & set(b))  # [2, 3]
```

---

### ✅ **15. Reverse a list without using `reverse()` or slicing**

```python
def reverse_list(lst):
    return list(reversed(lst))

# OR using loop
def manual_reverse(lst):
    rev = []
    for i in range(len(lst)-1, -1, -1):
        rev.append(lst[i])
    return rev
```

---

## Python List Slicing:

---

### ✅ 1. **Reverse a List**

```python
lst = [1, 2, 3, 4, 5]
rev = lst[::-1]
print(rev)  # [5, 4, 3, 2, 1]
```

---

### ✅ 2. **Extract Every Second Element**

```python
lst = ['a', 'b', 'c', 'd', 'e', 'f']
print(lst[::2])  # ['a', 'c', 'e']
```

---

### ✅ 3. **Remove Last N Elements Using Slicing**

```python
lst = [1, 2, 3, 4, 5, 6]
n = 2
print(lst[:-n])  # [1, 2, 3, 4]
```

---

### ✅ 4. **Clone a List (Deep Copy)**

```python
a = [100, 200, 300]
b = a[:]  # shallow copy, new object
b[0] = 999
print(a)  # [100, 200, 300]
print(b)  # [999, 200, 300]
```

---

### ✅ 5. **Rotate List Left by K Using Slicing**

```python
lst = [1, 2, 3, 4, 5]
k = 2
rotated = lst[k:] + lst[:k]
print(rotated)  # [3, 4, 5, 1, 2]
```

---

### ✅ 6. **Swap First and Second Halves**

```python
lst = [10, 20, 30, 40, 50, 60]
mid = len(lst) // 2
swapped = lst[mid:] + lst[:mid]
print(swapped)  # [40, 50, 60, 10, 20, 30]
```

---

### ✅ 7. **Extract Sublist in Reverse Order**

```python
lst = [0, 1, 2, 3, 4, 5, 6]
sub = lst[5:1:-1]  # from index 5 to 2 (non-inclusive)
print(sub)  # [5, 4, 3, 2]
```

---

### ✅ 8. **Skip Last Element and Reverse**

```python
lst = [1, 2, 3, 4, 5]
print(lst[-2::-1])  # [4, 3, 2, 1]
```

---

### ✅ 9. **Overwrite Elements Using Slice Assignment**

```python
lst = [1, 2, 3, 4, 5]
lst[1:4] = [8, 9]
print(lst)  # [1, 8, 9, 5]
```

---

### ✅ 10. **Interleave Two Lists with Slicing**

```python
a = [1, 3, 5]
b = [2, 4, 6]
result = [None]*(len(a)+len(b))
result[::2] = a
result[1::2] = b
print(result)  # [1, 2, 3, 4, 5, 6]
```

---


