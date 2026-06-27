# Security Operations Center (SOC)

Technology has made our lives easier and more efficient. However, as organizations increasingly store important information digitally, protecting that information has become a major challenge.

Instead of stealing physical documents, attackers now target **digital data**, such as:

* Customer information
* Employee records
* Financial data
* Passwords and credentials
* Business secrets

This sensitive information is called **secrets** because it must remain confidential.

# Why Is Cybersecurity Important?

Organizations store large amounts of confidential data in their:

* Computers
* Servers
* Databases
* Cloud services
* Networks

If an attacker gains unauthorized access, they can:

* Steal data
* Delete important files
* Modify information
* Disrupt business operations

Any of these actions can cause:

* Financial loss
* Reputation damage
* Legal issues
* Service downtime

# The Problem

Cyber threats continue to grow every day.

Attackers constantly:

* Discover new vulnerabilities.
* Develop new attack techniques.
* Exploit systems before organizations can fix them.

Because of this, simply installing antivirus software or a firewall is **not enough**.

Organizations need people who continuously monitor their systems for suspicious activity.

# What is a SOC?

**SOC** stands for **Security Operations Center**.

A **Security Operations Center (SOC)** is a dedicated team of cybersecurity professionals responsible for monitoring, detecting, analyzing, and responding to security threats within an organization.

The SOC's main goal is to identify attacks as early as possible and minimize damage.


# Why Do Organizations Need a SOC?

Instead of waiting until an attack causes damage, a SOC continuously watches the organization's environment for suspicious activities.

The SOC helps organizations:

* Detect cyber attacks quickly.
* Investigate suspicious events.
* Respond to security incidents.
* Reduce the impact of attacks.
* Protect important business data.


# What Does a SOC Monitor?

A SOC monitors many parts of an organization's infrastructure, including:

* Computers
* Servers
* Networks
* Firewalls
* Cloud services
* User activity
* Security logs
* Applications

Everything that generates security-related information can be monitored.

# SOC Works 24/7

Cyber attacks can happen at any time.

For this reason, most SOC teams operate:

* **24 hours a day**
* **7 days a week**
* **365 days a year**

Many organizations use rotating shifts so that security analysts are always available.

-----------
# Detection and Response in a SOC

The primary responsibility of a **Security Operations Center (SOC)** is to **Detect** security threats and **Respond** to them before they cause significant damage.

To achieve this, the SOC uses various security tools that collect logs and monitor all systems from a **centralized location**.

Instead of checking every computer individually, analysts can monitor the entire organization's network from one place.

Continuous monitoring allows the SOC to quickly identify suspicious activities and respond immediately.

 

# Detection

Detection is the process of identifying anything that could threaten the organization's security.

The SOC focuses on detecting the following:

 

## 1. Detect Vulnerabilities

A **vulnerability** is a weakness in software, hardware, or a system that attackers can exploit.

Examples include:

* Outdated operating systems
* Unpatched software
* Software bugs
* Misconfigured servers

### Example

Suppose Microsoft releases a security update for Windows because a serious vulnerability has been discovered.

If an organization's computers have **not installed the update**, attackers may exploit that vulnerability.

The SOC identifies these vulnerable systems and reports them so they can be patched.

> **Note:** Although patch management is usually handled by the IT or Vulnerability Management team, the SOC monitors these vulnerabilities because they directly affect the organization's security.

 

## 2. Detect Unauthorized Activity

Unauthorized activity occurs when someone performs actions they are **not allowed** to perform.

This may happen when:

* An attacker steals an employee's username and password.
* Someone logs in using stolen credentials.
* A compromised account accesses sensitive resources.

### Example

An employee normally logs in from **India** every day.

Suddenly, the same account logs in from another country within a short period.

This unusual activity may indicate that the account has been compromised.

The SOC investigates the login before the attacker causes further damage.

  

## 3. Detect Policy Violations

Organizations create **security policies** to define acceptable behavior and protect company resources.

A **policy violation** occurs when someone breaks these rules.

Examples include:

* Downloading pirated software.
* Sending confidential company files through unsecured channels.
* Installing unauthorized applications.
* Using personal USB drives on company computers.

The SOC monitors these activities and reports violations.
 

## 4. Detect Intrusions

An **intrusion** is any unauthorized access to a system or network.

Examples include:

* An attacker exploiting a vulnerable website.
* Malware infecting a user's computer.
* A hacker gaining access to an internal server.

The SOC continuously monitors systems to detect these attacks as early as possible.

 

# Response

Detection alone is not enough.

