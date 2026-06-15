# Networking Protocols

## DNS (Domain Name System)

### Overview

DNS (Domain Name System) is a naming service that translates human-readable domain names into IP addresses that computers can use for communication.

Example:

```text
google.com
     ↓
142.250.x.x
```

Without DNS, users would need to remember IP addresses for every website they visit.

### Purpose

DNS is responsible for:

* Resolving domain names to IP addresses
* Helping clients locate servers on a network
* Supporting web browsing, email delivery, and many other Internet services

### OSI Layer

```text
Application Layer (Layer 7)
```

### Ports

| Protocol | Port |
| -------- | ---- |
| UDP      | 53   |
| TCP      | 53   |

* UDP is used for most DNS queries.
* TCP is used for large responses and zone transfers.

### DNS Resolution Process

```text
User enters domain name
          |
          v
DNS Query Sent
          |
          v
DNS Server Resolves Domain
          |
          v
IP Address Returned
          |
          v
Connection Established
```

### Common DNS Records

#### A Record

Maps a hostname to an IPv4 address.

```text
example.com → 172.17.2.172
```

#### AAAA Record

Maps a hostname to an IPv6 address.

```text
example.com → 2606:2800:21f:cb07::1
```

#### CNAME Record

Creates an alias from one domain name to another.

```text
www.example.com → example.com
```

#### MX Record

Specifies the mail server responsible for handling email for a domain.

```text
example.com → mail.example.com
```

### DNS Records Summary

| Record | Purpose         |
| ------ | --------------- |
| A      | Domain → IPv4   |
| AAAA   | Domain → IPv6   |
| CNAME  | Domain → Domain |
| MX     | Mail Server     |

### DNS Lookup

Using `nslookup`:

```bash
nslookup www.example.com
```

Example output:

```text
Name: www.example.com
Address: 93.184.215.14
```

---

# Domain Registration and WHOIS

## Domain Registration

A domain name must be registered before it can be used on the Internet.

Examples:

```text
google.com
example.com
tryhackme.com
```

The owner of a domain controls its DNS records.

### Information Typically Provided During Registration

* Name
* Address
* Phone Number
* Email Address

### Domain Lifecycle

Domains are registered for a fixed period and must be renewed before expiration.

---

## WHOIS

WHOIS is a service used to retrieve information about a registered domain.

### Information Available Through WHOIS

* Domain Name
* Registrar
* Registrant Information
* Creation Date
* Expiration Date
* Name Servers

### Example

```bash
whois example.com
```

Example output:

```text
Domain Name: example.com
Registrar: GoDaddy
Creation Date: 2020
Expiration Date: 2027
```

### Privacy Protection

Many registrars offer privacy services that hide personal information from public WHOIS records.

---

# HTTP and HTTPS

## Overview

HTTP and HTTPS are protocols used for communication between web browsers and web servers.

```text
Browser ↔ Web Server
```

### HTTP

HTTP (HyperText Transfer Protocol) is used to transfer web pages and related content.

### HTTPS

HTTPS (HyperText Transfer Protocol Secure) is the encrypted version of HTTP.

### Ports

| Protocol | Port |
| -------- | ---- |
| HTTP     | 80   |
| HTTPS    | 443  |

### Communication Flow

```text
Browser
   |
   | HTTP Request
   |
   v
Web Server
   |
   | HTTP Response
   |
   v
Browser
```

### Common HTTP Methods

#### GET

Retrieves data from a server.

```http
GET /index.html HTTP/1.1
```

#### POST

Submits data to a server.

#### PUT

Creates or updates a resource.

#### DELETE

Removes a resource.

### HTTP Methods Summary

| Method | Purpose            |
| ------ | ------------------ |
| GET    | Retrieve Data      |
| POST   | Submit Data        |
| PUT    | Create/Update Data |
| DELETE | Remove Data        |

### Common HTTP Response Codes

| Code | Meaning               |
| ---- | --------------------- |
| 200  | OK                    |
| 301  | Moved Permanently     |
| 403  | Forbidden             |
| 404  | Not Found             |
| 500  | Internal Server Error |

---

# FTP (File Transfer Protocol)

## Overview

FTP is a protocol designed for transferring files between a client and a server.

### Uses

* Uploading files
* Downloading files
* Managing remote files

### Port

| Protocol | Port   |
| -------- | ------ |
| FTP      | TCP 21 |

### FTP Commands

#### USER

Provides a username.

```ftp
USER anonymous
```

#### PASS

