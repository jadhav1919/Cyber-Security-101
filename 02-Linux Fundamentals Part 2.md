# Linux Fundamentals Part 2

## Overview

This module builds on Linux Fundamentals Part 1 and introduces:

* Remote access using SSH
* Command flags and arguments
* Linux manual pages
* File and directory management
* File permissions
* User switching
* Important Linux directories

 

# SSH (Secure Shell)

## Definition

SSH (Secure Shell) is a protocol used to securely connect to and control remote Linux systems through the command line.

## Key Concepts

### Purpose of SSH

* Remote system administration
* Remote command execution
* Secure communication between devices

### How SSH Works

* User sends commands
* Commands are encrypted
* Data travels across the network securely
* Remote machine decrypts and executes commands

## SSH Syntax

```bash
ssh username@IP_ADDRESS
```

### Example

```bash
ssh tryhackme@10.10.10.10
```

## SSH Authentication

Requirements:

* Valid username
* Correct password
* Target machine IP address

## Important Points

* SSH traffic is encrypted.
* Password input is hidden while typing.
* Commands execute on the remote machine after login.

 

# Command Flags and Arguments

## Definition

Flags (switches) modify the behavior of commands.

### General Syntax

```bash
command -flag
```

or

```bash
command --option
```

 

## Using ls with Flags

### Default ls

```bash
ls
```

Displays visible files and directories.

### Show Hidden Files

```bash
ls -a
```

or

```bash
ls --all
```

Displays:

* Normal files
* Hidden files
* Hidden directories

### Human Readable Output

```bash
ls -lh
```

Displays file sizes in:

* KB
* MB
* GB

instead of raw bytes.

 

# Linux Manual Pages (man)

## Definition

Manual pages contain documentation for Linux commands.

## Syntax

```bash
man command
```

### Example

```bash
man ls
```

## Uses

* Learn command syntax
* View available flags
* Understand command behavior

## Navigation

| Key        | Action      |
| ---------- | ----------- |
| Up Arrow   | Scroll Up   |
| Down Arrow | Scroll Down |
| q          | Quit        |
| h          | Help        |

 

# File and Directory Management

## Creating Files

### touch

Creates an empty file.

```bash
touch filename
```

### Example

```bash
touch note
```

 

## Creating Directories

### mkdir

Creates a directory.

```bash
mkdir directory_name
```

### Example

```bash
mkdir mydirectory
```
 

## Removing Files

### rm

Deletes files.

```bash
rm filename
```

### Example

```bash
rm note
```

 

## Removing Directories

### Recursive Removal

```bash
rm -R directory
```

### Example

```bash
rm -R mydirectory
```

 Dangerous command. Deleted data is usually unrecoverable.

 

## Copying Files

### cp

Copies files.

```bash
cp source destination
```

### Example

```bash
cp note note2
```

 

## Moving Files

### mv

Moves or renames files.

```bash
mv source destination
```

### Move Example

```bash
mv myfile myfolder
```

### Rename Example

```bash
mv note2 note3
```

 

# Determining File Type

## file Command

Determines actual file type.

## Syntax

```bash
file filename
```

### Example

```bash
file note
```

Output:

```text
note: ASCII text
```

## Common File Types

| Output       | Meaning          |
| ------------ | ---------------- |
| ASCII text   | Text file        |
| JPEG image   | Image            |
| ELF          | Linux executable |
| PDF document | PDF file         |

 

# Linux Users and Groups

## Users

Individual accounts on a Linux system.

Examples:

* root
* tryhackme
* user2

## Groups

Collections of users sharing permissions.

Benefits:

* Easier permission management
* Shared access control

  
# Switching Users

## su Command

Switch user account.

### Syntax

```bash
su username
```

### Example

```bash
su user2
```

 

## Login Shell

### Syntax

```bash
su -l username
```

### Example

```bash
su -l user2
```

Benefits:

* Loads user environment
* Opens user's home directory
* Behaves like a real login

 

# Linux File Permissions

## Permission Types

| Symbol | Meaning |
| ------ | ------- |
| r      | Read    |
| w      | Write   |
| x      | Execute |

 

## Permission Structure

Example:

```text
rwxr-xr-x
```

Split into:

```text
rwx | r-x | r-x
Owner Group Others
```

 

## Numeric Permissions

| Permission | Value |
| ---------- | ----- |
| Read       | 4     |
| Write      | 2     |
| Execute    | 1     |

 

## Common Permission Values

| Symbolic  | Numeric | Meaning                  |
| --------- | ------- | ------------------------ |
| rwxrwxrwx | 777     | Full access for everyone |
| rwxr-xr-x | 755     | Owner full access        |
| rw-r--r-- | 644     | Owner read/write         |
| rwx------ | 700     | Owner only               |

 
## Permission Calculation

### Example

```text
rwx
```

Calculation:

```text
4 + 2 + 1 = 7
```

Therefore:

```text
rwxr-xr-x
```

becomes:

```text
755
```

 

## chmod Example

```bash
chmod 755 script.sh
```

```bash
chmod 700 secret.txt
```

```bash
chmod 644 notes.txt
```

 

# Viewing Permissions

## Long Listing Format

```bash
ls -l
```

### Example Output

```text
-rw-r--r-- 1 user group 0 file1
```

Important Columns:

| Section    | Meaning     |
| ---------- | ----------- |
| -rw-r--r-- | Permissions |
| user       | Owner       |
| group      | Group       |

 

# Important Linux Directories

## /etc

### Purpose

Stores system configuration files.

### Important Files

| File    | Purpose          |
| ------- | ---------------- |
| passwd  | User information |
| shadow  | Password hashes  |
| sudoers | Sudo permissions |

 
## /var

### Purpose

Stores variable data.

Examples:

* Logs
* Databases
* Application data

### Important Subdirectories

```text
/var/log
```

Stores log files.

 

## /root

### Purpose

Home directory of the root user.

```text
/root
```

 

## /tmp

### Purpose

Temporary storage.

Characteristics:

* Writable by all users
* Cleared after reboot
* Useful for scripts and temporary files

 

