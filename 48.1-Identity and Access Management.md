# Identity and Access Management

The main idea of this room is:

> **Who are you? → Prove it → What can you access? → Track what you do.**

This is called **IAAA**.

## IAAA Model

| Concept            | Simple Meaning     | Question             |
| ------------------ | ------------------ | -------------------- |
| **Identification** | Claim an identity  | Who are you?         |
| **Authentication** | Prove the identity | Can you prove it?    |
| **Authorisation**  | Decide permissions | What can you access? |
| **Accountability** | Track user actions | What did you do?     |

Easy flow:

**Identification → Authentication → Authorisation → Accountability**

Example: You enter your username, provide your password, get access to allowed files, and your activity is logged.


# Identification

**Identification** means a user, process, or system **claims an identity**.

Examples of identifiers:

* Username
* Email address
* Student ID
* Passport number
* Mobile number

Example:

`Username: sai`

You are saying:

> "I am sai"

But the system has **not yet confirmed that you really are sai**.

That confirmation happens during authentication.

> **Identification = Claim who you are.**

# Authentication

**Authentication** verifies that you are really the person you claim to be.

Example:

Identification:

`Username: sai`

Authentication:

`Password: ********`

The password proves that you are the account owner.

> **Authentication = Prove who you are.**

There are three main authentication factors.

| Factor                 | Meaning                  | Example             |
| ---------------------- | ------------------------ | ------------------- |
| **Something you know** | Secret you remember      | Password, PIN       |
| **Something you have** | Object you possess       | Phone, security key |
| **Something you are**  | Biometric characteristic | Fingerprint, face   |

### Something You Know

Information you remember.

Examples:

* Password
* Passphrase
* PIN

### Something You Have

A physical object you possess.

Examples:

* Mobile phone
* SIM card
* OTP device
* Hardware security key

For example, a website sends an OTP to your phone. Receiving the OTP proves that you have access to that phone or number.

### Something You Are

Biometric characteristics.

Examples:

* Fingerprint
* Face
* Retina
* Voice

Two less commonly used factors are **somewhere you are**, such as your location, and **something you do**, such as behavioural patterns.

# Multi-Factor Authentication (MFA)

**MFA** uses **two or more different authentication factors**.

Example:

`Password + OTP`

Password = **Something you know**

Phone receiving OTP = **Something you have**

Another example is an ATM:

`Bank Card + PIN`

Card = Something you have.

PIN = Something you know.

> **MFA = Two or more different authentication factors.**

**2FA** specifically uses two factors. **MFA** means two or more factors.

# Authentication and Replay Attacks

Imagine a user sends a password across a network in cleartext.

An attacker capturing the network traffic may steal the password.

One idea is to encrypt the password.

But there is still a problem.

Suppose the encrypted password always looks like:

`A7F91B82`

An attacker captures this value and sends the **same value again** to the server.

The attacker does not know the original password, but the server may accept the reused authentication message.

This is a **Replay Attack**.

> **Replay Attack = Capture a valid authentication message and resend it later.**

Simple flow:

**User sends valid response → Attacker captures it → Attacker resends it → Server accepts it**

## Preventing Replay Attacks

Authentication responses should be **unique and temporary**.

For example, the authentication process may include:

* Current timestamp
* Random value
* Unique challenge

A timestamp makes the authentication response valid only for a short period.

The main lesson is:

> **Do not create your own authentication protocol without proper security testing. Use established and tested protocols.**

# Authorisation

After authentication, the system decides **what the user is allowed to access or do**.

This is **Authorisation**.

Example:

A sales employee can access:

* Sales reports
* Customer sales information

But should not access:

* HR documents
* Payroll information

> **Authorisation = Decide what an authenticated user is allowed to do.**

# Access Control

**Access Control enforces authorisation decisions.**

There is a small but important difference:

> **Authorisation decides the permission.**

> **Access Control enforces the permission.**

Example:

Authorisation says:

`Sai can read sales.txt`

File permissions prevent Sai from modifying the file.

That enforcement is **Access Control**.

# Access Control Models

There are three important access control models:

| Model    | Access Controlled By   |
| -------- | ---------------------- |
| **DAC**  | Resource owner         |
| **RBAC** | User role              |
| **MAC**  | System security policy |

## DAC  Discretionary Access Control

In **DAC**, the **resource owner decides who gets access**.

Example: You upload photos to cloud storage and personally give access to your family members.

You decide:

`User A → View`

`User B → View`

`User C → No Access`

