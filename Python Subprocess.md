
The `subprocess` module in Python is a powerful tool to spawn and interact with additional processes, connect to their input/output/error pipes, and obtain their return codes. Below is a guide to the common arguments of `subprocess.run()` and related functions.

---

### **Basic Usage**

The most commonly used function is `subprocess.run()`.

```python
import subprocess

result = subprocess.run(["ls", "-l"], text=True, capture_output=True)
print(result.stdout)
```

---

### **Common Arguments in `subprocess.run()`**

Here's a list of the common arguments:

#### **1. `args`**

- **Description:** The command and its arguments to execute. Can be a list or a single string.
- **Type:** `list[str]` (preferred) or `str`
- **Example:**
    
    ```python
    subprocess.run(["ls", "-l"])  # List of command and arguments
    subprocess.run("ls -l", shell=True)  # Single string with `shell=True`
    ```
    

---

#### **2. `shell`**

- **Description:** If `True`, the command is executed through the shell (e.g., `/bin/sh` on Unix).
- **Type:** `bool`
- **Default:** `False`
- **Example:**
    
    ```python
    subprocess.run("echo $HOME", shell=True)
    ```
    

---

#### **3. `text` (or `universal_newlines`)**

- **Description:** If `True`, input and output are treated as strings (text mode). Otherwise, bytes.
- **Type:** `bool`
- **Default:** `False`
- **Example:**
    
    ```python
    subprocess.run(["echo", "hello"], text=True)
    ```
    

---

#### **4. `capture_output`**

- **Description:** If `True`, captures `stdout` and `stderr`. Cannot be used with `stdout` or `stderr` set to anything other than `None`.
- **Type:** `bool`
- **Default:** `False`
- **Example:**
    
    ```python
    result = subprocess.run(["ls", "-l"], capture_output=True, text=True)
    print(result.stdout)
    ```
    

---

#### **5. `stdout` and `stderr`**

- **Description:** Redirects the output streams (`stdout` and `stderr`). Can capture, discard, or redirect them to files.
- **Type:**
    - `subprocess.PIPE` (capture)
    - `subprocess.DEVNULL` (discard)
    - File object (redirect to file)
- **Default:** `None` (output to console)
- **Example:**
    
    ```python
    with open("output.txt", "w") as f:
        subprocess.run(["ls", "-l"], stdout=f)
    ```
    

---

#### **6. `stdin`**

- **Description:** Specifies the input stream for the subprocess.
- **Type:**
    - `subprocess.PIPE` (provide input)
    - `subprocess.DEVNULL` (discard)
    - File object (read from file)
- **Default:** `None`
- **Example:**
    
    ```python
    result = subprocess.run(["cat"], input="Hello, world!", text=True, stdin=subprocess.PIPE)
    print(result.stdout)
    ```
    

---

#### **7. `check`**

- **Description:** If `True`, raises a `subprocess.CalledProcessError` if the command exits with a non-zero return code.
- **Type:** `bool`
- **Default:** `False`
- **Example:**
    
    ```python
    try:
        subprocess.run(["false"], check=True)
    except subprocess.CalledProcessError as e:
        print(f"Command failed with return code {e.returncode}")
    ```
    

---

#### **8. `cwd`**

- **Description:** Sets the working directory for the subprocess.
- **Type:** `str` (path)
- **Default:** `None` (current working directory)
- **Example:**
    
    ```python
    subprocess.run(["ls"], cwd="/tmp")
    ```
    

---

#### **9. `env`**

- **Description:** Sets the environment variables for the subprocess. If `None`, inherits the parent environment.
- **Type:** `dict[str, str]` or `None`
- **Default:** `None`
- **Example:**
    
    ```python
    import os
    env = os.environ.copy()
    env["MY_VAR"] = "value"
    subprocess.run(["printenv", "MY_VAR"], env=env, text=True)
    ```
    

---

#### **10. `timeout`**

- **Description:** Sets the maximum time (in seconds) to wait for the command to complete. Raises `subprocess.TimeoutExpired` if the time exceeds.
- **Type:** `float` or `None`
- **Default:** `None` (no timeout)
- **Example:**
    
    ```python
    try:
        subprocess.run(["sleep", "5"], timeout=2)
    except subprocess.TimeoutExpired:
        print("Command timed out!")
    ```
    

---

#### **11. `close_fds`**

- **Description:** If `True`, closes file descriptors in the child process except `stdin`, `stdout`, and `stderr`.
- **Type:** `bool`
- **Default:** `True` (on Unix) or `False` (on Windows)
- **Example:**
    
    ```python
    subprocess.run(["ls"], close_fds=True)
    ```
    

---

#### **12. `bufsize`**

- **Description:** Specifies the buffering policy for the I/O streams.
- **Type:** `int`
    - `0`: Unbuffered
    - `1`: Line buffered
    - `-1`: Default (fully buffered)
- **Default:** `-1`
- **Example:**
    
    ```python
    subprocess.run(["ls"], bufsize=1, text=True)
    ```
    

---

#### **13. `executable`**

- **Description:** Specifies the executable to use instead of the first item in `args`.
- **Type:** `str` (path to executable)
- **Default:** None
- **Example:**
    
    ```python
    subprocess.run(["ls"], executable="/bin/ls")
    ```
    

---

### **Return Object**

The `subprocess.run()` function returns a `CompletedProcess` object.

#### Attributes of `CompletedProcess`:

- **`args`:** The list of arguments passed to the command.
- **`returncode`:** The return code of the process.
- **`stdout`:** Captured standard output (if `capture_output=True` or `stdout=subprocess.PIPE`).
- **`stderr`:** Captured standard error (if `capture_output=True` or `stderr=subprocess.PIPE`).

Example:

```python
result = subprocess.run(["echo", "Hello"], capture_output=True, text=True)
print(result.stdout)  # Output: Hello
print(result.returncode)  # Output: 0
```

---

### **Common Use Cases**

1. **Running a command and capturing its output:**
    
    ```python
    result = subprocess.run(["ls", "-l"], capture_output=True, text=True)
    print(result.stdout)
    ```
    
2. **Redirecting output to a file:**
    
    ```python
    with open("output.txt", "w") as f:
        subprocess.run(["ls", "-l"], stdout=f)
    ```
    
3. **Providing input to a command:**
    
    ```python
    result = subprocess.run(["cat"], input="Hello, world!", text=True, capture_output=True)
    print(result.stdout)
    ```
    
4. **Handling errors with `check`:**
    
    ```python
    try:
        subprocess.run(["false"], check=True)
    except subprocess.CalledProcessError as e:
        print(f"Command failed: {e}")
    ```
    
5. **Setting a timeout:**
    
    ```python
    try:
        subprocess.run(["sleep", "10"], timeout=2)
    except subprocess.TimeoutExpired:
        print("Command timed out!")
    ```
