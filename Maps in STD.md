## `std::unordered_map`

`std::unordered_map` requires its key to be [[Hashable]]. 

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

Using user defined types as keys for `std::unordered_map`, can be done by overloading `std::hash` and `operator==` if needed.
## `std::map`

`std::map` does not require its keys to be [[Hashable]], it only requires that keys be *sortable*.