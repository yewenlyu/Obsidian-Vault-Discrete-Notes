```shell
# Recursively zgrep a pattern in a log directory
find . -name "*.gz" -print0 | xargs -0 zgrep "pattern"
```