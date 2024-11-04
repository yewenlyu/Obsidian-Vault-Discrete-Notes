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
# if the remote branch has been deleted from the remote repository
git fetch --prune
```

```shell
### manually remove a specific remote-tracking branch reference
git branch -rd <remote-name>/<branch-name>
```

## Going Back in Time

> *From weakest to strongest*

### `git-clean` - Remove untracked files from the working tree

```shell
# dry run to show what files will be removed, recurse into directories
git clean -nd
```

```shell
# git clean will refuse to delete files or directories unless given -f
git clean -fd
```

### `git-restore` - Restore working tree files

#### `-W, --worktree, -S, --staged`

- *Default*, `--worktree`: only the **working tree** is restored
- `--staged`: only the **index** (**staging area**) is restored,
- `--staged --worktree`: effectively restoring the repository to the last commit


```shell
# restore all untracked files (worktree) to their last commited state
git restore .
```

```shell
# unstage files that have been added to the staging area
git restore --staged .
```

```shell
# restore the repository to the last commited state
git restore --staged --worktree .
```
### `git-revert` - Create a new commit that reverts other commits

```shell
# Create a new commit that undo the last commit
git revert HEAD
```

### `git-reset` - Reset current HEAD to the specified commit

```shell
# Moves the branch pointer back to a previous commit, keeping all changes in the staging area.
git reset --soft <commit>
```

```shell
# Default if no options specified. Resets the branch pointer to a specific commit and removes changes from the staging area but keeps them in the working directory.
git reset <commit>
git reset --mixed <commit>
```

```shell
# Completely resets the branch pointer, the staging area, and the working directory to a specified commit.
git reset --hard <commit>
```


> [!WARNING]
> Both `git restore --staged --worktree .` and `git reset --hard HEAD` effectively cleanup and restore the staging area and the working tree to the the last commit.
