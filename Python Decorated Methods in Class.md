
## `@classmethod`

- **Binding**: A `@classmethod` is bound to the class and not to an instance. It takes `cls` as its first parameter, which represents the class itself.
- **Access**: It can access and modify the class state that applies across all instances, meaning it can call other class methods or change class variables.
- **Use Case**: `@classmethod` is typically used for factory methods or when a method needs to perform operations relevant to the class itself rather than to an instance.

```python
class MyClass:
    class_variable = "Hello, class!"

    @classmethod
    def class_method(cls):
        return cls.class_variable

# Usage
print(MyClass.class_method())  # Outputs: Hello, class!
```

## `@staticmethod`

- **Binding**: A `@staticmethod` is not bound to the instance or the class; it takes no `self` or `cls` parameters.
- **Access**: It cannot access or modify instance or class state directly. It acts just like a regular function but resides within the class namespace for organizational purposes.
- **Use Case**: `@staticmethod` is used when the method performs an operation that is related to the class in a conceptual sense but doesn’t need access to class or instance data. It’s mostly used for utility functions within the class.

```python
class MyClass:
    @staticmethod
    def static_method():
        return "Hello, static!"

# Usage
print(MyClass.static_method())  # Outputs: Hello, static!
```

## `@property`

The `@property` decorator allows a method to be accessed like an attribute, making it useful for defining **getters**, **setters**, and **deleters** within a class. It provides a way to encapsulate access to an attribute, allowing the class to implement logic while still providing a clean attribute-like interface.

```python
class Human:
	def __init__(self):
		# Initialize property
		self._age = 0
	
    # A property is just like a getter.
    # It turns the method age() into a read-only attribute of the same name.
    # There's no need to write trivial getters and setters in Python, though.
    @property
    def age(self):
        return self._age

    # This allows the property to be set
    @age.setter
    def age(self, age):
        self._age = age

    # This allows the property to be deleted
    @age.deleter
    def age(self):
        del self._age
```