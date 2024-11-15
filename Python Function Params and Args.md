## Parameter Processing

```python
# You can define functions that take a variable number of
# positional arguments
def varargs(*args):
    return args

varargs(1, 2, 3)  # => (1, 2, 3)

# You can define functions that take a variable number of
# keyword arguments, as well
def keyword_args(**kwargs):
    return kwargs

# Let's call it to see what happens
keyword_args(big="foot", loch="ness")  # => {"big": "foot", "loch": "ness"}

# You can do both at once, if you like
def all_the_args(*args, **kwargs):
    print(args)
    print(kwargs)
"""
all_the_args(1, 2, a=3, b=4) prints:
    (1, 2)
    {"a": 3, "b": 4}
"""
```

## Argument Passing

```python
# When calling functions, you can do the opposite of args/kwargs!
# Use * to expand args (tuples) and use ** to expand kwargs (dictionaries).
args = (1, 2, 3, 4)
kwargs = {"a": 3, "b": 4}
all_the_args(*args)            # equivalent: all_the_args(1, 2, 3, 4)
all_the_args(**kwargs)         # equivalent: all_the_args(a=3, b=4)
all_the_args(*args, **kwargs)  # equivalent: all_the_args(1, 2, 3, 4, a=3, b=4)
```
