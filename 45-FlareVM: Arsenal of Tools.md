
# FLARE-VM (Forensics, Logic Analysis, and Reverse Engineering)

## What is FLARE-VM?

**FLARE-VM (Forensics, Logic Analysis, and Reverse Engineering)** is a **Windows-based malware analysis and reverse engineering environment** developed by **Mandiant (formerly FireEye FLARE Team)**.

It comes preloaded with hundreds of security tools used by:

* Malware Analysts
* Reverse Engineers
* Digital Forensic Investigators
* Incident Responders
* Penetration Testers

Instead of installing dozens of tools manually, FLARE-VM provides a ready-to-use Windows lab.

# Why Do We Need FLARE-VM?

Analyzing malware on your personal computer is dangerous.

Malware can:

* Encrypt your files
* Steal passwords
* Install backdoors
* Spread across your network
* Damage your operating system

FLARE-VM provides an **isolated Windows environment** where suspicious files can be analyzed safely.

---------

# FLARE-VM Tools Overview

## What is FLARE-VM?

**FLARE-VM (Forensics, Logic Analysis, and Reverse Engineering)** is a **Windows-based malware analysis and reverse engineering environment** developed by the **FLARE Team (FireEye/Mandiant)**.

It contains hundreds of pre-installed tools used for:

* Malware Analysis
* Reverse Engineering
* Digital Forensics
* Incident Response
* Penetration Testing
* Threat Hunting

Instead of installing each tool manually, FLARE-VM provides a ready-to-use Windows security lab.


# Tool Categories in FLARE-VM

FLARE-VM groups its tools into different categories based on their purpose.


# 1. Reverse Engineering & Debugging

## Purpose

Used to understand **how a program works internally** by examining its code.

Debugging allows analysts to execute programs **step-by-step**, inspect memory, registers, variables, and identify malicious behavior.

### Common Tools

| Tool             | Purpose                                                    |
| ---------------- | ---------------------------------------------------------- |
| **Ghidra**       | Open-source reverse engineering suite developed by the NSA |
| **x64dbg**       | Windows debugger for 32-bit and 64-bit executables         |
| **OllyDbg**      | Assembly-level debugger for Windows programs               |
| **Radare2**      | Open-source reverse engineering framework                  |
| **Binary Ninja** | Commercial disassembler and decompiler                     |
| **PEiD**         | Detects packers, cryptors, and compilers                   |

### Common Uses

* Reverse engineering malware
* Debugging executables
* Bypassing anti-debugging
* Understanding program logic


# 2. Disassemblers & Decompilers

## Purpose

Convert machine code into a readable format.

* **Disassembler** → Machine code → Assembly Language
* **Decompiler** → Machine code → High-level language (approximation)

### Common Tools

| Tool                    | Purpose                                         |
| ----------------------- | ----------------------------------------------- |
| **CFF Explorer**        | Analyze and edit Portable Executable (PE) files |
| **Hopper Disassembler** | Disassembler, debugger, and decompiler          |
| **RetDec**              | Open-source machine code decompiler             |

### Common Uses

* Analyze PE structure
* Study malware logic
* Inspect imported functions
* Recover source-like code


# 3. Static & Dynamic Analysis

## Purpose

Analyze malware **before** and **during** execution.

### Static Analysis

Examines files **without running them**.

Examples

* Strings
* Imports
* Sections
* Metadata
* Resources

### Dynamic Analysis

Runs malware inside an isolated environment to observe behavior.

Examples

* Process creation
* Registry modifications
* File activity
* Network connections

### Common Tools

| Tool                     | Purpose                                 |
| ------------------------ | --------------------------------------- |
| **Process Hacker**       | Process viewer and memory editor        |
| **PEview**               | Analyze PE file structure               |
| **Dependency Walker**    | Display DLL dependencies                |
| **Detect It Easy (DIE)** | Detect packers, compilers, and cryptors |


