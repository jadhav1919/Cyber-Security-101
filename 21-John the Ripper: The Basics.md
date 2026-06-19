# John the Ripper (JTR) - Complete GitHub Notes

# 1. Introduction to John the Ripper

## What is John the Ripper?

**John the Ripper (JTR)** is a popular password-cracking and hash-cracking tool used by:

* Penetration Testers
* Red Teamers
* Security Researchers
* Digital Forensic Analysts
* CTF Players

### Features

* Fast password cracking
* Supports hundreds of hash formats
* Dictionary attacks
* Brute-force attacks
* Custom rule-based attacks
* Cracks password-protected files
* Cracks SSH private key passwords

---

## Learning Objectives

Using John the Ripper for:

1. Cracking Windows NTLM hashes
2. Cracking Linux `/etc/shadow` passwords
3. Cracking ZIP archives
4. Cracking RAR archives
5. Cracking SSH private keys
6. Using Single Crack Mode
7. Creating Custom Rules

---

# 2. Understanding Hashes

## What is a Hash?

A hash is a fixed-length output generated from input data using a hashing algorithm.

### Example

Input:

```text
polo
```

MD5 Hash:

```text
b53759f3ce692de7aff1b5779d3964da
```

Input:

```text
polomints
```

MD5 Hash:

```text
584b6e4f4586e136bc280f27f9c64f3b
```

---

## Popular Hash Algorithms

| Algorithm | Length |
| --------- | ------ |
| MD4       | 32     |
| MD5       | 32     |
| SHA1      | 40     |
| SHA256    | 64     |
| SHA512    | 128    |
| NTLM      | 32     |

---

## Properties of Hash Functions

### Deterministic

Same input always produces same hash.

```text
password → 5f4dcc3b5aa765d61d8327deb882cf99
```

---

### Fixed Length

Any size input produces fixed-size output.

---

### One-Way Function

Easy:

```text
Password → Hash
```

Difficult:

```text
Hash → Password
```

---

### Collision Resistant

Two different inputs should not produce the same hash.

---

# 3. Why Hashes are Secure

Hash functions are designed to be computationally difficult to reverse.

---

## P vs NP Concept

### P (Polynomial Time)

Problems solved efficiently.

Example:

* Sorting data
* Searching

---

### NP (Non-deterministic Polynomial Time)

Easy to verify solutions but difficult to find them.

Example:

* Password cracking
* Hash reversing

---

## Why Cracking is Possible

Although hashes cannot be reversed directly:

1. Guess password
2. Hash guess
3. Compare with target hash

If matched:

```text
Password Found
```

This is called a:

### Dictionary Attack

---

# 4. Dictionary Attacks

## Definition

A dictionary attack tries passwords from a predefined wordlist.

Example:

```text
password
123456
qwerty
admin
welcome
```

Each word is hashed and compared to target hash.

---

## How John Uses Dictionary Attacks

```bash
john --wordlist=rockyou.txt hash.txt
```

John:

1. Reads passwords from wordlist
2. Hashes them
3. Compares hashes
4. Finds matching password

---

# 5. Jumbo John

## What is Jumbo John?

Enhanced community version of John the Ripper.

### Additional Tools

* zip2john
* rar2john
* ssh2john
* unshadow

### Why Use Jumbo John?

More formats and features.

---

# 6. Installation

## Kali Linux

Already installed.

Check:

```bash
john
```

Expected:

```text
John the Ripper jumbo
```

---

## Ubuntu

```bash
sudo apt install john
```

---

## Fedora

```bash
sudo dnf install john
```

---

## Build Jumbo John

Official source:

```bash
git clone https://github.com/openwall/john.git
```

Compile:

```bash
cd john/src
./configure
make
```

---

# 7. Wordlists

## What is a Wordlist?

A collection of passwords used in dictionary attacks.

Example:

```text
password
admin
welcome
letmein
```

---

## Common Sources

### SecLists

Large collection of security wordlists.

