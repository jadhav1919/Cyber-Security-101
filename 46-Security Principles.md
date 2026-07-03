# Security Principles 

### What Are Security Principles?

Security principles are basic concepts used to protect:
Data
Computers
Networks
Applications
Organizations

# CIA Triad and Security Elements

Before calling a system **secure**, we need to check **what security properties it protects**.

The three main security goals are called the **CIA Triad**:

```text
Confidentiality
Integrity
Availability
```

# 1. Confidentiality

**Confidentiality means only authorized people should be able to access data.**

Simple meaning:

> **Keep information secret from unauthorized people.**

### Example :Online Shopping

Your **credit card number** should only be accessible to the authorized payment processor.

If an attacker steals it:

```text
Credit Card Data
       ↓
Unauthorized Person
       ↓
Confidentiality Breach
```

### Security Controls

* Encryption
* Passwords
* Access control
* Multi-Factor Authentication (MFA)

### Remember

> **Confidentiality = Who can SEE the data?**

# 2. Integrity

**Integrity means data should not be changed without authorization.**

If data is changed, the system should be able to **detect the modification**.

### Example: Online Shopping

You enter:

```text
Shipping Address:
Kottayam
```

An attacker changes it to:

```text
Shipping Address:
Mumbai
```

Now the package is delivered to the wrong location.

This is an **integrity violation**.

### Medical Example

Original medicine:

```text
Medicine Dose: 10 mg
```

Attacker changes:

```text
Medicine Dose: 100 mg
```

This can be extremely dangerous.

### Security Controls

* Hashing
* Digital signatures
* File integrity monitoring
* Access control

### Remember

> **Integrity = Has the data been CHANGED?**

# 3. Availability

**Availability means systems and data should be accessible when required.**

### Example — Online Shopping

You want to purchase something.

```text
Open Website
      ↓
Server Down
      ↓
Cannot Order
```

The service is **unavailable**.

### Medical Example

A doctor needs a patient's medical history.

```text
Doctor
   ↓
Medical System Down
   ↓
Cannot Access Patient Records
```

This may affect diagnosis and treatment.

### Threats to Availability

* DoS attacks
* DDoS attacks
* Hardware failures
* Server crashes
* Ransomware

### Security Controls

* Backups
* Redundant servers
* Load balancing
* Disaster recovery

### Remember

> **Availability = Can I ACCESS the data or service?**

# CIA Triad

| Security Goal   | Simple Question                |
| --------------- | ------------------------------ |
| Confidentiality | Who can **see** the data?      |
| Integrity       | Has the data been **changed**? |
| Availability    | Can I **access** the data?     |

# Beyond the CIA Triad

Two additional security properties are:

* **Authenticity**
* **Nonrepudiation**

# 4. Authenticity

**Authenticity means verifying that data actually comes from the claimed source.**

Simple meaning:

> **Is the sender real?**

### Example

You receive an email:

```text
From: College Administration
```

But did the college really send it?

If we verify the real sender:

```text
Claimed Sender
      ↓
Verify Identity
      ↓
Real Sender Confirmed
```

This provides **authenticity**.

# 5. Nonrepudiation

**Nonrepudiation ensures that a person cannot deny performing an action.**

The word **repudiate** means **to deny or refuse to accept something**.

### Example

A customer places an order:

```text
Order: 1000 Cars
```

Later, the customer says:

> "I never placed that order."

If the company has a verified digital signature proving the customer's action, the customer cannot easily deny it.

This is **nonrepudiation**.

### Security Controls

* Digital signatures
* Audit logs
* Timestamps
* Certificates

### Remember

> **Nonrepudiation = You cannot DENY your action.**

---

# Parkerian Hexad

In **1998**, Donn Parker proposed the **Parkerian Hexad**.

It expands security from **3 elements to 6 elements**.

The six elements are:

| Element         | Meaning                               |
| --------------- | ------------------------------------- |
| Confidentiality | Protect data from unauthorized access |
| Integrity       | Prevent unauthorized modification     |
| Availability    | Ensure data is accessible             |
| Authenticity    | Verify the source                     |
| Utility         | Ensure data is useful                 |
| Possession      | Maintain control of data              |

Easy memory:

```text
C I A A U P
```

# 6. Utility

**Utility means information must be useful and usable.**

You may have the data, but if you cannot use it, it has **no utility**.

### Example

You have a laptop with an encrypted disk.

```text
Laptop      
Hard Disk   
Data        
```

But you lost the decryption key.

```text
Decryption Key 
```

The data still exists and is technically available.

However:

```text
Encrypted Data
      ↓
No Key
      ↓
Cannot Read Data
      ↓
No Utility
```

