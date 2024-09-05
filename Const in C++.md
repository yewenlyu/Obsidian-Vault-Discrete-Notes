### 1. **Defining Constant Variables**

The most basic use of `const` is to declare variables whose values cannot change after initialization.

```cpp
const int max_value = 100;
```

In this example, `max_value` is a constant integer with a value of 100. Any attempt to modify `max_value` later in the code will result in a compilation error.

### 2. **Pointers and `const`**

When dealing with pointers, `const` can have different meanings depending on its placement in the declaration.

#### 2.1 Constant Pointer to a Non-Constant Value

A **constant pointer** is a pointer that cannot change the address it is holding, but you can modify the value at that address.

```cpp
int value = 10;
int *const ptr = &value;  // ptr is a constant pointer to an int

*ptr = 20;   // OK: modifies the value at the address ptr points to
ptr = &another_value;  // Error: cannot change the address ptr is holding
```

#### 2.2 Pointer to a Constant Value

A **pointer to a constant** means the value being pointed to cannot be modified through the pointer, but the pointer itself can change to point to a different address.

```cpp
const int value = 10;
const int *ptr = &value;  // ptr is a pointer to a const int

*ptr = 20;   // Error: cannot modify the value through the pointer
ptr = &another_value;  // OK: ptr can point to another address
```

#### 2.3 Constant Pointer to a Constant Value

A **constant pointer to a constant value** means that neither the value being pointed to can be changed, nor can the pointer point to a different address.

```cpp
const int value = 10;
const int *const ptr = &value;  // ptr is a constant pointer to a const int

*ptr = 20;  // Error: cannot modify the value
ptr = &another_value;  // Error: cannot change the pointer address
```

### 3. **`const` with Function Parameters**

The `const` keyword can be used to protect function parameters from being modified inside the function body.

```cpp
void printValue(const int value) {
    // value is read-only and cannot be modified inside the function
    std::cout << value << std::endl;
}
```

If `value` is passed to `printValue`, any attempt to change `value` within the function will result in a compilation error.

### 4. **`const` with Reference Parameters**

You can use `const` to make a reference parameter constant, which is particularly useful when passing objects to functions to avoid copying while ensuring the object is not modified.

```cpp
void printVector(const std::vector<int>& vec) {
    // vec is read-only and cannot be modified
    for (const int& val : vec) {
        std::cout << val << ' ';
    }
}
```

In this example, `vec` is a constant reference to a `std::vector<int>`. This means `printVector` cannot modify `vec`, but it also avoids copying the vector, making the function more efficient.

### 5. **`const` with Member Functions**

In class definitions, a member function can be declared `const` to indicate that it does not modify any member variables of the class. This is particularly useful for functions that are meant to access data without changing the state of the object.

```cpp
class MyClass {
public:
    int getValue() const {
        return value;
    }
private:
    int value;
};
```

Here, `getValue()` is a `const` member function, which means it cannot modify any member variables of `MyClass`. This allows you to call this function on `const` instances of `MyClass`.

### 6. **`const` with Return Types**

The `const` keyword can also be used with function return types to prevent the modification of returned objects.

#### 6.1 Returning a `const` Value

Returning a constant value prevents the caller from modifying the returned value.

```cpp
const int getMax() {
    return 100;
}
```

However, this is rarely useful for primitive types as the returned value is a copy and not a reference.

#### 6.2 Returning a `const` Reference

More commonly, you will see a function return a constant reference.

```cpp
const std::string& getName() const {
    return name;
}
```

Here, the function `getName()` returns a reference to a constant `std::string`. This prevents the caller from modifying the `name` member of the class through the returned reference.

### 7. **`mutable` Keyword and `const`**

The `mutable` keyword can be used to allow specific member variables of a class to be modified even if they are accessed through a `const` member function.

```cpp
class MyClass {
public:
    void modifyCounter() const {
        counter++;  // allowed due to mutable
    }
private:
    mutable int counter = 0;
};
```

In this example, `counter` can be modified even in a `const` member function because it is declared as `mutable`.

### 8. **`const` in Function Overloading**

Functions can be overloaded based on whether they are `const` or not. This is particularly useful for classes that need both a constant and a non-constant version of a function.

```cpp
class Container {
public:
    int& operator[](int index) {
        return data[index];  // non-const version returns a modifiable reference
    }

    const int& operator[](int index) const {
        return data[index];  // const version returns a constant reference
    }
private:
    std::vector<int> data;
};
```

### 9. **`constexpr` vs. `const`**

The `constexpr` keyword, introduced in C++11, is related but different from `const`. A `constexpr` variable is implicitly `const`, but it can also be evaluated at compile-time, whereas a `const` variable is determined at runtime.

```cpp
constexpr int compileTimeConst = 10;
const int runtimeConst = someFunction();  // result is known only at runtime
```

### 10. **Best Practices for Using `const`**

- Use `const` whenever a variable, parameter, or return value should not be modified after its initialization.
- Prefer `const` references when passing large objects to functions to avoid unnecessary copying.
- Declare member functions `const` when they do not modify the object’s state.
- Use `const` with pointers and references to clarify whether the object pointed to can be modified.
- When using `const` in APIs, consider the intent of usage and clarity to ensure that the code is intuitive and maintainable.

### Summary

The `const` keyword in C++ is a powerful tool to ensure immutability and enhance code safety and clarity. Understanding the different contexts in which `const` can be used, and applying it appropriately, is essential for writing robust and maintainable C++ code.