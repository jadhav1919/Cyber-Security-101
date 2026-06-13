# PowerShell Fundamentals

## 1. What is PowerShell?

### Definition

PowerShell is Microsoft's command-line shell, scripting language, and automation framework.

### Simple Explanation

PowerShell helps administrators and security professionals:

* Manage Windows systems
* Automate tasks
* Execute commands
* Retrieve system information
* Manage remote systems

Unlike CMD, PowerShell works with **objects** instead of plain text.

---

## 2. Learning Objectives

After this room, you should be able to:

* Understand PowerShell
* Launch PowerShell
* Use basic cmdlets
* Manage files and folders
* Work with pipelines
* Retrieve system information
* Retrieve network information
* Understand PowerShell's role in Cyber Security

---

## 3. Why Was PowerShell Created?

Traditional Windows tools such as:

* cmd.exe
* Batch files

had limitations:

* Text-based output
* Limited automation
* Difficult administration in large environments

Microsoft created PowerShell to solve these issues.

---

## 4. History of PowerShell

| Year        | Event                         |
| ----------- | ----------------------------- |
| Early 2000s | Development Started           |
| 2006        | PowerShell Released           |
| 2016        | PowerShell Core Released      |
| Present     | Windows, Linux, macOS Support |

Creator:

**Jeffrey Snover**

---

## 5. What Makes PowerShell Different?

### CMD

Works with:

```text
Text
```

Example:

```cmd
ipconfig
```

Returns text output.

---

### PowerShell

Works with:

```text
Objects
```

Example:

```powershell
Get-Process
```

Returns:

* Process Name
* PID
* CPU Usage
* Memory Usage

---

## 6. What is an Object?

### Definition

An object contains:

### Properties

Information about something.

Examples:

* Name
* Size
* Color

### Methods

Actions that can be performed.

Examples:

* Copy()
* Delete()
* Move()

---

## 7. Launching PowerShell

### Method 1

Start Menu

```text
powershell
```

---

### Method 2

Run Dialog

```text
Win + R
```

Type:

```text
powershell
```

---

### Method 3

CMD

#### Command

```cmd
powershell
```

#### Result

```powershell
PS C:\Users\captain>
```

---

## 8. PowerShell Prompt

CMD Prompt:

```cmd
C:\Users\captain>
```

PowerShell Prompt:

```powershell
PS C:\Users\captain>
```

---

## 9. Cmdlets (PowerShell Commands)

PowerShell commands are called:

### Cmdlets

Naming format:

```text
Verb-Noun
```

Examples:

| Cmdlet       | Meaning            |
| ------------ | ------------------ |
| Get-Content  | Read file contents |
| Set-Location | Change directory   |
| Get-Process  | View processes     |
| Get-Service  | View services      |

---

## 10. Advantages of PowerShell

### Automation

Automates repetitive tasks.

### Remote Administration

Manage remote systems.

### Object-Oriented

Works with objects.

### Cross Platform

Supports:

* Windows
* Linux
* macOS

### Cyber Security Usage

#### Blue Team

* Threat Hunting
* Log Analysis
* Incident Response

#### Red Team

* Enumeration
* Automation
* Remote Execution

---

# 11. Basic Discovery Cmdlets

## Get-Command

### Purpose

Displays available PowerShell commands.

### Syntax

```powershell
Get-Command
```

### Example

```powershell
Get-Command
```

### Example (Functions Only)

```powershell
Get-Command -CommandType Function
```

---

## Get-Help

### Purpose

Displays help information about a cmdlet.

### Syntax

```powershell
Get-Help <cmdlet>
```

### Example

```powershell
Get-Help Get-Date
```

### Show Examples

```powershell
Get-Help Get-Date -Examples
```

### Show Detailed Help

```powershell
Get-Help Get-Date -Detailed
```

### Show Full Help

```powershell
Get-Help Get-Date -Full
```

---

## Get-Alias

### Purpose

Displays command aliases.

### Syntax

```powershell
Get-Alias
```

### Example

```powershell
Get-Alias
```

Common aliases:

| Alias | Actual Cmdlet |
| ----- | ------------- |
| dir   | Get-ChildItem |
| cd    | Set-Location  |
| cat   | Get-Content   |
| clear | Clear-Host    |

---

# 12. Finding and Installing Modules

## Find-Module

### Purpose

Search online PowerShell repositories.

### Syntax

```powershell
Find-Module -Name <name>
```

### Example

```powershell
Find-Module -Name PowerShell*
```

---

## Install-Module

### Purpose

Install a PowerShell module.

### Syntax

```powershell
Install-Module -Name <module>
```

### Example

```powershell
Install-Module -Name PowerShellGet
```

---

# 13. File and Directory Management

## Get-ChildItem

### Purpose

Display files and folders.

### Syntax

```powershell
Get-ChildItem
```

### Example

```powershell
Get-ChildItem
```

Equivalent:

```cmd
dir
```

---

## Set-Location

### Purpose

Change current directory.

### Syntax

```powershell
Set-Location -Path <directory>
```

### Example

```powershell
Set-Location -Path .\Documents
```

Equivalent:

```cmd
cd
```

---

## New-Item

### Purpose

Create files or directories.