> **DAC = Owner controls access.**

The disadvantage is that managing access becomes difficult when there are many users.


## RBAC Role-Based Access Control

In **RBAC**, access is based on the user's **job role**.

Example:

`Accountant → Accounting Files`

`HR Employee → HR Files`

`Developer → Source Code`

If a new accountant joins, simply add the user to the **Accountant role/group**.

If the employee changes jobs, change their role.

> **RBAC = Access based on role.**

This is easier to manage in large organisations.

## MAC — Mandatory Access Control

In **MAC**, access is controlled by **strict system security policies**.

Users cannot freely change permissions.

It is commonly used in systems that handle highly sensitive or classified data.

Examples of Linux MAC technologies include **AppArmor** and **SELinux**.

> **MAC = System policy controls access.**

Easy memory:

**DAC → Data owner decides**

**RBAC → Role decides**

**MAC → Mandatory system policy decides**

# Accountability

**Accountability** means users can be held responsible for their actions.

After a user logs in and receives access, the organisation must know:

* Who accessed the system?
* What did they access?
* What action did they perform?
* When did they perform it?

This is mainly achieved through **logging and auditing**.

> **Accountability = Track user actions and identify who did what.**

# Logging

**Logging** is the process of recording events and activities in a system.

Logs may record:

* User logins
* Failed login attempts
* File access
* File modification
* System errors
* Network activity

Example:

`10:30 → Sai logged in`

`10:35 → Sai accessed report.pdf`

`10:40 → Sai modified sales.txt`

Logs are useful for:

* Incident response
* Digital forensics
* Security monitoring
* Auditing
* Compliance

Logs should be protected from modification or deletion.

An attacker may try to delete logs to hide their activity.


# Log Forwarding

**Log Forwarding** means sending logs from systems to a **central logging server**.

Example:

**Server A → Central Log Server**

**Server B → Central Log Server**

**Firewall → Central Log Server**

**Windows PC → Central Log Server**

The main benefit is that logs are stored centrally and can be analyzed together.

> **Log Forwarding = Send logs to a central location.**

It also makes it harder for an attacker who compromises one machine to erase all evidence of their actions.

# SIEM

**SIEM stands for Security Information and Event Management.**

A SIEM collects logs from multiple systems and analyzes them for suspicious activity.

Simple flow:

**Windows + Firewall + Server + EDR → SIEM → Analyze Logs → Generate Alert**

SIEM can help detect:

* Repeated failed logins
* Unusual user activity
* Suspicious network connections
* Possible attacks

SIEM is also useful for:

* Incident response
* Compliance reporting
* Forensic investigations

> **SIEM = Centralize and analyze logs to detect security threats.**

# Identity Management (IdM)

**Identity Management (IdM)** focuses on managing **digital identities**.

Each user or device receives a digital identity.

IdM manages:

* User accounts
* User identities
* Authentication
* Permissions
* Access rights

One important process is **User Provisioning**.

**User Provisioning** means creating and managing user accounts.

Example:

A new employee joins.

The IdM system creates their account and assigns the required permissions.

> **IdM = Manage digital identities and their permissions.**

# Identity and Access Management (IAM)

**IAM** is a broader concept than IdM.

IAM manages **identities and access to organisational resources**.

IAM may include:

* User provisioning
* Authentication
* Authorisation
* Access control
* MFA
* RBAC
* SSO
* Identity governance
* Access auditing

It also manages the user identity lifecycle.

Example:

**Employee joins → Account created**

**Employee changes role → Permissions changed**

**Employee leaves → Access revoked**

> **IAM = Manage identities and control access to resources.**

### IdM vs IAM

| IdM                            | IAM                              |
| ------------------------------ | -------------------------------- |
| Focuses on identities          | Focuses on identities and access |
| Manages user accounts          | Controls access to resources     |
| Authentication and permissions | Broader access management        |
| Identity management            | Identity + Access management     |

The boundary between **IdM and IAM can sometimes be unclear**, and some sources use the terms interchangeably.

# Single Sign-On (SSO)

**SSO allows a user to log in once and access multiple services.**

Without SSO:

`Email → Login`

`File Server → Login`

`HR System → Login`

`Company Portal → Login`

With SSO:

`One Login → Email + File Server + HR System + Company Portal`

> **SSO = Authenticate once and access multiple authorised services.**

Benefits of SSO include:

* One strong password to remember.
* Easier MFA configuration.
* Easier password resets.
* Better user efficiency.
* Centralised authentication.

---
