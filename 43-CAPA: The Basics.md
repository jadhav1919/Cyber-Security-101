# CAPA (Common Analysis Platform for Artifacts)

## What is CAPA?

**CAPA** is a **static malware analysis tool** developed by **FireEye Mandiant**.

It analyzes executable files and automatically identifies **what the program is capable of doing** without running it.

Instead of telling you **how** malware works internally, CAPA tells you **what capabilities** it has.


# Why Use CAPA?

Manually reverse engineering malware takes a lot of time.

CAPA automates this process by using thousands of predefined rules.

It quickly answers questions like:

* Can this malware access files?
* Can it communicate over the network?
* Can it inject code into another process?
* Can it modify the registry?
* Can it create persistence?


# Static Analysis vs Dynamic Analysis

| Static Analysis               | Dynamic Analysis                  |
| ----------------------------- | --------------------------------- |
| Does **not** execute the file | Executes the file                 |
| Safe                          | Requires isolated sandbox/VM      |
| Faster                        | More time-consuming               |
| Looks at code and structure   | Observes runtime behavior         |
| CAPA is used here             | Sandboxes (Any.Run, Cuckoo, etc.) |


# Supported File Types

CAPA can analyze:

* Portable Executables (PE) (`.exe`, `.dll`)
* ELF binaries (Linux)
* .NET modules
* Shellcode
* Sandbox reports


-----------

# CAPA 

## Running CAPA

CAPA is very easy to use.

### Step 1: Open PowerShell

Open **PowerShell** (it may take a few seconds to load).


### Step 2: Go to the CAPA Directory

```powershell
cd C:\Users\Administrator\Desktop\capa
```


### Step 3: Run CAPA

```powershell
capa.exe .\cryptbot.bin
```

### Basic Syntax
```bash
capa.exe <file_name>
```

> This performs a **static analysis** of the file and displays its capabilities. 


# Useful CAPA Options

| Option | Purpose             | Example                       |
| ------ | ------------------- | ----------------------------- |
| `-h`   | Show help           | `capa -h`                     |
| `-v`   | Verbose output      | `capa.exe .\cryptbot.bin -v`  |
| `-vv`  | Very verbose output | `capa.exe .\cryptbot.bin -vv` |

> **Note:** `-v` and `-vv` provide more detailed information but take longer to complete



# Reading a Saved Report

Instead of waiting for CAPA to finish every time, you can open a pre-generated report.
```bash
Get-Content .\cryptbot.txt
```

This displays the saved CAPA analysis in PowerShell.

-----------
# CAPA Output Analysis 

After CAPA finishes analyzing a file, it displays several sections. Each section gives important information about the malware and its capabilities. 

# 1. Basic File Information

The first block provides general information about the analyzed file.

Example:

```text
MD5
SHA1
SHA256
Analysis
OS
Format
Architecture
Path
```


## Fields Explained

| Field            | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| **MD5**          | 128-bit file hash used to identify the file.                 |
| **SHA1**         | More secure file hash used for file verification.            |
| **SHA256**       | Strong cryptographic hash used to uniquely identify malware. |
| **Analysis**     | Shows the analysis type (Static or Dynamic).                 |
| **OS**           | Operating system the malware targets.                        |
| **Format**       | Executable file format (PE, ELF, etc.).                      |
| **Architecture** | CPU architecture (x86, x64, ARM).                            |
| **Path**         | Location of the analyzed file.                               |

## Example

```text
MD5        : 3b9d26...
SHA1       : 969437...
SHA256     : ae7bc6...
Analysis   : Static
OS         : Windows
Format     : PE
Architecture : i386 (32-bit)
Path       : cryptbot.bin
```

# 2. MITRE ATT&CK Section

CAPA maps malware behavior to the **MITRE ATT&CK Framework**, helping analysts understand what techniques the malware uses. 


## MITRE ATT&CK Structure

### Format 1

```text
Tactic
    ↓
Technique
    ↓
Technique ID
```

Example:

```text
Defense Evasion
    ↓
Obfuscated Files or Information
    ↓
T1027
```

### Format 2

```text
Tactic
    ↓
Technique
    ↓
Sub-Technique
    ↓
Technique ID
```

Example:

```text
Defense Evasion
    ↓
Obfuscated Files or Information
    ↓
Indicator Removal from Tools
    ↓
T1027.005
```

## Terms Explained

| Term              | Meaning                                      |
| ----------------- | -------------------------------------------- |
| **Tactic**        | The attacker's goal.                         |
| **Technique**     | How the attacker achieves the goal.          |
| **Sub-Technique** | More specific implementation of a technique. |
| **Technique ID**  | Unique MITRE identifier (e.g., T1027).       |

## Sample ATT&CK Results