Once a security incident is detected, the SOC must respond quickly.

The goal is to reduce the damage and restore normal operations.

The SOC supports the **Incident Response (IR) Team** by helping them investigate and contain the attack.

Typical response activities include:

* Identifying the affected systems.
* Containing the attack.
* Removing malicious files or malware.
* Recovering affected systems.
* Performing **Root Cause Analysis (RCA)** to determine how the incident occurred and how to prevent it in the future.

 

# The Three Pillars of a SOC

A successful SOC depends on three essential components:

* **People**
* **Process**
* **Technology**

These three pillars work together to build a mature and effective SOC.

 

## 1. People

People are the cybersecurity professionals who monitor, investigate, and respond to security incidents.

Examples include:

* SOC Analysts
* Incident Responders
* Threat Hunters
* Security Engineers

Without skilled people, security tools cannot effectively protect an organization.

 

## 2. Process

Processes are the documented procedures and workflows that guide how security incidents are handled.

Examples include:

* Incident Response procedures.
* Alert investigation steps.
* Escalation procedures.
* Recovery procedures.

Well-defined processes ensure that every incident is handled consistently and efficiently.

 

## 3. Technology

Technology refers to the security tools used by the SOC.

Examples include:

* SIEM (Security Information and Event Management)
* EDR (Endpoint Detection and Response)
* IDS/IPS (Intrusion Detection/Prevention Systems)
* Firewalls
* Antivirus software

These tools collect security data, detect suspicious activities, and assist analysts during investigations.

 

# Why Are All Three Pillars Important?

A SOC becomes effective only when **People, Processes, and Technology** work together.

For example:

* **People** analyze alerts and make decisions.
* **Processes** define how incidents should be handled.
* **Technology** detects threats and provides the necessary information.

If any one of these pillars is missing, the SOC becomes less effective.

------------

# People in a Security Operations Center (SOC)

Even though modern security tools can automatically detect suspicious activities, **people remain the most important part of a SOC**.

Security tools can generate thousands of alerts every day, but **not every alert is a real attack**.

Human analysts are needed to investigate these alerts, identify genuine threats, and respond appropriately.


# Why Are People Important?

Imagine a city's fire department.

Every fire alarm is connected to a central monitoring system.

One day, hundreds of alarms go off at the same time.

When firefighters arrive, they discover that many alarms were triggered by cooking smoke instead of actual fires.

If they treated every alert as a real emergency, they would waste:

* Time
* Resources
* Personnel

A SOC faces the same problem.

Security tools generate many alerts, but some are **false positives** (alerts that appear suspicious but are actually harmless).

SOC analysts determine which alerts are real threats and which can be safely ignored.


# What is the SOC Team?

The **SOC Team** is a group of cybersecurity professionals responsible for monitoring, investigating, and responding to security incidents.

Each member has a specific role.


# SOC Analyst - Level 1 (L1)

A **Level 1 SOC Analyst** is the **first responder** to security alerts.

Whenever a security tool detects suspicious activity, the alert is first reviewed by the Level 1 analyst.

### Responsibilities

* Monitor security alerts.
* Perform basic investigation (Alert Triage).
* Determine whether an alert is suspicious.
* Escalate serious alerts to Level 2.
* Document and report incidents.

### Example

An alert reports:

```text
Multiple failed login attempts.
```

The Level 1 analyst checks:

* Source IP address.
* Username.
* Login time.
* Whether the activity looks suspicious.

If it appears to be a real attack, the alert is escalated.


# What is Alert Triage?

**Alert Triage** is the process of quickly reviewing an alert to determine:

* Is it a real threat?
* Is it a false positive?
* Does it require further investigation?

Think of it like a hospital emergency room.

Doctors first decide which patients need immediate treatment.

Similarly, SOC analysts prioritize security alerts.


# SOC Analyst - Level 2 (L2)

Some alerts require more investigation than Level 1 can provide.

These alerts are handed over to **Level 2 Analysts**.

### Responsibilities

* Perform deeper investigations.
* Analyze multiple log sources.
* Correlate security events.
* Confirm whether an attack has occurred.
* Escalate serious incidents to Level 3.

### Example

Suppose an employee account logs in from another country.

Level 2 investigates:

* VPN logs
* Firewall logs
* Authentication logs
* Endpoint activity

They combine information from multiple sources before making a decision.

This process is called **Correlation**.


# What is Correlation?

**Correlation** means combining information from multiple security logs to understand the complete picture of an incident.

Instead of analyzing one log, analysts compare several logs together.

Example:

* Firewall log
* VPN log
* Windows Event Log
* EDR alert

