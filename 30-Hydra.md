# Hydra – Introduction

## Overview

**Hydra** is a fast **online password-cracking** and **brute-force** tool used to test login credentials against network services and web applications.

It automates the process of trying multiple username and password combinations until it finds valid credentials.

> **Note:** Hydra should only be used on systems you own or have explicit permission to test (e.g., labs, CTFs, or authorized penetration tests).


# What is Hydra?

Hydra is an open-source command-line tool that performs **online password attacks** against authentication services.

Instead of manually trying passwords one by one, Hydra automatically tests thousands of username/password combinations.


# Why Use Hydra?

Imagine you have a login page with:

```text
Username: admin
Password: ?
```

Manually trying passwords:

```text
admin123
password
letmein
qwerty
welcome
```

would take a long time.

Hydra automates this process by reading passwords from a wordlist and testing them efficiently.


# How Hydra Works

```text
Wordlist
    │
    ▼
Hydra
    │
    ▼
Target Login Service
    │
    ▼
Correct Credentials Found
```

Hydra continues testing credentials until:

* The correct password is found.
* The wordlist is exhausted.
* The process is stopped.


# Brute Force Attack

## What is Brute Force?

A **brute-force attack** is the process of trying many possible passwords until the correct one is found.

Example:

```text
password1
password2
password3
password4
...
```

Hydra automates this process.

# Dictionary Attack

Hydra commonly performs a **dictionary attack**.

Instead of trying every possible password combination, it tests passwords from a predefined **wordlist**.

Example wordlist:

```text
123456
password
admin
welcome
letmein
qwerty
```

This is much faster than trying every possible password.

# Supported Protocols

Hydra supports a wide variety of authentication protocols.

## Commonly Used Protocols

| Protocol   | Purpose                   |
| ---------- | ------------------------- |
| FTP        | File Transfer Protocol    |
| SSH        | Secure Shell              |
| Telnet     | Remote Login              |
| HTTP GET   | Web Authentication        |
| HTTP POST  | Web Login Forms           |
| HTTPS GET  | Secure Web Authentication |
| HTTPS POST | Secure Login Forms        |
| SMB        | Windows File Sharing      |
| RDP        | Remote Desktop            |
| MySQL      | Database Authentication   |
| PostgreSQL | Database Authentication   |
| SMTP       | Email Server              |
| POP3       | Email Retrieval           |
| IMAP       | Email Access              |
| LDAP       | Directory Services        |
| SNMP       | Network Management        |
| VNC        | Remote Desktop            |

Hydra also supports many additional services, making it one of the most versatile password-testing tools available.


# Common Uses

Hydra is often used during **authorized security assessments** to:

* Test weak passwords
* Identify default credentials
* Audit password policies
* Verify account security
* Assess exposed authentication services


# Example Scenario

Suppose a company allows SSH access.

```text
SSH Server
Username: admin
Password: Unknown
```

Hydra can test many passwords from a wordlist to determine whether weak credentials are in use.


# Why Strong Passwords Matter

Hydra is effective because many users choose weak or common passwords.

Examples of weak passwords:

```text
password
123456
admin
qwerty
welcome
```

These passwords appear in many publicly available wordlists.


# Default Credentials

Many devices and applications ship with default usernames and passwords.

Examples:

| Username | Password |
| -------- | -------- |
| admin    | admin    |
| admin    | password |
| root     | root     |
| admin    | 1234     |

If these credentials are not changed, attackers may gain access very quickly.


# Characteristics of a Strong Password

A strong password should:

* Be at least **12–16 characters** long.
* Include uppercase letters.
* Include lowercase letters.
* Include numbers.
* Include special characters.
* Avoid dictionary words.
* Be unique for each account.

Example:

```text
T7!xP@92#mLq
```


# Hydra Workflow

```text
Username
      │
Password Wordlist
      │
      ▼
Hydra
      │
      ▼
Authentication Service
      │
      ▼
Valid Credentials (if found)
```


# Advantages of Hydra

* Fast password testing.
* Supports many protocols.
* Highly customizable.
* Open source.
* Widely used in penetration testing.


# Limitations

* Online attacks can trigger account lockouts.
* Slow network connections reduce performance.
* Strong passwords are difficult to guess.
* Multi-factor authentication (MFA) greatly reduces its effectiveness.


# Best Practices (Defensive)

To protect systems from password attacks:

* Use long, complex passwords.
* Change default credentials immediately.
* Enable multi-factor authentication (MFA).
* Implement account lockout policies.
* Limit login attempts.
* Monitor authentication logs for repeated failures.


----------

# Hydra Commands (TryHackMe Lab)

## Overview

In this lab, you will use **Hydra** to perform **authorized password auditing** against the provided target machine. The exercises demonstrate how Hydra can automate login attempts against services such as **SSH** and **web login forms** in a controlled environment.

> **Important:** These commands are intended **only for labs or systems you own or have explicit permission to test**.

# Lab Setup

## Step 1 – Start the AttackBox

Click:

```text
Start AttackBox
```

