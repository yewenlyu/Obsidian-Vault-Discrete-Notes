## `std::unordered_map`

`std::unordered_map` requires its key to be *hashable*. 

For example, to declare `std::unordered_map<std::vector<int>, int>` we need to define a custom hash function. 

```cpp
auto vectorHash = [](const vector<int>& v) {
	size_t seed = v.size();
	for (const int& i : v) {
		seed ^= hash<int>()(i) + 0x9e3779b9 + (seed << 6) + (seed >> 2);
	}
	return seed;
};

unordered_map<vector<int>, int, decltype(vectorHash)> myMap(vectorHash);
```

## `std::map`

`std::map` does not require its keys to be *hashable*, it only requires that keys be *sortable*.

*Sortable* in C++ means that the "<" (less than) operator can be used to create a *strict weak ordering* of the elements.