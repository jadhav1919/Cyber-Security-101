# Windows Command Line (CMD) Fundamentals

## Overview

The Command Line Interface (CLI) allows users to interact with Windows using commands instead of a graphical interface (GUI).

Although GUI is easier for beginners, CLI becomes faster and more efficient once mastered.

---

# Why Use Command Line?

## Advantages of CLI

### Faster Operations

Instead of multiple mouse clicks:

```cmd
ipconfig
```

can instantly display network information.

---

### Lower Resource Usage

CLI consumes:

* Less RAM
* Less CPU
* Less storage

Useful for:

* Older systems
* Servers
* Cloud machines

---

### Automation

Commands can be placed into:

* Batch files (.bat)
* Scripts

To automate repetitive tasks.

---

### Remote Management

CLI works well with:

```text
SSH
```

Used to manage:

* Servers
* Routers
* IoT Devices

---

# Basic System Commands

## View Environment Variables

### Command

```cmd
set
```

### Purpose

Displays:

* System variables
* User variables
* PATH information

---

## Check Windows Version

### Command

```cmd
ver
```

### Purpose

Displays Windows version.

Example:

```cmd
Microsoft Windows [Version 10.0.17763.1821]
```

---

## View System Information

### Command

```cmd
systeminfo
```

### Purpose

Displays:

* Hostname
* OS Version
* Processor
* RAM
* Network Information

---

## View Long Output Page-by-Page

### Command

```cmd
command | more
```

Example:

```cmd
systeminfo | more
```

---

## Clear Screen

### Command

```cmd
cls
```

### Purpose

Clears Command Prompt window.

---

## Get Help

### Command

```cmd
help
```

or

```cmd
command /?
```

Example:

```cmd
ipconfig /?
```

---

# Network Commands

## IP Configuration

### Command

```cmd
ipconfig
```

### Purpose

Displays:

* IP Address
* Subnet Mask
* Default Gateway

---

### Example Output

```text
IPv4 Address: 10.10.230.237
Subnet Mask: 255.255.0.0
Default Gateway: 10.10.0.1
```

---

## Detailed Network Information

### Command

```cmd
ipconfig /all
```

### Displays

* MAC Address
* DHCP Information
* DNS Servers
* Lease Information

---

# Ping

## Definition

Tests connectivity between your machine and another host.

---

## Command

```cmd
ping example.com
```

---

## Purpose

Checks:

* Network connectivity
* Host availability
* Round-trip time

---

## Diagram

```text
Your PC
   |
 Ping Request
   |
Target Server
   |
 Ping Reply
```

---

# Traceroute

## Command

```cmd
tracert example.com
```

---

## Purpose

Shows every router between:

```text
Source → Destination
```

---

## Example

```text
PC
 |
Router 1
 |
Router 2
 |
Router 3
 |
Target Server
```

---

# NSLookup

## Definition

Queries DNS servers.

---

## Command

```cmd
nslookup example.com
```

---

## Purpose

Converts:

```text
Domain Name
     ↓
IP Address
```

---

## Use Custom DNS Server

```cmd
nslookup example.com 1.1.1.1
```

---

# Netstat

## Definition

Displays network connections and listening ports.

---

## Basic Command

```cmd
netstat
```

---

## Purpose

Shows:

* Active connections
* Protocols
* Connection state

---

## Advanced Command

```cmd
netstat -abon
```

---

## Flags

| Flag | Purpose                |
| ---- | ---------------------- |
| -a   | Show all connections   |
| -b   | Show executable        |
| -o   | Show PID               |
| -n   | Show numeric addresses |

---

## Example

```text
Port 22
 |
sshd.exe
 |
PID 2116
```

---

# File and Directory Management

## Current Directory

### Command

```cmd
cd
```

### Purpose

Displays current location.

---

# List Files and Folders

### Command

```cmd
dir
```

---

## Useful Options

### Show Hidden Files

```cmd
dir /a
```

---

### Show Subdirectories

```cmd
dir /s
```

---

# Display Folder Structure

### Command

```cmd
tree
```

---

## Example

```text
C:
|
├── Desktop
├── Documents
├── Downloads
└── Pictures
```

---

# Change Directory

## Move Into Folder

```cmd
cd Documents
```

---

## Move Up One Level

```cmd
cd ..
```

---

# Create Directory

## Command

```cmd
mkdir backup
```

---

## Purpose

Creates folder.

---

# Remove Directory

## Command

```cmd
rmdir backup
```

---

## Purpose

Deletes folder.

---

# File Operations

## View File Content

### Command

```cmd
type file.txt
```

---

## View Large File

### Command

```cmd
more file.txt
```

---

# Copy Files

## Command

```cmd
copy file1.txt file2.txt
```

---

## Purpose

Creates duplicate file.

---

# Move Files

## Command

```cmd
move file.txt destination
```

---

## Example

```cmd
move report.txt ..
```

Moves file to parent directory.

---

# Delete Files

## Command

```cmd
del file.txt
```

or

```cmd
erase file.txt
```

---

# Wildcards

## Copy All Markdown Files

```cmd
copy *.md C:\Markdown
```

---

## Meaning

```text
* = Any number of characters
```

---

# Process Management

## List Running Processes

### Command

```cmd
tasklist
```

---

## Displays

* Process Name
* PID
* Memory Usage

---

# Filter Process

## Command

```cmd
tasklist /FI "imagename eq sshd.exe"
```

---

## Purpose

Displays only:

```text
sshd.exe
```

processes.

---

# Kill Process

## Command

```cmd
taskkill /PID 4567
```

---

## Purpose

Terminates process.

---

# Shutdown Commands

## Shutdown System

```cmd
shutdown /s
```

---

## Restart System

```cmd
shutdown /r
```

---

## Abort Shutdown

```cmd
shutdown /a
```

---

# Additional Useful Commands

## Check Disk

```cmd
chkdsk
```

### Purpose

Checks disk for:

* Errors
* Bad sectors

---

## Driver Information

```cmd
driverquery
```

### Purpose

Displays installed drivers.

---

## System File Checker

```cmd
sfc /scannow
```

### Purpose

Scans and repairs corrupted system files.

---