| Tactic          | Technique                                  |
| --------------- | ------------------------------------------ |
| Defense Evasion | Obfuscated Files or Information (T1027)    |
| Defense Evasion | Indicator Removal from Tools (T1027.005)   |
| Defense Evasion | Virtualization/Sandbox Evasion (T1497.001) |
| Discovery       | File and Directory Discovery (T1083)       |
| Execution       | PowerShell Execution (T1059.001)           |
| Execution       | Shared Modules (T1129)                     |
| Impact          | Resource Hijacking (T1496)                 |
| Persistence     | Scheduled Task (T1053.005)                 |


## Why is MITRE ATT&CK Important?

It helps analysts:

* Understand attacker behavior
* Identify attack techniques
* Map malware to known threats
* Improve detection rules
* Speed up incident response

# 3. MAEC (Malware Attribute Enumeration and Characterization)

MAEC is a standard language used to describe malware behavior consistently. CAPA assigns MAEC categories to explain what kind of malware the file behaves like. 

## Example

```text
Malware Category
Launcher
```

## Common MAEC Values

| MAEC Value     | Description                                             |
| -------------- | ------------------------------------------------------- |
| **Launcher**   | Executes or launches malicious actions or payloads.     |
| **Downloader** | Downloads additional malicious files from the Internet. |


# Launcher Behavior

If CAPA labels malware as a **Launcher**, it may:

* Drop additional malware
* Execute malicious programs
* Create persistence
* Connect to Command-and-Control (C2) servers
* Launch malicious functions


# Downloader Behavior

If CAPA labels malware as a **Downloader**, it may:

* Download additional payloads
* Retrieve configuration files
* Download updates
* Execute second-stage malware


# Why MAEC is Useful

MAEC helps analysts:

* Classify malware quickly
* Understand malware behavior
* Share malware information using a standard format
* Improve threat intelligence

----------

# CAPA Output Analysis (Beginner Notes)

After CAPA finishes analyzing a file, it displays several sections. Each section gives important information about the malware and its capabilities. 


# 1. Basic File Information

The first block provides general information about the analyzed file.

Example:

```text
MD5
SHA1
SHA256
Analysis
OS
Format
Architecture
Path
```

## Fields Explained

| Field            | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| **MD5**          | 128-bit file hash used to identify the file.                 |
| **SHA1**         | More secure file hash used for file verification.            |
| **SHA256**       | Strong cryptographic hash used to uniquely identify malware. |
| **Analysis**     | Shows the analysis type (Static or Dynamic).                 |
| **OS**           | Operating system the malware targets.                        |
| **Format**       | Executable file format (PE, ELF, etc.).                      |
| **Architecture** | CPU architecture (x86, x64, ARM).                            |
| **Path**         | Location of the analyzed file.                               |


## Example

```text
MD5        : 3b9d26...
SHA1       : 969437...
SHA256     : ae7bc6...
Analysis   : Static
OS         : Windows
Format     : PE
Architecture : i386 (32-bit)
Path       : cryptbot.bin
```

# 2. MITRE ATT&CK Section

CAPA maps malware behavior to the **MITRE ATT&CK Framework**, helping analysts understand what techniques the malware uses. 

## MITRE ATT&CK Structure

### Format 1

```text
Tactic
    ↓
Technique
    ↓
Technique ID
```

Example:

```text
Defense Evasion
    ↓
Obfuscated Files or Information
    ↓
T1027
```

### Format 2

```text
Tactic
    ↓
Technique
    ↓
Sub-Technique
    ↓
Technique ID
```

Example:

```text
Defense Evasion
    ↓
Obfuscated Files or Information
    ↓
Indicator Removal from Tools
    ↓
T1027.005
```

## Terms Explained

| Term              | Meaning                                      |
| ----------------- | -------------------------------------------- |
| **Tactic**        | The attacker's goal.                         |
| **Technique**     | How the attacker achieves the goal.          |
| **Sub-Technique** | More specific implementation of a technique. |
| **Technique ID**  | Unique MITRE identifier (e.g., T1027).       |

## Sample ATT&CK Results

| Tactic          | Technique                                  |
| --------------- | ------------------------------------------ |
| Defense Evasion | Obfuscated Files or Information (T1027)    |
| Defense Evasion | Indicator Removal from Tools (T1027.005)   |
| Defense Evasion | Virtualization/Sandbox Evasion (T1497.001) |
| Discovery       | File and Directory Discovery (T1083)       |
| Execution       | PowerShell Execution (T1059.001)           |
| Execution       | Shared Modules (T1129)                     |
| Impact          | Resource Hijacking (T1496)                 |
| Persistence     | Scheduled Task (T1053.005)                 |


## Why is MITRE ATT&CK Important?

It helps analysts:

* Understand attacker behavior
* Identify attack techniques
* Map malware to known threats
* Improve detection rules
* Speed up incident response

# 3. MAEC (Malware Attribute Enumeration and Characterization)

MAEC is a standard language used to describe malware behavior consistently. CAPA assigns MAEC categories to explain what kind of malware the file behaves like. 

