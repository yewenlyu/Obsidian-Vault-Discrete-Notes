In Unix systems, **hard links** and **soft links** (also known as symbolic links) are used to reference files and directories. Here’s a detailed introduction to both:

## Hard Links

### Definition:

A **hard link** is a *direct reference* to the physical data on the disk. It is essentially another name for an existing file.

### Characteristics:

1. **Same Inode Number:** Hard links share the same inode number as the original file. The inode contains metadata about the file, including its physical location on the disk.
2. **Data Independence:** The file data remains intact as long as there is at least one hard link pointing to it. Deleting the original file does not remove the data of the original file as long as a hard link exists.
3. **Cannot Cross Filesystems:** Hard links can only be created within the same filesystem.
4. **No Links to Directories:** Generally, hard links to directories are not allowed to prevent filesystem loops and complexities in navigation.

### Usage

  ```sh
  # Creating a hard link
  ln existing_file new_hard_link
  ```

### Hard Links in Unix File System

#### Inode

In Unix-like operating systems, files are stored in a filesystem that uses **inodes**. An **inode** is a data structure that stores information about a file or directory, such as its size, ownership, permissions, and the location of its data blocks on the disk.

#### File Reference

Fire reference

A **file reference** refers to any reference to a file's **inode**. This can include **directory entries** (file names) and **hard links**.

The filesystem uses directory entries to map file names to their corresponding inodes. When you create a file, a **directory entry** is created that points to the file's **inode**. The **inode**, in turn, points to the actual data blocks on the disk.

#### Creating a Hard Link

When you create a **hard link**, you are essentially creating another **directory entry** that points to the same inode as the original file. This means that both the _original file name_ and the _hard link name_ refer to the same underlying data.

#### Data Persistence with Hard Links

##### Deleting the Original File:

When you delete a file (using the `rm` command, for example), you are actually removing a **directory entry** that points to the **inode** of the file. The operating system decrements the **reference count** of the **inode** by one.

##### Data Survival:

As long as the **reference count** of an **inode** is greater than zero, the **inode** and its associated data blocks remain intact on the disk. The data is only actually deleted when the **reference count** drops to zero, meaning no directory entries point to that inode anymore.

## Soft Links (Symbolic Links)

### Definition:
- A **soft link** (or **symbolic link**) is a special type of file that points to another file or directory by name. It is a pointer or shortcut to the original file.

### Characteristics:
1. **Different Inode Number:** Soft links have a different inode number from the original file. They contain the pathname of the target file.
2. **Path Dependency:** If the original file is deleted, the soft link becomes a dangling link, pointing to a non-existent file.
3. **Cross Filesystems:** Soft links can span across different filesystems.
4. **Can Link to Directories:** Soft links can reference directories as well as files.

### Usage

  ```sh
  # Creating a soft link
  ln -s target_file symbolic_link
  ```

```sh
# Check the physical path of current working directory
pwd -P
```

## Key Differences

| Feature               | Hard Link                               | Soft Link                                            |
| --------------------- | --------------------------------------- | ---------------------------------------------------- |
| Inode Number          | Same as the original file               | Different from the original file                     |
| Data Availability     | Data remains as long as one link exists | Data is inaccessible if the original file is deleted |
| Filesystem Limitation | Must be on the same filesystem          | Can cross filesystems                                |
| Directory Linking     | Generally not allowed                   | Allowed                                              |

## Practical Considerations

- **Performance:** Hard links are more efficient since they directly reference the data blocks.
- **Flexibility:** Soft links offer more flexibility, especially when dealing with directory structures or across different filesystems.
- **Backup and Restore:** Care should be taken with backups to ensure links are properly preserved and restored.