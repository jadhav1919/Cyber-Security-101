# Introduction to Digital Forensics

**Forensics** is the process of using scientific methods and procedures to investigate crimes and collect evidence.

When the investigation involves **computers, mobile phones, storage devices, or other digital systems**, it is called **Digital Forensics**.

Digital forensics helps investigators find, preserve, analyze, and present digital evidence that can be used in legal proceedings.

  

# What is Digital Forensics?

**Digital Forensics** is the branch of forensic science that investigates crimes involving digital devices.

Its main goal is to:

* Collect digital evidence.
* Preserve the evidence.
* Analyze the evidence.
* Report the findings.

The evidence must remain unchanged so it can be accepted in court.


# What is Cyber Crime?

A **Cyber Crime** is any criminal activity that involves a digital device or computer network.

Examples include:

* Hacking
* Data theft
* Ransomware attacks
* Identity theft
* Online fraud
* Cyber stalking
* Unauthorized system access

Digital forensics helps investigators determine:

* What happened?
* Who did it?
* When did it happen?
* How was it done?


# Why is Digital Forensics Important?

Today, almost everyone uses digital devices.

Examples:

* Computers
* Laptops
* Mobile phones
* Hard drives
* USB drives
* Cloud storage

These devices often contain valuable evidence that can help solve crimes.

Without digital forensics, much of this evidence could be lost or overlooked.


# Example Investigation

Suppose the police arrest a bank robbery suspect after obtaining a legal search warrant.

During the search, they seize several digital devices:

* Laptop
* Mobile phone
* Hard drive
* USB drive

These devices are handed over to the **Digital Forensics Team** for investigation.


# Evidence Found

During the investigation, the team discovers the following evidence.

### Laptop

They find:

* A digital map of the bank.
* Photos and videos from previous robberies.

This suggests the suspect planned the robbery and may have committed similar crimes before.


### Hard Drive

Investigators find:

* A document showing the bank's entrance and exit routes.
* A document describing the bank's physical security systems.

This indicates that the suspect carefully planned how to enter, escape, and bypass security.


### Mobile Phone

The phone contains:

* Chat messages.
* Call records.
* Communication with accomplices.

This helps investigators identify other people involved in the crime.


### USB Drive

The USB may contain:

* Stolen files.
* Backup copies.
* Additional documents.
* Malware or hacking tools.

Every storage device is carefully examined.


# Why is This Evidence Important?

The collected evidence helps investigators:

* Reconstruct the crime.
* Identify the suspect's actions.
* Support legal proceedings.
* Present evidence in court.

Digital evidence can often prove:

* Planning
* Communication
* Intent
* Criminal activity


# What Does a Digital Forensics Team Do?

A Digital Forensics Team follows a structured process.

Their responsibilities include:

* Securely collecting evidence.
* Preserving evidence.
* Analyzing digital devices.
* Documenting findings.
* Preparing investigation reports.
-------------

# Phases and Types of Digital Forensics

Every digital forensics investigation is different, but investigators generally follow a **standard process**.

The **National Institute of Standards and Technology (NIST)** defines a digital forensics process consisting of **four phases**:

1. Collection
2. Examination
3. Analysis
4. Reporting

Following these phases ensures that evidence is collected and analyzed properly while maintaining its integrity.

# 1. Collection

**Collection** is the first phase of digital forensics.

In this phase, investigators identify and collect all possible digital evidence from the crime scene.

Examples of evidence include:

* Desktop computers
* Laptops
* Mobile phones
* Hard drives
* USB drives
* Memory cards
* Digital cameras

The evidence must be collected **without modifying or damaging the original data**.

Investigators also document every item they collect.

 

## Why is Documentation Important?

Every collected device must be recorded.

Documentation usually includes:

* Device type
* Serial number
* Owner
* Date and time collected
* Investigator's name
* Location where it was found

Proper documentation helps maintain the **Chain of Custody**, ensuring the evidence remains legally valid.
 

## Example

At a crime scene, investigators collect:

* Laptop
* Mobile phone
* USB drive

Each device is:

* Labeled
* Documented
* Safely packaged
* Sent to the forensic laboratory

 

# 2. Examination

After collecting evidence, investigators often have a huge amount of data.

The **Examination** phase focuses on **filtering and extracting only the relevant data**.

Instead of analyzing everything, investigators narrow down the information related to the case.

 

## Example

Suppose a digital camera contains **10,000 photos**.

The investigation only concerns events that happened on **June 5, 2024**.

During examination, investigators filter the photos taken on that specific date.

Only those photos move to the next phase.

 