## Example

```text
Malware Category
Launcher
```

## Common MAEC Values

| MAEC Value     | Description                                             |
| -------------- | ------------------------------------------------------- |
| **Launcher**   | Executes or launches malicious actions or payloads.     |
| **Downloader** | Downloads additional malicious files from the Internet. |


# Launcher Behavior

If CAPA labels malware as a **Launcher**, it may:

* Drop additional malware
* Execute malicious programs
* Create persistence
* Connect to Command-and-Control (C2) servers
* Launch malicious functions

# Downloader Behavior

If CAPA labels malware as a **Downloader**, it may:

* Download additional payloads
* Retrieve configuration files
* Download updates
* Execute second-stage malware

# Why MAEC is Useful

MAEC helps analysts:

* Classify malware quickly
* Understand malware behavior
* Share malware information using a standard format
* Improve threat intelligence

--------

# CAPA Output Analysis (MBC)

The **Malware Behavior Catalog (MBC)** section explains **what the malware is capable of doing**. It provides a standardized way to describe malware behaviors and complements the MITRE ATT&CK framework. 

# What is MBC?

**MBC (Malware Behavior Catalog)** is a framework that describes malware behaviors in a standardized format.

It helps analysts:

* Identify malware behavior
* Classify malware activities
* Produce standardized reports
* Map behaviors to MITRE ATT&CK
* Compare malware samples

> MBC complements MITRE ATT&CK by focusing specifically on malware behavior. 



# MBC Output Format

## Format 1

```text
OBJECTIVE
      ↓
BEHAVIOR
      ↓
METHOD
      ↓
IDENTIFIER
```

Example

```text
ANTI-STATIC ANALYSIS
        ↓
Executable Code Obfuscation
        ↓
Argument Obfuscation
        ↓
B0032.020
```


## Format 2

```text
OBJECTIVE
      ↓
BEHAVIOR
      ↓
IDENTIFIER
```

Example

```text
COMMUNICATION
        ↓
HTTP Communication
        ↓
C0002
```

# MBC Components

| Component      | Meaning                                  |
| -------------- | ---------------------------------------- |
| **Objective**  | Malware's overall goal                   |
| **Behavior**   | Action performed by malware              |
| **Method**     | Specific way the behavior is carried out |
| **Identifier** | Unique MBC ID                            |


# MBC Objectives

These describe the malware's main purpose.

| Objective                    | Description                                          |
| ---------------------------- | ---------------------------------------------------- |
| **Anti-Behavioral Analysis** | Avoids sandboxes and debuggers.                      |
| **Anti-Static Analysis**     | Makes static analysis difficult through obfuscation. |
| **Collection**               | Collects information from the victim.                |
| **Command and Control (C2)** | Communicates with attacker-controlled servers.       |
| **Credential Access**        | Steals usernames and passwords.                      |
| **Defense Evasion**          | Avoids detection by security tools.                  |
| **Discovery**                | Collects system and network information.             |
| **Execution**                | Runs malicious commands or code.                     |
| **Exfiltration**             | Steals sensitive data.                               |
| **Impact**                   | Damages or disrupts systems.                         |
| **Lateral Movement**         | Spreads to other systems.                            |
| **Persistence**              | Maintains long-term access.                          |
| **Privilege Escalation**     | Gains higher privileges.                             |



# Micro-Objectives

Micro-objectives describe **low-level actions** that are not always malicious by themselves but are commonly used by malware.

| Micro-Objective   | Description                              |
| ----------------- | ---------------------------------------- |
| **PROCESS**       | Create, terminate, or manage processes.  |
| **MEMORY**        | Allocate or modify memory.               |
| **COMMUNICATION** | HTTP, DNS, FTP, SMTP, ICMP traffic.      |
| **DATA**          | Check, encode, decode, or compress data. |


# Common MBC Behaviors

| Behavior                        | Identifier | Description                            |
| ------------------------------- | ---------- | -------------------------------------- |
| Lab Machine Detection           | B0009      | Detects virtual machines or sandboxes. |
| Executable Code Obfuscation     | B0032      | Hides code to prevent analysis.        |
| Command & Scripting Interpreter | E1059      | Executes PowerShell, CMD, Bash, etc.   |
| File and Directory Discovery    | E1083      | Searches files and folders.            |
| Obfuscated Files or Information | E1027      | Encodes or encrypts data to hide it.   |



# Common Micro-Behaviors

| Micro-Behavior     | Identifier | Description                                  |
| ------------------ | ---------- | -------------------------------------------- |
| Allocate Memory    | C0007      | Allocates memory for execution or unpacking. |
| Create Process     | C0017      | Starts a new process.                        |
| HTTP Communication | C0002      | Sends or receives HTTP traffic.              |
| Check String       | C0019      | Looks for specific strings or patterns.      |
| Encode Data        | C0026      | Encodes data using Base64 or XOR.            |
| Create Directory   | C0046      | Creates folders.                             |
| Delete File        | C0047      | Deletes files.                               |
| Read File          | C0051      | Reads files.                                 |
| Write File         | C0052      | Writes data to files.                        |



