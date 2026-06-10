# Linux Fundamentals Part 3

## Overview

This module focuses on practical Linux administration and daily-use utilities, including:

* Text editors (Nano and Vim)
* Downloading and transferring files
* Running a web server with Python
* Process management
* Background and foreground jobs
* System services and systemctl
* Task automation with Cron
* Package management using APT
* Linux logging


# Terminal Text Editors

## Key Concepts

Text editors allow users to create, view, and modify files directly from the terminal.

 

## Nano

### Definition

Nano is a beginner-friendly terminal text editor.

### Creating or Editing a File

```bash
nano filename
```

### Example

```bash
nano notes.txt
```

### Common Nano Shortcuts

| Shortcut | Function    |
| -------- | ----------- |
| Ctrl + X | Exit        |
| Ctrl + O | Save File   |
| Ctrl + W | Search Text |
| Ctrl + K | Cut Line    |
| Ctrl + U | Paste       |
| Ctrl + G | Help        |

### Important Points

* Easy for beginners.
* Installed on most Linux systems.
* Suitable for quick file edits.

 

## Vim

### Definition

Vim is a powerful and advanced text editor.

### Advantages

* Highly customizable
* Syntax highlighting
* Fast editing
* Available on most Linux systems

### Important Points

* Steeper learning curve.
* Popular among system administrators and developers.

 

# Downloading Files

## wget

### Definition

Downloads files from websites using HTTP or HTTPS.

### Syntax

```bash
wget URL
```

### Example

```bash
wget https://example.com/file.txt
```

### Uses

* Download scripts
* Download tools
* Download images
* Download files from web servers

 

# Secure File Transfer

## SCP (Secure Copy)

### Definition

Securely transfers files between systems using SSH.

### Advantages

* Encrypted transfer
* Authentication through SSH
* Secure remote file copying

 

## Local → Remote

### Syntax

```bash
scp localfile user@IP:/destination/path
```

### Example

```bash
scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt
```

 

## Remote → Local

### Syntax

```bash
scp user@IP:/remote/file localfile
```

### Example

```bash
scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt
```

 

# Hosting Files with Python

## Python HTTP Server

### Definition

A lightweight web server built into Python.

### Start Server

```bash
python3 -m http.server
```

### Default Port

```text
8000
```

### Example

```bash
python3 -m http.server
```

Output:

```text
Serving HTTP on 0.0.0.0 port 8000
```
 

## Download Hosted Files

### Syntax

```bash
wget http://IP:8000/filename
```

### Example

```bash
wget http://10.10.10.10:8000/file.txt
```

### Important Points

* Serves files from the current directory.
* Useful during penetration testing.
* Useful for transferring tools to compromised systems.

 

# Process Management

## What is a Process?

A process is a running program managed by the Linux kernel.

Every process has:

* PID (Process ID)
* Owner
* Status
* Resource usage

 

# Viewing Processes

## ps

Displays running processes.

### Current User Processes

```bash
ps
```

### All Processes

```bash
ps aux
```

 

## top

Displays real-time process information.

### Syntax

```bash
top
```

### Information Displayed

* CPU usage
* Memory usage
* Running processes
* Process IDs

 

# Process Signals

## kill Command

Used to send signals to processes.

### Syntax

```bash
kill PID
```

### Example

```bash
kill 1337
```
 

## Important Signals

| Signal  | Purpose              |
| ------- | -------------------- |
| SIGTERM | Gracefully terminate |
| SIGKILL | Force terminate      |
| SIGSTOP | Pause process        |

### Recommended Signal

```text
SIGTERM
```

Allows cleanup before termination.

 

# Process Hierarchy

## systemd

### Definition

The primary process manager in Ubuntu Linux.

### Characteristics

* Starts during boot
* Manages services
* Creates child processes

### Important Fact

```text
systemd
```

is one of the first processes started after boot.

 

# Managing Services

## systemctl

### Definition

Controls services managed by systemd.

### Syntax

```bash
systemctl [option] service
```

 

## Start Service

```bash
systemctl start apache2
```

 

## Stop Service

```bash
systemctl stop apache2
```

 

## Enable Service at Boot

```bash
systemctl enable apache2
```

 

## Disable Service

```bash
systemctl disable apache2
```

 

## Service Status

```bash
systemctl status apache2
```

 

## Common Options

