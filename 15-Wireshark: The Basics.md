# Wireshark Basics 

## Overview

**Wireshark** is an open-source, cross-platform network protocol analyzer used for:

* Capturing live network traffic
* Analyzing packet captures (PCAP files)
* Troubleshooting network issues
* Investigating security incidents
* Learning network protocols

> **Note:** Wireshark is not an Intrusion Detection System (IDS). It only captures and analyzes packets without modifying them.

---

# Learning Objectives

* Navigate the Wireshark interface
* Load and inspect PCAP files
* Understand packet structure and OSI layers
* Apply display filters
* Follow network conversations
* Export packets and objects

---

# Wireshark Interface

## Main Components

### 1. Toolbar

Provides quick access to:

* Open files
* Start/Stop capture
* Export data
* Statistics
* Filtering tools

### 2. Display Filter Bar

Used to filter displayed packets.

Example:

```text
http
```

```text
ip.addr == 192.168.1.10
```

---

### 3. Recent Files

Shows previously opened capture files.

---

### 4. Capture Interfaces

Available network interfaces for packet capturing.

Examples:

* eth0
* ens33
* lo (Loopback)

---

### 5. Status Bar

Displays:

* Capture status
* Number of packets
* Current profile

---

# Loading a PCAP File

Methods:

1. File → Open
2. Drag and Drop
3. Double-click the PCAP file

After loading, Wireshark displays packet details in three panes.

---

# Packet Analysis Panes

## Packet List Pane

Shows:

* Packet Number
* Source
* Destination
* Protocol
* Information

---

## Packet Details Pane

Displays protocol breakdown of the selected packet.

---

## Packet Bytes Pane

Displays:

* Hexadecimal data
* ASCII representation

Selecting fields in the details pane highlights corresponding bytes.

---

# Packet Colorization

Wireshark uses colors to quickly identify protocols and anomalies.

### Default Colors

| Color      | Purpose        |
| ---------- | -------------- |
| Green      | TCP Traffic    |
| Light Blue | UDP Traffic    |
| Black      | Marked Packets |
| Red        | Errors         |

### Types

* Temporary Coloring
* Permanent Coloring Rules

---

# Capturing Traffic

## Start Capture

Click:

```text
Blue Shark Icon
```

## Stop Capture

Click:

```text
Red Square Icon
```

## Restart Capture

Click:

```text
Green Restart Icon
```

---

# Packet Dissection

Wireshark decodes packet information according to OSI layers.

## Layer 1 – Frame

Contains:

* Frame Number
* Arrival Time
* Packet Length

---

## Layer 2 – Ethernet (MAC)

Contains:

* Source MAC Address
* Destination MAC Address

Example:

```text
00:1A:2B:3C:4D:5E
```

---

## Layer 3 – IP

Contains:

* Source IP
* Destination IP

Example:

```text
192.168.1.100
```

---

## Layer 4 – TCP/UDP

Contains:

* Source Port
* Destination Port
* Sequence Numbers
* Flags

Example:

```text
TCP Port 80
```

---

## Layer 5 – Application Protocol

Examples:

* HTTP
* FTP
* DNS
* SMB

---

## Application Data

Displays transmitted application content.

Examples:

* HTTP Requests
* Usernames
* File Contents

---

# Packet Numbers

Each packet receives a unique number.

Benefits:

* Easier navigation
* Event tracking
* Quick packet lookup

---

# Finding Packets

Navigate:

```text
Edit → Find Packet
```

Search Types:

* Display Filter
* Hex Value
* String
* Regular Expression (Regex)

---

# Marking Packets

Purpose:

* Highlight important packets
* Simplify investigations

Navigation:

```text
Right Click → Mark Packet
```

Marked packets appear in black.

---

# Packet Comments

Allows analysts to leave notes on packets.

Navigation:

```text
Right Click → Packet Comment
```

Useful for:

* Incident investigations
* Team collaboration

---

# Exporting Data

## Export Packets

Navigation:

```text
File → Export Specified Packets
```

Used to:

* Share suspicious traffic
* Reduce capture size

---

## Export Objects

Extract transferred files from traffic.

Supported Protocols:

* HTTP
* SMB
* IMF
* TFTP
* DICOM

Navigation:

```text
File → Export Objects
```

---

# Time Display Formats

Default:

```text
Seconds Since Beginning of Capture
```

Recommended:

```text
UTC Date and Time
```

Navigation:

```text
View → Time Display Format
```

---

# Expert Information

Navigation:

```text
Analyze → Expert Information
```

Used to identify:

* Protocol errors
* Warnings
* Malformed packets
* Suspicious behavior

### Severity Levels

| Level   | Color  |
| ------- | ------ |
| Chat    | Blue   |
| Note    | Cyan   |
| Warning | Yellow |
| Error   | Red    |

---

# Packet Filtering

## Types of Filters

### Capture Filters

Filter packets before capture.

### Display Filters

Filter packets after capture.

Most commonly used during analysis.

---

# Apply as Filter

Quick filtering method.

Navigation:

```text
Right Click → Apply as Filter
```

---

# Conversation Filter

Displays only packets belonging to the selected conversation.

Navigation:

```text
Right Click → Conversation Filter
```

Useful for:

* Client-Server analysis
* Session tracking

---

# Colorize Conversation

Highlights a conversation without filtering out other traffic.

Navigation:

```text
Right Click → Colorize Conversation
```

---

# Prepare as Filter

Creates a filter without immediately applying it.

Navigation:

```text
Right Click → Prepare as Filter
```

---

# Apply as Column

Adds packet fields as new columns.

Navigation:

```text
Right Click → Apply as Column
```

Useful for:

* Tracking IP addresses
* Tracking ports
* Protocol analysis

---

# Follow Stream

Reconstructs application-layer conversations.

Supported:

* TCP Streams
* UDP Streams
* HTTP Streams

Navigation:

```text
Right Click → Follow Stream
```

Can reveal:

* Usernames
* Passwords
* Requests
* Responses

---

# Common Display Filters

## Filter HTTP Traffic

```text
http
```

---

## Filter TCP Port 80

```text
tcp.port == 80
```

---

## Filter UDP Port 53 (DNS)

```text
udp.port == 53
```

---

## Filter Specific IP

```text
ip.addr == 192.168.1.10
```

---

## Filter Source IP

```text
ip.src == 192.168.1.10
```

---

## Filter Destination IP

```text
ip.dst == 192.168.1.10
```

---

# Quick Revision

### Important Shortcuts

| Task           | Action                       |
| -------------- | ---------------------------- |
| Open File      | File → Open                  |
| Start Capture  | Blue Shark Icon              |
| Stop Capture   | Red Stop Button              |
| Find Packet    | Ctrl + F                     |
| Apply Filter   | Display Filter Bar           |
| Follow Stream  | Right Click → Follow Stream  |
| Export Packets | File → Export                |
| Expert Info    | Analyze → Expert Information |

---

# Key Takeaways

* Wireshark is a powerful packet analysis tool.
* Packet analysis follows the OSI model.
* Display filters are essential for efficient investigations.
* Follow Stream helps reconstruct communications.
* Expert Information highlights potential issues.
* Export Objects can recover transferred files from network traffic.