# Common Methods

Methods explain **how** a behavior is performed.

| Behavior                        | Method                      | Identifier | Description                                   |
| ------------------------------- | --------------------------- | ---------- | --------------------------------------------- |
| Executable Code Obfuscation     | Argument Obfuscation        | B0032.020  | Calculates arguments at runtime to hide them. |
| Executable Code Obfuscation     | Stack Strings               | B0032.017  | Builds strings in memory to avoid detection.  |
| HTTP Communication              | Read Header                 | C0002.014  | Reads HTTP headers.                           |
| Encode Data                     | Base64                      | C0026.001  | Encodes data using Base64.                    |
| Encode Data                     | XOR                         | C0026.002  | Encodes data using XOR.                       |
| Obfuscated Files or Information | Encoding Standard Algorithm | E1027.m02  | Uses standard encodings such as Base64.       |

# Example

CAPA Output:

```text
MBC Objective : DATA
MBC Behavior  : Encode Data::Base64 [C0026.001]
```

### Interpretation

| Field          | Meaning     |
| -------------- | ----------- |
| **Objective**  | DATA        |
| **Behavior**   | Encode Data |
| **Method**     | Base64      |
| **Identifier** | C0026.001   |

### What does this mean?

The malware **can encode data using Base64**. This behavior may be used to hide or transform data before sending or storing it. 


# MBC vs MITRE ATT&CK

| MITRE ATT&CK                              | MBC                               |
| ----------------------------------------- | --------------------------------- |
| Describes attacker tactics and techniques | Describes malware behaviors       |
| Focuses on adversary actions              | Focuses on malware capabilities   |
| Used for threat mapping                   | Used for malware characterization |
| Covers the attack lifecycle               | Explains what malware can do      |

# How to Read an MBC Result

```text
Objective
      │
      ▼
What is the malware trying to achieve?

      │
      ▼
Behavior
      │
      ▼
What action is it performing?

      │
      ▼
Method
      │
      ▼
How is it performing that action?

      │
      ▼
Identifier
      │
      ▼
Unique MBC reference ID
```

-----------

# CAPA Output Analysis (Capability & Namespace) 

The last section of the CAPA report contains two important columns:

* **Capability** → What the malware can do.
* **Namespace** → The category where CAPA groups that capability.

Namespaces organize thousands of CAPA rules into logical groups, making malware analysis much easier. 


# Capability & Namespace Format

```
Capability (Rule Name)
          │
          ▼
Top-Level Namespace (TLN)
          │
          ▼
Namespace
```

Example

```
reference anti-VM strings
          │
          ▼
anti-analysis
          │
          ▼
anti-vm/vm-detection
```

# Components Explained

| Component                     | Description                              |
| ----------------------------- | ---------------------------------------- |
| **Capability**                | The behavior or feature CAPA detected.   |
| **Top-Level Namespace (TLN)** | The broad category of behavior.          |
| **Namespace**                 | A more specific subgroup inside the TLN. |


# Example

```
Capability:
reference anti-VM strings

Namespace:
anti-analysis/anti-vm/vm-detection
```

### Interpretation

* Malware searches for Virtual Machine artifacts.
* CAPA classifies it under:

  * **TLN:** anti-analysis
  * **Namespace:** anti-vm/vm-detection

This usually means the malware tries to detect if it is running inside a virtual machine or sandbox to avoid analysis. 

# What is a Namespace?

A **Namespace** is simply a folder or category that groups similar CAPA detection rules together.

Think of it like folders on your computer.

```
Documents
│
├── College
├── Projects
└── Notes
```

Similarly, CAPA organizes its rules like this:

```
anti-analysis
│
├── anti-vm
├── obfuscation
└── anti-debug
```

# Common Top-Level Namespaces (TLNs)

## 1. anti-analysis

Detects techniques malware uses to avoid analysis.

Examples:

* VM detection
* Sandbox detection
* Packing
* Obfuscation
* Anti-debugging

Example Namespace

```
anti-analysis/anti-vm/vm-detection
```

## 2. collection

Detects malware collecting information.

Examples:

* Files
* Credentials
* System information


## 3. communication

Detects network communication.

Examples:

* HTTP
* DNS
* FTP
* C2 communication

Example

```
communication/http
```

## 4. compiler

Detects which compiler or build environment created the executable.

Examples:

* Visual Studio
* GCC
* Delphi

## 5. data-manipulation

Detects data transformations.

Examples:

* Base64
* XOR
* String encryption
* Encoding

Example

```
data-manipulation/encoding/base64
```

## 6. executable

Detects executable file characteristics.

Examples:

* PE Sections
* TLS Sections
* Debug Information