| Command | Purpose               |
| ------- | --------------------- |
| start   | Start service         |
| stop    | Stop service          |
| enable  | Start on boot         |
| disable | Prevent start on boot |
| status  | View status           |

 

# Background and Foreground Processes

## Background Process

Runs without occupying the terminal.

### Example

```bash
echo "Hello" &
```

### Result

Process runs in the background.

 

## Suspend Process

### Shortcut

```text
Ctrl + Z
```

### Function

Pauses and backgrounds the process.

 

## Foreground Process

Bring a backgrounded process back.

### Command

```bash
fg
```

 

# Cron Jobs

## Definition

Cron automates tasks on Linux systems.

Managed by:

```text
cron
```

 

## Edit Cron Jobs

```bash
crontab -e
```

 

## Cron Format

```text
MIN HOUR DOM MON DOW CMD
```

| Field | Meaning      |
| ----- | ------------ |
| MIN   | Minute       |
| HOUR  | Hour         |
| DOM   | Day of Month |
| MON   | Month        |
| DOW   | Day of Week  |
| CMD   | Command      |

 

## Example

```bash
0 */12 * * * cp -R /home/cmnatic/Documents /var/backups/
```

### Meaning

Every 12 hours:

```text
Copy Documents folder to backups
```

 

## Wildcard (*)

### Meaning

Any value.

Example:

```text
*
```

means:

```text
Every possible value
```
 

# Package Management

## APT

### Definition

Advanced Package Tool (APT) manages software installation and updates.

 

## Update Repositories

```bash
sudo apt update
```

 

## Install Software

```bash
sudo apt install package-name
```

### Example

```bash
sudo apt install sublime-text
```

 

## Remove Software

```bash
sudo apt remove package-name
```

### Example

```bash
sudo apt remove sublime-text
```

 

# Repositories

## Definition

Repositories store software packages available for installation.

### Benefits

* Easy installation
* Easy updates
* Trusted software sources

 

## Add Repository

```bash
sudo add-apt-repository repository
```

 

## Repository Files

Common location:

```text
/etc/apt/sources.list.d/
```

 

# GPG Keys

## Definition

GPG keys verify software authenticity.

### Purpose

Ensures:

* Software integrity
* Trusted developers
* Protection against tampered packages

 

# Linux Logs

## Definition

Logs record system and application activity.

### Log Directory

```text
/var/log
```

 

# Common Log Types

## Access Logs

Record:

* Website visits
* IP addresses
* Requested resources

 

## Error Logs

Record:

* Application errors
* Server failures
* Service issues

 

# Important Services with Logs

## Apache2

Web server logs.

Common files:

```text
/var/log/apache2/access.log
```

```text
/var/log/apache2/error.log
```

 

## Fail2Ban

Monitors:

* Brute-force attacks
* Authentication failures

 

## UFW

Firewall logs.

Records:

* Allowed connections
* Blocked connections

 

# Process / Workflow

## SCP Transfer Workflow

```text
Local Machine
      |
      v
      SCP
      |
      v
Encrypted SSH Connection
      |
      v
Remote Machine
```

---

## Python Web Server Workflow

```text
Python HTTP Server
        |
        v
Port 8000
        |
        v
Browser / wget
        |
        v
Download File
```

---

## Process Lifecycle

```text
System Boot
      |
      v
systemd
      |
      v
Service / Application
      |
      v
Process (PID)
```

---

## Cron Workflow

```text
Crontab
   |
   v
Cron Service
   |
   v
Scheduled Execution
```

---

# Commands / Syntax

## Text Editing

```bash
nano file.txt
```

```bash
vim file.txt
```

---

## Downloading Files

```bash
wget URL
```

---

## File Transfer

```bash
scp file user@IP:/path
```

```bash
scp user@IP:/path/file localfile
```

---

## Python Web Server

```bash
python3 -m http.server
```

---

## Process Management

```bash
ps
```

```bash
ps aux
```

```bash
top
```

```bash
kill PID
```

---

## Service Management

```bash
systemctl start service
```

```bash
systemctl stop service
```

```bash
systemctl enable service
```

```bash
systemctl disable service
```

```bash
systemctl status service
```

---

## Cron

```bash
crontab -e
```

---

## Package Management

```bash
sudo apt update
```

```bash
sudo apt install package
```

```bash
sudo apt remove package
```

---

