In the newer versions of Mockito (3.4.0 and later), mocking static methods is supported via the `MockedStatic` feature. You can do it like this:

```java
try (MockedStatic<MyClass> theMock = Mockito.mockStatic(MyClass.class)) {
    theMock.when(MyClass::myStaticMethod).thenReturn("mocked output");
    // ...
}
```

Remember, the static mock only remains in effect within the try block. Once the control goes out of the block, the original method is not mocked anymore.