### Syntax

```powershell
New-Item -Path <path> -ItemType <type>
```

### Create Folder

```powershell
New-Item -Path .\TestFolder -ItemType Directory
```

### Create File

```powershell
New-Item -Path .\test.txt -ItemType File
```

---

## Remove-Item

### Purpose

Delete files or folders.

### Syntax

```powershell
Remove-Item -Path <path>
```

### Example

```powershell
Remove-Item -Path .\test.txt
```

Equivalent:

```cmd
del
```

---

## Copy-Item

### Purpose

Copy files or folders.

### Syntax

```powershell
Copy-Item -Path <source> -Destination <destination>
```

### Example

```powershell
Copy-Item test.txt backup.txt
```

---

## Move-Item

### Purpose

Move files or folders.

### Syntax

```powershell
Move-Item test.txt .\Backup\
```

---

## Get-Content

### Purpose

Display file contents.

### Syntax

```powershell
Get-Content -Path <file>
```

### Example

```powershell
Get-Content .\notes.txt
```

Equivalent:

```cmd
type
```

---

# 14. PowerShell Pipeline

## What is a Pipeline?

A pipeline passes output from one command to another.

Symbol:

```powershell
|
```

---

## Sort-Object

### Purpose

Sort objects.

### Syntax

```powershell
Get-ChildItem | Sort-Object Length
```

Sort files by size.

---

## Where-Object

### Purpose

Filter objects.

### Syntax

```powershell
Get-ChildItem | Where-Object Property -eq Value
```

### Example

```powershell
Get-ChildItem | Where-Object Extension -eq ".txt"
```

---

### Common Operators

| Operator | Meaning               |
| -------- | --------------------- |
| -eq      | Equal                 |
| -ne      | Not Equal             |
| -gt      | Greater Than          |
| -ge      | Greater Than or Equal |
| -lt      | Less Than             |
| -le      | Less Than or Equal    |
| -like    | Pattern Match         |

---

## Select-Object

### Purpose

Select specific properties.

### Example

```powershell
Get-ChildItem | Select-Object Name,Length
```

---

## Select-String

### Purpose

Search text inside files.

### Syntax

```powershell
Select-String -Path <file> -Pattern <text>
```

### Example

```powershell
Select-String -Path notes.txt -Pattern password
```

Equivalent:

```cmd
findstr
```

---

# 15. System Information Commands

## Get-ComputerInfo

### Purpose

Display detailed system information.

### Syntax

```powershell
Get-ComputerInfo
```

Equivalent:

```cmd
systeminfo
```

---

## Get-LocalUser

### Purpose

Display local user accounts.

### Syntax

```powershell
Get-LocalUser
```

---

# 16. Network Information Commands

## Get-NetIPConfiguration

### Purpose

Display network configuration.

### Syntax

```powershell
Get-NetIPConfiguration
```

Shows:

* IP Address
* Gateway
* DNS Server

---

## Get-NetIPAddress

### Purpose

Display all IP addresses.

### Syntax

```powershell
Get-NetIPAddress
```

---

## Get-NetTCPConnection

### Purpose

Display active TCP connections.

### Syntax

```powershell
Get-NetTCPConnection
```

Useful for:

* Incident Response
* Malware Analysis
* Threat Hunting

---

# 17. Process and Service Management

## Get-Process

### Purpose

Display running processes.

### Syntax

```powershell
Get-Process
```

Equivalent:

```cmd
tasklist
```

---

## Get-Service

### Purpose

Display services.

### Syntax

```powershell
Get-Service
```

Useful for:

* Troubleshooting
* Malware Investigation

---

# 18. File Integrity and ADS

## Get-FileHash

### Purpose

Generate file hashes.

### Syntax

```powershell
Get-FileHash -Path <file>
```

### Example

```powershell
Get-FileHash ship-flag.txt
```

Used in:

* Incident Response
* Malware Analysis
* File Verification

---

## Get-Item -Stream *

### Purpose

View Alternate Data Streams (ADS).

### Syntax

```powershell
Get-Item -Path <file> -Stream *
```

### Example

```powershell
Get-Item -Path house_log.txt -Stream *
```

---

# 19. PowerShell Scripting

## What is Scripting?

A script is a file containing multiple commands that run automatically.

Example:

```powershell
Get-Process
Get-Service
Get-ComputerInfo
```

Benefits:

* Automation
* Consistency
* Saves Time
* Reduces Errors

---

# 20. Remote Command Execution

## Invoke-Command

### Purpose

Execute commands on remote systems.

### Syntax

```powershell
Invoke-Command -ComputerName <computer> -ScriptBlock { command }
```

### Example

```powershell
Invoke-Command -ComputerName Server01 -ScriptBlock { Get-Service }
```

### Run Script Remotely

```powershell
Invoke-Command -FilePath script.ps1 -ComputerName Server01
```

---

# 21. Cyber Security Importance

## Blue Team

Used for:

* Log Analysis
* Threat Hunting
* Malware Analysis
* Incident Response

## Red Team

Used for:

* Enumeration
* Automation
* Remote Execution
* Security Assessments

## System Administration

Used for:

* User Management
* Service Management
* System Monitoring
* Security Enforcement

---

