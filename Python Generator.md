---
aliases:
  - generator
---
In Python, a **generator** is a special type of [[Python Iterator|iterator]] that allows you to create a sequence of values on the fly, one at a time, rather than generating and storing the entire sequence in memory. Generators are defined using functions that yield values instead of returning them, making them memory-efficient and ideal for working with large datasets or streams of data.

### How Generators Work

**Generators** are created using functions that contain one or more `yield` statements. When a generator function is called, it doesn’t execute immediately but returns a **generator object**. This object can then be iterated over, with each call to `next()` on the generator resuming from where it left off in the function, running until it encounters the next `yield` statement or the end of the function.

### Defining a Generator

To define a generator, you use a function with the `yield` keyword. Here’s a basic example:

```python
def simple_generator():
    yield 1
    yield 2
    yield 3

# Usage
gen = simple_generator()
print(next(gen))  # Outputs: 1
print(next(gen))  # Outputs: 2
print(next(gen))  # Outputs: 3
```

In this example:
- Calling `simple_generator()` returns a generator object.
- Each call to `next()` retrieves the next value from the generator, resuming the function execution from where it left off after the previous `yield`.

### Differences Between `yield` and `return`

- **`yield`**: Suspends the function and saves its state so it can resume later, producing a generator.
- **`return`**: Ends the function immediately and returns a value, without saving the function's state for continuation.

### Example: Generator for a Sequence

Let’s look at a generator that yields a sequence of numbers, similar to a range function.

```python
def count_up_to(max):
    count = 1
    while count <= max:
        yield count
        count += 1

# Usage
for number in count_up_to(5):
    print(number)
# Outputs: 1 2 3 4 5
```

Here, `count_up_to` generates numbers up to a specified maximum value. It yields each number in sequence without building an entire list in memory.

### Advantages of Generators

1. **Memory Efficiency**: Generators produce items only when requested, making them ideal for working with large datasets or infinite sequences.
2. **Lazy Evaluation**: Generators only generate values as needed, reducing computation and memory usage for large or expensive-to-calculate datasets.
3. **Readable Code**: Generators can help simplify code, especially when working with complex loops or sequences.

### Generator Expressions

Python provides **generator expressions**, similar to list comprehensions, but enclosed in parentheses instead of square brackets. These expressions create generators in a concise, single-line format.

#### Example:

```python
# Generator expression to produce squares of numbers
squares = (x * x for x in range(5))

for square in squares:
    print(square)
# Outputs: 0 1 4 9 16
```

This generator expression produces the squares of numbers from 0 to 4, calculating each square only when requested.

### Using Generators with `next()`

Generators can be manually iterated using the `next()` function. Each call to `next()` retrieves the next value from the generator, and when the generator is exhausted, it raises a `StopIteration` exception.

```python
gen = (x * x for x in range(3))

print(next(gen))  # Outputs: 0
print(next(gen))  # Outputs: 1
print(next(gen))  # Outputs: 4
print(next(gen))  # Raises StopIteration
```

### Practical Examples of Generators

Generators are especially useful for:
- **Processing large files**: Read and process large files line by line without loading the entire file into memory.
- **Streaming data**: Handle data from streams, such as sensor data or network data, where data is produced over time.
- **Infinite Sequences**: Define sequences without a predefined end, like an infinite series or repeating sequence.

#### Example: Reading a Large File with a Generator

```python
def read_large_file(file_path):
    with open(file_path) as file:
        for line in file:
            yield line

# Usage
for line in read_large_file("large_file.txt"):
    print(line)
```

In this example:
- `read_large_file` is a generator function that reads a file line by line, yielding each line without loading the entire file into memory.
- This approach is memory-efficient for handling large files.

#### Example: Infinite Sequence Generator

```python
def infinite_counter(start=1):
    count = start
    while True:
        yield count
        count += 1

# Usage
counter = infinite_counter()
print(next(counter))  # Outputs: 1
print(next(counter))  # Outputs: 2
print(next(counter))  # Outputs: 3
```

This generator creates an infinite counter, which continues yielding incremented values indefinitely. This is useful for scenarios where the sequence doesn’t have a predefined end.

### Summary

- **Generators** are functions that yield values one at a time, allowing you to iterate over them on demand.
- They use **lazy evaluation**, generating items only when requested, making them memory-efficient for large datasets or streams.
- The **`yield`** statement suspends and saves the state of the generator, allowing it to resume from where it left off.
- **Generator expressions** provide a compact syntax for creating generators.
- **Generators** are ideal for processing large files, creating infinite sequences, or working with data streams.

**Generators** are a powerful feature in Python, allowing you to create efficient and readable code when working with large or infinite sequences. They provide both memory and computational efficiency, especially in data-intensive applications.