## Another Example

A computer has:

* 8 user accounts

The investigation concerns only one employee.

The examiner extracts data belonging only to that user.

 

# Difference Between Collection and Examination

| Collection            | Examination                   |
| --------------------- | ----------------------------- |
| Collect all evidence. | Filter relevant evidence.     |
| Nothing is ignored.   | Only useful data is selected. |

 

# 3. Analysis

The **Analysis** phase is the most important part of digital forensics.

Here, investigators study the extracted evidence to determine **what actually happened**.

They combine information from different sources to reconstruct the incident.

This process is called **Correlation**.

 

## What Happens During Analysis?

Investigators determine:

* What happened?
* When did it happen?
* Who performed the actions?
* How did it happen?
* What evidence supports the findings?

The goal is to build a **chronological timeline** of the incident.

 

## Example

Investigators discover:

* Browser history
* Downloaded malware
* Suspicious login
* USB insertion
* File deletion

By arranging these events in order, they reconstruct the attack.

Example timeline:

```text id="m7b8vk"
10:00 AM → User downloads file

10:05 AM → Malware executes

10:08 AM → Attacker gains access

10:15 AM → Sensitive files copied

10:20 AM → Files deleted
```

This helps investigators understand the complete sequence of events.

 

# 4. Reporting

The final phase is **Reporting**.

After completing the investigation, the forensic examiner prepares a detailed report.

This report explains:

* What evidence was collected.
* How the investigation was performed.
* What was discovered.
* Conclusions.
* Recommendations.

The report may be presented to:

* Law enforcement
* Courts
* Company management
* Incident Response teams

 

## Executive Summary

Not everyone reading the report is a technical expert.

Therefore, reports usually include an **Executive Summary**.

An Executive Summary is a short, easy-to-understand overview of:

* What happened.
* Main findings.
* Final conclusion.

It allows managers and executives to understand the incident without reading the entire technical report.

   

# NIST Digital Forensics Process

```text id="rnbs3c"
Collection
      │
      ▼
Examination
      │
      ▼
Analysis
      │
      ▼
Reporting
```

 

# Types of Digital Forensics

Different devices require different investigation techniques.

Therefore, digital forensics has several specialized branches.
 

# 1. Computer Forensics

Investigates desktop and laptop computers.

Evidence may include:

* Documents
* Browser history
* Installed software
* Deleted files
* User accounts
* Event logs

This is the most common type of digital forensics.

 

# 2. Mobile Forensics

Focuses on smartphones and tablets.

Investigators extract evidence such as:

* Call logs
* SMS messages
* WhatsApp chats
* Photos
* Videos
* GPS locations
* Installed apps

 

# 3. Network Forensics

Investigates network activity.

Instead of examining one device, investigators analyze communication across the network.

Evidence includes:

* Network traffic
* Firewall logs
* Router logs
* VPN logs
* Packet captures (PCAP)

Network forensics helps identify attacks moving through the network.

 

# 4. Database Forensics

Investigates databases that store important organizational information.

Investigators look for:

* Unauthorized access
* Data modification
* Data deletion
* Data theft (Data Exfiltration)

 

## What is Data Exfiltration?

**Data Exfiltration** is the unauthorized transfer or theft of data from an organization.

Example:

An attacker steals customer records from a company database.

 

# 5. Cloud Forensics

Investigates systems hosted in cloud environments.

Examples:

* AWS
* Microsoft Azure
* Google Cloud

Cloud forensics can be challenging because investigators often have limited direct access to the cloud infrastructure.

 

# 6. Email Forensics

Investigates emails used during cyber attacks.

Examples include:

* Phishing emails
* Fraudulent messages
* Business Email Compromise (BEC)
* Malicious attachments

Investigators analyze:

* Sender
* Recipient
* Email headers
* Attachments
* Links

----------


# Evidence Acquisition in Digital Forensics

**Evidence Acquisition** is the process of collecting digital evidence from devices **without changing or damaging the original data**.

This is one of the most important phases in digital forensics because even a small change to the original evidence can affect the investigation or make the evidence unacceptable in court.

Different devices (computers, mobile phones, hard drives, USB drives, etc.) may require different collection methods, but some general principles must always be followed.

# 1. Proper Authorization

Before collecting any digital evidence, investigators must obtain **legal authorization**.

This ensures the investigation follows the law and protects the privacy of individuals and organizations.

Without proper authorization, the collected evidence may **not be accepted in court**.

## Example

Police suspect someone of cybercrime.

Before searching the suspect's laptop, they first obtain a **search warrant** from the court.

