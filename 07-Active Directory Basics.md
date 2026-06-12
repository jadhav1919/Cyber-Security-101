# Active Directory (AD) Fundamentals

## Overview

Active Directory (AD) is Microsoft's directory service used in companies and organizations.

It helps administrators manage:

* Users
* Computers
* Servers
* Printers
* Groups
* Permissions
* Security Policies

Think of Active Directory as a **central database** that stores information about everything in a company's network.

---

# Why Active Directory?

Without Active Directory:

```text
100 Computers
100 User Accounts
100 Passwords
100 Configurations
```

An administrator would need to manage every device separately.

With Active Directory:

```text
Domain Controller
       |
       |
-----------------------
|     |      |       |
PC1  PC2   PC3    PC4
```

Everything can be managed from one place.

---

# Active Directory Domain Services (AD DS)

## Definition

AD DS is the core service of Active Directory.

It stores information about all objects inside a domain.

---

## Objects Stored in AD

Examples:

* Users
* Computers
* Groups
* Printers
* Shared Folders
* Services

---

# Active Directory Objects

## What is an Object?

Anything stored in Active Directory is called an Object.

Examples:

```text
User
Computer
Printer
Group
Folder
```

---

# Users

## Definition

A user account represents a person or service.

Users are Security Principals.

---

## What is a Security Principal?

An object that:

* Can log in
* Can be authenticated
* Can receive permissions

---

## Types of Users

### 1. Human Users

Example:

```text
John
Alice
Mark
```

Used by employees.

---

### 2. Service Users

Used by applications.

Examples:

```text
IIS
MSSQL
Apache
```

These accounts run services.

---

# Machines (Computers)

## Definition

Whenever a computer joins a domain, AD creates a machine account.

---

## Example

Computer Name:

```text
PC01
```

Machine Account:

```text
PC01$
```

Notice the dollar sign ($).

---

## Machine Account Facts

* Security Principal
* Has its own password
* Can authenticate to domain
* Password rotates automatically

---

## Machine Account Password

Typically:

```text
120 random characters
```

Automatically changed by Windows.

---

# Security Groups

## Definition

Groups are collections of users and computers.

Instead of giving permissions to each user individually, permissions are assigned to groups.

---

## Example

Without Groups:

```text
Alice -> Printer Access
Bob -> Printer Access
John -> Printer Access
```

With Groups:

```text
Employees Group
      |
----------------
|      |       |
Alice Bob    John
```

Give permission once to the group.

---

# Benefits of Groups

* Easier management
* Less work
* Better organization
* Centralized permissions

---

# Important Default Groups

## Domain Admins

### Permissions

Full control of the entire domain.

Can manage:

* Users
* Computers
* Servers
* Domain Controllers

---

## Server Operators

Can manage Domain Controllers.

Cannot change admin memberships.

---

## Backup Operators

Can access any file.

Used for backups.

---

## Account Operators

Can create and modify accounts.

---

## Domain Users

Contains all users.

---

## Domain Computers

Contains all computers.

---

## Domain Controllers

Contains all Domain Controllers.

---

# Active Directory Users and Computers (ADUC)

## Purpose

Main tool used to manage:

* Users
* Groups
* Computers
* OUs

---

## Launch

```text
Start Menu
→ Active Directory Users and Computers
```

---

# Organizational Units (OU)

## Definition

Containers used to organize users and computers.

---

## Example

Company Structure:

```text
THM
|
|-- IT
|-- Sales
|-- Marketing
|-- Management
|-- R&D
```

Each department gets its own OU.

---

# Why Use OUs?

Used for:

* Organization
* Applying policies
* Easier administration

---

## Important Rule

A user can belong to:

```text
Only ONE OU
```

---

# Default Containers

## Builtin

Contains default Windows groups.

---

## Computers

New computers join here.

---

## Domain Controllers

Contains DCs.

---

## Users

Default users and groups.

---

## Managed Service Accounts

Service accounts used by applications.

---

# OU vs Security Groups

## Organizational Unit (OU)

Purpose:

```text
Apply Policies
```

Example:

```text
Sales Department Policy
```

---

## Security Group

Purpose:

```text
Grant Permissions
```

Example:

```text
Printer Access
Shared Folder Access
```

---

## Comparison Table

| OU                | Security Group       |
| ----------------- | -------------------- |
| Used for policies | Used for permissions |
| User in one OU    | User in many groups  |
| Organization      | Access Control       |

---

# Delegation

## Definition

Giving limited administrative rights to specific users.

---

## Example

Helpdesk employee:

```text
Reset Passwords
```

without becoming Domain Admin.

---

## Benefit

Domain Admin does not need to do every task.

---

