# Linux Command Line & Shell Scripting Notes

## 1. Introduction to Linux Shell

### What is a Shell?

A **Shell** is a program that allows users to interact with the Linux Operating System through commands.

Think of it like:

* GUI → Click buttons and menus
* Shell → Type commands directly

The shell acts as a bridge between:

```text
User → Shell → Operating System
```

### Why Use Shell Instead of GUI?

#### Advantages

* Faster execution
* Uses fewer system resources
* Better control over the system
* Easy automation using scripts
* Preferred by system administrators and hackers

---

## 2. Learning Objectives

After completing this room, you should be able to:

* Interact with Linux Shell
* Use basic Linux commands
* Understand different Linux shells
* Write shell scripts
* Use variables, loops, and conditions
* Automate tasks

---

# 3. Connecting to the Lab

### SSH Credentials

```text
Username: user
Password: user@Tryhackme
IP: MACHINE_IP
```

### SSH Command

#### Purpose

Connect to a remote Linux machine.

#### General Syntax

```bash
ssh username@IP_Address
```

#### Example

```bash
ssh user@10.10.10.10
```

---

# 4. Basic Linux Shell Commands

---

## pwd

### Purpose

Displays the current working directory.

### General Syntax

```bash
pwd
```

### Example

```bash
user@tryhackme:~$ pwd
```

### Output

```bash
/home/user
```

---

## cd

### Purpose

Change current directory.

### General Syntax

```bash
cd directory_name
```

### Example

```bash
cd Desktop
```

### Result

```bash
user@tryhackme:~/Desktop$
```

---

## ls

### Purpose

Display contents of a directory.

### General Syntax

```bash
ls
```

### Example

```bash
ls
```

### Output

```bash
Desktop
Documents
Downloads
Pictures
Videos
```

---

## cat

### Purpose

Display contents of a file.

### General Syntax

```bash
cat filename
```

### Example

```bash
cat notes.txt
```

### Output

```text
This is line 1
This is line 2
```

---

## grep

### Purpose

Search for a word or pattern inside a file.

### General Syntax

```bash
grep keyword filename
```

### Example

```bash
grep THM dictionary.txt
```

### Output

```text
The flag is THM
```

---

# 5. Checking Current Shell

## echo $SHELL

### Purpose

Displays currently active shell.

### General Syntax

```bash
echo $SHELL
```

### Example

```bash
echo $SHELL
```

### Output

```bash
/bin/bash
```

---

# 6. Display Available Shells

## cat /etc/shells

### Purpose

Display all installed shells.

### General Syntax

```bash
cat /etc/shells
```

### Example

```bash
cat /etc/shells
```

### Output

```bash
/bin/bash
/bin/zsh
/bin/dash
/bin/sh
```

---

# 7. Switching Shells

## Open Another Shell

### Purpose

Switch to another shell temporarily.

### General Syntax

```bash
shell_name
```

### Example

```bash
zsh
```

### Output

```bash
tryhackme%
```

---

## Change Default Shell

### Purpose

Permanently change default shell.

### General Syntax

```bash
chsh -s shell_path
```

### Example

```bash
chsh -s /usr/bin/zsh
```

---

# 8. Types of Linux Shells

---

## Bash (Bourne Again Shell)

### Features

* Default shell in most Linux distributions
* Supports scripting
* Command history
* Tab completion
* Highly stable

### Useful Commands

#### Show Command History

```bash
history
```

---

## Fish (Friendly Interactive Shell)

### Features

* Beginner friendly
* Auto spell correction
* Syntax highlighting
* Better suggestions
* Theme customization

---

## Zsh (Z Shell)

### Features

* Advanced tab completion
* Auto correction
* Plugin support
* Highly customizable
* Supports scripting

---

# 9. Shell Comparison

| Feature             | Bash      | Fish     | Zsh       |
| ------------------- | --------- | -------- | --------- |
| Scripting           | Excellent | Limited  | Excellent |
| Auto Correction     | No        | Yes      | Yes       |
| Syntax Highlighting | No        | Yes      | Plugin    |
| Tab Completion      | Basic     | Advanced | Advanced  |
| Customization       | Basic     | Good     | Excellent |
| Beginner Friendly   | Medium    | High     | High      |