Only after receiving legal authorization can they collect the evidence.
 

# 2. Chain of Custody

The **Chain of Custody (CoC)** is a document that records **every action performed on the evidence** from the moment it is collected until the investigation is complete.

Its purpose is to prove that the evidence has **not been altered, lost, or tampered with**.


## Why is Chain of Custody Important?

Imagine investigators collect a hard drive.

After a few days:

* Nobody knows where it was stored.
* Multiple people handled it.
* Some files appear to have changed.

Now the court cannot determine:

* Who accessed the evidence.
* Whether it was modified.
* Whether it is still trustworthy.

A Chain of Custody prevents this problem.


## What Information Does a Chain of Custody Contain?

A Chain of Custody typically records:

* Evidence description
* Evidence type
* Person who collected it
* Date and time of collection
* Storage location
* Every person who accessed it
* Date and time of every access

This creates a complete history of the evidence.

## Benefits of Chain of Custody

* Maintains evidence integrity.
* Tracks every person who handled the evidence.
* Prevents unauthorized access.
* Makes the evidence legally admissible.

  

# 3. Write Blockers

A **Write Blocker** is a hardware or software device that allows investigators to **read data from a storage device without writing or modifying anything on it**.

It protects the original evidence from accidental changes.


## Why Are Write Blockers Needed?

Suppose investigators connect a suspect's hard drive directly to a forensic workstation.

The operating system may automatically:

* Update timestamps.
* Create hidden files.
* Modify metadata.
* Write system information.

Even these small changes alter the original evidence.

## Solution: Write Blocker

A write blocker prevents the forensic workstation from writing anything to the suspect's drive.

The investigator can:

* Read data.
* Copy data.
* Create forensic images.

But **cannot accidentally modify the original device**.

## Advantages of Write Blockers

* Prevent accidental modification.
* Preserve timestamps.
* Protect metadata.
* Maintain evidence integrity.
* Ensure legal admissibility.

------------

# Windows Forensics

One of the most common devices investigated during digital forensic investigations is a **Windows computer or laptop**.

Since Windows is widely used, it is frequently involved in cybercrime investigations.

The first step in Windows forensics is to **collect forensic images** of the system.

A **forensic image** is an **exact bit-by-bit copy** of the original data.

> **Bit-by-bit copy:** Every bit of data is copied exactly as it exists on the original device, including deleted files, unused space, and system data.

The original device is **never analyzed directly**. Instead, investigators analyze the forensic image to preserve the original evidence.

 

# Types of Forensic Images

When investigating a Windows system, investigators usually collect **two types of forensic images**:

1. Disk Image
2. Memory Image

 

# 1. Disk Image

A **Disk Image** is a complete bit-by-bit copy of the computer's storage device, such as:

* HDD (Hard Disk Drive)
* SSD (Solid State Drive)

It contains **non-volatile data**.

 

## What is Non-Volatile Data?

**Non-volatile data** remains stored **even after the computer is shut down or restarted**.

This means the data is permanent until someone deletes or modifies it.

 

## What Does a Disk Image Contain?

A disk image may include:

* Documents
* Photos
* Videos
* Installed programs
* Browser history
* Downloads
* User accounts
* Registry files
* Deleted files
* File system metadata

 

## Example

Suppose a suspect stored stolen documents on their laptop.

Even if the laptop is turned off, those documents remain on the hard drive.

Investigators can recover them from the **disk image**.

 

# 2. Memory Image

A **Memory Image** is a copy of the computer's **RAM (Random Access Memory)**.

RAM stores information that the operating system is currently using.

It contains **volatile data**.

  
## What is Volatile Data?

**Volatile data** is temporary data stored in RAM.

It is **lost immediately** when the computer is:

* Shut down
* Restarted
* Powered off

 

## What Does a Memory Image Contain?

A memory image may contain:

* Running processes
* Running programs
* Open files
* Active user sessions
* Network connections
* Encryption keys
* Malware running in memory
* Passwords stored in RAM

 

## Why Must Memory Be Collected First?

Memory is temporary.

If investigators restart or shut down the computer before collecting RAM, all volatile data disappears forever.

Therefore:

> **Memory image should always be acquired before powering off the system.**

 

## Example

Suppose ransomware is currently running.

If investigators immediately shut down the computer:

* Running malware disappears from RAM.
* Current network connections disappear.
* Encryption keys may be lost.

Capturing the **memory image first** preserves this valuable evidence.

 

# Disk Image vs Memory Image