# Computers in Active Directory

## Types of Computers

### Workstations

Employee computers.

Examples:

```text
Desktop PCs
Laptops
```

---

### Servers

Provide services.

Examples:

```text
Web Server
Database Server
File Server
```

---

### Domain Controllers

Most important systems.

Store:

* User Accounts
* Password Hashes
* Policies

---

# Recommended OU Structure

```text
thm.local
|
|-- Workstations
|-- Servers
|-- Domain Controllers
```

---

# Group Policy Objects (GPO)

## Definition

A collection of settings applied to users or computers.

---

## Purpose

Automatically configure systems.

---

## Examples

* Password policy
* Disable Control Panel
* Lock screen automatically
* Restrict USB devices

---

# GPO Management Tool

```text
Group Policy Management
```

---

# How GPO Works

```text
Create GPO
      |
      v
Link GPO to OU
      |
      v
Policy Applied
```

---

# Example GPO

## Password Policy

Require:

```text
Minimum 10 characters
```

---

## Auto Lock Screen

Lock computer after:

```text
5 minutes
```

---

## Restrict Control Panel

Users cannot open:

```text
Control Panel
Settings
```

---

# SYSVOL

## Definition

Network share that stores GPO files.

---

## Location

```text
C:\Windows\SYSVOL\sysvol
```

---

## Purpose

Distributes policies to computers.

---

# Force Policy Update

Command:

```powershell
gpupdate /force
```

Used when GPO changes don't apply immediately.

---

# Authentication in Active Directory

## Two Protocols

1. Kerberos
2. NetNTLM

---

# Kerberos Authentication

## Default Authentication Protocol

Used by modern Windows domains.

---

## Key Components

### KDC

Key Distribution Center

Usually located on Domain Controller.

---

### TGT

Ticket Granting Ticket

Used to request more tickets.

---

### TGS

Ticket Granting Service Ticket

Used to access specific services.

---

# Kerberos Flow

```text
User Login
    |
    v
KDC
    |
    v
TGT Issued
    |
    v
Request TGS
    |
    v
Access Service
```

---

# Benefits of Kerberos

* Secure
* Fast
* Password not repeatedly sent
* Ticket-based authentication

---

# NetNTLM Authentication

## Legacy Protocol

Older authentication method.

Still enabled in many environments.

---

# NetNTLM Process

```text
Client
   |
Authentication Request
   |
Server
   |
Challenge
   |
Client
   |
Response
   |
Domain Controller
```

---

## Important

Password is never sent directly.

Only challenge-response data is sent.

---

# Domains

## Definition

A logical group of users, computers, and resources.

Example:

```text
thm.local
```

---

# Trees

## Definition

Multiple domains sharing the same namespace.

---

## Example

```text
thm.local
|
|-- uk.thm.local
|
|-- us.thm.local
```

This structure is called a Tree.

---

# Benefits

* Easier management
* Separate administration
* Different policies

---

# Enterprise Admins

## Definition

Highest administrative group.

Controls:

```text
All Domains
All Domain Controllers
Entire Enterprise
```

---

# Forest

## Definition

Collection of multiple Trees.

---

## Example

```text
thm.local

mht.local
```

Combined together:

```text
Forest
```

---

# Forest Diagram

```text
Forest
|
|-- thm.local
|
|-- mht.local
```

---

# Trust Relationships

## Definition

Allow users from one domain to access resources in another domain.

---

# One-Way Trust

Example:

```text
AAA trusts BBB
```

Result:

```text
BBB users
can access AAA resources
```

---

# Two-Way Trust

Both domains trust each other.

```text
AAA <----> BBB
```

Users from both domains can be authorized.

---

# Important Note

Trust does NOT automatically give access.

It only allows access to be granted.

Administrator still decides permissions.

---

# Active Directory Hierarchy

```text
Forest
|
|-- Tree
|    |
|    |-- Domain
|         |
|         |-- OU
|               |
|               |-- Users
|               |-- Computers
|               |-- Groups
```

---

# Quick Revision

## AD DS

Stores all domain objects.

---

## User

Represents people or services.

---

## Machine Account

Computer account ending with "$".

Example:

```text
PC01$
```

---

## Security Group

Used for permissions.

---

## OU

Used for organization and policies.

---

## GPO

Used to enforce settings.

---

## SYSVOL

Stores GPO files.

---

## Kerberos

Default authentication protocol.

Uses:

```text
TGT
TGS
```

---

## NetNTLM

Legacy authentication protocol.

Uses challenge-response.

---

## Domain

Logical network container.

---

## Tree

Multiple domains with same namespace.

---

## Forest

Multiple trees together.

---

## Trust

Allows cross-domain access.

---