Together, these logs provide a much clearer understanding of what happened.


# SOC Analyst - Level 3 (L3)

Level 3 Analysts are the most experienced analysts in the SOC.

They handle complex incidents and actively search for threats.

### Responsibilities

* Threat Hunting
* Incident Response
* Malware analysis
* Root Cause Analysis
* Support containment and recovery

They usually work on high-priority incidents.


# What is Threat Hunting?

Most SOC work is **reactive**.

The SOC waits for alerts.

Threat Hunting is different.

Instead of waiting, Level 3 analysts **proactively search for hidden attackers** inside the network before any alert is generated.


# Security Engineer

SOC analysts rely on many security tools.

Someone must install and maintain these tools.

That is the responsibility of the **Security Engineer**.

### Responsibilities

* Install security solutions.
* Configure SIEM.
* Configure EDR.
* Maintain IDS/IPS.
* Troubleshoot security tools.
* Ensure all security tools function correctly.

Without Security Engineers, analysts would not have the tools needed to detect threats.


# Detection Engineer

Security tools detect threats using **detection rules**.

A **Detection Engineer** creates and improves these rules.

### Responsibilities

* Write detection rules.
* Tune existing rules.
* Reduce false positives.
* Improve detection accuracy.

Example:

A Detection Engineer creates a rule that generates an alert whenever:

* More than 20 failed logins occur within one minute.


# SOC Manager

The **SOC Manager** leads the SOC team.

They ensure that the team operates effectively and follows proper procedures.

### Responsibilities

* Manage SOC operations.
* Assign tasks.
* Improve SOC processes.
* Monitor team performance.
* Coordinate with management.
* Report security status to the **Chief Information Security Officer (CISO)**.

# What is a CISO?

**CISO** stands for **Chief Information Security Officer**.

The CISO is the senior executive responsible for the organization's overall cybersecurity strategy.

The SOC Manager regularly reports to the CISO about:

* Current threats.
* Security incidents.
* SOC performance.
* Overall security posture.

# SOC Team Hierarchy

```text
CISO
   │
   ▼
SOC Manager
   │
   ├───────────────┐
   │               │
Security      Detection
Engineer       Engineer
   │
   ▼
SOC Analyst L3
   │
   ▼
SOC Analyst L2
   │
   ▼
SOC Analyst L1
```


# Do All Companies Have These Roles?

No.

The size of the SOC depends on the organization.

### Small Company

One person may perform multiple roles.

Example:

* SOC Analyst
* Security Engineer
* Detection Engineer

may all be the same person.

----------


# SOC Processes

In a SOC, every team member follows **defined processes** to ensure security incidents are handled consistently and efficiently.

These processes help analysts:

* Investigate alerts.
* Prioritize incidents.
* Report findings.
* Respond to attacks.
* Identify the root cause.

Some of the most important SOC processes are:

* Alert Triage
* Reporting
* Incident Response
* Digital Forensics


# 1. Alert Triage

**Alert Triage** is the **first step** after a security alert is generated.

Its purpose is to determine:

* Is the alert real?
* How serious is it?
* Does it require immediate action?

The first person to perform alert triage is usually the **Level 1 SOC Analyst**.


## Goal of Alert Triage

The main goal is to:

* Analyze the alert.
* Determine its severity.
* Prioritize it.
* Decide whether it should be escalated.

Not every alert is a cyber attack.

Some alerts are **False Positives** and do not require further action.


# The 5 Ws of Alert Triage

During triage, analysts answer five important questions known as the **5 Ws**.

| Question   | Purpose              |
| ---------- | -------------------- |
| **What?**  | What happened?       |
| **When?**  | When did it happen?  |
| **Where?** | Where did it happen? |
| **Who?**   | Who was involved?    |
| **Why?**   | Why did it happen?   |

These questions help analysts understand the incident quickly.


# Example Alert

Suppose a security tool generates this alert:

```text
Malware detected on Host: GEORGE-PC
```

The analyst begins answering the 5 Ws.


## What?

**What happened?**

Answer:

A malicious file was detected on one of the organization's computers.


## When?

**When did it happen?**

Answer:

The malware was detected at:

```text
13:20
June 5, 2024
```

Knowing the time helps analysts investigate related events.


## Where?

**Where did it happen?**

Answer:

The malicious file was found on:

```text
GEORGE-PC
```

The analyst now knows which computer is affected.


## Who?

**Who was involved?**

Answer:

The affected user is:

```text
George
```

The analyst may contact George for more information.


## Why?

**Why did it happen?**