---

### RockYou

Most popular password list.

Obtained from:

```text
RockYou Data Breach (2009)
```

Contains millions of real passwords.

---

## Location in Kali

```bash
/usr/share/wordlists/
```

RockYou:

```bash
/usr/share/wordlists/rockyou.txt
```

---

# 8. Basic John Syntax

## General Syntax

```bash
john [options] [hash_file]
```

---

### Components

| Component | Description          |
| --------- | -------------------- |
| john      | Run JTR              |
| options   | Cracking options     |
| hash_file | File containing hash |

---

# 9. Automatic Hash Cracking

John automatically detects hash format.

## Syntax

```bash
john --wordlist=rockyou.txt hash.txt
```

Example:

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

---

## Advantages

* Easy
* No format specification

---

## Disadvantages

* Detection may fail
* Wrong format selected

---

# 10. Identifying Hashes

Sometimes John cannot detect hash type.

---

## Hash Identifier Tool

Download:

```bash
wget https://gitlab.com/kalilinux/packages/hash-identifier/-/raw/kali/master/hash-id.py
```

Run:

```bash
python3 hash-id.py
```

Input:

```text
2e728dd31fb5949bc39cac5a9f066498
```

Possible output:

```text
MD5
NTLM
```

---

## Other Methods

### List Supported Formats

```bash
john --list=formats
```

---

### Search Format

```bash
john --list=formats | grep -i md5
```

---

# 11. Format-Specific Cracking

## Syntax

```bash
john --format=<format> --wordlist=rockyou.txt hash.txt
```

---

### MD5 Example

```bash
john --format=raw-md5 \
--wordlist=/usr/share/wordlists/rockyou.txt \
hash.txt
```

---

### Common Formats

| Hash         | Format      |
| ------------ | ----------- |
| MD5          | raw-md5     |
| SHA1         | raw-sha1    |
| SHA256       | raw-sha256  |
| SHA512       | raw-sha512  |
| NTLM         | nt          |
| SHA512 Crypt | sha512crypt |

---

# 12. Cracking Windows Password Hashes

## NTLM (NTHash)

Windows stores password hashes using:

```text
NTLM
```

---

## Stored In

### SAM Database

```text
Security Account Manager
```

---

### Active Directory

```text
NTDS.dit
```

---

## Obtaining NTLM Hashes

Common tools:

* Mimikatz
* secretsdump.py
* pwdump

---

## Cracking NTLM

```bash
john --format=nt \
--wordlist=/usr/share/wordlists/rockyou.txt \
ntlm.txt
```

---

# 13. Linux Password Hash Cracking

## /etc/passwd

Contains:

* Username
* UID
* GID
* Shell

Example:

```text
root:x:0:0::/root:/bin/bash
```

---

## /etc/shadow

Contains password hashes.

Example:

```text
root:$6$abc123...
```

---

## Why Use Unshadow?

John requires both files.

---

# 14. Unshadow

## Syntax

```bash
unshadow passwd shadow > unshadowed.txt
```

Example:

```bash
unshadow local_passwd local_shadow > unshadowed.txt
```

---

## Crack Password

```bash
john \
--wordlist=/usr/share/wordlists/rockyou.txt \
unshadowed.txt
```

---

## Specify Format If Needed

```bash
john \
--format=sha512crypt \
--wordlist=/usr/share/wordlists/rockyou.txt \
unshadowed.txt
```

---

# 15. Single Crack Mode

## What is Single Mode?

Uses username information to generate passwords.

---

### Example Username

```text
Markus
```

Generated guesses:

```text
Markus1
Markus2
Markus!
MARKus
```

---

## Word Mangling

Word mangling modifies usernames to create password candidates.

---

## Syntax

```bash
john --single --format=<format> hash.txt
```

Example:

```bash
john --single --format=raw-sha256 hash.txt
```

---

## Required Format

Instead of:

```text
1efee03cdcb96d90ad48ccc7b8666033
```

