By definition, an object is **hashable** if it meets two conditions within the standard library in C++.

1. There is a specialization of `std::hash<T>` that permits `T` type objects to be hashed. The `std::hash` is a function object or functor that constructs hash values for a given object.
2. The type `T` supports equivalence. In other words, given `a` and `b` of type `T`, you can evaluate `a == b` and get a boolean value. This is typically achieved by overloading the `operator==` function for the type `T`.

This allows objects of type `T` to be used as keys in an unordered associative container like `std::unordered_map<K, V>` and `std::unordered_set<Key>`, where the key-value pair in the collection is stored and retrieved using the hash key for optimal performance.