After investigation, the analyst discovers:

* George downloaded software from a pirated website.
* The downloaded file contained malware.

This explains the root cause of the alert.


# Example Summary

| 5 W        | Example Answer                              |
| ---------- | ------------------------------------------- |
| **What?**  | Malware detected.                           |
| **When?**  | 13:20, June 5, 2024.                        |
| **Where?** | GEORGE-PC.                                  |
| **Who?**   | User George.                                |
| **Why?**   | Downloaded software from a pirated website. |


# 2. Reporting

After triage, the analyst prepares a **security report**.

If the alert is serious, it is **escalated** to higher-level analysts.


## What is Escalation?

**Escalation** means sending an incident to someone with greater expertise or authority.

For example:

```text
SOC Analyst L1
        │
        ▼
SOC Analyst L2
        │
        ▼
SOC Analyst L3
```

Each level handles more complex investigations.


## What Should a Report Include?

A good SOC report should contain:

* The **5 Ws**
* Description of the incident
* Severity level
* Investigation results
* Evidence (logs, screenshots, alerts)
* Recommended actions


## Why Are Screenshots Important?

Screenshots serve as **evidence**.

They help:

* Document the incident.
* Support investigations.
* Verify findings.
* Provide proof during audits.


# 3. Incident Response

Some incidents are highly critical.

Examples include:

* Ransomware attack
* Data breach
* Server compromise
* Active malware infection

In these cases, the **Incident Response (IR) Team** becomes involved.


## What is Incident Response?

**Incident Response** is the process of handling a security incident to minimize damage and restore normal operations.

Typical Incident Response activities include:

* Identify the incident.
* Contain the attack.
* Remove the threat.
* Recover affected systems.
* Prevent future incidents.


# Example

Suppose ransomware infects a company server.

The Incident Response team may:

* Disconnect the infected server.
* Remove the ransomware.
* Restore files from backups.
* Investigate how the ransomware entered.


# 4. Digital Forensics

Sometimes investigators need to understand **exactly what happened**.

This is called **Digital Forensics**.


## What is Digital Forensics?

Digital Forensics is the process of collecting and analyzing digital evidence to determine:

* How the attack happened.
* When it happened.
* What the attacker did.
* Which systems were affected.
* Who was responsible (when possible).


## Digital Evidence

Examples include:

* System logs
* Network logs
* Memory dumps
* Hard disk images
* Browser history
* Registry entries
* Malware files


## Root Cause Analysis (RCA)

One important goal of forensics is finding the **Root Cause**.

**Root Cause Analysis (RCA)** identifies the original reason the incident occurred.

Example:

The investigation finds that:

* The employee downloaded pirated software.
* The installer contained malware.
* The malware infected the system.

The **root cause** is:

```text
Downloading software from an untrusted website.
```

Finding the root cause helps prevent similar incidents in the future.


-----------

# Technology in a Security Operations Center (SOC)

Having skilled **People** and well-defined **Processes** is important, but they are not enough on their own.

A SOC also needs **Technology**—security tools that help analysts detect, investigate, and respond to cyber threats.

Without these tools, analysts would have to manually monitor every computer, server, and network device, which is nearly impossible in large organizations.

Technology helps by:

* Collecting security data.
* Monitoring the entire network.
* Detecting suspicious activities.
* Automating responses.
* Reducing manual work.
 

# Why is Technology Important?

A company may have:

* Hundreds or thousands of computers.
* Servers.
* Firewalls.
* Routers.
* Cloud services.
* Applications.

Monitoring each system individually would require enormous time and effort.

Security tools collect information from all these systems and display it in one central location, allowing analysts to monitor everything efficiently.

 
# Main Security Technologies Used in a SOC

Some of the most common security solutions are:

* SIEM
* EDR
* Firewall
* Antivirus
* EPP
* IDS/IPS
* XDR
* SOAR

 

# 1. SIEM (Security Information and Event Management)

**SIEM** is one of the most important tools used in almost every SOC.

Its main job is to **collect, analyze, and correlate security logs** from multiple devices.

> **Remember:** SIEM mainly provides **Detection**, not Response.

 

## What are Logs?

A **log** is a record of an event that happened on a system.

Examples:

* User login
* Failed login
* File deleted
* Program executed
* Firewall blocked traffic
* Malware detected

Every important event is recorded as a log.

 

## What are Log Sources?

A **Log Source** is any device or application that sends logs to the SIEM.

Examples include:

* Windows computers
* Linux servers
* Firewalls
* Routers
* Web servers
* Antivirus
* Active Directory
* Cloud services