### Remember

> **Utility = Is the data USEFUL?**

# 7. Possession

**Possession means maintaining control over information.**

The data should not be taken, copied, or controlled by an unauthorized person.

### Example: Stolen Backup Drive

An attacker steals your backup drive.

```text
Backup Drive
      ↓
Attacker Takes It
      ↓
Loss of Possession
```

The data may still exist.

However, the attacker now **possesses the data**.

### Ransomware Example

```text
Your Data
    ↓
Ransomware Encrypts It
    ↓
Attacker Controls Access
    ↓
Loss of Possession
```

### Remember

> **Possession = Who CONTROLS the data?**

# Parkerian Hexad — Simple Questions

| Element         | Ask This Question        |
| --------------- | ------------------------ |
| Confidentiality | Who can **see** it?      |
| Integrity       | Has it been **changed**? |
| Availability    | Can I **access** it?     |
| Authenticity    | Is the source **real**?  |
| Utility         | Is the data **useful**?  |
| Possession      | Who **controls** it?     |

-----------

# DAD Triad — Opposite of CIA Triad

The **CIA Triad** explains what we want to **protect**.

The **DAD Triad** explains how attackers can **damage security**.

| CIA Triad           | Opposite — DAD Triad     |
| ------------------- | ------------------------ |
| **Confidentiality** | **Disclosure**           |
| **Integrity**       | **Alteration**           |
| **Availability**    | **Destruction / Denial** |

Easy way to remember:

```text
CIA = Protection Goals

DAD = Attacks Against Those Goals
```

# 1. Disclosure

**Disclosure means confidential information is exposed to unauthorized people.**

It is the opposite of **Confidentiality**.

```text
Confidentiality
      ↕
Disclosure
```

### Example

An attacker steals patient medical records and publishes them online.

```text
Medical Records
       ↓
Attacker Steals Data
       ↓
Publishes Data Online
       ↓
Disclosure
```

Now unauthorized people can see private information.

### Cybersecurity Examples

* Stolen passwords
* Leaked customer data
* Exposed credit card details
* Medical record leaks
* Confidential company files published online

### Remember

> **Disclosure = Secret data is EXPOSED.**


# 2. Alteration

**Alteration means unauthorized modification of data.**

It is the opposite of **Integrity**.

```text
Integrity
    ↕
Alteration
```

### Example — Medical Record

Original record:

```text
Medicine Dose: 10 mg
```

Attacker changes it:

```text
Medicine Dose: 100 mg
```

The data has been modified.

This is an **alteration attack**.

The result could be life-threatening because the patient may receive incorrect treatment.

### Cheque Example

Original cheque:

```text
₹1,000
```

Attacker adds a zero:

```text
₹10,000
```

The integrity of the cheque has been compromised.

### Cybersecurity Examples

* Modifying database records
* Changing account balances
* Changing file contents
* Modifying system configurations
* Changing medical records

### Remember

> **Alteration = Data is CHANGED.**

# 3. Destruction / Denial

**Destruction or Denial means making data or services unavailable.**

It is the opposite of **Availability**.

```text
Availability
      ↕
Destruction / Denial
```

### Example — Hospital

Imagine a hospital is completely paperless.

All patient records are stored digitally.

```text
Doctor
   ↓
Patient Database
   ↓
Patient Records
```

An attacker makes the database unavailable.

```text
Attacker
   ↓
Database Unavailable
   ↓
Doctors Cannot Access Records
   ↓
Hospital Operations Affected
```

This is a **Denial attack**.

### Cybersecurity Examples

* DoS attack
* DDoS attack
* Deleting important files
* Destroying databases
* Ransomware making files inaccessible
* Shutting down critical servers

### Remember

> **Destruction / Denial = Data or service is NOT AVAILABLE.**

# CIA vs DAD

| Security Goal   | Attack               | Simple Meaning              |
| --------------- | -------------------- | --------------------------- |
| Confidentiality | Disclosure           | Data exposed                |
| Integrity       | Alteration           | Data changed                |
| Availability    | Destruction / Denial | Data or service unavailable |

Easy memory:

```text
C → D
Confidentiality → Disclosure

I → A
Integrity → Alteration

A → D
Availability → Destruction / Denial
```

-------------


# Security Models

**Security models** are rules used to control how users access and modify data.

The three important models are:

| Model             | Main Goal       |
| ----------------- | --------------- |
| **Bell-LaPadula** | Confidentiality |
| **Biba**          | Integrity       |
| **Clark-Wilson**  | Integrity       |

# 1. Bell-LaPadula Model

