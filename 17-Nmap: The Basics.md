# Nmap Basics

## What is Nmap?

**Nmap (Network Mapper)** is an open-source network scanning tool used to:

* Discover live hosts
* Identify open ports
* Detect running services
* Identify service versions
* Detect operating systems
* Perform network reconnaissance

### Why Use Nmap?

Without Nmap, discovering hosts and services manually would require:

* Pinging every IP address
* Trying connections to thousands of ports
* Writing scripts for automation

Nmap automates all of this efficiently.

---



# Target Specification

Nmap supports multiple target formats.

## Single IP

```bash
nmap 192.168.1.10
```

---

## IP Range

Scan:

```text
192.168.1.1 → 192.168.1.10
```

```bash
nmap 192.168.1.1-10
```

---

## Subnet

```bash
nmap 192.168.1.0/24
```

Equivalent to:

```text
192.168.1.0 - 192.168.1.255
```

---

## Hostname

```bash
nmap example.com
```

---

# Host Discovery

## Question

Before scanning ports, we first need to know:

```text
Which devices are online?
```

Nmap uses **Host Discovery**.

---

# Ping Scan (-sn)

### Syntax

```bash
nmap -sn TARGET
```

### Example

```bash
sudo nmap -sn 192.168.1.0/24
```

### Purpose

* Finds live hosts
* Does NOT scan ports
* Faster scan
* Generates less traffic

---

# Local Network Discovery

Example:

```bash
sudo nmap -sn 192.168.66.0/24
```

Output:

```text
Host is up
MAC Address: 44:DF:65:D8:FE:6C
```

### How It Works

For local networks Nmap uses:

```text
ARP Requests
```

Process:

```text
ARP Request
      ↓
Device Responds
      ↓
Host Marked "UP"
```

---

# Remote Network Discovery

Example:

```bash
sudo nmap -sn 192.168.11.0/24
```

Because routers separate the networks:

```text
ARP cannot be used
```

Nmap uses:

* ICMP Echo Requests (Ping)
* ICMP Timestamp Requests
* TCP SYN Probes
* TCP ACK Probes

---

# List Scan (-sL)

Lists targets without scanning.

### Example

```bash
nmap -sL 192.168.1.0/24
```

### Purpose

Verify targets before launching scan.

---

# Host Discovery Summary

| Option | Description              |
| ------ | ------------------------ |
| -sn    | Discover live hosts only |
| -sL    | List targets only        |

---

# Port Scanning

## Question

After finding live hosts:

```text
Which services are running?
```

To answer this, we scan ports.

---

# TCP Connect Scan (-sT)

### Syntax

```bash
nmap -sT TARGET
```

### How It Works

Completes full TCP 3-Way Handshake.

```text
SYN
 ↓
SYN-ACK
 ↓
ACK
```

Connection established.

Then Nmap closes connection.

---

# Connect Scan Workflow

### Open Port

```text
Nmap → SYN
Target → SYN-ACK
Nmap → ACK

Connection Established
```

---

### Closed Port

```text
Nmap → SYN
Target → RST-ACK
```

Port is closed.

---

# TCP SYN Scan (-sS)

Also called:

```text
Stealth Scan
Half-Open Scan
```

### Syntax

```bash
sudo nmap -sS TARGET
```

### How It Works

Only sends:

```text
SYN
```

Receives:

```text
SYN-ACK
```

Then immediately sends:

```text
RST
```

Instead of completing handshake.

---

# SYN Scan Workflow

```text
Nmap → SYN
Target → SYN-ACK
Nmap → RST
```

Connection never established.

### Advantages

* Faster
* Stealthier
* Less logging

---

# Connect vs SYN Scan

| Feature        | -sT | -sS |
| -------------- | --- | --- |
| Full Handshake | Yes | No  |
| Faster         | No  | Yes |
| Stealthy       | No  | Yes |
| Root Required  | No  | Yes |

---

# UDP Scan (-sU)

Many services use UDP.

Examples:

| Service | Port    |
| ------- | ------- |
| DNS     | 53      |
| DHCP    | 67/68   |
| NTP     | 123     |
| SNMP    | 161     |
| VoIP    | Various |

### Syntax

```bash
sudo nmap -sU TARGET
```

---

# UDP Scan Behavior

### Closed Port

Target replies:

```text
ICMP Port Unreachable
```

### Open Port

Usually:

```text
No Response
```

Which makes UDP scanning slower.

---

# Limiting Port Scans

## Fast Mode

Scans top 100 ports.

```bash
nmap -F TARGET
```

---

## Scan Specific Range

### Example

```bash
nmap -p10-100 TARGET
```

Scans:

```text
10 → 100
```

---

## Scan First 25 Ports

