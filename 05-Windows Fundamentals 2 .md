# Windows Fundamentals 2

## Overview

This module introduces important Windows administrative and troubleshooting utilities, including:

* System Configuration (MSConfig)
* Advanced System Settings
* User Account Control (UAC)
* Computer Management
* Task Scheduler
* Event Viewer
* Shared Folders
* Performance Monitor
* Device Manager
* Disk Management
* Services
* WMI
* System Information (msinfo32)
* Resource Monitor
* Command Prompt
* Windows Registry

These tools are commonly used by:

* System Administrators
* SOC Analysts
* Incident Responders
* Penetration Testers
* IT Support Engineers

---

# System Configuration (MSConfig)

## Definition

System Configuration (MSConfig) is an advanced troubleshooting tool used to diagnose startup and boot issues.

## Launch

```text
msconfig
```

Requires Administrator privileges.

---

## MSConfig Tabs

| Tab      | Purpose               |
| -------- | --------------------- |
| General  | Startup configuration |
| Boot     | Boot options          |
| Services | System services       |
| Startup  | Startup programs      |
| Tools    | Administrative tools  |

---

# General Tab

## Purpose

Controls what Windows loads during startup.

### Startup Modes

| Mode               | Description                      |
| ------------------ | -------------------------------- |
| Normal Startup     | Loads everything                 |
| Diagnostic Startup | Loads basic drivers and services |
| Selective Startup  | Custom startup configuration     |

---

# Boot Tab

## Purpose

Configure operating system boot options.

### Common Uses

* Safe Mode
* Boot logging
* Timeout settings
* Default operating system

---

# Services Tab

## Purpose

Displays all services on the system.

### Service Definition

A service is a special application that runs in the background.

### Information Displayed

* Service Name
* Manufacturer
* Status
* Startup Type

---

# Startup Tab

## Purpose

Historically used to manage startup applications.

### Modern Windows

Startup applications are managed through:

```text
Task Manager
```

### Windows Server

Use:

```text
shell:startup
```

to view startup applications.

---

# Tools Tab

## Purpose

Provides quick access to administrative utilities.

Examples:

* System Information
* Event Viewer
* Resource Monitor
* Computer Management
* Command Prompt

---

# Advanced System Settings

## Access

Search:

```text
View advanced system settings
```

---

# Performance Options

## Purpose

Controls:

* Visual effects
* Virtual memory
* Processor scheduling

---

# Virtual Memory (Page File)

## Definition

Additional storage space used when physical RAM becomes full.

### Purpose

Prevents:

* System slowdowns
* Application crashes

---

## Information Available

* Drive location
* Initial size
* Maximum size
* Automatic management status

---

# Startup and Recovery

## Purpose

Controls system behavior after crashes.

---

# Crash Dumps

## Definition

Files created when Windows crashes.

Used for:

* Troubleshooting
* Forensics
* Debugging

---

## Dump Types

| Type                  | Description         |
| --------------------- | ------------------- |
| Automatic Memory Dump | Default             |
| Kernel Memory Dump    | Kernel data only    |
| Small Memory Dump     | 256 KB              |
| Complete Memory Dump  | Full memory capture |
| None                  | No dump created     |

---

# User Account Control (UAC)

## Definition

Security feature that prevents unauthorized administrative actions.

---

## UAC Configuration Utility

Executable:

```text
UserAccountControlSettings.exe
```

---

## UAC Levels

### Always Notify

Highest security level.

Prompts for:

* User actions
* Application actions

---

### Notify for Apps

Default setting.

Prompts only when applications attempt changes.

---

### Notify Without Dimming

Same as default but screen remains active.

---

### Never Notify

No security prompts.

⚠️ Not recommended.

---

# Computer Management

## Launch

```text
compmgmt.msc
```

---

## Main Sections

```text
Computer Management
│
├── System Tools
├── Storage
└── Services and Applications
```

---

# Task Scheduler

## Purpose

Automates tasks.

---

## Launch

```text
taskschd.msc
```

---

## Common Uses

* Run scripts
* Launch applications
* Perform backups
* Execute maintenance tasks

---

## Example Trigger

```text
Daily at 10:00 AM
```

---

# Event Viewer

## Purpose

Displays system and application logs.

---

## Launch

```text
eventvwr.msc
```

---

## Main Components

| Component   | Purpose       |
| ----------- | ------------- |
| Left Pane   | Log tree      |
| Middle Pane | Event details |
| Right Pane  | Actions       |

---

## Event Types

| Type          | Meaning                    |
| ------------- | -------------------------- |
| Information   | Normal event               |
| Warning       | Potential issue            |
| Error         | Failure occurred           |
| Success Audit | Successful security action |
| Failure Audit | Failed security action     |

---

## Windows Logs

| Log              | Purpose             |
| ---------------- | ------------------- |
| Application      | Application events  |
| Security         | Security events     |
| Setup            | Installation events |
| System           | OS events           |
| Forwarded Events | Remote events       |

---

# Shared Folders

## Purpose

View network shares.

---

## Sections

### Shares

Shared folders.

Examples:

```text
C$
ADMIN$
```

---

### Sessions

Connected users.

---

### Open Files

Files currently accessed remotely.

---