The **Bell-LaPadula Model** focuses on **Confidentiality**.

Its goal is to prevent sensitive information from being disclosed to unauthorized users.

Imagine two security levels:

```text
TOP SECRET
     ↑
   SECRET
     ↑
   PUBLIC
```

## No Read Up

A user with a **lower security level cannot read higher-level information**.

Example:

```text
PUBLIC user  ✗  Read TOP SECRET file
```

A normal employee cannot read a secret military document.

**Remember: No Read Up.**


## No Write Down

A user with a **higher security level cannot write information to a lower-level location**.

Example:

```text
TOP SECRET user  ✗  Write to PUBLIC file
```

Why?

Because secret information could leak to lower-level users.

**Remember: No Write Down.**

## Easy Rule

Bell-LaPadula:

> **Read Down, Write Up**

Example:

```text
TOP SECRET
     ↑
   Write
     ↑
   SECRET
     ↓
    Read
     ↓
   PUBLIC
```

### Main Goal

**Protect Confidentiality.**

# 2. Biba Model

The **Biba Model** focuses on **Integrity**.

**Integrity means protecting data from unauthorized or incorrect modification.**

Biba is almost the **opposite of Bell-LaPadula**.

## No Read Down

A user or process with **high integrity should not read data from a lower-integrity source**.

Example:

A trusted company system should not accept information from an untrusted website.

```text
Trusted System  ✗  Read Untrusted Data
```

The untrusted data could contain false or malicious information.

**Remember: No Read Down.**


## No Write Up

A lower-integrity user or process cannot modify higher-integrity data.

Example:

```text
Untrusted User  ✗  Modify Critical Database
```

This protects important information from being changed by untrusted users.

**Remember: No Write Up.**


## Easy Rule

Biba:

> **Read Up, Write Down**

### Main Goal

**Protect Integrity.**



# Bell-LaPadula vs Biba

| Model             | Read Rule    | Write Rule    | Protects        |
| ----------------- | ------------ | ------------- | --------------- |
| **Bell-LaPadula** | No Read Up   | No Write Down | Confidentiality |
| **Biba**          | No Read Down | No Write Up   | Integrity       |

### Easy Memory Trick

```text
Bell-LaPadula = Secrets should not LEAK

Biba = Data should not be CORRUPTED
```

# 3. Clark-Wilson Model

The **Clark-Wilson Model** also focuses on **Integrity**.

Its idea is simple:

> **Users should not directly modify important data. They must use authorized programs or procedures.**

### Example

Think about a banking system.

You should not directly open the bank database and change:

```text
Balance = 1000

to

Balance = 100000
```

Instead, you must use an authorized banking application.

```text
User
  ↓
Bank Application
  ↓
Validation
  ↓
Database Updated
```

This helps maintain data integrity.

# Important Clark-Wilson Terms

| Term    | Simple Meaning            |
| ------- | ------------------------- |
| **CDI** | Important protected data  |
| **UDI** | Untrusted or normal input |
| **TP**  | Authorized operation      |
| **IVP** | Checks data integrity     |

### CDI — Constrained Data Item

Data whose integrity must be protected.

Example:

```text
Bank Account Balance
```

### UDI — Unconstrained Data Item

Data that is not yet trusted or validated.

Example:

```text
User Input
```

### TP — Transformation Procedure

An authorized process that modifies protected data.

Example:

```text
Transfer Money Function
```

### IVP — Integrity Verification Procedure

Checks whether the protected data is correct and valid.

Example:

```text
Check whether account balances are valid
```

# Quick Revision

| Model             | Remember                                                             |
| ----------------- | -------------------------------------------------------------------- |
| **Bell-LaPadula** | Confidentiality → No Read Up, No Write Down                          |
| **Biba**          | Integrity → No Read Down, No Write Up                                |
| **Clark-Wilson**  | Integrity → Modify important data only through authorized procedures |

--------------

# Defence-in-Depth

**Defence-in-Depth** means using **multiple layers of security** to protect a system.

It is also called **Multi-Level Security**.

The main idea is:

> **Never depend on only one security control.**

If one security layer fails, another layer can still protect the system.

### Simple Example

Imagine you have expensive items in a drawer.

Instead of using only a **drawer lock**, you use multiple security layers:

```text
Building Gate
      ↓
Security Camera
      ↓
Apartment Door Lock
      ↓
Room Lock
      ↓
Drawer Lock
      ↓
Valuable Items
```

If a thief bypasses the **building gate**, they still need to bypass the **apartment door**.

If they bypass the apartment door, they still face the **room lock and drawer lock**.

The same concept is used in cybersecurity.