# 4. Forensics & Incident Response

## Purpose

Collect, preserve, and analyze digital evidence after a cyber incident.

### Common Tools

| Tool           | Purpose                               |
| -------------- | ------------------------------------- |
| **Volatility** | Memory forensics framework            |
| **Rekall**     | Memory analysis framework             |
| **FTK Imager** | Disk acquisition and forensic imaging |

### Common Uses

* Memory analysis
* Disk imaging
* Incident investigations
* Evidence preservation


# 5. Network Analysis

## Purpose

Monitor, analyze, and troubleshoot network traffic.

### Common Tools

| Tool          | Purpose                                  |
| ------------- | ---------------------------------------- |
| **Wireshark** | Packet capture and protocol analysis     |
| **Nmap**      | Network scanning and service discovery   |
| **Netcat**    | Read/write data over network connections |

### Common Uses

* Packet analysis
* Port scanning
* Traffic inspection
* Network troubleshooting


# 6. File Analysis

## Purpose

Inspect file contents, binary data, and file structures.

### Common Tools

| Tool            | Purpose                          |
| --------------- | -------------------------------- |
| **FileInsight** | Binary file analysis and editing |
| **Hex Fiend**   | Lightweight hex editor           |
| **HxD**         | Hex editor for binary files      |

### Common Uses

* Inspect binary files
* Modify file contents
* Analyze malware payloads
* Recover hidden data


# 7. Scripting & Automation

## Purpose

Automate repetitive security tasks.

### Common Tools

| Tool                  | Purpose                                |
| --------------------- | -------------------------------------- |
| **Python**            | Automation and scripting               |
| **PowerShell Empire** | PowerShell post-exploitation framework |

### Common Uses

* Automation
* Malware scripting
* Incident response scripts
* Custom forensic tools


# 8. Sysinternals Suite

## Purpose

Advanced Windows system monitoring and troubleshooting tools developed by Microsoft.

### Common Tools

| Tool                          | Purpose                                                            |
| ----------------------------- | ------------------------------------------------------------------ |
| **Autoruns**                  | Shows startup programs and persistence mechanisms                  |
| **Process Explorer**          | Advanced process viewer                                            |
| **Process Monitor (Procmon)** | Monitors file, registry, process, and thread activity in real time |

### Common Uses

* Detect persistence
* Monitor malware behavior
* Investigate suspicious processes
* Troubleshoot Windows issues

-----------

# Investigation Tools Overview

| Tool                          | Primary Purpose                       | Investigation Value                                   |
| ----------------------------- | ------------------------------------- | ----------------------------------------------------- |
| **Procmon (Process Monitor)** | Monitor Windows activity in real time | Tracks file, registry, process, and thread activity   |
| **Process Explorer**          | Advanced process viewer               | Shows parent-child processes, DLLs, process paths     |
| **HxD**                       | Hex editor                            | Examine and modify binary files                       |
| **Wireshark**                 | Network analyzer                      | Capture and inspect network traffic                   |
| **CFF Explorer**              | PE file analyzer                      | View PE information, generate hashes, inspect headers |
| **PEStudio**                  | Static malware analysis               | Analyze executables without running them              |
| **FLOSS**                     | String extraction                     | Extract and de-obfuscate hidden strings from malware  |



# 1. Process Monitor (Procmon)

## Purpose

**Process Monitor (Procmon)** is a Microsoft Sysinternals tool that records **real-time Windows system activity**.

It monitors:

* File System activity
* Registry activity
* Process creation
* Thread creation
* DLL loading

Unlike Task Manager, Procmon records everything occurring inside Windows.



## What Procmon Can Monitor

* File reads
* File writes
* Registry reads
* Registry writes
* Process creation
* Thread creation
* DLL loading
* Network-related activity (limited)


## Investigation Value

Procmon helps investigators determine:

* Which files malware creates
* Which registry keys are modified
* Which processes malware starts
* Which DLLs are loaded
* Whether malware establishes persistence



## Example

Suppose Procmon records:

```
Process Name:
lsass.exe

Operation:
ReadFile

Path:
C:\Windows\System32\lsasrv.dll

Result:
SUCCESS
```

### Explanation

This means:

* Process: **lsass.exe**
* Action: Read a file
* File accessed: **lsasrv.dll**
* Operation succeeded

Normally this is expected because:

**LSASS (Local Security Authority Subsystem Service)** handles:

* User authentication
* Password verification
* Security policies


## Malware Investigation

Attackers often target LSASS for:

* Credential Dumping
* Password extraction
* NTLM hash dumping

Example tools:

* Mimikatz
* Cobalt Strike
* Nanodump

If Procmon shows unusual access to **lsass.exe**, investigate further.


## Common Uses

* Malware analysis
* Troubleshooting
* Incident response
* Registry monitoring
* Persistence detection



# 2. Process Explorer (Procexp)

## Purpose

Process Explorer is an advanced version of Windows Task Manager.

It provides detailed information about:

* Running processes
* Parent-child relationships
* DLLs loaded
* Process paths
* Handles
* CPU and memory usage



## What It Shows

* Process ID (PID)
* Parent Process ID (PPID)
* Executable path
* Loaded DLLs
* Digital signature
* Command line
* User account



## Parent-Child Relationship

Example

```
explorer.exe
    |
    +---- winword.exe
              |
              +---- powershell.exe
                        |
                        +---- cmd.exe
```

This hierarchy helps identify suspicious behavior.



## Investigation Value

Attackers commonly use:

* Word documents
* LNK shortcuts
* ISO files
* PDFs

These may spawn:

```
WINWORD.EXE
      ↓
powershell.exe
      ↓
cmd.exe
      ↓
payload.exe
```

Process Explorer clearly shows this chain.



## Common Uses

* Process investigation
* Malware behavior
* Parent-child analysis
* DLL inspection
* Handle analysis



# 3. HxD

## Purpose

HxD is a professional **Hex Editor**.

It allows investigators to inspect files at the byte level.


## What is Hex?

Computers store files as binary.

Hex editors display binary in hexadecimal.

Example

```
4D 5A 90 00
```

ASCII view

```
MZ..
```



## MZ Header

Every Windows executable begins with

```
4D 5A
```

ASCII:

```
MZ
```

This is called the **DOS Header**.

If a file named:

```
invoice.pdf
```

starts with

```
4D 5A
```

it is actually an executable.



## Investigation Value

HxD helps identify:

* Fake file extensions
* Hidden executables
* Embedded malware
* Corrupted files
* Binary modifications



## Data Inspector

HxD includes **Data Inspector**, which displays selected bytes as:

* Integer
* Float
* Double
* Hex
* Binary

This simplifies binary analysis.



## Common Uses

* File signature analysis
* Binary editing
* Malware inspection
* Data recovery
* File repair



# 4. CFF Explorer

## Purpose

CFF Explorer analyzes **Portable Executable (PE)** files.

It provides detailed information about Windows executables.



## Displays

* PE Header
* Imports
* Exports
* Sections
* Resources
* Digital signatures
* Hashes



## Investigation Value

It can generate:

* MD5
* SHA1
* SHA256

Hashes help:

* Verify integrity
* Detect tampering
* Compare malware samples



## Example

```
File:
cryptominer.bin

Architecture:
64-bit

Created:
23 September 2024

SHA1:
...

MD5:
...
```

Investigators can compare these hashes with:

* VirusTotal
* MalwareBazaar
* Internal IOC databases



## Common Uses

* PE analysis
* Integrity verification
* Malware identification
* Header inspection



# 5. Wireshark

## Purpose

Wireshark captures and analyzes network traffic.

It displays packets exchanged between computers.



## Displays