```bash
nmap -p-25 TARGET
```

---

## Scan All Ports

```bash
nmap -p- TARGET
```

Equivalent:

```bash
nmap -p1-65535 TARGET
```

---

# Well-Known Ports

```text
1 - 1023
```

Most common services exist here.

Example:

```bash
nmap -p1-1023 TARGET
```

---

# Port Scanning Summary

| Option | Description      |
| ------ | ---------------- |
| -sT    | TCP Connect Scan |
| -sS    | TCP SYN Scan     |
| -sU    | UDP Scan         |
| -F     | Top 100 Ports    |
| -p     | Port Range       |
| -p-    | All Ports        |

---

# Operating System Detection

## Option

```bash
nmap -O TARGET
```

### Example

```bash
sudo nmap -O 192.168.1.10
```

Output:

```text
Linux 4.x
Linux 5.x
Windows
FreeBSD
```

### How It Works

Analyzes:

* TCP Responses
* TTL Values
* Window Sizes
* Network Behavior

---

# Service Version Detection

## Option

```bash
nmap -sV TARGET
```

### Example

```bash
sudo nmap -sV 192.168.1.10
```

Output:

```text
22/tcp OpenSSH 8.9
80/tcp Apache 2.4
```

---

# Aggressive Scan (-A)

### Syntax

```bash
sudo nmap -A TARGET
```

### Includes

* OS Detection
* Version Detection
* Traceroute
* Script Scanning

Think of:

```text
-A = Everything Important
```

---

# Force Scan Hosts (-Pn)

Sometimes a host blocks ICMP.

Nmap may think:

```text
Host is Down
```

Even though it is alive.

---

## Force Port Scan

```bash
nmap -Pn TARGET
```

### Meaning

```text
Treat host as online
```

---

# Detection Summary

| Option | Purpose           |
| ------ | ----------------- |
| -O     | OS Detection      |
| -sV    | Version Detection |
| -A     | Aggressive Scan   |
| -Pn    | Assume Host Is Up |

---

# Timing Templates

Nmap provides scan speed controls.

---

## Timing Levels

| Level | Name       |
| ----- | ---------- |
| T0    | Paranoid   |
| T1    | Sneaky     |
| T2    | Polite     |
| T3    | Normal     |
| T4    | Aggressive |
| T5    | Insane     |

---

# Example

```bash
nmap -sS -T4 TARGET
```

Aggressive scan.

---

# When to Use

| Timing | Use Case           |
| ------ | ------------------ |
| T0     | IDS Evasion        |
| T1     | Very Stealthy      |
| T2     | Slow Networks      |
| T3     | Default            |
| T4     | Fast Recon         |
| T5     | Very Fast Networks |

---

# Parallelism Control

Control simultaneous probes.

### Minimum

```bash
--min-parallelism 10
```

### Maximum

```bash
--max-parallelism 100
```

---

# Packet Rate Control

## Minimum Rate

```bash
--min-rate 100
```

100 packets/sec

---

## Maximum Rate

```bash
--max-rate 500
```

500 packets/sec

---

# Host Timeout

Stop scanning slow hosts.

```bash
--host-timeout 30s
```

---

# Timing Summary

| Option         | Description |
| -------------- | ----------- |
| -T0            | Paranoid    |
| -T1            | Sneaky      |
| -T2            | Polite      |
| -T3            | Normal      |
| -T4            | Aggressive  |
| -T5            | Insane      |
| --min-rate     | Minimum PPS |
| --max-rate     | Maximum PPS |
| --host-timeout | Time Limit  |

---

# Verbose Output

### Enable Verbose Mode

```bash
nmap -v TARGET
```

Shows:

* Scan stages
* Progress updates
* Open ports as discovered

---

# More Verbose

```bash
nmap -vv TARGET
```

```bash
nmap -vvvv TARGET
```

---

# Debug Mode

### Debug Output

```bash
nmap -d TARGET
```

---

### Maximum Debug

```bash
nmap -d9 TARGET
```

Produces extensive technical information.

---

# Saving Scan Results

---

## Normal Output

```bash
nmap -oN report.txt TARGET
```

Human-readable.

---

## XML Output

```bash
nmap -oX report.xml TARGET
```

Useful for tools.

---

## Grepable Output

```bash
nmap -oG report.gnmap TARGET
```

Useful for:

```bash
grep
awk
```

---

## All Formats

```bash
nmap -oA scan TARGET
```

Creates:

```text
scan.nmap
scan.xml
scan.gnmap
```

---

# Output Summary

| Option | Description |
| ------ | ----------- |
| -oN    | Normal      |
| -oX    | XML         |
| -oG    | Grepable    |
| -oA    | All Formats |

---

