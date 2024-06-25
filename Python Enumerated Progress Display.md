```python
for i, element in enumerate(iterable, start=1):
    print(f'Processing {i}/{len(iterable)} elements', end='\r', flush=True)
```

- `\r` is a **carriage return** (CR), it represents the action of moving the cursor or print head back to the beginning of a line. By default, `print()` ends with a newline character (`\n`), using `end=\r` will overwrite the existing line. This is commonly used to create a dynamic, updating display in the console without adding new lines.
- `flush=True`: Normally, Python's output is buffered. Setting `flush=True` forces the `print()` function to "flush" the internal buffer, effectively ensuring that the output is written to the terminal immediately. This is particularly useful in scenarios where you have an updating display (like with `end='\r'`) and need to see the changes in real-time.