* Source IP
* Destination IP
* Source Port
* Destination Port
* Protocol
* Packet Length
* Packet Contents


## Investigation Value

Detect:

* Malware communication
* C2 traffic
* Data exfiltration
* DNS tunneling
* Suspicious protocols


## Example

```
Source:
192.168.1.20

Destination:
104.18.xx.xx

Protocol:
TLSv1.2

Port:
443
```

This indicates an encrypted HTTPS connection.

Although encrypted traffic is common, investigators should determine whether the destination is legitimate or suspicious.



## Common Uses

* Packet capture
* Malware traffic analysis
* Network troubleshooting
* Threat hunting


# 6. PEstudio

## Purpose

PEStudio performs **static malware analysis**.

It analyzes executable files **without executing them**.


## Displays

* Imports
* Exports
* Sections
* Resources
* Strings
* Entropy
* Certificates
* Indicators


## Entropy

Entropy measures randomness.

Higher entropy often indicates:

* Packing
* Encryption
* Obfuscation

Typical values:

| Entropy | Meaning                 |
| ------- | ----------------------- |
| 0–5     | Normal                  |
| 6–7     | Possibly packed         |
| 7–8     | Likely packed/encrypted |


## Example

```
File:
PsExec.exe

Architecture:
32-bit

Compiler:
Visual C++

Entropy:
6.596
```

Interpretation:

* Slightly high entropy
* Possible packing
* Needs further investigation

## Investigation Value

PEStudio quickly identifies:

* Suspicious imports
* Hidden APIs
* Packed executables
* Dangerous capabilities

without executing malware.


## Common Uses

* Static analysis
* Malware triage
* PE inspection
* IOC extraction


# 7. FLOSS

## Full Form

**FLARE Obfuscated String Solver**

Developed by:

**FLARE Team (FireEye/Mandiant)**


## Purpose

Extracts strings from malware, including:

* Static strings
* Stack strings
* Tight strings
* Decoded strings

Unlike the basic `strings` utility, FLOSS can recover **obfuscated strings** hidden by malware.


## Command

```powershell
floss malware.exe
```


## Output Example

```
INFO: extracting static strings

INFO: extracting stackstrings

INFO: decoding strings

Finished successfully
```

## What FLOSS Can Find

* URLs
* Domains
* IP addresses
* Registry paths
* File paths
* API names
* Command-line arguments
* C2 servers
* Encryption keys
* Mutex names


## Investigation Value

Suppose malware hides:

```
hxxp://evilserver.com
```

using XOR.

Normal `strings.exe` cannot recover it.

FLOSS automatically:

* Detects decoder
* Executes decoder
* Displays decoded string



## Common Uses

* Malware triage
* IOC extraction
* Configuration recovery
* Reverse engineering
----------------
------------------

# FlareVM Practical Malware Investigation Notes (Complete)

This task demonstrates a **real-world malware triage workflow** using multiple tools available in FlareVM. The investigation begins with **static analysis**, then moves to **dynamic analysis** to observe runtime behavior and network communication.

# Investigation Scenario

**Incident**

A suspicious executable named:

```text
windows.exe
```

was downloaded by a user on:

```text
09/24/2024
03:43 AM
```

The SOC (Security Operations Center) flagged the download as suspicious and requested malware analysis.

Location:

```text
C:\Users\Administrator\Desktop\Sample
```

---

# Investigation Workflow

```text
Suspicious File
        │
        ▼
PEStudio
(Static Analysis)
        │
        ▼
FLOSS
(String Extraction)
        │
        ▼
Run Sample
(Dynamic Analysis)
        │
        ▼
Process Explorer
(Process + TCP Connections)
        │
        ▼
Process Monitor
(Verify Runtime Activity)
        │
        ▼
Conclusion
```

---

# Step 1 Static Analysis using PEStudio

## Purpose

PEStudio performs **static analysis**.

It inspects the executable **without running it**.