## 7. host-interaction

Detects interaction with the operating system.

Examples:

* Read files
* Write files
* Delete files
* Create directories
* Create processes


## 8. impact

Detects behaviors that damage or affect systems.

Examples:

* Cryptocurrency mining
* Data destruction
* Data modification

## 9. internal

Internal CAPA rules.

These are **not intended for analysts**.

## 10. lib

Helper rules used to build other CAPA rules.

## 11. linking

Detects dynamically loaded libraries.

Examples:

* Runtime linking
* DLL loading

## 12. load-code

Detects dynamically loaded or injected code.

Examples:

* PowerShell
* Shellcode
* PE Loading

## 13. malware-family

Rules specific to known malware families.

---

## 14. nursery

Experimental CAPA rules that are still being developed.


## 15. persistence

Detects persistence mechanisms.

Examples:

* Scheduled Tasks
* Registry Run Keys
* Startup folders


## 16. runtime

Detects programming languages or runtime environments.

Examples:

* .NET
* Java
* Python

## 17. targeting

Detects malware targeting specific devices.

Example:

* ATM Malware


# Sample Capability & Namespace Analysis

| Capability                       | Namespace                                    | Meaning                     |
| -------------------------------- | -------------------------------------------- | --------------------------- |
| Reference anti-VM strings        | anti-analysis/anti-vm/vm-detection           | Detects Virtual Machines    |
| Contain obfuscated stack strings | anti-analysis/obfuscation/string/stackstring | Uses string obfuscation     |
| Reference HTTP User-Agent        | communication/http                           | Uses HTTP communication     |
| Reference Base64 string          | data-manipulation/encoding/base64            | Uses Base64 encoding        |
| Encode data using XOR            | data-manipulation/encoding/xor               | Uses XOR encoding           |
| Create directory                 | host-interaction/file-system/create          | Creates folders             |
| Delete file                      | host-interaction/file-system/delete          | Deletes files               |
| Read file                        | host-interaction/file-system/read            | Reads files                 |
| Write file                       | host-interaction/file-system/write           | Writes files                |
| Create process                   | host-interaction/process/create              | Starts new processes        |
| Allocate RWX memory              | host-interaction/process/inject              | Allocates executable memory |
| Schedule task                    | persistence/scheduled-tasks                  | Creates persistence         |
| Run PowerShell                   | load-code/powershell                         | Executes PowerShell         |


# How CAPA Organizes Rules

```
Top-Level Namespace
        │
        ▼
Namespace
        │
        ▼
Rule Files (.yml)
```

Example

```
anti-analysis
        │
        ▼
anti-vm
        │
        ▼
vm-detection
        │
        ▼
reference-anti-vm-strings-targeting-virtualbox.yml
reference-anti-vm-strings-targeting-virtualpc.yml
```

## Another Example

```
anti-analysis
        │
        ▼
obfuscation
        │
        ▼
obfuscated-with-dotfuscator.yml
obfuscated-with-smartassembly.yml
```

These rule files allow CAPA to recognize specific malware behaviors. 

# Why Namespaces Matter

Namespaces help analysts:

* Quickly understand malware behavior
* Organize thousands of CAPA rules
* Find related detections easily
* Improve malware classification
* Speed up malware analysis

-------------

# CAPA Output Analysis (Capability, Namespace & Rule YAML Files)

The last section of the CAPA report contains two important columns:

* **Capability** → What the malware is capable of doing.
* **Namespace** → The category where CAPA groups that capability.

Behind every capability is a **Rule YAML file**. This is the rule CAPA matched while analyzing the executable.

```
Executable
      │
      ▼
CAPA Rule (.yml)
      │
      ▼
Capability Detected
      │
      ▼
Grouped into Namespace
      │
      ▼
Displayed in Report
```

# Capability Format

```
Capability (Rule Name)
        │
        ▼
Top-Level Namespace (TLN)
        │
        ▼
Namespace
        │
        ▼
Rule YAML File
```

Example

```
Capability
reference anti-VM strings

TLN
anti-analysis

Namespace
anti-vm/vm-detection

Rule
reference-anti-vm-strings.yml
```


# Components

| Component                     | Description                                      |
| ----------------------------- | ------------------------------------------------ |
| **Capability**                | The malware behavior detected by CAPA.           |
| **Top-Level Namespace (TLN)** | Broad behavior category.                         |
| **Namespace**                 | Subcategory inside the TLN.                      |
| **Rule YAML File**            | The CAPA rule that matched the malware behavior. |


# Important Concept

**Capability = Rule Name**

The Rule YAML file is usually the **same as the Capability name**, except spaces are replaced with hyphens (`-`) and the extension `.yml` is added.

Example

```
Capability

reference Base64 string

↓

Rule YAML File

reference-base64-string.yml
```

Another example

```
Capability

create directory

↓

Rule YAML File

create-directory.yml
```