| Disk Image                                 | Memory Image                                                         |
| ------------------------------------------ | -------------------------------------------------------------------- |
| Copies HDD/SSD.                            | Copies RAM.                                                          |
| Contains non-volatile data.                | Contains volatile data.                                              |
| Data remains after shutdown.               | Data is lost after shutdown.                                         |
| Documents, browser history, deleted files. | Running processes, open files, network connections, encryption keys. |

 

# Windows Forensics Workflow

```text id="pqur9v"
Windows Computer
        │
        ▼
Capture Memory Image (First)
        │
        ▼
Capture Disk Image
        │
        ▼
Analyze Both Images
```

 

# Popular Windows Forensics Tools

Several tools are used to acquire and analyze Windows forensic images.

  

# 1. FTK Imager

**FTK Imager** is one of the most widely used forensic tools.

It is mainly used for:

* Acquiring disk images.
* Viewing disk image contents.
* Basic forensic analysis.

It provides a **graphical user interface (GUI)**, making it beginner-friendly.

 

## Main Features

* Create disk images.
* View image contents.
* Export files.
* Calculate hash values.
* Preview deleted files.

 

## Used For

* Disk image acquisition.
* Basic disk image analysis.

 

# 2. Autopsy

**Autopsy** is a popular **open-source digital forensics platform**.

Unlike FTK Imager, Autopsy focuses mainly on **analyzing** forensic images.

Investigators import a disk image into Autopsy, and it automatically performs detailed analysis.

 

## Features

* Keyword searching.
* Deleted file recovery.
* File metadata analysis.
* Browser history analysis.
* Email analysis.
* Extension mismatch detection.
* Timeline generation.

 

## What is Extension Mismatch Detection?

Sometimes attackers rename malicious files.

Example:

```text id="rw7jyu"
virus.exe

↓

holiday_photo.jpg
```

The filename appears to be an image, but the file is actually an executable program.

Autopsy can detect these mismatches.

 

# 3. DumpIt

**DumpIt** is a tool used to **capture memory images** from Windows systems.

It uses a **command-line interface (CLI)**.

 

## Main Purpose

* Acquire RAM (memory) images.
* Preserve volatile evidence before shutdown.
 

## Used For

Memory acquisition only.

 

# 4. Volatility

**Volatility** is one of the most popular **open-source memory forensic tools**.

It is used to analyze memory images captured by tools such as DumpIt.

 

## What Can Volatility Analyze?

Using different plugins, Volatility can examine:

* Running processes
* Network connections
* DLLs
* Registry information
* Command history
* Malware in memory
* Loaded drivers
* Open files

 

## What is a Plugin?

A **plugin** is a small module that performs a specific forensic task.

Each plugin analyzes a different artifact from the memory image.

Example:

One plugin lists running processes.

Another plugin lists active network connections.



## Supported Operating Systems

Volatility supports:

* Windows
* Linux
* macOS
* Android


# Tool Summary

| Tool           | Purpose                              |
| -------------- | ------------------------------------ |
| **FTK Imager** | Acquire and view disk images.        |
| **Autopsy**    | Analyze disk images in detail.       |
| **DumpIt**     | Capture memory (RAM) images.         |
| **Volatility** | Analyze memory images using plugins. |

---

# Windows Forensics Process

```text id="7mjlwm"
Windows Computer
        │
        ▼
Capture Memory Image
   (DumpIt)
        │
        ▼
Analyze Memory
 (Volatility)
        │
        ▼
Capture Disk Image
 (FTK Imager)
        │
        ▼
Analyze Disk Image
   (Autopsy)
```

---

# Metadata Analysis Tools

## 1. pdfinfo

**Purpose:** Reads metadata from PDF files.

### What it can show

* Creator software
* Author
* Creation date
* Last modification date
* Number of pages
* PDF version
* Whether the PDF is encrypted

### Command

```bash
pdfinfo DOCUMENT.pdf
```

### Example

```bash
pdfinfo ransom_note.pdf
```

### Why is it useful?

Investigators use **pdfinfo** to determine:

* Which software created the document.
* When it was created or modified.
* Basic information about the PDF.



## 2. exiftool

**Purpose:** Reads (and can also modify) metadata from images and many other file types.

### What it can show

* Camera/Phone model
* Date and time the photo was taken
* GPS coordinates
* Camera settings
* File metadata

### Command

```bash
exiftool IMAGE.jpg
```

### Example

```bash
exiftool suspect_photo.jpg
```

### Why is it useful?

Investigators use **ExifTool** to determine:

* Where a photo was taken (GPS)
* When it was taken
* Which device captured it
* Other hidden metadata


