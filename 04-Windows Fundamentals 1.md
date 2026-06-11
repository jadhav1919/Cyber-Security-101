# Windows Fundamentals 1

## Overview

This module introduces the Windows Operating System, its user interface, file system, user accounts, permissions, security mechanisms, system settings, and Task Manager.

Topics Covered:

* Windows Versions
* Windows Desktop GUI
* NTFS File System
* Windows Directory Structure
* User Accounts & Groups
* User Account Control (UAC)
* Settings vs Control Panel
* Task Manager

---

# Windows Operating System Overview

## Definition

Windows is Microsoft's operating system for desktops, laptops, and servers.

## Evolution of Windows

| Version             | Notes                   |
| ------------------- | ----------------------- |
| Windows XP          | Very popular            |
| Windows Vista       | Poor reception          |
| Windows 7           | Widely adopted          |
| Windows 8/8.1       | Short lifespan          |
| Windows 10          | Long-term mainstream OS |
| Windows 11          | Current desktop OS      |
| Windows Server 2025 | Current server OS       |

---

## Windows 11 Editions

### Home

Designed for home users.

### Pro

Includes advanced business and security features.

### Key Difference

| Feature              | Home | Pro |
| -------------------- | ---- | --- |
| BitLocker Encryption | ❌    | ✅   |

---

# Windows Desktop GUI

## Definition

GUI (Graphical User Interface) is the visual interface displayed after login.

---

## Main Components

### Desktop

Stores shortcuts for:

* Files
* Folders
* Applications

### Start Menu

Provides access to:

* Installed applications
* Settings
* Power options
* User profile

### Search Box

Used to search:

* Files
* Applications
* Settings

### Task View

Displays open windows and virtual desktops.

### Taskbar

Displays:

* Running applications
* Pinned applications

### Notification Area

Located bottom-right corner.

Contains:

* Clock
* Network status
* Volume control
* System notifications

---

# Desktop Customization

## Right-Click Desktop Options

Allows:

* Change icon size
* Sort icons
* Create folders
* Create shortcuts
* Open Display Settings
* Open Personalization Settings

---

## Display Settings

Used for:

* Screen resolution
* Orientation
* Multi-monitor setup

---

## Personalization

Used for:

* Wallpaper
* Themes
* Colors
* Fonts

---

# Start Menu

## Purpose

Central location for:

* Applications
* User actions
* System settings

---

## Start Menu Sections

### Account Section

Contains:

* User profile
* Documents
* Pictures
* Settings
* Power options

---

### Applications Section

Displays:

* Recently Added Apps
* Installed Apps

Apps are organized alphabetically.

---

### Tiles Section

Contains pinned applications.

Examples:

* Browser
* Calculator
* Mail

---

# Taskbar

## Purpose

Displays active applications.

### Features

* Open applications
* Pinned applications
* Task View
* Search

---

## Preview Feature

Hovering over an application shows:

* Thumbnail preview
* Application name

---

# Notification Area

## Purpose

Displays system status information.

### Common Icons

| Icon    | Purpose        |
| ------- | -------------- |
| Clock   | Time/Date      |
| Network | Connectivity   |
| Volume  | Audio Settings |

---

# NTFS File System

## Definition

NTFS = New Technology File System

Modern Windows file system.

---

## Previous File Systems

| File System | Description                  |
| ----------- | ---------------------------- |
| FAT16       | Older file system            |
| FAT32       | Common in USB devices        |
| HPFS        | High Performance File System |
| NTFS        | Modern Windows file system   |

---

## NTFS Features

### Supports Large Files

Files larger than:

```text
4 GB
```

---

### Permissions

Allows granular access control.

---

### Compression

Reduces storage usage.

---

### Encryption

Uses:

```text
EFS (Encrypting File System)
```

---

### Journaling

Maintains logs to recover from failures.

---

# NTFS Permissions

## Permission Types

| Permission           | Purpose         |
| -------------------- | --------------- |
| Full Control         | Complete access |
| Modify               | Edit and delete |
| Read & Execute       | View and run    |
| List Folder Contents | View folder     |
| Read                 | View only       |
| Write                | Create/Edit     |

---

## Viewing Permissions

### Steps

1. Right-click file/folder
2. Select Properties
3. Open Security tab

---

# Alternate Data Streams (ADS)

## Definition

NTFS feature allowing multiple data streams in a file.

---

## Purpose

Stores:

* Metadata
* Additional file information

---

## Security Relevance

Attackers may:

* Hide malicious code
* Hide data

---

## Example Use

Downloaded files receive metadata indicating:

```text
Downloaded from Internet
```

---

# Windows Directory Structure

## Windows Folder

Default location:

```text
C:\Windows
```

Contains operating system files.

---

# Environment Variables

## Definition

Variables containing system information.

### Examples

| Variable     | Purpose           |
| ------------ | ----------------- |
| %windir%     | Windows directory |
| %temp%       | Temporary files   |
| %systemroot% | System root       |

---

## Important Environment Variable

```text
%windir%
```

Points to:

```text
C:\Windows
```

---

# System32

## Location

```text
C:\Windows\System32
```

---

## Purpose

Stores critical operating system files.

Contains:

* DLL files
* Drivers
* Utilities
* Administrative tools

---

## Warning

Deleting files from System32 can make Windows unusable.

---

# User Accounts

## Types of Accounts

### Administrator

Can:

* Install software
* Create users
* Delete users
* Modify settings

---

### Standard User

Can:

* Use applications
* Modify personal files

Cannot:

* Install software requiring admin rights
* Change system settings

---

# User Profiles

## Location

```text
C:\Users
```

---

## Example

```text
C:\Users\Max
```

---

## Common Profile Folders

| Folder    |
| --------- |
| Desktop   |
| Documents |
| Downloads |
| Pictures  |
| Music     |

---

# Local Users and Groups

## Tool

```text
lusrmgr.msc
```

---

## Launch Method

```text
Run → lusrmgr.msc
```

---

## Sections

### Users

Contains local accounts.

### Groups

Contains local groups.

---

# Groups

## Definition

Collections of users sharing permissions.

---

## Benefits

* Easier permission management
* Role-based access

---

## Example Groups

| Group          | Purpose             |
| -------------- | ------------------- |
| Administrators | Full system control |
| Users          | Standard access     |
| Guests         | Limited access      |

---

# User Account Control (UAC)

## Definition

Security feature preventing unauthorized administrative actions.

---

## Purpose

Reduces malware impact.

---

## How UAC Works

Administrator accounts normally run without elevated privileges.

When a privileged action occurs:

1. UAC Prompt appears
2. User confirms action
3. Action executes

---

## Example Actions

* Software installation
* Registry modifications
* System changes

---

## Benefits

### Prevents

* Unauthorized changes
* Malware execution
* Silent software installation

---

# Settings vs Control Panel

## Settings

Modern configuration interface.

Introduced in:

```text
Windows 8
```

---

## Common Tasks

* Wallpaper
* Updates
* Accounts
* Network

---

# Control Panel

## Purpose

Advanced system configuration.

---

## Common Tasks

* Programs and Features
* User Accounts
* Network Settings
* Administrative Tools

---

## Installed Programs

Location:

```text
Control Panel
→ Programs
→ Programs and Features
```

Displays:

* Program Name
* Publisher
* Version

---

# Task Manager

## Definition

Utility used to monitor and manage processes.

---

## Opening Task Manager

### Method 1

```text
Right-click Taskbar
→ Task Manager
```

### Method 2

```text
Ctrl + Shift + Esc
```

---

# Task Manager Sections

## Processes

Displays:

* Running applications
* Background processes

---

## Performance

Displays:

* CPU usage
* Memory usage
* Disk usage
* Network usage

---

## Users

Displays:

* Logged-in users
* Resource usage

---

## Services

Displays:

* Running services
* Stopped services

---

# Process / Workflow

## User Login Process

```text
Login Screen
      |
      v
User Authentication
      |
      v
Profile Creation
      |
      v
Desktop GUI
```

---

## UAC Workflow

```text
User Action
      |
      v
Requires Admin Rights?
      |
      +---- No ---> Execute
      |
      +---- Yes
               |
               v
         UAC Prompt
               |
               v
      Allow / Deny
```

---

## NTFS Permission Model

```text
File / Folder
      |
      +--> User Permissions
      |
      +--> Group Permissions
      |
      +--> Special Permissions
```

---

# Tables

## Windows Versions

| Version | Status                   |
| ------- | ------------------------ |
| XP      | End of Life              |
| Vista   | End of Life              |
| 7       | End of Life              |
| 8/8.1   | End of Life              |
| 10      | Supported until Oct 2025 |
| 11      | Current Desktop OS       |

---

## Administrator vs Standard User

| Feature               | Administrator | Standard User |
| --------------------- | ------------- | ------------- |
| Install Software      | ✅             | ❌             |
| Create Users          | ✅             | ❌             |
| Modify System         | ✅             | ❌             |
| Modify Personal Files | ✅             | ✅             |

---

