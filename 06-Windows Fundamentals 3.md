# Windows Fundamentals 3 - Security Features

## Overview

This module focuses on the built-in security features of Windows designed to protect:

* Operating System
* User Accounts
* Files and Data
* Applications
* Network Traffic
* System Recovery

Topics Covered:

* Windows Update
* Windows Security
* Microsoft Defender Antivirus
* Windows Firewall
* Microsoft Defender SmartScreen
* Device Security
* TPM (Trusted Platform Module)
* BitLocker
* Volume Shadow Copy Service (VSS)
* Living Off The Land (LOTL)

---

# Windows Update

## Definition

Windows Update is a Microsoft service that provides:

* Security updates
* Bug fixes
* Feature updates
* Microsoft Defender updates

---

## Patch Tuesday

### Definition

Microsoft usually releases updates on:

```text
Second Tuesday of every month
```

Known as:

```text
Patch Tuesday
```

---

## Purpose

Updates help:

* Fix vulnerabilities
* Improve stability
* Add new features
* Update malware definitions

---

## Accessing Windows Update

### Method 1

```text
Settings → Update & Security → Windows Update
```

### Method 2

```cmd
control /name Microsoft.WindowsUpdate
```

---

## Important Points

* Updates may require a reboot.
* Critical updates can be released outside Patch Tuesday.
* Modern Windows versions force important updates eventually.
* Delaying updates increases security risk.

---

# Windows Security

## Definition

Central dashboard for Windows security features.

---

## Access

```text
Settings → Windows Security
```

---

## Protection Areas

| Area                          | Purpose                               |
| ----------------------------- | ------------------------------------- |
| Virus & Threat Protection     | Malware defense                       |
| Firewall & Network Protection | Network traffic control               |
| App & Browser Control         | Phishing and malicious app protection |
| Device Security               | Hardware security                     |

---

## Status Icons

| Color  | Meaning                   |
| ------ | ------------------------- |
| Green  | Protected                 |
| Yellow | Recommendation available  |
| Red    | Immediate action required |

---

# Microsoft Defender Antivirus

## Definition

Built-in antivirus solution in Windows.

---

# Current Threats

## Scan Options

### Quick Scan

Checks common malware locations.

---

### Full Scan

Checks:

* All files
* Running programs

Takes longer to complete.

---

### Custom Scan

Allows selection of:

* Specific folders
* Specific drives
* Specific files

---

# Threat History

## Last Scan

Displays latest scan activity.

---

## Quarantined Threats

Threats isolated from the system.

---

## Allowed Threats

Threats manually permitted by the user.

⚠️ Only allow trusted items.

---

# Virus & Threat Protection Settings

## Real-Time Protection

### Purpose

Monitors files continuously.

Detects:

* Malware
* Viruses
* Suspicious activity

---

## Cloud-Delivered Protection

### Purpose

Uses Microsoft's cloud intelligence.

Benefits:

* Faster detection
* Latest threat intelligence

---

## Automatic Sample Submission

### Purpose

Uploads suspicious files to Microsoft.

Helps improve detection capabilities.

---

# Controlled Folder Access

## Purpose

Protects files against ransomware.

---

## Protected Areas

* Documents
* Pictures
* Videos
* Other selected folders

---

## Benefit

Blocks unauthorized applications from modifying files.

---

# Exclusions

## Definition

Files or folders excluded from scanning.

---

## Usage

Used to reduce false positives.

⚠️ Improper exclusions can introduce security risks.

---

# Ransomware Protection

## Purpose

Protects against file encryption attacks.

Depends on:

```text
Real-Time Protection
```

and

```text
Controlled Folder Access
```

---

# Firewall and Network Protection

## What is a Firewall?

A firewall controls network traffic entering and leaving a system.

Think of it as:

```text
Security Guard
        |
        v
Allowed Traffic
Blocked Traffic
```

---

# Windows Firewall Profiles

## Domain Profile

### Used For

Corporate environments.

Requirements:

* Domain Controller
* Active Directory

---

## Private Profile

### Used For

Trusted networks.

Examples:

* Home Wi-Fi
* Personal LAN

---

## Public Profile

### Used For

Untrusted networks.

Examples:

* Airports
* Cafes
* Hotels

---

# Firewall Actions

## Enable Firewall

Protects network communications.

---

## Disable Firewall

⚠️ Not recommended.

---

## Block Incoming Connections

Blocks unsolicited traffic.

---

# Allow an App Through Firewall

## Purpose

Permits applications to communicate.

Examples:

* Web browsers
* Remote Desktop
* File sharing

---

# Advanced Firewall

## Launch

```cmd
WF.msc
```

---

## Purpose

Advanced rule creation.

Examples:

* Allow specific ports
* Block IP addresses
* Restrict applications

---

# Microsoft Defender SmartScreen

## Definition

Protection against:

* Phishing websites
* Malicious downloads
* Untrusted applications

---

## Modes