This is true for almost every capability in CAPA.


# Complete Capability Reference

| Capability                                     | TLN                                         | Namespace                      | Rule YAML File                                     | Explanation                                     |
| ---------------------------------------------- | ------------------------------------------- | ------------------------------ | -------------------------------------------------- | ----------------------------------------------- |
| reference anti-VM strings                      | Anti-Analysis                               | anti-vm/vm-detection           | reference-anti-vm-strings.yml                      | Detects generic VM detection strings.           |
| reference anti-VM strings targeting VMware     | Anti-Analysis                               | anti-vm/vm-detection           | reference-anti-vm-strings-targeting-vmware.yml     | Detects VMware artifacts.                       |
| reference anti-VM strings targeting VirtualBox | Anti-Analysis                               | anti-vm/vm-detection           | reference-anti-vm-strings-targeting-virtualbox.yml | Detects VirtualBox artifacts.                   |
| contain obfuscated stackstrings                | Anti-Analysis                               | obfuscation/string/stackstring | contain-obfuscated-stackstrings.yml                | Detects stack string obfuscation.               |
| reference HTTP User-Agent string               | Communication                               | http/client                    | reference-http-user-agent-string.yml               | Detects HTTP User-Agent strings.                |
| check HTTP status code                         | Communication                               | http                           | check-http-status-code.yml                         | Detects checking of HTTP response codes.        |
| reference Base64 string                        | Data Manipulation                           | encoding/base64                | reference-base64-string.yml                        | Detects Base64 encoding usage.                  |
| encode data using XOR                          | Data Manipulation                           | encoding/xor                   | encode-data-using-xor.yml                          | Detects XOR encoding.                           |
| contain a thread local storage (.tls) section  | Executable                                  | pe/section/tls                 | contain-a-thread-local-storage-tls-section.yml     | Detects TLS section inside PE files.            |
| get common file path                           | Host-Interaction                            | file-system                    | get-common-file-path.yml                           | Detects retrieval of common file paths.         |
| create directory                               | Host-Interaction                            | file-system/create             | create-directory.yml                               | Detects directory creation.                     |
| delete file                                    | Host-Interaction                            | file-system/delete             | delete-file.yml                                    | Detects file deletion.                          |
| read file on Windows                           | Host-Interaction                            | file-system/read               | read-file-on-windows.yml                           | Detects reading files.                          |
| write file on Windows                          | Host-Interaction                            | file-system/write              | write-file-on-windows.yml                          | Detects writing files.                          |
| get thread local storage value                 | Host-Interaction *(Rule stored in Nursery)* | process                        | get-thread-local-storage-value.yml                 | Reads TLS values.                               |
| allocate or change RWX memory                  | Host-Interaction                            | process/inject                 | allocate-or-change-rwx-memory.yml                  | Allocates executable memory (often injection).  |
| create process on Windows                      | Host-Interaction                            | process/create                 | create-process-on-windows.yml                      | Detects process creation.                       |
| reference cryptocurrency strings               | Impact *(Rule stored in Nursery)*           | impact/cryptocurrency          | reference-cryptocurrency-strings.yml               | Detects cryptocurrency/mining strings.          |
| link function at runtime on Windows            | Linking                                     | runtime-linking                | link-function-at-runtime-on-windows.yml            | Detects dynamic API linking.                    |
| parse PE header                                | Load-Code                                   | pe                             | parse-pe-header.yml                                | Parses Portable Executable headers.             |
| resolve function by parsing PE exports         | Load-Code                                   | pe                             | resolve-function-by-parsing-pe-exports.yml         | Resolves APIs dynamically.                      |
| run PowerShell expression                      | Load-Code                                   | powershell                     | run-powershell-expression.yml                      | Executes PowerShell commands.                   |
| schedule task via at                           | Persistence                                 | scheduled-tasks                | schedule-task-via-at.yml                           | Creates persistence using **at**.               |
| schedule task via schtasks                     | Persistence                                 | scheduled-tasks                | schedule-task-via-schtasks.yml                     | Creates persistence using Windows **schtasks**. |


# Example 1

CAPA Output

```
Capability

reference anti-VM strings

Namespace

anti-analysis/anti-vm/vm-detection
```

Explanation

* Capability detected:

  * Malware searches for VM artifacts.

* Top-Level Namespace:

  * **Anti-Analysis**

* Namespace:

  * **anti-vm/vm-detection**

* Rule matched:

```
reference-anti-vm-strings.yml
```

Meaning

The malware checks whether it is running inside a virtual machine (VMware, VirtualBox, etc.) to evade analysis or sandbox detection.


# Example 2

CAPA Output

```
Capability

schedule task via schtasks

Namespace

persistence/scheduled-tasks
```

Explanation

* Capability detected:

  * Creates scheduled tasks.

* TLN:

  * Persistence

* Namespace:

  * scheduled-tasks

