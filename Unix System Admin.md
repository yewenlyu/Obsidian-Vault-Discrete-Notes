## Disk Usage

```bash
# Summarize disk usage for each file in the current direcotory, sort in descending order
du -sh * | sort -hr
```

## Searching

```shell
# Recursively zgrep a pattern in a log directory
find . -name "*.gz" -print0 | xargs -0 zgrep "pattern"
```