| Mode  | Purpose           |
| ----- | ----------------- |
| Warn  | Notify user       |
| Block | Prevent execution |
| Off   | No protection     |

---

# SmartScreen Components

## Check Apps and Files

Analyzes downloaded files.

---

## Reputation-Based Protection

Uses Microsoft reputation services.

---

# Exploit Protection

## Definition

Built-in mitigation against exploitation techniques.

---

## Purpose

Protects applications from:

* Memory corruption
* Buffer overflow attacks
* Exploit chains

---

## Recommendation

Keep default settings.

---

# Device Security

## Definition

Hardware-based security protections.

---

# Core Isolation

## Purpose

Separates critical operating system processes.

---

## Memory Integrity

### Function

Prevents malicious code injection into protected processes.

---

## Benefits

Protects:

* Kernel
* System processes
* Security services

---

# Trusted Platform Module (TPM)

## Definition

TPM = Trusted Platform Module

Hardware security chip.

---

## Functions

### Cryptographic Operations

Performs secure encryption.

---

### Secure Storage

Stores:

* Encryption keys
* Certificates
* Credentials

---

### Anti-Tampering

Protects security functions from malware.

---

# TPM Benefits

| Feature               | Benefit                  |
| --------------------- | ------------------------ |
| Secure Keys           | Protects encryption keys |
| Secure Boot Support   | Prevents tampering       |
| BitLocker Integration | Strong disk encryption   |

---

# BitLocker

## Definition

Microsoft's full disk encryption technology.

---

## Purpose

Protects data if:

* Laptop is stolen
* Drive is removed
* Device is lost

---

## Best Configuration

```text
BitLocker + TPM
```

---

## Benefits

### Protects

* Operating system files
* User files
* Entire disk contents

---

## Threats Mitigated

* Data theft
* Offline attacks
* Lost devices

---

# Volume Shadow Copy Service (VSS)

## Definition

Creates snapshots of system data.

Also known as:

* Shadow Copy
* Point-in-Time Copy

---

# Purpose

Allows:

* Restore points
* File recovery
* System recovery

---

# Storage Location

```text
System Volume Information
```

---

# Common Uses

## Create Restore Point

Manual system checkpoint.

---

## System Restore

Rollback to previous state.

---

## Configure Protection

Control storage usage.

---

## Delete Restore Points

Remove stored snapshots.

---

# Security Relevance

## Ransomware Target

Attackers often delete shadow copies.

Reason:

```text
Prevent Victim Recovery
```

---

## Common Malware Behavior

```cmd
vssadmin delete shadows
```

Used by ransomware to remove recovery options.

---

# Living Off The Land (LOTL)

## Definition

Attackers abuse legitimate Windows tools instead of dropping malware.

---

## Why Attackers Use LOTL

* Avoid detection
* Blend into normal activity
* Use trusted binaries

---

# Common LOTL Tools

| Tool       | Purpose                    |
| ---------- | -------------------------- |
| PowerShell | Automation                 |
| CMD        | Command execution          |
| WMIC       | System management          |
| MSHTA      | HTML application execution |
| Certutil   | File transfer/encoding     |
| Rundll32   | DLL execution              |
| Regsvr32   | Script execution           |

---

# Process / Workflow

## Windows Security Architecture

```text
Windows Update
        |
        v
Microsoft Defender
        |
        v
Firewall
        |
        v
SmartScreen
        |
        v
Device Security
        |
        v
Protected System
```

---

## Defender Scan Workflow

```text
File Downloaded
        |
        v
Real-Time Protection
        |
        v
Threat Detected?
      /   \
    Yes    No
     |      |
     v      v
Quarantine Continue
```

---

## Firewall Traffic Flow

```text
Internet
    |
    v
Windows Firewall
    |
+---+---+
|       |
Allow  Block
```

---

## Ransomware Protection Workflow

```text
Application
      |
      v
Controlled Folder Access
      |
      v
Authorized?
    /     \
  Yes      No
   |        |
   v        v
Modify   Blocked
```

---

# Commands / Syntax

## Open Windows Update

```cmd
control /name Microsoft.WindowsUpdate
```

---

## Open Firewall

```cmd
WF.msc
```

---

## Open Windows Security

```text
Settings → Windows Security
```

---

## Common VSS Command

```cmd
vssadmin list shadows
```

---

## Delete Shadow Copies

```cmd
vssadmin delete shadows
```

 Often abused by ransomware.

---

# Tables

## Windows Security Components

| Component          | Purpose                |
| ------------------ | ---------------------- |
| Windows Update     | Security patches       |
| Defender Antivirus | Malware protection     |
| Firewall           | Network filtering      |
| SmartScreen        | Web/App protection     |
| Device Security    | Hardware protection    |
| TPM                | Cryptographic security |
| BitLocker          | Disk encryption        |
| VSS                | Recovery snapshots     |

---

## Defender Scan Types

| Scan   | Scope                  |
| ------ | ---------------------- |
| Quick  | Common locations       |
| Full   | Entire system          |
| Custom | Selected files/folders |

---

