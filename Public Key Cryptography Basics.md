# Public Key Cryptography Basics

## Overview

Cryptography protects communication in the presence of attackers.

The main security goals are:

* Authentication
* Authenticity
* Integrity
* Confidentiality

This module focuses on **Public Key Cryptography (Asymmetric Cryptography)** and its real-world applications.

---

# Security Concepts

## 1. Authentication

Authentication verifies the identity of a user or system.

### Example

When you meet someone in person, you can visually confirm their identity.

In cyberspace:

```text
Are you really talking to the intended person?
```

Authentication answers this question.

---

## 2. Authenticity

Authenticity verifies that a message truly came from the claimed sender.

### Example

If Bob sends a message:

```text
Hello Alice
```

Authenticity ensures that Bob actually sent it.

---

## 3. Integrity

Integrity guarantees that data has not been modified.

### Example

Original Message:

```text
Transfer ₹1000
```

Modified Message:

```text
Transfer ₹100000
```

Integrity mechanisms detect such changes.

---

## 4. Confidentiality

Confidentiality ensures that unauthorized people cannot read the data.

### Example

Encrypted chat messages.

---

# Symmetric vs Asymmetric Encryption

## Symmetric Encryption

Uses the same key for:

* Encryption
* Decryption

```text
Shared Secret Key
       ↓
Encrypt → Ciphertext → Decrypt
```

### Problem

How do you securely share the secret key?

---

## Asymmetric Encryption

Uses two keys:

```text
Public Key
Private Key
```

### Public Key

Can be shared publicly.

### Private Key

Must remain secret.

---

# Why Asymmetric Cryptography?

Asymmetric cryptography solves the key-distribution problem.

Instead of sharing a secret key:

```text
Sender uses Public Key
Receiver uses Private Key
```

Only the receiver can decrypt the message.

---

# Lock and Box Analogy

Imagine:

| Real World  | Cryptography  |
| ----------- | ------------- |
| Lock        | Public Key    |
| Lock Key    | Private Key   |
| Secret Code | Symmetric Key |

Process:

1. Receiver sends lock.
2. Sender places secret inside box.
3. Sender locks box.
4. Receiver unlocks using private key.

Only receiver can open it.

---

# RSA (Rivest-Shamir-Adleman)

RSA is the most popular public-key cryptosystem.

---

## Main Idea

RSA security depends on:

```text
Factoring Large Numbers
```

Multiplication is easy.

Example:

```text
113 × 127 = 14351
```

But finding:

```text
14351 = ?
```

is much harder.

---

# RSA Key Generation

Choose two large prime numbers:

```text
p
q
```

Calculate:

```text
n = p × q
```

Generate:

```text
Public Key  = (n,e)
Private Key = (n,d)
```

---

# RSA Variables

These appear frequently in CTFs.

| Variable | Meaning          |
| -------- | ---------------- |
| p        | First prime      |
| q        | Second prime     |
| n        | p × q            |
| e        | Public exponent  |
| d        | Private exponent |
| m        | Plaintext        |
| c        | Ciphertext       |

---

# RSA Encryption

Encryption:

```text
c = m^e mod n
```

---

# RSA Decryption

Decryption:

```text
m = c^d mod n
```

---

# RSA Workflow

```text
Bob Generates Keys

Public Key  → Shared
Private Key → Secret

Alice Encrypts Message
        ↓
Ciphertext
        ↓
Bob Decrypts
```

---

# RSA in CTFs

Common tasks:

* Factor n
* Recover p and q
* Calculate d
* Decrypt ciphertext

Useful tools:

```bash
RsaCtfTool
rsatool
```

---

# Diffie-Hellman Key Exchange

## Purpose

Securely establish a shared secret over an insecure network.

---

## Problem

Alice and Bob need a shared key.

They do NOT want to send the key directly.

---

## Public Values

Both agree on:

```text
p = Prime Number
g = Generator
```

These values are public.

---

## Private Values

Alice chooses:

```text
a
```

Bob chooses:

```text
b
```