* Rule matched

```
schedule-task-via-schtasks.yml
```

Meaning

The malware creates a Windows Scheduled Task using **schtasks.exe** so it automatically runs again after reboot.


# Example 3

CAPA Output

```
Capability

reference Base64 string

Namespace

data-manipulation/encoding/base64
```

Explanation

| Field          | Value                       | Meaning                             |
| -------------- | --------------------------- | ----------------------------------- |
| Capability     | reference Base64 string     | Malware uses Base64 encoding.       |
| TLN            | data-manipulation           | Malware transforms or encodes data. |
| Namespace      | encoding/base64             | Base64-related behavior.            |
| Rule YAML File | reference-base64-string.yml | CAPA rule that matched.             |

Meaning

The malware is capable of encoding or decoding data using the Base64 encoding scheme.


# Rule YAML Files

Every capability shown by CAPA comes from a **Rule YAML (.yml) file**.

These files contain:

* Detection logic
* Byte patterns
* API calls
* Strings
* Conditions
* Metadata
* MITRE ATT&CK mappings
* MBC mappings

When CAPA analyzes an executable:

```
Executable
      │
      ▼
Read all YAML Rules
      │
      ▼
Find Matching Rule
      │
      ▼
Display Capability
```

# Exception (Nursery Rules)

Most Rule YAML files are stored under their corresponding Top-Level Namespace.

Example

```
Persistence

↓

scheduled-task-via-schtasks.yml
```

However, some rules are **still experimental** and are stored under the **Nursery** TLN instead of their expected namespace.

Examples

| Capability                       | Expected TLN     | Actual Location |
| -------------------------------- | ---------------- | --------------- |
| reference cryptocurrency strings | Impact           | Nursery         |
| get thread local storage value   | Host-Interaction | Nursery         |

The **Nursery** is a staging area for rules that are still being tested or refined before moving into their final namespace.

-----------

# CAPA Very Verbose Analysis (`-vv`) & CAPA Web Explorer

## Why use `-vv`?

By default, CAPA only tells you **what capability was detected**.

Using the **Very Verbose (`-vv`)** option shows:

* Why a rule matched
* Which conditions were satisfied
* Which strings/APIs/instructions triggered the rule
* Exact evidence used by CAPA

Think of it as:

> **Normal CAPA → "What did the malware do?"**
> **CAPA -vv → "How did CAPA know it?"**


# Verbose Options

| Option | Description                                 | Example                     |
| ------ | ------------------------------------------- | --------------------------- |
| `-v`   | Verbose output                              | `capa.exe -v cryptbot.bin`  |
| `-vv`  | Very Verbose output (includes rule matches) | `capa.exe -vv cryptbot.bin` |


# Running CAPA with `-vv`

```powershell
capa.exe -vv .\cryptbot.bin
```

Example

```text
loading : 100%
analyzing program...
```

The output contains **thousands of lines** because CAPA prints every rule match.

Example

```
cryptbot_vv.txt
```


# Viewing the Output

Open the generated file.

```powershell
Get-Content .\cryptbot_vv.txt
```

The output may contain **3000+ lines**, making manual analysis difficult.


# Exporting as JSON

Instead of viewing text output, export everything as JSON.

```powershell
capa.exe -j -vv .\cryptbot.bin > cryptbot_vv.json
```

### Parameters

| Option | Meaning                          |
| ------ | -------------------------------- |
| `-j`   | Export output as JSON            |
| `-vv`  | Include very verbose information |
| `>`    | Save output into a file          |

Output

```
cryptbot_vv.json
```

# Why JSON?

JSON output is:

* Structured
* Easy to search
* Easy to visualize
* Compatible with CAPA Web Explorer

Instead of reading thousands of text lines, JSON lets tools display everything in a clean interface.


# CAPA Web Explorer

CAPA Web Explorer is a graphical interface for viewing CAPA JSON reports.

It makes investigation much easier.

Instead of this:

```
3000+ lines
```

You get:

* Search
* Filters
* Rule navigation
* Namespace navigation
* Capability view
* Rule matching evidence


# Opening CAPA Web Explorer

You can use either:

### Online

Official CAPA Web Explorer

### Offline

```
capa_web_explorer_offline.html
```

Located on the Desktop inside the lab VM.


# Uploading the JSON Report

1. Open CAPA Web Explorer.
2. Click **Upload from Local**.
3. Select

```
cryptbot_vv.json
```

4. Wait for parsing.
5. The report appears in graphical form.


# What CAPA Web Explorer Shows

The interface allows you to explore:

* Capabilities
* Namespaces
* ATT&CK Mapping
* MBC Mapping
* Rule YAML
* Evidence
* Strings
* APIs
* Functions
* Conditions


# Biggest Advantage

Normal CAPA tells you

```
Capability

↓

Reference Base64 String
```

Web Explorer tells you

