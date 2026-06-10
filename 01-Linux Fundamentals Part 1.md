# Linux Fundamentals - Part 1

# 1. Introduction to Linux

Linux is an **Operating System (OS)** like:

* Windows
* macOS
* Android

It is one of the most widely used operating systems in the world.

Linux powers:

* Websites
* Android phones
* Smart devices
* Servers
* Supercomputers
* Traffic systems
* Car entertainment systems


# 2. Linux Distributions (Flavours)

Linux has many different versions called **Distributions (Distros)**.

Popular Linux distributions:

* Ubuntu
* Debian
* Kali Linux
* Parrot OS
* Fedora

For this room, Ubuntu is used.

### Important Note

Ubuntu Server can run with only:

```bash
512MB RAM
```
# Important Notes

## Linux First Release

* First Linux release year: **1991**

Created by:

* Linus Torvalds

# 3. Terminal Basics

Linux is commonly controlled using the **Terminal**.

The terminal is text-based.

Example terminal:

```bash
tryhackme@linux1:~$
```

# 4. Basic Linux Commands

## `echo`

Used to display text.

### Syntax

```bash
echo text
```

### Examples

```bash
echo Hello
```

Output:

```bash
Hello
```

```bash
echo "Hello Friend!"
```

Output:

```bash
Hello Friend!
```

## `whoami`

Shows the currently logged-in user.

### Syntax

```bash
whoami
```

### Example

```bash
whoami
```

Output:

```bash
tryhackme
```


# 5. File System Navigation

## Important Commands

| Command | Full Form               | Purpose              |
| ------- | ----------------------- | -------------------- |
| `ls`    | listing                 | Show files/folders   |
| `cd`    | change directory        | Move between folders |
| `cat`   | concatenate             | View file contents   |
| `pwd`   | print working directory | Show current path    |


## `ls` - List Files

Shows files and folders in the current directory.

### Syntax

```bash
ls
```

### Example

```bash
ls
```

Output:

```bash
Documents  Pictures  Notes
```

## `cd` - Change Directory

Used to move into another folder.

### Syntax

```bash
cd foldername
```

### Example

```bash
cd Pictures
```

## `cat` - View File Contents

Displays the content of a file.

### Syntax

```bash
cat filename
```

### Example

```bash
cat todo.txt
```

Output:

```bash
Here's something important for me to do later!
```

## `pwd` - Print Working Directory

Shows the full path of the current directory.

### Syntax

```bash
pwd
```

### Example

```bash
pwd
```

Output:

```bash
/home/ubuntu/Documents
```

# 6. Finding Files with `find`

The `find` command searches for files and folders.

---

## Find a Specific File

### Syntax

```bash
find -name filename
```

### Example

```bash
find -name passwords.txt
```

Output:

```bash
./folder1/passwords.txt
```

---

## Find All `.txt` Files

### Syntax

```bash
find -name *.txt
```

### Example Output

```bash
./folder1/passwords.txt
./Documents/todo.txt
```

---

# 7. Searching with `grep`

`grep` searches inside files for specific text.

---

## Basic `grep`

### Syntax

```bash
grep "text" filename
```

### Example

```bash
grep "81.143.211.90" access.log
```

Output:

```bash
81.143.211.90 - - [25/Mar/2021]
```

---

## Recursive Search with `grep -R`

Searches all files and subdirectories.

### Syntax

```bash
grep -R "text" directory
```

### Example

```bash
grep -R "PRETTY_NAME" /etc/
```

Output:

```bash
/etc/os-release:PRETTY_NAME="Ubuntu"
```

---

# 8. Linux Operators

| Operator | Purpose                        |
| -------- | ------------------------------ |
| `&`      | Run command in background      |
| `&&`     | Run multiple commands together |
| `>`      | Overwrite file output          |
| `>>`     | Append output to file          |

---

## `&` Operator

Runs commands in the background.

### Example

```bash
command &
```

---

## `&&` Operator

Runs the second command only if the first command succeeds.

### Example

```bash
command1 && command2
```

---

## `>` Operator

Overwrites file contents.

### Example

```bash
echo hey > welcome
```

Check file:

```bash
cat welcome
```

Output:

```bash
hey
```

---

## `>>` Operator

Appends text to a file without removing old content.

### Example

```bash
echo hello >> welcome
```

Output:

```bash
hey
hello
```

---
