In Python, a **decorator** is a design pattern that allows you to modify the behavior of a function, method, or class. Decorators are functions that take another function (or method) as an argument, add functionality to it, and return a modified function. Decorators are widely used in Python for things like logging, authorization, measuring execution time, and modifying or extending behavior without directly altering the original function.

### How Decorators Work

A decorator is defined as a function that accepts another function as its parameter, wraps some additional code around it, and returns the modified function. Decorators are applied to functions or methods using the `@` symbol.

Here's a basic structure of a decorator:

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        # Code to execute before the function call
        print("Something is happening before the function is called.")
        
        result = func(*args, **kwargs)  # Call the function
        
        # Code to execute after the function call
        print("Something is happening after the function is called.")
        
        return result
    return wrapper
```

### Applying a Decorator

You can apply a decorator to a function using the `@decorator_name` syntax:

```python
@my_decorator
def say_hello():
    print("Hello!")

# Usage
say_hello()
# Output:
# Something is happening before the function is called.
# Hello!
# Something is happening after the function is called.
```

This is equivalent to calling `say_hello = my_decorator(say_hello)`.

### Why Use Decorators?

Decorators allow you to add functionality to functions in a **clean** and **readable** way, following the **DRY (Don’t Repeat Yourself)** principle by enabling code reuse. They are often used for tasks such as:

- **Logging**: Tracking function calls, inputs, and outputs.
- **Authorization**: Checking permissions before executing sensitive functions.
- **Caching**: Storing the result of expensive function calls.
- **Timing**: Measuring the execution time of functions.

### Commonly Used Built-in Decorators

Python has several built-in decorators, especially for methods in classes:

1. **`@staticmethod`**: Declares a static method that doesn’t access class or instance data.
2. **`@classmethod`**: Declares a class method that takes `cls` as its first argument, enabling it to modify class-level data.
3. **`@property`**: Allows a method to be accessed like an attribute, typically used for getters, setters, and deleters.

### Example: Logging with Decorators

Let’s create a decorator to log the function name and arguments every time a function is called:

```python
def log_function_call(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__} with arguments {args} and keyword arguments {kwargs}")
        return func(*args, **kwargs)
    return wrapper

@log_function_call
def add(a, b):
    return a + b

# Usage
add(5, 10)
# Output:
# Calling add with arguments (5, 10) and keyword arguments {}
# 15
```

Here, `log_function_call` acts as a decorator to log every call to `add`.

### Advanced Decorators: Using `functools.wraps`

When you create a decorator, the wrapped function loses some metadata (like its name and docstring). To preserve the original function’s metadata, you can use the `functools.wraps` decorator within your custom decorator.

```python
import functools

def log_function_call(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__} with arguments {args} and keyword arguments {kwargs}")
        return func(*args, **kwargs)
    return wrapper
```

Using `@functools.wraps(func)` in the wrapper function preserves the original function’s metadata, making it more transparent and compatible.

### Decorators with Arguments

Sometimes, decorators need to accept arguments themselves. To achieve this, you wrap the decorator in another function that takes the arguments.

```python
def repeat(num_times):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            for _ in range(num_times):
                result = func(*args, **kwargs)
            return result
        return wrapper
    return decorator

@repeat(3)
def greet(name):
    print(f"Hello, {name}!")

# Usage
greet("Alice")
# Output:
# Hello, Alice!
# Hello, Alice!
# Hello, Alice!
```

In this example, the `repeat` decorator takes an argument `num_times` and repeats the execution of `greet` the specified number of times.

### Applying Multiple Decorators

You can stack multiple decorators on a single function. Decorators are applied from the top down.

```python
def uppercase(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return result.upper()
    return wrapper

def exclaim(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return f"{result}!"
    return wrapper

@uppercase
@exclaim
def greet(name):
    return f"Hello, {name}"

# Usage
print(greet("Alice"))  # Outputs: HELLO, ALICE!
```

In this example:
1. `exclaim` adds an exclamation mark to the result.
2. `uppercase` converts the result to uppercase.

### Summary

- **Decorators** are functions that wrap another function to modify or extend its behavior.
- They are applied with the `@decorator_name` syntax and can be used on functions, methods, and even classes.
- Common uses include logging, authorization, caching, and timing.
- **`functools.wraps`** helps preserve the original function's metadata in the decorated version.
- Decorators can accept arguments and be stacked for layered functionality.

Decorators are powerful tools in Python for creating modular, reusable code. They add functionality to functions in a clean and expressive way, without modifying the original function logic directly.