# Networking Concepts 


# 1. Introduction to Networking

## What is Networking?

Networking is the process of connecting devices so they can communicate and exchange data.

Examples:

* Browsing websites
* Sending emails
* Streaming videos
* Online gaming

## Learning Objectives

After completing this room, you should understand:

* OSI Model
* TCP/IP Model
* IP Addresses
* Subnets
* Routing
* TCP vs UDP
* Port Numbers
* Encapsulation
* Packet Flow
* Using Telnet

# 2. OSI Model (Open Systems Interconnection)

## What is OSI Model?

The OSI Model is a conceptual framework that explains how data moves across a network.

### Purpose

* Standardize network communication
* Simplify troubleshooting
* Understand networking protocols


## OSI Layers

| Layer | Name         |
| ----- | ------------ |
| 7     | Application  |
| 6     | Presentation |
| 5     | Session      |
| 4     | Transport    |
| 3     | Network      |
| 2     | Data Link    |
| 1     | Physical     |


# Layer 1 – Physical Layer

## Purpose

Handles physical transmission of bits (0 and 1).

### Responsibilities

* Electrical signals
* Optical signals
* Wireless signals
* Cables and antennas


### Examples

* Ethernet Cable
* Fiber Optic Cable
* WiFi Radio Signals


# . Layer 2 – Data Link Layer

## Purpose

Transfers data between devices on the same network.

### Responsibilities

* MAC Addressing
* Frame Creation
* Local Communication


## MAC Address

### What is MAC Address?

Unique hardware address assigned to network devices.

### Format

```text
AA:BB:CC:DD:EE:FF
```

### Characteristics

* 6 Bytes (48 bits)
* First 3 bytes identify manufacturer


### Protocol Examples

* Ethernet (802.3)
* WiFi (802.11)


#  Layer 3 – Network Layer

## Purpose

Transfers packets between different networks.

### Responsibilities

* IP Addressing
* Routing
* Path Selection


### Examples

* IP
* ICMP
* IPSec VPN


### Real Example

```text
Computer A
   ↓
 Router
   ↓
 Router
   ↓
Computer B
```

The Network Layer determines the best route.


#  Layer 4 – Transport Layer

## Purpose

Provides end-to-end communication.

### Responsibilities

* Segmentation
* Reliability
* Error Detection
* Flow Control


### Protocols

* TCP
* UDP



# Layer 5 – Session Layer

## Purpose

Creates and manages communication sessions.

### Responsibilities

* Session establishment
* Synchronization
* Recovery


### Examples

* RPC
* NFS


#  Layer 6 – Presentation Layer

## Purpose

Formats data for applications.

### Responsibilities

* Encoding
* Encryption
* Compression


### Examples

* ASCII
* Unicode
* JPEG
* PNG
* MIME


#  Layer 7 – Application Layer

## Purpose

Provides services directly to user applications.

### Examples

* HTTP
* HTTPS
* FTP
* DNS
* SMTP
* POP3
* IMAP


# OSI Summary Table

| Layer | Name         | Function                 | Examples    |
| ----- | ------------ | ------------------------ | ----------- |
| 7     | Application  | User services            | HTTP, DNS   |
| 6     | Presentation | Encoding                 | JPEG, PNG   |
| 5     | Session      | Session management       | RPC         |
| 4     | Transport    | End-to-end communication | TCP, UDP    |
| 3     | Network      | Routing                  | IP          |
| 2     | Data Link    | Local delivery           | Ethernet    |
| 1     | Physical     | Signal transmission      | Cable, WiFi |



# 3. TCP/IP Model

## What is TCP/IP?

Practical networking model used on the Internet.

Developed by:

```text
Department of Defense (DoD)
```


## TCP/IP Layers

| TCP/IP Layer | Corresponding OSI Layers |
| ------------ | ------------------------ |
| Application  | 5, 6, 7                  |
| Transport    | 4                        |
| Internet     | 3                        |
| Link         | 2                        |
| Physical     | 1                        |


## TCP/IP Stack

```text
Application
Transport
Internet
Link
Physical
```


# 4 IP Address

## What is an IP Address?

A unique logical address assigned to a device.

Example:

```text
192.168.1.10
```


## IPv4 Structure

IPv4 = 32 bits

```text
192.168.1.10
```

Contains:

```text
4 Octets
```

Each octet:

```text
0 - 255
```


## IPv4 Example

```text
192.168.1.10

192
168
1
10
```

4 octets = 32 bits


# 5. Network Address and Broadcast Address

Example Network:

```text
192.168.1.0/24
```

### Network Address

```text
192.168.1.0
```

### Broadcast Address

```text
192.168.1.255
```

### Usable Hosts

```text
192.168.1.1
to
192.168.1.254
```


# 6 Viewing IP Configuration



## Linux - ifconfig

### Purpose

Show network configuration.

### General Syntax

```bash
ifconfig
```

### Example

```bash
ifconfig
```


## Linux - ip a s

### Purpose

Display network interfaces and IP addresses.

### General Syntax

```bash
ip a s
```

### Example

```bash
ip a s
```