These values remain secret.

---

## Public Keys

Alice calculates:

```text
A = g^a mod p
```

Bob calculates:

```text
B = g^b mod p
```

These are exchanged.

---

## Shared Secret

Alice computes:

```text
B^a mod p
```

Bob computes:

```text
A^b mod p
```

Both obtain:

```text
g^(ab) mod p
```

Same shared secret.

---

# Diffie-Hellman Workflow

```text
Public:
p, g

Alice Secret = a
Bob Secret   = b

A = g^a mod p
B = g^b mod p

Exchange A and B

Shared Secret:

Alice → B^a mod p
Bob   → A^b mod p
```

---

# RSA vs Diffie-Hellman

| Feature                  | RSA | Diffie-Hellman |
| ------------------------ | --- | -------------- |
| Encryption               | Yes | No             |
| Authentication           | Yes | No             |
| Key Exchange             | Yes | Yes            |
| Shared Secret Generation | No  | Yes            |

---

# Digital Signatures

## Purpose

Provide:

* Authentication
* Integrity
* Non-Repudiation

---

## Concept

Instead of encrypting with a public key:

```text
Encrypt with Private Key
```

Verification:

```text
Decrypt with Public Key
```

If successful:

```text
Message is authentic
```

---

# Digital Signature Process

```text
Document
    ↓
Hash
    ↓
Encrypt Hash
with Private Key
    ↓
Signature
```

Verification:

```text
Signature
     ↓
Decrypt using Public Key
     ↓
Compare Hashes
```

If hashes match:

```text
Integrity Verified
Authenticity Verified
```

---

# Certificates

Certificates prove identity online.

---

## Why Needed?

Without certificates:

```text
How do you know
google.com
is really Google?
```

---

# Certificate Authority (CA)

Trusted organizations that issue certificates.

Examples:

* DigiCert
* GlobalSign
* Let's Encrypt

---

# Chain of Trust

```text
Root CA
   ↓
Intermediate CA
   ↓
Website Certificate
```

Browser trusts Root CA.

Therefore:

```text
Browser trusts website certificate.
```

---

# HTTPS

HTTPS uses:

```text
TLS Certificate
```

Benefits:

* Encryption
* Authentication
* Integrity

---

# SSH Key Authentication

SSH supports key-based authentication.

Generate:

```bash
ssh-keygen
```

Creates:

```text
id_rsa
id_rsa.pub
```

---

## Private Key

```text
id_rsa
```

Keep secret.

---

## Public Key

```text
id_rsa.pub
```

Upload to server.

---

# PGP and GPG

## PGP

Pretty Good Privacy.

Used for:

* Email encryption
* File encryption
* Digital signatures

---

## GPG

GNU Privacy Guard

Open-source implementation of OpenPGP.

---

# Generate GPG Key

```bash
gpg --full-gen-key
```

---

# Import Existing Key

```bash
gpg --import backup.key
```

---

# Decrypt File

```bash
gpg --decrypt secret.gpg
```

---

# Cryptography vs Cryptanalysis

## Cryptography

Protecting information.

```text
Create Secure Systems
```

---

## Cryptanalysis

Breaking cryptographic systems.

```text
Attack Secure Systems
```

---

# Brute Force Attack

Try every possible key.

```text
0000
0001
0002
...
9999
```

Guaranteed success eventually.

Very slow.

---

# Dictionary Attack

Uses likely passwords.

Example:

```text
password
welcome
admin123
football
```

Faster than brute force.

---

# Quick Revision

## RSA

```text
Public Key  = (n,e)
Private Key = (n,d)

Encryption:
c = m^e mod n

Decryption:
m = c^d mod n
```

---

## Diffie-Hellman

```text
Shared Secret Generation

A = g^a mod p
B = g^b mod p

Secret:

B^a mod p
=
A^b mod p
```

---

## Digital Signatures

```text
Private Key → Sign
Public Key  → Verify
```

---

## Certificates

```text
Certificate
      ↓
Certificate Authority
      ↓
Trust
```

---