The AttackBox contains:

* Hydra (pre-installed)
* Firefox
* Common penetration testing tools


## Step 2 – Start the Lab Machine

Click:

```text
Start Lab Machine
```

Wait **2–3 minutes** for the machine to finish booting.


## Step 3 – Open the Target Website

Visit:

```text
http://<Target-IP>
```

You should see the web application that will be used throughout the lab.


# Installing Hydra (Optional)

Hydra is already installed on the TryHackMe AttackBox.

If using your own Linux system:

### Ubuntu / Debian

```bash
sudo apt update
sudo apt install hydra
```

### Fedora

```bash
sudo dnf install hydra
```


# Basic Hydra Command Structure

```bash
hydra [options] target service
```

Example:

```bash
hydra -l user -P passwords.txt ftp://192.168.1.10
```

Hydra will:

1. Use the username `user`
2. Read passwords from `passwords.txt`
3. Attempt authentication against the FTP service


# Hydra Command Options

| Option | Description                          |
| ------ | ------------------------------------ |
| `-l`   | Specify a single username            |
| `-L`   | Specify a file containing usernames  |
| `-p`   | Specify a single password            |
| `-P`   | Specify a password wordlist          |
| `-t`   | Number of parallel threads           |
| `-V`   | Verbose output (shows every attempt) |
| `-s`   | Specify a non-default port           |


# Brute-Forcing SSH

## Syntax

```bash
hydra -l <username> -P <password_list> <target_ip> -t 4 ssh
```


## Example

```bash
hydra -l root -P passwords.txt 192.168.1.10 -t 4 ssh
```


## Command Breakdown

| Part               | Explanation                   |
| ------------------ | ----------------------------- |
| `hydra`            | Starts the Hydra tool         |
| `-l root`          | Uses `root` as the username   |
| `-P passwords.txt` | Reads passwords from the file |
| `192.168.1.10`     | Target machine                |
| `-t 4`             | Uses 4 concurrent threads     |
| `ssh`              | Attack the SSH service        |


## What Happens?

```text
Username
      │
Password List
      │
      ▼
Hydra
      │
      ▼
SSH Service
      │
      ▼
Correct Password Found (if present)
```


# Why Use Threads?

The `-t` option controls how many login attempts Hydra performs simultaneously.

Example:

```bash
-t 4
```

Means:

```text
Thread 1
Thread 2
Thread 3
Thread 4
```

Each thread tests passwords independently, increasing speed.

> Using too many threads against a real service may trigger rate limiting or account lockouts.


# Brute-Forcing a Web Login Form

Many websites authenticate users using HTML forms.

Hydra supports:

* HTTP GET forms
* HTTP POST forms
* HTTPS GET forms
* HTTPS POST forms


# POST Login Form Syntax

```bash
hydra -l <username> -P <wordlist> <target_ip> http-post-form "<path>:<parameters>:<failure_string>"
```


# Understanding the Command

Example:

```bash
hydra -l admin -P passwords.txt 192.168.1.10 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect"
```


## Command Breakdown

### `-l admin`

Use the username:

```text
admin
```


### `-P passwords.txt`

Passwords are read from:

```text
passwords.txt
```


### `http-post-form`

Indicates the login form uses the **HTTP POST** method.


### `/`

The login page.

If the login page is:

```text
http://example.com/login.php
```

then the path becomes:

```text
/login.php
```


### `username=^USER^`

Hydra replaces:

```text
^USER^
```

with the username supplied using `-l`.

Example:

```text
username=admin
```


### `password=^PASS^`

Hydra replaces:

```text
^PASS^
```

with each password from the wordlist.

Example:

```text
password=password123
```


### `F=incorrect`

This tells Hydra how to recognize a failed login.

If the webpage displays:

```text
incorrect
```

after an unsuccessful login, Hydra knows that attempt failed and continues testing the next password.


# Verbose Mode

Adding:

```bash
-V
```

shows every login attempt.

Example:

```text
Trying password123
Trying admin123
Trying letmein
```

This is useful for learning and troubleshooting.

# Non-Default Ports

If the web server runs on a custom port, specify it with:

```bash
-s <port>
```

Example:

```bash
-s 8080
```

# Finding Form Information

Before using Hydra against a web form, determine:

1. **Request method** (GET or POST)
2. **Form field names**
3. **Failure message**

You can find these using:

* Browser Developer Tools → Network tab
* Burp Suite Proxy
* Page source


# Hydra Workflow

```text
Username
      │
Password Wordlist
      │
      ▼
Hydra
      │
      ▼
Web Login Form
      │
      ▼
Checks Failure Message
      │
      ▼
Success or Continue
```

# Best Practices (Authorized Testing)

* Confirm the request method (GET/POST) before configuring Hydra.
* Identify the correct form field names (`username`, `password`, etc.).
* Use the correct failure string so Hydra can distinguish failed logins.
* Adjust thread count carefully to avoid overwhelming the service.
* Perform password auditing only on systems where you have explicit authorization.

---