Use:

```text
mike:1efee03cdcb96d90ad48ccc7b8666033
```

---

# 16. GECOS Field

## What is GECOS?

Stores user information.

Examples:

* Full Name
* Office Number
* Phone Number

---

## Why Important?

John can use:

* User name
* Full name
* Home directory

To generate password guesses.

---

# 17. Custom Rules

## Why Use Custom Rules?

Many users follow patterns.

Example:

```text
Password1!
Admin123@
Welcome2024#
```

---

## Location

```bash
/etc/john/john.conf
```

or

```bash
/opt/john/john.conf
```

---

## Rule Structure

```text
[List.Rules:RuleName]
```

Example:

```text
[List.Rules:PoloPassword]
```

---

## Common Modifiers

| Modifier | Function   |
| -------- | ---------- |
| c        | Capitalize |
| Az       | Append     |
| A0       | Prepend    |

---

## Character Sets

| Pattern | Meaning     |
| ------- | ----------- |
| [0-9]   | Numbers     |
| [A-Z]   | Uppercase   |
| [a-z]   | Lowercase   |
| [A-z]   | All letters |
| [!@#$%] | Symbols     |

---

## Example Rule

```text
[List.Rules:PoloPassword]

cAz"[0-9][!@#$%]"
```

Generates:

```text
Password1!
Password5@
Password9#
```

---

## Using Custom Rule

```bash
john \
--wordlist=rockyou.txt \
--rule=PoloPassword \
hash.txt
```

---

# 18. Cracking ZIP Passwords

## zip2john

Converts ZIP file into crackable hash.

---

## Syntax

```bash
zip2john file.zip > zip_hash.txt
```

Example:

```bash
zip2john secret.zip > zip_hash.txt
```

---

## Crack ZIP Password

```bash
john \
--wordlist=/usr/share/wordlists/rockyou.txt \
zip_hash.txt
```

---

## Workflow

```text
ZIP File
   ↓
zip2john
   ↓
Hash File
   ↓
john
   ↓
Password
```

---

# 19. Cracking RAR Passwords

## rar2john

Converts RAR archive to hash.

---

## Syntax

```bash
rar2john file.rar > rar_hash.txt
```

Example:

```bash
rar2john secret.rar > rar_hash.txt
```

---

## Crack Password

```bash
john \
--wordlist=/usr/share/wordlists/rockyou.txt \
rar_hash.txt
```

---

## Workflow

```text
RAR File
   ↓
rar2john
   ↓
Hash File
   ↓
john
   ↓
Password
```

---

# 20. Cracking SSH Private Keys

## What is id_rsa?

Private SSH authentication key.

---

## Why Crack It?

If encrypted with a passphrase:

```text
Need passphrase before SSH login
```

---

# 21. ssh2john

Converts SSH private key into hash format.

---

## Syntax

```bash
ssh2john id_rsa > id_rsa_hash.txt
```

or

```bash
python3 /opt/john/ssh2john.py id_rsa > id_rsa_hash.txt
```

---

## Crack Password

```bash
john \
--wordlist=/usr/share/wordlists/rockyou.txt \
id_rsa_hash.txt
```

---

## Workflow

```text
id_rsa
   ↓
ssh2john
   ↓
Hash File
   ↓
john
   ↓
Passphrase
```

---

# 22. Useful Commands

## Show Cracked Passwords

```bash
john --show hash.txt
```

---

## Resume Cracking Session

```bash
john --restore
```

---

## List Formats

```bash
john --list=formats
```

---

## Search Format

```bash
john --list=formats | grep -i sha
```

---

## Check Version

```bash
john --version
```

---

# 23. Quick Revision

| Tool     | Purpose                 |
| -------- | ----------------------- |
| john     | Crack hashes            |
| unshadow | Combine passwd + shadow |
| zip2john | ZIP → Hash              |
| rar2john | RAR → Hash              |
| ssh2john | SSH Key → Hash          |

---

