```bash
#!/bin/zsh

default_command="pwd"

if [[ "$(basename "$PWD")" != "src" ]]; then
    echo "Error: This script must be run from the \"src\" directory."
    exit 1
fi

if [ $# -gt 0 ]; then
    command="$1"
else
    command="$default_command"
fi

for dir in */ ; do
    echo "Excuting command \"$command\" in diretory [./$dir]..."
    (cd "$dir" && eval "$command")
done
```