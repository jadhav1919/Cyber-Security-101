# Network Security Fundamentals - Concept Notes

---

# Introduction

When computers communicate over a network, they exchange data in the form of packets.

For example:

```text
Browser → Web Server
Email Client → Mail Server
Laptop → Remote Linux Server
```

The Internet was originally designed to deliver packets from one machine to another, not to provide security.

As a result, early Internet protocols transmitted information in plain text.

This created three major security problems:

## 1. Confidentiality Problem

Anyone who captures packets can read the data.

Example:

```text
Username: admin
Password: secret123
```

---

## 2. Integrity Problem

Attackers can modify data while it is being transmitted.

Example:

```text
Transfer ₹100
```

might become

```text
Transfer ₹100000
```

---

## 3. Authentication Problem

How do we know we are communicating with the real server?

Example:

```text
https://bank.com
```

How can we verify that the server is actually owned by the bank?

---

Modern security protocols such as TLS, SSH, and VPN were created to solve these problems.

---

# TLS (Transport Layer Security)

## Why TLS Exists

Before TLS, protocols such as:

* HTTP
* SMTP
* POP3
* IMAP
* FTP

sent data without encryption.

Anyone connected to the same network could capture packets and read sensitive information.

Example:

```text
Username: john
Password: welcome123
```

This made online banking, shopping, and email unsafe.

TLS was designed to secure communication over untrusted networks.

---

# What TLS Actually Does

TLS provides three important services.

## Confidentiality

TLS encrypts data.

Before encryption:

```text
Password = secret123
```

After encryption:

```text
a8d9f73be20d...
```

An attacker sees only meaningless encrypted bytes.

---

## Integrity

TLS ensures that data has not been modified.

If an attacker changes even one bit of encrypted data:

```text
Original Data ≠ Received Data
```

TLS detects the modification and terminates the connection.

---

## Authentication

TLS allows a client to verify the identity of the server.

This prevents attackers from pretending to be:

```text
bank.com
google.com
amazon.com
```

---

# How TLS Works

TLS operates between the application layer and transport layer.

```text
HTTP
  ↓
TLS
  ↓
TCP
  ↓
IP
```

Notice:

* HTTP remains HTTP
* TCP remains TCP
* TLS simply adds security

---

# TLS Handshake

Before encrypted communication begins, the client and server perform a handshake.

Purpose:

1. Verify identity
2. Exchange cryptographic information
3. Create encryption keys

Simplified flow:

```text
Client → Hello

Server → Certificate

Client → Verify Certificate

Client ↔ Server → Create Session Keys

Secure Communication Begins
```

After the handshake, all application data becomes encrypted.

---

# Digital Certificates

A certificate is an electronic identity card for a server.

It contains:

* Domain Name
* Organization Name
* Public Key
* Validity Dates
* CA Signature

Example:

```text
www.bank.com
```

The certificate proves ownership of the domain.

---

# Certificate Authority (CA)

A Certificate Authority is a trusted organization that verifies identities.

Examples:

* Let's Encrypt
* DigiCert
* Sectigo

The CA signs certificates using its private key.

Browsers trust these signatures.

---

# HTTPS

## What is HTTPS?

Many beginners think HTTPS is a separate protocol.

It is not.

HTTPS is simply:

```text
HTTP + TLS
```

---

# How HTTP Works

Without HTTPS:

```text
Browser
   ↓
TCP Connection
   ↓
HTTP Request
   ↓
HTTP Response
```

All traffic is readable.

Example:

```http
GET /login

username=john
password=secret123
```

---

# How HTTPS Works

HTTPS adds TLS before HTTP communication.

```text
Browser
   ↓
TCP Handshake
   ↓
TLS Handshake
   ↓
Encrypted HTTP
```

The browser still sends:

```http
GET /index.html
```

but TLS encrypts it before transmission.

---

# Why Wireshark Cannot Read HTTPS

When packets are captured:

HTTP traffic appears as:

```http
GET /login
```

HTTPS traffic appears as:

```text
Application Data
```

because the HTTP content is encrypted by TLS.

Without session keys, Wireshark cannot decrypt the traffic.

---

# SSH (Secure Shell)

## Why SSH Exists

Before SSH, administrators used TELNET.

TELNET provided remote access but transmitted everything in plain text.

Example:

```text
Username: root
Password: admin123
```

Anyone monitoring the network could see credentials.

---

# What SSH Does

SSH provides:

1. Secure Authentication
2. Encryption
3. Integrity Checking
4. Tunneling

---

# SSH Architecture

```text
Laptop
   ↓
SSH
   ↓
Linux Server
```

SSH creates an encrypted channel between the client and server.

Everything sent through the channel is protected.

---

# SSH Authentication

Two common methods:

## Password Authentication

```text
Username + Password
```

---

## Public Key Authentication

The user generates:

```text
Private Key
Public Key
```

The public key is stored on the server.

The private key remains with the user.

This is more secure than passwords.

---

# SFTP

SFTP stands for:

```text
SSH File Transfer Protocol
```

It is not FTP.

It is a completely different protocol built on top of SSH.

---

# How SFTP Works

```text
Client
   ↓
SSH Tunnel
   ↓
Server
```

Since SSH already provides:

* Encryption
* Authentication
* Integrity

SFTP automatically inherits those protections.

---

# FTPS

FTPS means:

```text
FTP + TLS
```

Unlike SFTP, FTPS is still FTP.

It simply adds TLS encryption.

---

# Why FTPS Is More Complex

FTP uses two connections:

## Control Channel

For commands

```text
LIST
GET
PUT
```

## Data Channel

For file transfers

This makes FTPS harder to configure through firewalls.

---

# VPN (Virtual Private Network)

## Why VPN Exists

Organizations often have:

```text
Head Office
Branch Office
Remote Employees
```

All need secure access to internal resources.

Using the public Internet directly is risky.

VPN solves this problem.

---

# What a VPN Actually Does

A VPN creates an encrypted tunnel between two endpoints.

```text
Laptop
    ↓
Encrypted Tunnel
    ↓
VPN Server
```

Anyone observing the Internet sees encrypted packets but cannot read their contents.

---

# VPN Components

## VPN Client

Installed on:

* Laptop
* Mobile Phone
* Router

---

## VPN Server

Located in:

* Corporate Network
* Data Center
* Cloud Environment

---

# VPN Tunnel Concept

Think of the Internet as a public highway.

Without VPN:

```text
Your Traffic
      ↓
Public Internet
```

Everyone can observe metadata.

With VPN:

```text
Your Traffic
      ↓
Encrypted Tunnel
      ↓
VPN Server
```

Traffic is protected while crossing the Internet.

---

# SSH vs VPN

SSH protects a single connection.

Example:

```text
Laptop → Linux Server
```

VPN protects entire network traffic.

Example:

```text
Laptop → Entire Corporate Network
```

SSH secures one session.

VPN secures an entire network path.

---

# TLS Decryption in Wireshark

Normally Wireshark cannot read HTTPS traffic because TLS encrypts it.

To decrypt TLS:

1. Capture packets
2. Obtain TLS session keys
3. Provide key log file to Wireshark

Example:

```text
sslkeylog.log
```

Wireshark uses these keys to decrypt traffic.

Once decrypted:

```http
GET /login
```

becomes visible again.

This technique is commonly used during:

* Malware Analysis
* Penetration Testing
* Application Debugging
* Network Troubleshooting

---

