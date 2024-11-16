---
aliases:
  - iterable
---
In Python, an **iterable** is any object capable of returning its elements one at a time. An iterable is a collection of items (like a list, tuple, or dictionary) or a custom object that conforms to Python's **iterator protocol**. Iterables are fundamental to Python’s design, enabling operations like looping through elements using `for` loops.

---

### **What Makes an Object Iterable?**

An object is **iterable** if:
1. It implements the **`__iter__()`** method, which returns an [[Python Iterator|iterator]].
2. Alternatively, it implements the **`__getitem__()`** method, which enables indexed access to its elements (an older protocol still supported for backward compatibility).

The [[Python Iterator|iterator]] returned by `__iter__()` must implement the `__next__()` method, which provides the next value in the sequence.

#### Examples of Iterable Objects:

- Built-in collections: `list`, `tuple`, `set`, `dict`, `str`, etc.
- Custom objects implementing the `__iter__()` or `__getitem__()` method.

---

### **Using an Iterable**

You can loop through an iterable using:
1. A `for` loop (the most common approach). ([[#^430c7e]])
2. Explicitly converting it into an iterator using the `iter()` function.

#### Example: Looping Through an Iterable

```python
# Iterable: List
numbers = [1, 2, 3, 4]

# Using a for loop
for num in numbers:
    print(num)
# Outputs: 1 2 3 4
```

#### Example: Using `iter()`

```python
# Convert iterable to an iterator
iterator = iter(numbers)

# Access elements using next()
print(next(iterator))  # Outputs: 1
print(next(iterator))  # Outputs: 2
```

#### **For Loops on Iterables**

^430c7e

When a `for...in` loop is used in Python, the process involves several steps under the hood, leveraging the **iterator** protocol. Here's what happens:

1. **Calling `iter()`**:  
   When you write `for item in iterable:`, Python first calls the built-in `iter()` function on the `iterable` object. This function returns an **iterator** object.  
   - An **iterable** is any object that implements the `__iter__()` method or has a `__getitem__()` method (in older Python versions).
   - An **iterator** is an object that implements both the `__iter__()` and `__next__()` methods.

2. **Obtaining the iterator**:  
   The iterator object returned by `iter()` is what will drive the loop. This object keeps track of the iteration state.

3. **Calling `next()`**:  
   On each iteration of the loop, Python calls the `__next__()` method of the iterator to get the next item in the sequence.
   - If the iterator provides a value, it is assigned to the loop variable (e.g., `item` in `for item in iterable:`).
   - If the iterator is exhausted and cannot produce further values, it raises a `StopIteration` exception, which signals Python to exit the loop.

4. **Exiting the loop**:  
   When `StopIteration` is raised, the loop ends gracefully, and any subsequent code outside the loop executes.

---

### **Iterables vs Iterators**

| **Feature**           | **Iterable**                          | **Iterator**                         |
|------------------------|---------------------------------------|---------------------------------------|
| **Definition**         | An object that can return an iterator. | An object that represents a stream of data. |
| **Key Method**         | Implements `__iter__()`               | Implements `__iter__()` and `__next__()` |
| **Example**            | Lists, tuples, strings, dictionaries  | Object returned by `iter()`          |
| **Reusability**        | Can be used to create new iterators   | Cannot be reused; once exhausted, must recreate or reset |

---

### **Checking if an Object is Iterable**

You can check whether an object is iterable by importing and using the `collections.abc.Iterable` class:

```python
from collections.abc import Iterable

print(isinstance([1, 2, 3], Iterable))  # True (list is iterable)
print(isinstance(10, Iterable))        # False (integer is not iterable)
```

---

### **Built-in Iterables in Python**

1. **Sequences**: These are collections that support indexed access and maintain order.
   - Examples: `list`, `tuple`, `str`, `range`

2. **Non-sequences**: These do not maintain order but are still iterable.
   - Examples: `set`, `dict`, `frozenset`

3. **Generators**: These are special iterables that generate values lazily.
   - Examples: Created using generator functions or generator expressions.

---

### **Custom Iterables**

You can create your own iterable by defining the `__iter__()` method in a class.

#### Example: Custom Iterable

```python
class MyIterable:
    def __init__(self, max_value):
        self.max_value = max_value

    def __iter__(self):
        self.current = 0
        return self

    def __next__(self):
        if self.current >= self.max_value:
            raise StopIteration
        self.current += 1
        return self.current

# Usage
my_iterable = MyIterable(5)
for num in my_iterable:
    print(num)
# Outputs: 1 2 3 4 5
```

Here:
- The `__iter__()` method initializes the iteration state and returns the object itself.
- The `__next__()` method defines the logic for generating the next element.

---

### **Iterables in Python's Ecosystem**

1. **`for` Loops**: Automatically use the `iter()` function to get an iterator and call `__next__()` until `StopIteration` is raised.
2. **Comprehensions**: List, set, and dictionary comprehensions are built on iterable objects.
3. **Functions That Work with Iterables**:
   - `sum(iterable)`: Sums elements in an iterable.
   - `min(iterable)`, `max(iterable)`: Find the minimum or maximum value.
   - `sorted(iterable)`: Returns a sorted list.
   - `zip(iterables)`: Combines multiple iterables into tuples.
   - `enumerate(iterable)`: Adds an index to each element in an iterable.

#### Example:

```python
# Using built-in functions with iterables
numbers = [3, 1, 4, 1, 5]
print(sum(numbers))       # Outputs: 14
print(sorted(numbers))    # Outputs: [1, 1, 3, 4, 5]
```

---

### **Practical Use Cases for Iterables**

1. **Data Processing**: Iterate over large datasets or streams without loading them entirely into memory.
2. **File Handling**: Process files line by line (e.g., read large files efficiently).
3. **Streaming Data**: Handle real-time data streams, such as logs or API responses.

#### Example: Reading a File Line by Line (Efficiently)

```python
with open("large_file.txt") as file:
    for line in file:
        print(line.strip())
```

Here, the `file` object acts as an iterable, and the `for` loop reads it line by line.

---
### Summary

| **Feature**          | **Description**                                                                |
| -------------------- | ------------------------------------------------------------------------------ |
| **Definition**       | An object capable of returning an iterator to iterate over its elements.       |
| **Key Method**       | Implements `__iter__()` (or `__getitem__()`).                                  |
| **Examples**         | Lists, tuples, strings, dictionaries, sets, generators, custom objects.        |
| **Common Use Cases** | Looping with `for`, comprehensions, working with large datasets, file reading. |

### Conclusion

Python **iterables** are foundational to its design, enabling efficient and intuitive iteration through various data structures. By understanding iterables and how they work with iterators, you can write cleaner, more Pythonic code and work effectively with collections, custom objects, and streams.