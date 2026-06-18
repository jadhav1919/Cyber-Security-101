# Cryptography Basics

## What is Cryptography?

Cryptography is the science of protecting information and communication from unauthorized access.

### Definition

> Cryptography is the practice and study of techniques used for secure communication and data protection in the presence of adversaries.

Its primary goal is to ensure:

* **Confidentiality** → Prevent unauthorized reading of data.
* **Integrity** → Prevent unauthorized modification of data.
* **Authenticity** → Verify the identity of communicating parties.

---

# Why is Cryptography Important?

Cryptography is used every day without users noticing it.

## Real-World Examples

### 1. Website Login

When you log into a website:

```text
Username + Password
        ↓
    Encrypted
        ↓
      Server
```

This prevents attackers from stealing credentials.

---

### 2. SSH Connections

SSH creates an encrypted tunnel:

```text
Your PC  <==== Encrypted Tunnel ====> Server
```

No one can read your commands or outputs.

---

### 3. Online Banking

Cryptography ensures:

* You're communicating with the real bank.
* Attackers cannot impersonate the bank.

---

### 4. File Verification

Hash functions help verify:

```text
Downloaded File == Original File ?
```

If hashes match:

```text
Integrity Verified
```

---

# Security Goals of Cryptography

| Goal            | Description                |
| --------------- | -------------------------- |
| Confidentiality | Data remains secret        |
| Integrity       | Data cannot be modified    |
| Authenticity    | Verify identity            |
| Non-Repudiation | Sender cannot deny sending |

---

# Fundamental Cryptography Terms

---

## Plaintext

Original readable data before encryption.

### Examples

```text
Hello World
Password123
Credit Card Data
Medical Records
```

---

## Ciphertext

Encrypted unreadable version of plaintext.

### Example

```text
Plaintext : HELLO

Ciphertext : KHOOR
```

Without the key, ciphertext should appear meaningless.

---

## Cipher

Algorithm used to perform encryption and decryption.

### Examples

* Caesar Cipher
* AES
* DES
* RSA

---

## Key

A secret value used by a cipher.

```text
Plaintext + Key + Cipher
           ↓
      Ciphertext
```

Security depends on the key, not on keeping the algorithm secret.

---

## Encryption

Process of converting:

```text
Plaintext
    ↓
Ciphertext
```

---

## Decryption

Reverse process:

```text
Ciphertext
    ↓
Plaintext
```

---

# Encryption Process

```text
Plaintext
    │
    ▼
Encryption Algorithm
      +
     Key
    │
    ▼
Ciphertext
```

---

# Decryption Process

```text
Ciphertext
     │
     ▼
Decryption Algorithm
       +
      Key
     │
     ▼
Plaintext
```

---

# Caesar Cipher

One of the oldest encryption methods.

Developed during the time of:

Julius Caesar

---

## Working Principle

Each letter is shifted by a fixed number.

### Example

```text
Plaintext : TRYHACKME

Key : 3
```

Shift every letter 3 positions right.

```text
T → W
R → U
Y → B
```

Result:

```text
Ciphertext : WUBKDFNPH
```

---

## Decryption

Shift letters left by the same key.

```text
W → T
U → R
B → Y
```

Recovered:

```text
TRYHACKME
```

---

## Weakness of Caesar Cipher

Only 25 possible keys exist.

An attacker can try all possibilities:

```text
Key 1
Key 2
Key 3
...
Key 25
```

This is called:

### Brute Force Attack

Therefore:

```text
Caesar Cipher = Insecure
```

---

# Historical Ciphers

| Cipher          | Era          |
| --------------- | ------------ |
| Caesar Cipher   | Ancient Rome |
| Vigenère Cipher | 16th Century |
| Enigma Machine  | World War II |
| One-Time Pad    | Cold War     |

---

# Types of Encryption

There are two major categories:

```text
Encryption
│
├── Symmetric Encryption
│
└── Asymmetric Encryption
```

---

# Symmetric Encryption

Uses the **same key** for:

* Encryption
* Decryption

---

## Concept

```text
Shared Secret Key
       │
 ┌─────┴─────┐
 │           │
Encrypt   Decrypt
```

---

## Problem

How do you securely share the secret key?

Example:

```text
Encrypted File
      +
Password
```

Sending both by email defeats the purpose.

---

## Symmetric Encryption Algorithms

### DES (Data Encryption Standard)

| Property     | Value   |
| ------------ | ------- |
| Standardized | 1977    |
| Key Size     | 56 bits |

Weak because modern computers can crack it.

---

### 3DES (Triple DES)

DES applied three times.

