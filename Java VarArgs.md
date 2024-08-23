## What

**Variable-length Arguments**, is a feature introduced in Java 5 that allows a method to accept an arbitrary number of arguments. 

**VarArgs** enables you to define a method that can accept *zero or more* arguments of a specified type. When a method has a VarArgs parameter, you can call that method with any number of arguments of that parameter's type, including no arguments at all.

To define a VarArgs parameter in a method, you use an ellipsis (`...`) followed by the parameter type.
```java
returnType methodName(dataType... variableName) {
    // method body
}
```
## How

When you use **VarArgs** in a method, Java automatically handles the parameters as an **array** of the specified type. Internally, the **VarArgs** parameter is converted into an **array**, allowing the method to iterate over the arguments or access them using an index.

1. **Single VarArgs per Method**: A method can have only one VarArgs parameter, and it must be the last parameter in the method signature.
2. **VarArgs and Arrays**: VarArgs is syntactic sugar for an array.
3. **Compatibility with Overloading**: Methods with VarArgs can coexist with overloaded methods that have a fixed number of parameters, but care must be taken to avoid ambiguity.

### Why

**VarArgs** in Java offers a flexible and clean way to handle methods that require multiple arguments. It is especially useful when you need to pass a varying number of arguments to a method without overloading it excessively.