```
Capability

↓

Which Rule Matched

↓

Which String Matched

↓

Which Condition Was True

↓

Where It Happened
```

# Rule Matching

Every capability comes from a **Rule YAML File**.

CAPA checks every rule against the executable.

If every required condition is satisfied,

↓

The capability is reported.

Workflow

```text
Executable
      │
      ▼
Rule YAML
      │
      ▼
Conditions Checked
      │
      ▼
Rule Matches
      │
      ▼
Capability Reported
```


# Example 1

Capability

```
reference anti-VM strings targeting VMware
```

Rule

```
reference-anti-vm-strings-targeting-vmware.yml
```

Inside the Rule

```yaml
features:
  - string: /VMWare/i
```


## Explanation

The rule searches for the string

```
VMWare
```

The `/i` means:

**Case-insensitive matching**

So all of these match:

```
VMWare
vmware
VMWARE
VmWaRe
```

If this string exists,

↓

CAPA triggers

```
reference anti-VM strings targeting VMware
```


## Why Malware Uses It

Malware checks whether it is running inside

* VMware
* VirtualBox
* Hyper-V

If a virtual machine is detected,

the malware may:

* Exit
* Hide
* Delay execution
* Disable malicious behavior

This helps evade malware analysts.


# Example 2

Capability

```
schedule task via schtasks
```

Rule

```
schedule-task-via-schtasks.yml
```

Rule Content

```yaml
rule:
  meta:
    name: schedule task via schtasks

    namespace: persistence/scheduled-tasks

    att&ck:
      - Persistence::Scheduled Task/Job::Scheduled Task [T1053.005]

features:
  - and:
      - match: host-interaction/process/create
      - or:
          - and:
              - string: /schtasks/i
              - string: /\/create/i
          - string: /Register-ScheduledTask/i
```


# Rule Breakdown

The rule requires:

### Condition 1

```yaml
match:

host-interaction/process/create
```

Meaning

The malware creates a process.


### Condition 2

Either

```yaml
schtasks
```

AND

```yaml
/create
```

OR

```yaml
Register-ScheduledTask
```


# What CAPA Detects

If the malware runs:

```cmd
schtasks /create
```

or

```powershell
Register-ScheduledTask
```

CAPA concludes

```
Persistence

↓

Scheduled Task Created
```


# Why Malware Uses Scheduled Tasks

Scheduled Tasks allow malware to:

* Execute automatically
* Run after reboot
* Maintain persistence
* Survive system restarts


# Understanding Rule Features

The **features** section is the most important part of every CAPA rule.

Example

```yaml
features:

- string: /VMWare/i
```

CAPA checks

```
Does this executable contain this string?
```

If YES

↓

Rule may match.


Another example

```yaml
features:

- string: /schtasks/i

- string: /\/create/i
```

CAPA asks

```
Does this executable contain

schtasks

AND

/create
```

If YES

↓

Rule matches.


# Common Feature Types

| Feature  | Purpose                             |
| -------- | ----------------------------------- |
| `string` | Search for strings                  |
| `api`    | Detect Windows API usage            |
| `number` | Match numeric constants             |
| `match`  | Reuse another CAPA rule             |
| `and`    | All conditions must be true         |
| `or`     | At least one condition must be true |
| `not`    | Condition must not exist            |
| `regex`  | Regular expression matching         |


# Regex Example

```yaml
string: /VMWare/i
```

Breakdown

| Part     | Meaning                    |
| -------- | -------------------------- |
| `/`      | Regex delimiter            |
| `VMWare` | Pattern                    |
| `i`      | Ignore uppercase/lowercase |


# Logical Operators

## AND

```yaml
and:

- condition A

- condition B
```

Both must be true.


## OR

```yaml
or:

- condition A

- condition B
```

Either one is enough.


## MATCH

```yaml
match:

host-interaction/process/create
```

Instead of checking everything again,

CAPA reuses another rule that has already matched.


# CAPA Web Explorer Features

## Global Search

Allows searching across the report.

Examples

Search

```
PowerShell
```

Finds every PowerShell-related capability.

Search

```
Base64
```

Finds every Base64 rule.

Search

```
schtasks
```

Finds every scheduled task rule.


## Filters

Filters help narrow the report by:

* Capability
* Namespace
* ATT&CK
* MBC
* Rule

# Investigation Workflow

```text
Run CAPA

↓

Generate JSON

↓

Upload JSON

↓

Browse Capabilities

↓

Open Rule

↓

Inspect Features

↓

See Exact Match

↓

Understand Malware Behavior
```

# Why Use CAPA Web Explorer?

Compared to reading raw text:

| Text File            | Web Explorer            |
| -------------------- | ----------------------- |
| 3000+ lines          | Organized GUI           |
| Hard to search       | Instant search          |
| Difficult navigation | Clickable capabilities  |
| No visualization     | Graphical interface     |
| Manual inspection    | Interactive exploration |

-------------

