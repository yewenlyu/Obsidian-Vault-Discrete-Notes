## Listing Branches

### List Local Branches

```shell
git branch
```

### List Remote Tracking Branches

```shell
git branch -r
```

### List All Branches

```shell
git branch -a
```

Use `-v, --verbose` option to show **SHA1** and **commit subject** for each line.

## Creating Branches

### Create a new branch based off a remote branch

```shell
git fetch <remote_name> <remote_branch_name>
git checkout -b <new_branch_name> <remote_name>/<remote_branch_name>
```