## Windows - ipconfig

### Purpose

Display IP configuration.

### General Syntax

```cmd
ipconfig
```

### Example

```cmd
ipconfig
```


# 7. Subnet Mask

Example:

```text
255.255.255.0
```

Equivalent:

```text
/24
```

Meaning:

```text
First 24 bits remain fixed
```

Example Network:

```text
192.168.66.0/24
```

Host Range:

```text
192.168.66.1
to
192.168.66.254
```


# 8 Private IP Addresses

## Purpose

Used inside private networks.

Cannot be reached directly from the Internet.


## Private IP Ranges

### Class A

```text
10.0.0.0 - 10.255.255.255
```

### Class B

```text
172.16.0.0 - 172.31.255.255
```

### Class C

```text
192.168.0.0 - 192.168.255.255
```


## Must Memorize

```text
10.0.0.0/8

172.16.0.0/12

192.168.0.0/16
```


# 9 Public IP vs Private IP

| Public IP           | Private IP            |
| ------------------- | --------------------- |
| Internet Accessible | Internal Network Only |
| Globally Unique     | Reusable              |
| Assigned by ISP     | Assigned by Router    |


# 10. Routing

## What is Routing?

Process of forwarding packets toward destination networks.


## Device Used

```text
Router
```



### Router Responsibilities

* Read destination IP
* Choose best path
* Forward packet


### Example

```text
Laptop
 ↓
Router
 ↓
Internet
 ↓
Server
```


# 11. Transport Layer Protocols

Two main protocols:

```text
TCP
UDP
```


# 12. UDP (User Datagram Protocol)

## Purpose

Fast communication without guarantees.

### Characteristics

* Connectionless
* No acknowledgment
* No reliability
* Faster


### Examples

* DNS
* VoIP
* Online Gaming
* Streaming


## UDP Data Unit

```text
Datagram
```



# 13. TCP (Transmission Control Protocol)

## Purpose

Reliable communication.

### Characteristics

* Connection-oriented
* Reliable
* Ordered delivery
* Error detection



### Examples

* Web Browsing
* Email
* File Transfer



## TCP Data Unit

```text
Segment
```



# 14. Port Numbers

## Purpose

Identify specific applications.

### Range

```text
1 - 65535
```

Port:

```text
0 = Reserved
```



## Examples

| Port | Service |
| ---- | ------- |
| 7    | Echo    |
| 13   | Daytime |
| 22   | SSH     |
| 80   | HTTP    |
| 443  | HTTPS   |



# 15. TCP Three-Way Handshake

## Purpose

Establish TCP Connection.



### Step 1

Client → Server

```text
SYN
```



### Step 2

Server → Client

```text
SYN + ACK
```



### Step 3

Client → Server

```text
ACK
```



### Diagram

```text
Client          Server

SYN -------->

<---- SYN ACK

ACK -------->
```

Connection Established



# 16. Encapsulation

## What is Encapsulation?

Process of wrapping data with protocol headers.



## Step 1

Application creates data.

```text
Application Data
```



## Step 2

Transport Layer adds header.

```text
TCP Segment
or
UDP Datagram
```


## Step 3

Network Layer adds IP Header.

```text
IP Packet
```



## Step 4

Data Link Layer adds frame information.

```text
Ethernet/WiFi Frame
```



## Encapsulation Flow

```text
Application Data
        ↓
TCP Segment / UDP Datagram
        ↓
IP Packet
        ↓
Ethernet Frame
```


# 17. Packet Life Cycle

Example: Search on TryHackMe



### Step 1

User searches.

```text
Browser creates HTTP request
```


### Step 2

TCP establishes connection.

```text
3-Way Handshake
```



### Step 3

TCP creates segments.

```text
HTTP → TCP Segment
```



### Step 4

IP Layer adds:

```text
Source IP
Destination IP
```



### Step 5

Link Layer creates frame.

```text
Ethernet Frame
```



### Step 6

Router forwards packet.

```text
Router → Router → Router
```



### Step 7

Destination receives packet.



### Step 8

Decapsulation occurs.

```text
Frame
 ↓
Packet
 ↓
Segment
 ↓
Application Data
```



# 18. Telnet

## What is Telnet?

A TCP client used to connect to remote services.



## General Syntax

```bash
telnet IP PORT
```



# 19. Echo Server

## Purpose

Returns whatever you send.

### Port

```text
7
```



### Command

```bash
telnet 10.48.139.39 7
```

### Example

```text
Hi
Hi

Hello
Hello
```


# 20. Daytime Server

## Purpose

Returns current date and time.

### Port

```text
13
```



### Command

```bash
telnet 10.48.139.39 13
```

### Example Output

```text
Thu Jun 20 12:36:32 PM UTC 2024
```



# 21. HTTP Server Using Telnet

## Purpose

Request webpage manually.

### Port

```text
80
```


### Command

```bash
telnet 10.48.139.39 80
```



### HTTP Request

```http
GET / HTTP/1.1
Host: telnet.thm
```

Press Enter Twice



### Response

```http
HTTP/1.1 200 OK
Content-Type: text/html
```

---