```text
Firewall
   ↓
IDS / IPS
   ↓
Antivirus / EDR
   ↓
Access Control
   ↓
Encryption
   ↓
Important Data
```

### Why is Defence-in-Depth Important?

Multiple security layers can:

* Stop many attacks.
* Slow down attackers.
* Detect suspicious activity.
* Reduce the damage if one security control fails.

--------------

# ISO/IEC 19249 Security Principles

**ISO/IEC 19249** provides security principles for designing secure systems, products, and applications.

It contains:

* **5 Architectural Principles**
* **5 Design Principles**

# 5 Architectural Principles

| Principle             | Simple Meaning                                  |
| --------------------- | ----------------------------------------------- |
| **Domain Separation** | Separate components based on security level.    |
| **Layering**          | Use multiple layers of security.                |
| **Encapsulation**     | Hide internal data and allow controlled access. |
| **Redundancy**        | Keep backup components to maintain operation.   |
| **Virtualization**    | Isolate systems using virtual environments.     |

### 1. Domain Separation

Divide the system into separate **security domains**.

Each domain has different permissions and security levels.

Example:

```text
Ring 0 → OS Kernel → Highest Privilege
Ring 3 → User Applications → Lowest Privilege
```

This prevents normal applications from directly accessing critical kernel resources.

**Remember:** Domain Separation = **Separate by privilege/security level**.

### 2. Layering

Build the system using multiple layers.

Each layer performs a specific function and can apply its own security controls.

Example: the **OSI Model** has seven layers, and each layer provides services to the layer above it.

Layering is related to **Defence-in-Depth**.

**Remember:** Layering = **Multiple security levels/layers**.

### 3. Encapsulation

Hide internal data and prevent users from modifying it directly.

Instead, provide controlled methods to access or change the data.

Example:

Instead of directly changing:

```text
seconds = 100000
```

Use:

```text
increment()
```

The method controls how the value changes and prevents invalid data.

Another example is using an **API** to access a database instead of allowing an application to directly manipulate the database.

**Remember:** Encapsulation = **Hide internal data and provide controlled access**.

### 4. Redundancy

Use backup components so the system continues working if one component fails.

Example:

```text
Power Supply 1 fails
        ↓
Power Supply 2 continues working
```

Another example is **RAID 5**. If one disk fails, the remaining disks can keep the data available.

Redundancy helps protect:

* **Availability**
* **Integrity**

**Remember:** Redundancy = **Backup components**.

### 5. Virtualization

Virtualization allows multiple operating systems to share the same physical hardware while remaining separated.

Example:

```text
Physical Server
      ↓
Hypervisor
      ↓
VM 1   VM 2   VM 3
```

Virtualization provides **isolation (sandboxing)**.

For example, malware can be analyzed inside a virtual machine without directly affecting the main system.

**Remember:** Virtualization = **Isolated virtual environments**.


# 5 Design Principles


| Number | Design Principle                           |
| ------ | ------------------------------------------ |
| **1**  | Least Privilege                            |
| **2**  | Attack Surface Minimisation                |
| **3**  | Centralized Parameter Validation           |
| **4**  | Centralized General Security Services      |
| **5**  | Preparing for Error and Exception Handling |

### 1. Least Privilege

Give users **only the minimum permissions required to perform their job**.

Example:

If a user only needs to read a document:

```text
Read → Allowed
Write → Not Allowed
```

Do not give unnecessary permissions.

**Remember:** Least Privilege = **Minimum required permission**.

### 2. Attack Surface Minimisation

Reduce the number of possible ways an attacker can attack a system.

Example:

If a Linux service is not required:

```bash
Disable the service
```

Fewer running services mean fewer possible vulnerabilities.

**Remember:** Attack Surface Minimisation = **Remove or disable unnecessary things**.

### 3. Centralized Parameter Validation

User input must be checked before the system processes it.

Example:

```text
User Input
    ↓
Validation
    ↓
Application
```

Instead of different parts of the application validating input differently, validation should be handled in a **centralized location or library**.

This helps prevent vulnerabilities such as:

* SQL Injection
* Remote Code Execution
* Denial of Service

**Remember:** Centralized Parameter Validation = **Validate all inputs in one central place**.

### 4. Centralized General Security Services

Security services should be managed from a centralized location.

Example:

```text
Application 1 ─┐
Application 2 ─┼──→ Central Authentication Server
Application 3 ─┘
```

Instead of every application creating its own authentication system, they use one centralized authentication service.

**Remember:** Centralized Security Services = **One central security service**.

### 5. Preparing for Error and Exception Handling

Systems should be designed to handle errors safely.

