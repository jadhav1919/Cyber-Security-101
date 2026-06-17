# Tcpdump Basics & Packet Capture – GitHub Notes

## Lab Setup

Before starting the room:

1. Start the **AttackBox** (if not using VPN).
2. Start the **Target Machine**.
3. Open the terminal provided by TryHackMe.

### SSH Credentials

```bash
Username: user
Password: THM123
```

---

# Why Learn Tcpdump?

Most networking activities happen behind graphical interfaces.

Examples:

* Visiting a website → Hidden TCP 3-Way Handshake
* Accessing a device on LAN → Hidden ARP Requests
* DNS Resolution → Hidden DNS Queries

Without packet captures, these protocol conversations remain invisible.

**Tcpdump** allows us to:

* Capture network traffic
* Analyze protocols
* Troubleshoot networks
* Investigate security incidents
* Create packet captures (.pcap files)

---

# What is Tcpdump?

Tcpdump is a command-line packet analyzer.

### Features

* Captures live network traffic
* Saves traffic into `.pcap` files
* Reads existing packet captures
* Applies advanced filters
* Displays packet details in different formats

### Background

| Component       | Description            |
| --------------- | ---------------------- |
| Tcpdump         | Packet capture tool    |
| libpcap         | Packet capture library |
| Language        | C/C++                  |
| Platform        | Unix/Linux             |
| Windows Version | WinPcap                |

---

# Basic Tcpdump Syntax

```bash
tcpdump [options] [filters]
```

---

# Network Interfaces

Before capturing traffic, identify available interfaces.

```bash
ip a s
```

Example:

```bash
1: lo
2: ens5
```

### Common Interfaces

| Interface | Purpose               |
| --------- | --------------------- |
| lo        | Loopback              |
| eth0      | Ethernet              |
| ens5      | Ethernet (new naming) |
| wlan0     | Wi-Fi                 |
| any       | All interfaces        |

---

# Capture on Specific Interface

### Syntax

```bash
tcpdump -i INTERFACE
```

### Example

```bash
sudo tcpdump -i ens5
```

Captures packets from interface `ens5`.

---

# Capture on All Interfaces

```bash
sudo tcpdump -i any
```

Captures traffic from every available interface.

---

# Save Captured Packets

### Syntax

```bash
tcpdump -w FILE
```

### Example

```bash
sudo tcpdump -i ens5 -w capture.pcap
```

### Notes

* Packets are saved to file.
* Output is not displayed on screen.
* Useful for later analysis in Wireshark.

---

# Read Packets from a PCAP File

### Syntax

```bash
tcpdump -r FILE
```

### Example

```bash
tcpdump -r capture.pcap
```

Reads packets from an existing capture.

---

# Limit Number of Packets

### Syntax

```bash
tcpdump -c COUNT
```

### Example

```bash
sudo tcpdump -i ens5 -c 10
```

Captures only 10 packets.

Without `-c`, capture continues until:

```bash
CTRL + C
```

---

# Disable Name Resolution

## Disable DNS Resolution

```bash
tcpdump -n
```

Displays:

```text
10.10.10.1
```

Instead of:

```text
example.com
```

---

## Disable DNS and Port Resolution

```bash
tcpdump -nn
```

Displays:

```text
192.168.1.5.80
```

Instead of:

```text
192.168.1.5.http
```

---

# Verbose Output

## Normal

```bash
tcpdump
```

Basic packet information.

---

## Verbose

```bash
tcpdump -v
```

Additional packet details.

---

## More Verbose

```bash
tcpdump -vv
```

---

## Maximum Verbosity

```bash
tcpdump -vvv
```

Provides extensive protocol details.

---

# Important Basic Commands

| Command              | Purpose                   |
| -------------------- | ------------------------- |
| tcpdump -i eth0      | Capture on interface      |
| tcpdump -w file.pcap | Save packets              |
| tcpdump -r file.pcap | Read packets              |
| tcpdump -c 50        | Capture 50 packets        |
| tcpdump -n           | Disable DNS lookup        |
| tcpdump -nn          | Disable DNS & port lookup |
| tcpdump -v           | Verbose output            |

---

# Packet Filtering

Capturing everything creates too much noise.

Filters help focus on relevant traffic.

---

# Filter by Host

## Specific Host

```bash
sudo tcpdump host example.com
```

or

```bash
sudo tcpdump host 192.168.1.10
```

Captures traffic to/from that host.

---

## Source Host

```bash
sudo tcpdump src host 192.168.1.10
```

Captures packets originating from that host.

---

## Destination Host

```bash
sudo tcpdump dst host 192.168.1.10
```

Captures packets sent to that host.

---

# Filter by Port

## Any Traffic on Port 53

```bash
sudo tcpdump port 53
```

Useful for DNS traffic.

---

## Source Port

```bash
sudo tcpdump src port 53
```

---

## Destination Port

```bash
sudo tcpdump dst port 53
```

---

### Common Ports

| Port | Service |
| ---- | ------- |
| 22   | SSH     |
| 53   | DNS     |
| 80   | HTTP    |
| 443  | HTTPS   |
| 123  | NTP     |

---

# Filter by Protocol

## TCP

```bash
sudo tcpdump tcp
```

---

## UDP

```bash
sudo tcpdump udp
```

---

## ICMP

```bash
sudo tcpdump icmp
```

Useful for:

```bash
ping
```

traffic.

---

## IPv4

```bash
sudo tcpdump ip
```

---

## IPv6