---

# 10. What is Shell Scripting?

### Definition

A shell script is a file containing multiple shell commands.

Instead of typing commands repeatedly, we can save them inside a script and execute them together.

### Benefits

* Automation
* Saves time
* Reduces mistakes
* Handles repetitive tasks

---

# 11. Creating a Bash Script

## Step 1: Create Script File

### Purpose

Create a script file.

### General Syntax

```bash
nano filename.sh
```

### Example

```bash
nano first_script.sh
```

---

## Step 2: Add Shebang

### Purpose

Tell Linux which interpreter should execute the script.

### Syntax

```bash
#!/bin/bash
```

### Example

```bash
#!/bin/bash
```

Every Bash script should begin with:

```bash
#!/bin/bash
```

---

# 12. Variables in Shell Scripting

## What is a Variable?

A variable stores data.

### Example Script

```bash
#!/bin/bash

echo "What's your name?"
read name

echo "Welcome, $name"
```

---

### Commands Used

#### echo

Displays text.

##### Syntax

```bash
echo text
```

##### Example

```bash
echo "Hello"
```

---

#### read

Accepts user input.

##### Syntax

```bash
read variable_name
```

##### Example

```bash
read name
```

---

# 13. Executing a Script

## chmod

### Purpose

Give execute permission.

### General Syntax

```bash
chmod +x filename.sh
```

### Example

```bash
chmod +x first_script.sh
```

---

## Execute Script

### Purpose

Run script.

### General Syntax

```bash
./filename.sh
```

### Example

```bash
./first_script.sh
```

### Output

```text
What's your name?
John
Welcome, John
```

---

# 14. Loops in Shell Scripting

## What is a Loop?

A loop repeats a task multiple times.

---

## For Loop

### Example Script

```bash
#!/bin/bash

for i in {1..10}
do
    echo $i
done
```

### Output

```text
1
2
3
...
10
```

---

### Loop Structure

```bash
for variable in range
do
    commands
done
```

---

# 15. Conditional Statements

## What is a Conditional Statement?

Used to make decisions.

Example:

```text
IF condition is true
    do something
ELSE
    do something else
```

---

## Example Script

```bash
#!/bin/bash

echo "Enter your name:"
read name

if [ "$name" = "Stewart" ]
then
    echo "Welcome Stewart! Here is the secret."
else
    echo "Access Denied."
fi
```

---

### Conditional Structure

```bash
if [ condition ]
then
    commands
else
    commands
fi
```

---

# 16. Comments in Scripts

## Purpose

Comments improve readability.

Comments are ignored during execution.

---

### Single-Line Comment

```bash
# This is a comment
```

---

### Example

```bash
#!/bin/bash

# Ask user for name
echo "Enter your name"

# Store user input
read name
```

---

# 17. Complete Locker Authentication Script

## Objective

Allow access only if:

```text
Username = John
Company = Tryhackme
PIN = 7385
```

---

## Script

```bash
#!/bin/bash

username=""
companyname=""
pin=""

for i in {1..3}
do
    if [ "$i" -eq 1 ]
    then
        echo "Enter Username:"
        read username

    elif [ "$i" -eq 2 ]
    then
        echo "Enter Company Name:"
        read companyname

    else
        echo "Enter PIN:"
        read pin
    fi
done

if [ "$username" = "John" ] && \
   [ "$companyname" = "Tryhackme" ] && \
   [ "$pin" = "7385" ]
then
    echo "Authentication Successful"
else
    echo "Authentication Denied"
fi
```

---

# 18. Become Root User

## sudo su

### Purpose

Switch to root account.

### General Syntax

```bash
sudo su
```

### Example

```bash
sudo su
```

### Output

```bash
root@tryhackme:/home/user#
```

---

# 19. Script Challenge Solution

The script contains empty quotes:

```bash
""
```

You must replace them with:

### Flag

```bash
thm-flag01-script
```

### Directory

```bash
/var/log
```

---

### Example

If script contains:

```bash
keyword=""
directory=""
```

Replace with:

```bash
keyword="thm-flag01-script"
directory="/var/log"
```

---