## Information Obtained

### File Hashes

MD5

```text
9FDD4767DE5AEC8E577C1916ECC3E1D6
```

SHA1

```text
A1BC55A7931BFCD24651357829C460FD3DC4828F
```

## Why Hashes Matter

Hashes uniquely identify a file.

They help analysts:

* Verify file integrity
* Search malware databases
* Compare samples
* Identify known malware

Common services:

* VirusTotal
* MalwareBazaar
* Hybrid Analysis

If no detection exists:

* Could be a new malware
* Could be modified malware
* Could be a custom attack

---

# Suspicious File Description

PEStudio shows:

```text
Windows Registry Editor
(REGEDIT)
```

This appears legitimate.

However:

Actual location:

```text
C:\Users\Administrator\Desktop\Sample
```

Legitimate Registry Editor resides in:

```text
C:\Windows\System32\regedit.exe
```

---

## Why Suspicious?

Malware often impersonates legitimate Windows programs.

Examples:

```text
explorer.exe
svchost.exe
regedit.exe
services.exe
chrome.exe
```

This technique is called:

## Masquerading

(MITRE ATT&CK T1036)

Purpose:

* Trick users
* Evade detection
* Blend with Windows

# Version Information

PEStudio displays metadata containing Russian text.

Example:

```text
Редактор реестра
```

Translation:

```text
Registry Editor
```

Another entry:

```text
Операционная система Microsoft Windows
```

Translation:

```text
Microsoft Windows Operating System
```

## Why Suspicious?

If the organization:

* Does not use Russian
* Has no Russian users

Russian metadata may indicate:

* Foreign malware
* Malware builder
* Compiled on Russian system

It is **not proof**, but an investigation clue.

# Missing Rich Header

PEStudio reports:

```text
Rich Header
Not Present
```

## What is Rich Header?

The Rich Header stores:

* Compiler information
* Linker information
* Build environment

Many malware authors remove it.

Reasons:

* Prevent attribution
* Evade static analysis
* Hide compiler details



## Investigation Meaning

Missing Rich Header may indicate:

* Packing
* Obfuscation
* Malware
* Manual modification

# Import Address Table (IAT)

PEStudio lists imported APIs.

These APIs reveal what malware is capable of doing.


# Important Imported APIs

## 1. UseShellExecute

```text
UseShellExecute
```

Purpose

Allows Windows Shell to launch another process.

Used by malware to:

* Launch PowerShell
* Launch CMD
* Launch payloads
* Execute downloaded malware

## 2. CryptoStream

```text
CryptoStream
```

Purpose

Encrypts or decrypts data.

Possible malware usage:

* Encrypt stolen data
* Encrypt C2 traffic
* Encrypt files


## 3. RijndaelManaged

```text
RijndaelManaged
```

Purpose

Implements AES encryption.

Possible malware usage:

* File encryption
* Ransomware
* Secure communication


## 4. CipherMode

```text
CipherMode
```

Purpose

Defines encryption mode.

Examples:

* CBC
* ECB
* CFB

## 5. CreateDecryptor

```text
CreateDecryptor
```

Purpose

Decrypt encrypted data.

Possible malware usage:

* Decrypt payload
* Decode configuration
* Decrypt strings

# Static Analysis Conclusion

The executable appears capable of:

* Launching processes
* Encrypting data
* Decrypting payloads

This suggests ransomware or loader-like behavior.


# Step 2  String Extraction using FLOSS

## Command

```powershell
FLOSS.exe .\windows.exe > windows.txt
```

## Command Breakdown

```powershell
FLOSS.exe
```

Runs FLOSS.

```powershell
.\windows.exe
```

Target file.

```powershell
>
```

Redirect output.

```powershell
windows.txt
```

Save extracted strings.

## FLOSS Output

Example

```text
WARNING:
.NET string extraction not supported

INFO:
Extracting static strings

Finished
```

## Findings