Provides a password.

```ftp
PASS password
```

#### RETR

Downloads a file.

```ftp
RETR file.txt
```

#### STOR

Uploads a file.

```ftp
STOR report.txt
```

### FTP Connections

FTP uses two separate connections:

#### Control Connection

Used for commands:

```text
USER
PASS
LIST
RETR
STOR
QUIT
```

#### Data Connection

Used for:

* File transfers
* Directory listings

### FTP Response Codes

| Code | Meaning                 |
| ---- | ----------------------- |
| 220  | Service Ready           |
| 230  | Login Successful        |
| 331  | Password Required       |
| 150  | Opening Data Connection |
| 226  | Transfer Complete       |
| 221  | Goodbye                 |

---

# SMTP (Simple Mail Transfer Protocol)

## Overview

SMTP is the standard protocol used for sending emails.

### Functions

* Email Client → Mail Server
* Mail Server → Mail Server

### Port

| Protocol | Port   |
| -------- | ------ |
| SMTP     | TCP 25 |

### SMTP Workflow

```text
Client
   |
   | HELO
   | MAIL FROM
   | RCPT TO
   | DATA
   |
   v
Mail Server
```

### SMTP Commands

#### HELO / EHLO

Initiates communication.

```smtp
HELO client.thm
```

#### MAIL FROM

Specifies the sender.

```smtp
MAIL FROM:<user@client.thm>
```

#### RCPT TO

Specifies the recipient.

```smtp
RCPT TO:<strategos@server.thm>
```

#### DATA

Starts the email body section.

```smtp
DATA
```

#### QUIT

Ends the session.

```smtp
QUIT
```

### SMTP Response Codes

| Code | Meaning                  |
| ---- | ------------------------ |
| 220  | Service Ready            |
| 250  | Success                  |
| 354  | Start Sending Email Data |
| 221  | Connection Closing       |

---

# POP3 (Post Office Protocol Version 3)

## Overview

POP3 is an email retrieval protocol used to download emails from a mail server.

### Port

| Protocol | Port    |
| -------- | ------- |
| POP3     | TCP 110 |

### Workflow

```text
Email Client
      |
      | Authentication
      |
      v
POP3 Server
      |
      | Download Emails
      |
      v
Client
```

### POP3 Commands

| Command | Purpose            |
| ------- | ------------------ |
| USER    | Specify username   |
| PASS    | Specify password   |
| STAT    | Mailbox statistics |
| LIST    | List emails        |
| RETR    | Retrieve email     |
| DELE    | Delete email       |
| QUIT    | End session        |

### Security Consideration

POP3 transmits:

* Username
* Password
* Email Content

in plain text by default.

---

# IMAP (Internet Message Access Protocol)

## Overview

IMAP is an email retrieval and synchronization protocol that keeps emails on the server and synchronizes them across multiple devices.

### Port

| Protocol | Port    |
| -------- | ------- |
| IMAP     | TCP 143 |

### Features

* Multiple device support
* Mailbox synchronization
* Folder management
* Server-side email storage

### IMAP Commands

| Command | Purpose           |
| ------- | ----------------- |
| LOGIN   | Authenticate user |
| SELECT  | Open mailbox      |
| FETCH   | Retrieve message  |
| MOVE    | Move message      |
| COPY    | Copy message      |
| LOGOUT  | End session       |

### Synchronization Example

```text
Laptop
    |
    v
Server Updated
    |
    v
Phone
Tablet
```

### POP3 vs IMAP

| Feature                | POP3       | IMAP      |
| ---------------------- | ---------- | --------- |
| Downloads Emails       | Yes        | Yes       |
| Keeps Emails on Server | Usually No | Yes       |
| Multiple Devices       | Limited    | Excellent |
| Synchronization        | No         | Yes       |
| Server Storage Usage   | Low        | High      |

---

# Protocol Reference Table

| Protocol | Purpose                  | Transport Protocol | Default Port |
| -------- | ------------------------ | ------------------ | ------------ |
| TELNET   | Remote Terminal Access   | TCP                | 23           |
| DNS      | Domain Name Resolution   | UDP/TCP            | 53           |
| HTTP     | Web Communication        | TCP                | 80           |
| HTTPS    | Secure Web Communication | TCP                | 443          |
| FTP      | File Transfer            | TCP                | 21           |
| SMTP     | Send Email               | TCP                | 25           |
| POP3     | Download Email           | TCP                | 110          |
| IMAP     | Email Synchronization    | TCP                | 143          |