# Local Users and Groups

## Launch

```text
lusrmgr.msc
```

---

## Sections

| Section | Purpose           |
| ------- | ----------------- |
| Users   | Local accounts    |
| Groups  | Permission groups |

---

# Performance Monitor

## Launch

```text
perfmon
```

---

## Purpose

Monitor system performance.

### Metrics

* CPU
* Memory
* Disk
* Network

---

## Uses

* Troubleshooting
* Performance tuning
* Capacity planning

---

# Device Manager

## Launch

```text
devmgmt.msc
```

---

## Purpose

Manage hardware devices.

### Actions

* Enable devices
* Disable devices
* Update drivers
* View device status

---

# Disk Management

## Launch

```text
diskmgmt.msc
```

---

## Purpose

Manage storage devices.

---

## Common Tasks

### Create New Volume

Set up new storage.

### Extend Partition

Increase partition size.

### Shrink Partition

Reduce partition size.

### Change Drive Letter

Example:

```text
E:
F:
G:
```

---

# Services

## Definition

Background applications managed by Windows.

---

## Launch

```text
services.msc
```

---

## Startup Types

| Type      | Description        |
| --------- | ------------------ |
| Automatic | Starts during boot |
| Manual    | Starts when needed |
| Disabled  | Cannot start       |

---

## Service Properties

Displays:

* Service Name
* Display Name
* Executable Path
* Startup Type
* Status

---

# Windows Management Instrumentation (WMI)

## Definition

Framework for managing Windows systems.

---

## Uses

* Automation
* System management
* Remote administration
* Monitoring

---

## Legacy Tool

```text
WMIC
```

Deprecated.

---

## Modern Replacement

```text
PowerShell
```

---

# System Information (MSInfo32)

## Launch

```text
msinfo32
```

---

## Purpose

Provides detailed system information.

---

## Main Sections

### System Summary

General system specifications.

Examples:

* Processor
* BIOS Version
* Memory

---

### Hardware Resources

Hardware-level information.

---

### Components

Information about:

* Display devices
* Storage devices
* Input devices

---

### Software Environment

Information about:

* Drivers
* Running tasks
* Environment variables
* Network connections

---

# Environment Variables

## Definition

Values used by Windows and applications.

---

## Examples

| Variable | Purpose                 |
| -------- | ----------------------- |
| %WINDIR% | Windows folder          |
| %TEMP%   | Temporary folder        |
| %PATH%   | Executable search paths |

---

## Viewing Environment Variables

### Method 1

```text
msinfo32
```

### Method 2

```text
Advanced System Settings
→ Environment Variables
```

---

# Resource Monitor

## Launch

```text
resmon
```

---

## Purpose

Advanced system monitoring.

---

## Main Sections

### CPU

Processor usage.

### Memory

RAM usage.

### Disk

Disk activity.

### Network

Network activity.

---

## Uses

* Deadlock detection
* File lock troubleshooting
* Process analysis
* Performance diagnostics

---

# Command Prompt

## Launch

```text
cmd
```

---

## Purpose

Command-line interaction with Windows.

---

# Basic Commands

## hostname

Displays computer name.

```cmd
hostname
```

---

## whoami

Displays logged-in user.

```cmd
whoami
```

---

## ipconfig

Displays network configuration.

```cmd
ipconfig
```

---

## ipconfig Help

```cmd
ipconfig /?
```

---

## Clear Screen

```cmd
cls
```

---

## netstat

Displays:

* Network connections
* Listening ports
* Protocol statistics

```cmd
netstat
```

---

## net Command

Network resource management.

```cmd
net
```

---

## Net Help

```cmd
net help
```

---

## User Management Help

```cmd
net help user
```

---

# Windows Registry

## Definition

Hierarchical database storing Windows configuration data.

---

## Stored Information

### User Profiles

User-specific settings.

### Installed Applications

Program configuration.

### Hardware Configuration

Device settings.

### Network Information

Port and connection settings.

---

## Registry Editor

Launch:

```text
regedit
```

---

## Warning

⚠️ Incorrect registry changes can make Windows unstable or unusable.

---

# Process / Workflow

## Windows Startup Process

```text
Power On
    |
    v
Windows Boot
    |
    v
Services Start
    |
    v
Startup Applications
    |
    v
User Login
```

---

## Scheduled Task Workflow

```text
Task Scheduler
       |
       v
Trigger
       |
       v
Action
       |
       v
Program Executes
```

---

## Crash Dump Workflow

```text
System Crash
      |
      v
BSOD
      |
      v
Crash Dump Created
      |
      v
Administrator Analysis
```

---

# Commands / Syntax

## Administrative Utilities

```cmd
msconfig
```

```cmd
compmgmt.msc
```

```cmd
eventvwr.msc
```

```cmd
perfmon
```

```cmd
devmgmt.msc
```

```cmd
diskmgmt.msc
```

```cmd
services.msc
```

```cmd
msinfo32
```

```cmd
resmon
```

```cmd
regedit
```

---

## Command Prompt

```cmd
hostname
```

```cmd
whoami
```

```cmd
ipconfig
```

```cmd
ipconfig /?
```

```cmd
netstat
```

```cmd
net help
```

```cmd
cls
```

---