The SIEM collects logs from all these sources into one centralized platform.

 

## How SIEM Works

```text
Windows Logs
        │
Firewall Logs
        │
Server Logs
        │
Cloud Logs
        │
        ▼
      SIEM
        │
Analyzes & Correlates Logs
        │
        ▼
Generates Security Alerts
```

 

## Detection Rules

A SIEM uses **Detection Rules**.

These are predefined conditions that identify suspicious activities.

### Example

Rule:

```text
If one user fails to log in
more than 20 times
within 1 minute

↓

Generate an Alert
```

Whenever this condition is met, the SIEM alerts the SOC team.

 

## What is Correlation?

**Correlation** means combining logs from multiple sources to understand what is happening.

Example:

Instead of looking only at:

* Firewall logs

The SIEM combines:

* Firewall logs
* Windows logs
* VPN logs
* Antivirus logs

This provides a much clearer picture of an attack.

 

## Modern SIEM Features

Modern SIEM platforms can also provide:

### User Behavior Analytics (UBA)

The SIEM learns what **normal user behavior** looks like.

If a user suddenly behaves differently, it generates an alert.

Example:

An employee normally logs in between **9 AM and 5 PM**.

Suddenly the same account logs in at **3 AM** from another country.

The SIEM identifies this as unusual behavior.

 

### Threat Intelligence

Modern SIEMs use **Threat Intelligence**.

Threat intelligence is information about known cyber threats.

Examples include:

* Malicious IP addresses
* Malware hashes
* Known attacker domains

The SIEM compares network activity with this intelligence and generates alerts if a match is found.

 
### Machine Learning

Modern SIEMs also use **Machine Learning (ML)**.

Instead of relying only on fixed rules, machine learning identifies unusual behavior automatically.

This helps detect attacks that traditional rules may miss.

---

# 2. EDR (Endpoint Detection and Response)

**EDR** stands for **Endpoint Detection and Response**.

Unlike SIEM, which collects logs from many devices, EDR focuses on individual endpoints.

An **Endpoint** is any device connected to the network.

Examples:

* Desktop
* Laptop
* Server

  

## What Does EDR Do?

EDR provides:

* Real-time monitoring.
* Historical activity.
* Threat detection.
* Automated response.

It allows analysts to investigate exactly what happened on a specific computer.
 

## Example

Suppose malware is detected on a laptop.

Using EDR, analysts can see:

* Which process started the malware.
* Which files were modified.
* Which network connections were made.
* Which user executed it.

If necessary, the analyst can isolate the infected computer with just a few clicks.

 

# SIEM vs EDR

| SIEM                                  | EDR                                            |
| ------------------------------------- | ---------------------------------------------- |
| Collects logs from many devices.      | Focuses on individual endpoints.               |
| Mainly provides detection.            | Provides both detection and response.          |
| Correlates events across the network. | Investigates activity on one device in detail. |
| Centralized monitoring.               | Endpoint-level monitoring.                     |

 

# 3. Firewall

A **Firewall** protects a network by controlling incoming and outgoing network traffic.

It acts as a barrier between:

* Internal Network
* External Network (Internet)

 

## How Does a Firewall Work?

Every network connection is checked against security rules.

If the traffic is allowed:

 It passes.

If it is not allowed:

 It is blocked.

 

## Example

Suppose an attacker tries to connect to a blocked port.

The firewall:

* Detects the connection.
* Blocks it.
* Records the event.
* Sends a log to the SIEM.


# Other Security Technologies

Besides SIEM, EDR, and Firewalls, organizations use many other security tools.


## Antivirus

Detects and removes known malware.


## EPP (Endpoint Protection Platform)

Provides endpoint protection by preventing malware and other threats.


## IDS (Intrusion Detection System)

Monitors network traffic and alerts when suspicious activity is detected.


## IPS (Intrusion Prevention System)

Detects malicious traffic and automatically blocks it.


## XDR (Extended Detection and Response)

Combines security information from multiple sources such as:

* Endpoints
* Email
* Network
* Cloud

to improve threat detection and response.


## SOAR (Security Orchestration, Automation and Response)

Automates repetitive SOC tasks.

Examples:

* Automatically create tickets.
* Block malicious IP addresses.
* Isolate infected computers.
* Notify analysts.

This reduces manual work for the SOC team.



# Choosing Security Technologies

Not every organization uses every security tool.

The choice depends on:

* Organization size.
* Budget.
* Type of business.
* Number of users.
* Threat landscape.
* Available security staff.

Larger organizations usually deploy more advanced security solutions.
----------