```bash
sudo tcpdump ip6
```

---

# Logical Operators

## AND

Both conditions must be true.

```bash
tcpdump host 1.1.1.1 and tcp
```

---

## OR

Either condition can be true.

```bash
tcpdump udp or icmp
```

---

## NOT

Exclude matching traffic.

```bash
tcpdump not tcp
```

Captures:

* UDP
* ICMP
* ARP
* Others

---

# Practical Examples

## Capture SSH Traffic

```bash
tcpdump -i any tcp port 22
```

---

## Capture DNS Traffic

```bash
tcpdump -i any port 53
```

---

## Capture HTTPS Traffic to Specific Host

```bash
tcpdump -i eth0 host example.com and tcp port 443
```

---

## Save HTTPS Traffic

```bash
tcpdump -i eth0 host example.com and tcp port 443 -w https.pcap
```

---

# Counting Matching Packets

Example:

```bash
tcpdump -r traffic.pcap src host 192.168.124.1 -n | wc
```

Output:

```text
910 17415 140616
```

Meaning:

```text
Lines Words Characters
```

Total packets:

```text
910
```

---

# Advanced Filters

## Packet Length

### Greater Than

```bash
tcpdump greater 100
```

Packets:

```text
Length >= 100 bytes
```

---

### Less Than

```bash
tcpdump less 100
```

Packets:

```text
Length <= 100 bytes
```

---

# Binary Operations

Tcpdump uses binary operators for advanced filtering.

---

## AND (&)

| A | B | A&B |
| - | - | --- |
| 0 | 0 | 0   |
| 0 | 1 | 0   |
| 1 | 0 | 0   |
| 1 | 1 | 1   |

---

## OR (|)

| A | B | A|B |
| - | - | --- |
| 0 | 0 | 0   |
| 0 | 1 | 1   |
| 1 | 0 | 1   |
| 1 | 1 | 1   |

---

## NOT (!)

| A | !A |
| - | -- |
| 0 | 1  |
| 1 | 0  |

---

# TCP Flag Filtering

TCP Flags:

| Flag | Meaning          |
| ---- | ---------------- |
| SYN  | Start connection |
| ACK  | Acknowledgment   |
| FIN  | Close connection |
| RST  | Reset connection |
| PUSH | Push data        |

---

## SYN Only

```bash
tcpdump "tcp[tcpflags] == tcp-syn"
```

Captures packets containing only SYN.

---

## SYN Present

```bash
tcpdump "tcp[tcpflags] & tcp-syn != 0"
```

Captures packets with SYN flag set.

---

## SYN or ACK Present

```bash
tcpdump "tcp[tcpflags] & (tcp-syn|tcp-ack) != 0"
```

Captures packets containing SYN or ACK.

---

# Packet Display Formats

Tcpdump can display packets in different formats.

---

# Quick Output

```bash
tcpdump -q
```

Shows:

* Timestamp
* Source
* Destination
* Protocol
* Length

Minimal information.

---

# Show MAC Addresses

```bash
tcpdump -e
```

Displays:

* Source MAC
* Destination MAC
* Ethernet Header

Useful for:

* ARP
* DHCP
* Layer 2 analysis

---

# ASCII Output

```bash
tcpdump -A
```

Displays packet data as readable text.

Useful for:

* HTTP
* Telnet
* Plain-text protocols

---

# Hexadecimal Output

```bash
tcpdump -xx
```

Displays packet contents in hex format.

Useful for:

* Protocol analysis
* Header inspection
* Malware investigations

---

# Hex + ASCII Output

```bash
tcpdump -X
```

Displays:

```text
Hexadecimal + ASCII
```

Best option for deep packet analysis.

---

# Display Options Summary

| Command     | Description        |
| ----------- | ------------------ |
| tcpdump -q  | Brief output       |
| tcpdump -e  | Show MAC addresses |
| tcpdump -A  | ASCII format       |
| tcpdump -xx | Hexadecimal format |
| tcpdump -X  | Hex + ASCII        |

---

# Common Commands Cheat Sheet

```bash
# Capture on interface
sudo tcpdump -i eth0

# Capture 20 packets
sudo tcpdump -i eth0 -c 20

# Save packets
sudo tcpdump -i eth0 -w capture.pcap

# Read packets
tcpdump -r capture.pcap

# Capture DNS traffic
sudo tcpdump port 53

# Capture ICMP traffic
sudo tcpdump icmp

# Capture SSH traffic
sudo tcpdump tcp port 22

# Capture HTTPS traffic
sudo tcpdump tcp port 443

# Disable DNS lookup
sudo tcpdump -n

# Disable DNS and port lookup
sudo tcpdump -nn

# Show MAC addresses
sudo tcpdump -e

# Show ASCII data
sudo tcpdump -A

# Show Hex data
sudo tcpdump -xx

# Show Hex + ASCII
sudo tcpdump -X
```

---

# Quick Revision

### Capture Packets

```bash
tcpdump -i eth0
```

### Save Packets

```bash
tcpdump -w file.pcap
```

### Read Packets

```bash
tcpdump -r file.pcap
```

### Filter by Host

```bash
tcpdump host 192.168.1.10
```

### Filter by Port

```bash
tcpdump port 53
```

### Filter by Protocol

```bash
tcpdump tcp
```

### Show MAC Addresses

```bash
tcpdump -e
```

### Show ASCII Data

```bash
tcpdump -A
```

### Show Hex + ASCII

```bash
tcpdump -X
```

---