Example: if a firewall crashes, it should:

```text
Block All Traffic
```

instead of:

```text
Allow All Traffic
```

This is called **Fail Safe**.

Error messages should also not expose sensitive information such as:

* Passwords
* Database details
* Memory contents
* Internal system information

**Remember:** Error Handling = **Fail safely and don't leak sensitive information**.

----------

# Trust Security Principles

There are **two important security principles related to trust**:

| Principle            | Simple Meaning                                               |
| -------------------- | ------------------------------------------------------------ |
| **Trust but Verify** | Trust the user/system, but still monitor and check activity. |
| **Zero Trust**       | Never trust automatically; always verify.                    |


# 1. Trust but Verify

**Trust but Verify** means:

> **We trust an entity, but we still check its activities.**

An **entity** can be a:

* User
* Computer
* Server
* Application

### Example

A company trusts its employee.

But the company still:

* Records login activity.
* Collects logs.
* Monitors network traffic.
* Detects suspicious actions.

```text
Trusted User
     ↓
Activity Logged
     ↓
Security Monitoring
     ↓
Verify Behaviour
```

Because manually checking every action is difficult, automated security tools are used.

Examples:

* Proxy
* IDS (Intrusion Detection System)
* IPS (Intrusion Prevention System)

**Remember:**

> **Trust but Verify = Trust + Monitor**


# 2. Zero Trust

**Zero Trust** treats trust as a possible security risk.

The main idea is:

> **Never Trust, Always Verify**

A user or device is **not automatically trusted** because it is:

* Inside the company network.
* Using a company laptop.
* Connected from the office.

Every user and device must be **authenticated and authorized** before accessing a resource.

### Example

```text
User Requests File
        ↓
Verify Identity
        ↓
Check Permission
        ↓
Allow / Deny Access
```

Even if the user is already inside the company network, their access is still checked.

### Why is Zero Trust Important?

Zero Trust helps protect against:

* Insider threats.
* Stolen user accounts.
* Compromised devices.
* Attackers inside the network.

If an attacker compromises one system, Zero Trust can help **limit the attack from spreading to other systems**.

# Microsegmentation

**Microsegmentation** is one way to implement Zero Trust.

It divides a network into **very small isolated segments**.

A segment can even contain **only one computer or host**.

```text
Host A
  │
Authentication + Access Check
  │
Host B
  │
Authentication + Access Check
  │
Host C
```

Communication between segments may require:

* Authentication.
* Authorization.
* ACL (Access Control List) checks.
* Other security checks.

This makes it harder for an attacker to move from one system to another.

**Remember:**

> **Microsegmentation = Divide the network into small isolated security zones.**

# Quick Revision

| Concept               | Remember                                    |
| --------------------- | ------------------------------------------- |
| **Trust but Verify**  | Trust, but monitor and check                |
| **Zero Trust**        | Never trust, always verify                  |
| **Microsegmentation** | Divide network into small isolated segments |

### Easy Memory

**Trust but Verify:** `I trust you, but I will check.`

**Zero Trust:** `I don't trust automatically. Prove who you are every time.`

**Microsegmentation:** `Break the network into small protected parts.`

--------------

# Vulnerability, Threat, and Risk

These **three terms are different** and very important in cybersecurity.

| Term              | Simple Meaning                            |
| ----------------- | ----------------------------------------- |
| **Vulnerability** | A weakness                                |
| **Threat**        | A potential danger                        |
| **Risk**          | Chance of exploitation + resulting impact |

### Vulnerability

A **vulnerability is a weakness** in a system.

Example: A database has an unpatched security flaw.

> **Vulnerability = Weakness**

### Threat

A **threat is a potential danger that can exploit a vulnerability**.

Example: An attacker has working exploit code for the database vulnerability.

> **Threat = Potential danger**

### Risk

**Risk is the likelihood that the threat will exploit the vulnerability and the impact it will cause.**

Simple idea:

> **Risk = Likelihood + Impact**

Example: If the vulnerable hospital database is exploited, patient medical records may be stolen. We consider **how likely the attack is and how much damage it could cause**.

### Easy Example

Imagine a showroom with glass windows.

| Concept           | Example                                         |
| ----------------- | ----------------------------------------------- |
| **Vulnerability** | Glass is easy to break                          |
| **Threat**        | A thief may break the glass                     |
| **Risk**          | Chance of theft and the financial damage caused |

### Quick Revision

> **Vulnerability = Weakness**

> **Threat = Danger**

> **Risk = How likely the danger is to exploit the weakness + how much damage it causes**

**Easy flow:** `Vulnerability → Threat exploits it → Risk to the business`