Near the bottom of the report:

FLOSS extracted strings similar to:

```text
UseShellExecute

CryptoStream

CipherMode

CreateDecryptor

RijndaelManaged
```

## Why Important?

The same APIs were seen in PEStudio.

Finding identical indicators using multiple tools increases confidence.

This process is called:

## Cross Validation

Never trust only one tool.

Always verify using another.

# Static Analysis Summary

Evidence collected:

 Cryptographic APIs

 Process creation APIs

 Suspicious metadata

 Fake Registry Editor

 Missing Rich Header

-------------

# Step 3 — Dynamic Analysis

Now execute malware inside the isolated FlareVM.

Target:

```text
cobaltstrike.exe
```

# Process Explorer

Purpose

Observe runtime behavior.

## After execution

Open:

```text
Process Explorer
```
Example Process Tree

```text
explorer.exe
        │
        └── cobaltstrike.exe
```

## Parent Process

```text
explorer.exe
```

Reason:

User manually launched malware.


## Child Process

```text
cobaltstrike.exe
```

## Investigation Value

Process Explorer shows:

* Parent process
* Child process
* Process ID
* Executable path
* Loaded DLLs
* Network connections

# TCP/IP Tab

Open:

```
Right Click

Properties

TCP/IP
```

Displays:

* Remote IP
* Local Port
* Remote Port
* Connection State



Observed Connection

Destination IP

```text
47.120.46.210
```

This suggests malware is contacting a remote server.

Possible purposes:

* Command & Control (C2)
* Download payload
* Upload stolen data
* Beaconing

# Step 4 — Verification using Process Monitor

Never rely on a single tool.

Verify findings.


Open:

```text
Process Monitor
```

# Filtering

Shortcut:

```text
CTRL + L
```

Create Filter

```
Now, using this filter involves several steps. This includes:
1.Select the Process Name
2.Select contains
3.type any value containing any word related to the process. In this case, cobalt
4.Click include
5.And then Add and Click on Apply
6.You should be able to see the conditions added.
```

This removes unrelated Windows activity.


# Observations

Process Monitor confirms:

* Malware starts
* Executes APIs
* Opens files
* Contacts remote IP

The observed network communication matches Process Explorer.

# Verified IOC

Remote IP

```text
47.120.46.210
```

# Why Verification Matters

Process Explorer:

Shows current connection.

Process Monitor:

Shows detailed system events.

Both tools confirm:

```text
cobaltstrike.exe

↓

Connected to

47.120.46.210
```

Confidence increases because two independent tools agree.

# Indicators of Compromise (IOCs)

## File

```text
windows.exe
```

## Location

```text
C:\Users\Administrator\Desktop\Sample
```

## MD5

```text
9FDD4767DE5AEC8E577C1916ECC3E1D6
```

## SHA1

```text
A1BC55A7931BFCD24651357829C460FD3DC4828F
```

## Remote IP

```text
47.120.46.210
```

## Suspicious APIs

```text
UseShellExecute

CryptoStream

CipherMode

CreateDecryptor

RijndaelManaged
```

## Suspicious Behaviors

* Masquerading as Registry Editor
* Missing Rich Header
* Uses cryptographic APIs
* Creates processes
* Connects to unknown remote IP
* Possible malware loader
* Possible ransomware functionality


# Complete Investigation Flow

```text
User downloads:

windows.exe
        │
        ▼
PEStudio
│
├── MD5
├── SHA1
├── Russian metadata
├── Missing Rich Header
├── Imported APIs
│
▼
FLOSS
│
├── Extract strings
├── Confirm APIs
│
▼
Run Malware
│
▼
Process Explorer
│
├── Parent Process
├── Child Process
├── TCP/IP Connection
│
▼
Process Monitor
│
├── Filter Process
├── Observe Runtime
├── Verify Network Activity
│
▼
Confirmed IOC

47.120.46.210
```

-----------