| Property           | Value    |
| ------------------ | -------- |
| Key Size           | 168 bits |
| Effective Security | 112 bits |

Deprecated in 2019.

---

### AES (Advanced Encryption Standard)

Current industry standard.

| AES Version | Key Size |
| ----------- | -------- |
| AES-128     | 128 bits |
| AES-192     | 192 bits |
| AES-256     | 256 bits |

Most widely used symmetric cipher today.

---

# Asymmetric Encryption

Uses two different keys.

```text
Public Key
Private Key
```

---

## Concept

```text
Public Key
     │
Encrypt
     │
Ciphertext
     │
Decrypt
     │
Private Key
```

---

## Key Pair

### Public Key

Can be shared with everyone.

### Private Key

Must remain secret.

---

## Example

Alice wants to send a secret message to Bob.

```text
Bob shares Public Key
        │
Alice encrypts message
        │
Bob decrypts using Private Key
```

Only Bob can read it.

---

# Common Asymmetric Algorithms

---

## RSA

Most common public-key algorithm.

Recommended key sizes:

```text
2048 bits
3072 bits
4096 bits
```

---

## Diffie-Hellman

Used for secure key exchange.

Recommended minimum:

```text
2048 bits
```

---

## ECC (Elliptic Curve Cryptography)

Provides equivalent security with much smaller keys.

Example:

```text
ECC 256-bit
≈
RSA 3072-bit
```

Advantages:

* Faster
* Smaller keys
* Less resource consumption

---

# Symmetric vs Asymmetric Encryption

| Feature     | Symmetric       | Asymmetric                   |
| ----------- | --------------- | ---------------------------- |
| Keys        | One             | Two                          |
| Speed       | Fast            | Slower                       |
| Key Sharing | Difficult       | Easy                         |
| Examples    | AES, DES        | RSA, ECC                     |
| Usage       | Bulk encryption | Key exchange, authentication |

---

# Cryptography Characters

Two fictional characters are commonly used:

```text
Alice
Bob
```

Used to represent secure communication examples.

---

# Mathematical Foundations of Cryptography

Modern cryptography relies heavily on mathematics.

Two important operations:

1. XOR
2. Modulo

---

# XOR Operation

XOR = Exclusive OR

Symbol:

```text
⊕
^
```

---

## XOR Truth Table

| A | B | A ⊕ B |
| - | - | ----- |
| 0 | 0 | 0     |
| 0 | 1 | 1     |
| 1 | 0 | 1     |
| 1 | 1 | 0     |

---

## Example

```text
1010
1100
```

Bit-by-bit XOR:

```text
1⊕1=0
0⊕1=1
1⊕0=1
0⊕0=0
```

Result:

```text
0110
```

---

# Important XOR Properties

## Property 1

```text
A ⊕ A = 0
```

Example:

```text
1010 ⊕ 1010 = 0000
```

---

## Property 2

```text
A ⊕ 0 = A
```

---

## Property 3 (Commutative)

```text
A ⊕ B = B ⊕ A
```

---

## Property 4 (Associative)

```text
(A ⊕ B) ⊕ C
=
A ⊕ (B ⊕ C)
```

---

# XOR as Encryption

Let:

```text
P = Plaintext
K = Key
```

Encryption:

```text
C = P ⊕ K
```

Decryption:

```text
P = C ⊕ K
```

Because:

```text
K ⊕ K = 0
```

---

# Modulo Operation

Modulo returns the remainder after division.

Symbol:

```text
%
mod
```

---

## Examples

### Example 1

```text
25 % 5 = 0
```

Because:

```text
25 = 5 × 5 + 0
```

---

### Example 2

```text
23 % 6 = 5
```

Because:

```text
23 = 3 × 6 + 5
```

---

### Example 3

```text
23 % 7 = 2
```

Because:

```text
23 = 3 × 7 + 2
```

---

# Important Property of Modulo

Modulo is **not reversible**.

Example:

```text
x % 5 = 4
```

Possible values:

```text
4
9
14
19
24
...
```

Infinite solutions exist.

---

# Quick Revision

### Core Terms

```text
Plaintext  → Original Data
Ciphertext → Encrypted Data
Cipher     → Encryption Algorithm
Key        → Secret Value
Encryption → Plaintext → Ciphertext
Decryption → Ciphertext → Plaintext
```

---

### Symmetric Encryption

```text
Same Key
AES
DES
3DES
Fast
```

---

### Asymmetric Encryption

```text
Public Key + Private Key
RSA
ECC
Diffie-Hellman
Slower
```

---

### Important Formulas

```text
C = P ⊕ K

P = C ⊕ K

X % Y = Remainder
```

---

