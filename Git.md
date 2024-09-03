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

## Deleting Branches

### Delete a Local Branch

```shell
# delete a branch that has already been merged
git branch -d branch_name
```

```shell
# forcefully delete a branch, regardless of its merge status
git branch -D branch_name
```

### Delete a Remote Branch

```shell
git push origin --delete branch_name
```

When you delete a remote branch, Git automatically removes its tracking reference in your local repository.

### Delete a Remote Tracking Branch Only

```shell
### if the remote branch has been deleted from the remote repository
git fetch --prune
```

```shell
### manually remove a specific remote-tracking branch reference
git branch -rd <remote-name>/<branch-name>
```