# Hashing Basics

## Overview

Hashing is one of the most important concepts in Cybersecurity.

It is used for:

* Password Storage
* Data Integrity Verification
* Digital Signatures
* Authentication Systems
* HMAC
* Malware Analysis
* Digital Forensics

Unlike encryption, hashing is a **one-way process**.

---

# What is Hashing?

## Definition

A hash function takes input data of any size and produces a fixed-size output called a hash value (digest).

```text
Input Data
      │
      ▼
 Hash Function
      │
      ▼
 Hash Value
```

---

## Example

Input:

```text
TryHackMe
```

Output:

```text
SHA256:
95c5c7e...
```

Even a tiny change creates a completely different hash.

---

# Properties of a Good Hash Function

## 1. Fixed Output Size

Input can be any size:

```text
A
Hello
100 MB File
10 GB File
```

Output size remains fixed.

Example:

```text
SHA256 → 256 bits
```

---

## 2. Deterministic

Same input always produces the same output.

```text
Hash("Hello")
=
Hash("Hello")
```

---

## 3. Fast Computation

Hashes should be calculated quickly.

---

## 4. Avalanche Effect

A small change in input causes a huge change in output.

Example:

```text
T
U
```

Only one bit differs.

Yet:

```text
MD5(T)
≠
MD5(U)
```

Completely different hashes.

---

## 5. One-Way Function

Given:

```text
Password123
```

You can calculate:

```text
Hash(Password123)
```

But from the hash:

```text
a8f5f167...
```

You should NOT be able to recover the password.

---

# Common Hashing Algorithms

| Algorithm | Status      |
| --------- | ----------- |
| MD5       | Broken      |
| SHA1      | Broken      |
| SHA256    | Secure      |
| SHA512    | Secure      |
| bcrypt    | Secure      |
| scrypt    | Secure      |
| Argon2    | Recommended |
| PBKDF2    | Secure      |

---

# Hashing vs Encryption

| Feature            | Hashing | Encryption |
| ------------------ | ------- | ---------- |
| Reversible         | No      | Yes        |
| Uses Key           | No      | Yes        |
| Confidentiality    | No      | Yes        |
| Integrity Checking | Yes     | No         |
| Password Storage   | Yes     | No         |

---

# Hashing vs Encoding

| Feature    | Hashing   | Encoding            |
| ---------- | --------- | ------------------- |
| Reversible | No        | Yes                 |
| Security   | Yes       | No                  |
| Purpose    | Integrity | Data Representation |

---

## Example

Base64 Encoding

Input:

```text
TryHackMe
```

Encoded:

```text
VHJ5SGFja01l
```

Decoded:

```text
TryHackMe
```

Therefore:

```text
Encoding ≠ Encryption
Encoding ≠ Hashing
```

---

# Hash Collisions

## Definition

A collision occurs when:

```text
Input A ≠ Input B
```

But:

```text
Hash(A) = Hash(B)
```

---

## Example

```text
File 1
      │
      ▼
Hash = ABC

File 2
      │
      ▼
Hash = ABC
```

Different files produce the same hash.

---

# Why Collisions Exist?

Because:

```text
Infinite Inputs
Finite Outputs
```

This creates the:

## Pigeonhole Principle

If:

```text
21 pigeons
16 holes
```

At least two pigeons share one hole.

Similarly:

```text
Many Inputs
Limited Hash Values
```

Collisions are unavoidable.

---

# Broken Hash Functions

## MD5

Produces:

```text
128-bit hash
```

Not secure.

Collision attacks exist.

---

## SHA1

Produces:

```text
160-bit hash
```

Also broken.

Collision attacks exist.

---

# Secure Alternatives

Use:

```text
SHA256
SHA512
Argon2
bcrypt
scrypt
PBKDF2
```

---

# Password Storage

---

## Bad Practice #1

### Storing Plaintext Passwords

Database:

| User  | Password    |
| ----- | ----------- |
| Alice | password123 |
| Bob   | admin123    |

If database leaks:

```text
All passwords exposed
```

---

## Real Example

RockYou Breach

Over:

```text
14 million passwords
```

stored in plaintext.

Source of:

```text
rockyou.txt
```

used by attackers today.

---

# Bad Practice #2

Using Encryption

Example:

```text
Password
      ↓
Encrypted
      ↓
Stored
```

Problem:

```text
Encryption Key
```

must also be stored.

If key is stolen:

```text
All passwords recovered
```

---

# Bad Practice #3

Weak Hash Functions

Example:

```text
MD5
SHA1
```

Fast and vulnerable to attacks.

---

# Secure Password Storage

Modern systems use:

```text
Argon2
bcrypt
scrypt
PBKDF2
```

---

# Password Salting

## Problem

Two users choose:

```text
password123
```

Without salt:

```text
Hash(password123)
=
Same Hash
```

---

## Solution

Add random value:

```text
Password + Salt
```

Example:

```text
Password:
AL4RMc10k

Salt:
Y4UV*^(=go_!
```

Combined:

```text
AL4RMc10kY4UV*^(=go_!
```

Hash the result.

---

# Benefits of Salt

## Prevents Rainbow Tables

## Prevents Duplicate Hashes

## Makes Cracking Harder

Even identical passwords produce:

```text
Different Hashes
```

---

# Rainbow Tables

## Definition

Precomputed database:

```text
Hash → Password
```

Example:

| Hash                             | Password |
| -------------------------------- | -------- |
| e10adc3949ba59abbe56e057f20f883e | 123456   |
| e99a18c428cb38d5f260853678922e03 | abc123   |

---

## Purpose

Instead of cracking:

```text
Lookup Hash
```

Instant recovery.

---

# Linux Password Hashes

Stored in:

```bash
/etc/shadow
```

---

## Format

```text
$prefix$options$salt$hash
```

---

# Common Linux Prefixes

| Prefix | Algorithm     |
| ------ | ------------- |
| $y$    | yescrypt      |
| $gy$   | gost-yescrypt |
| $7$    | scrypt        |
| $2y$   | bcrypt        |
| $6$    | SHA512        |
| $1$    | MD5           |

---

## Example

```text
$y$j9T$76UzfgEM5PnymhQ7TlJey1$/OOSg64...
```

Components:

```text
Algorithm = yescrypt
Options   = j9T
Salt      = 76UzfgEM5PnymhQ7TlJey1
Hash      = /OOSg64...
```

---

# Windows Password Hashes

Stored in:

```text
SAM Database
```

Hash Type:

```text
NTLM
```

---

# Cracking Hashes

Hashes cannot be decrypted.

Instead:

```text
Guess Password
      ↓
Hash Guess
      ↓
Compare
```

If match:

```text
Password Found
```

---

# Popular Cracking Tools

## John the Ripper

```bash
john hashes.txt
```

---

## Hashcat

```bash
hashcat -m HASH_TYPE -a 0 hash.txt wordlist.txt
```

---

# to find hasg type
#  step1 first identify the hash  for that go to this url : https://hashes.com/en/tools/hash_identifier
# step2: then to find the number of that hash type go to this url and ctrl +f for seach : https://hashcat.net/wiki/doku.php?id=example_hashes
# step3: use the tool hash cat for find
# step 4: if still not found then use this website : https://hashes.com/en/decrypt/hash

# Important Hashcat Parameters

## Hash Type

```bash
-m
```

Example:

```bash
-m 1000
```

NTLM

---

## Attack Mode

```bash
-a 0
```

Dictionary Attack

---

# Brute Force Attack

Tries:

```text
000000
000001
000002
...
```

Eventually succeeds.

Very slow.

---

# Dictionary Attack

Uses:

```text
rockyou.txt
```

Tries:

```text
password
welcome
admin123
football
```

Much faster.

---

# GPU Password Cracking

GPUs contain:

```text
Thousands of Cores
```

Excellent for:

```text
Hash Calculations
```

---

## Resistant Algorithms

Designed against GPU acceleration:

```text
bcrypt
scrypt
Argon2
```

---

# Integrity Verification

Hashing can verify files.

---

## Example

Downloaded:

```text
Fedora.iso
```

Website provides:

```text
SHA256 Hash
```

Verify:

```bash
sha256sum Fedora.iso
```

Compare outputs.

If equal:

```text
File Integrity Verified
```

---

# Duplicate File Detection

If:

```text
Hash(File1)
=
Hash(File2)
```

Then:

```text
Files are identical
```

Useful in:

* Digital Forensics
* Storage Optimization

---

# HMAC

## Full Form

Hash-based Message Authentication Code

---

## Purpose

Provides:

* Integrity
* Authenticity

---

## Formula

```text
HMAC(K,M)
=
H((K⊕opad)||H((K⊕ipad)||M))
```

Where:

```text
K = Secret Key
M = Message
```

---

# Why HMAC?

Normal hash:

```text
Integrity
```

HMAC:

```text
Integrity
+
Authentication
```

Because it uses a secret key.

---

# Hashing, Encoding, Encryption

## Hashing

```text
One Way
Cannot Reverse
```

Example:

```text
SHA256
bcrypt
```

---

## Encoding

```text
Reversible
No Security
```

Example:

```text
Base64
UTF-8
ASCII
```

---

## Encryption

```text
Reversible
Uses Key
Provides Confidentiality
```

Example:

```text
AES
RSA
ChaCha20
```

---

# Quick Revision

## Hash Function

```text
Any Input
↓
Fixed-Length Output
```

---

## Secure Password Storage

```text
Password
+
Salt
↓
Argon2 / bcrypt
↓
Store Hash
```

---

## Never Use

```text
MD5
SHA1
Plaintext Passwords
```

---

## Use Instead

```text
Argon2
bcrypt
scrypt
PBKDF2
```

---
