# Introduction to Intrusion Detection System (IDS)

A **Firewall** protects a network by checking traffic **before** it enters or leaves the network.

However, attackers may sometimes bypass the firewall using legitimate-looking traffic.

Once inside the network, they may perform malicious activities.

To detect these activities, organizations use an **Intrusion Detection System (IDS)**.

# Why Do We Need an IDS?

A firewall cannot detect everything.

Example:

* An attacker sends a normal-looking request.
* The firewall allows it.
* After entering the network, the attacker starts scanning systems or stealing data.

The firewall has already allowed the connection.

Now we need another security system that monitors activities **inside the network**.

This is the job of an **IDS**.

# What is an IDS?

An **Intrusion Detection System (IDS)** is a security solution that continuously monitors network or system activities to detect suspicious or malicious behavior.

When it detects an attack, it **generates an alert** for security administrators.

> **Important:** An IDS **only detects and alerts**. It **does not block** the attack.

# Building Security Analogy

Imagine a company's office building.

### Firewall = Security Guard

* Checks everyone entering the building.
* Allows or blocks entry.

### IDS = CCTV Cameras

* Monitors activities inside the building.
* Detects suspicious behavior.
* Alerts the security team.

```text id="e9p4eu"
Internet
     │
     ▼
 Firewall (Security Guard)
     │
     ▼
 Company Network
     │
     ▼
 IDS (CCTV Camera)
     │
     ▼
 Alert Security Team
```

-----------------
# Types of IDS

IDS (Intrusion Detection System) can be classified based on:

1. **Deployment Mode** (Where it is installed)
2. **Detection Mode** (How it detects attacks)


# 1. Deployment Modes

## A. Host Intrusion Detection System (HIDS)

A **Host Intrusion Detection System (HIDS)** is installed on an **individual computer (host)**.

It monitors only that specific system for suspicious activities.

### What HIDS Monitors

* File changes
* Running processes
* System logs
* User activities
* Registry changes (Windows)
* Login attempts


### Advantages

* Detailed visibility of one host.
* Detects attacks directly on the system.
* Monitors system files and processes.


### Disadvantages

* Must be installed on every computer.
* Difficult to manage in large organizations.
* Uses system resources (CPU, RAM).


### Example

A hacker modifies a system file on a Windows computer.

↓

The HIDS installed on that computer detects the file modification and generates an alert.


# B. Network Intrusion Detection System (NIDS)

A **Network Intrusion Detection System (NIDS)** monitors the **entire network** instead of a single computer.

It analyzes network traffic passing through the network to detect suspicious activities.


### What NIDS Monitors

* Network packets
* Network connections
* Protocols
* Incoming traffic
* Outgoing traffic


### Advantages

* Monitors the whole network.
* Centralized monitoring.
* One IDS can protect many devices.


### Disadvantages

* Cannot see detailed host activities.
* May miss attacks that occur only inside a single host.


### Example

A hacker performs a **port scan** on multiple servers.

↓

NIDS detects the unusual scanning activity and alerts the security team.


# HIDS vs NIDS

| HIDS                                | NIDS                             |
| ----------------------------------- | -------------------------------- |
| Installed on a single host.         | Installed on the network.        |
| Monitors one computer.              | Monitors the entire network.     |
| Detects host-level attacks.         | Detects network-based attacks.   |
| Detailed host visibility.           | Centralized network visibility.  |
| Harder to manage in large networks. | Easier to manage large networks. |


# 2. Detection Modes

IDS can detect attacks in different ways.

There are three common detection methods:

1. Signature-Based IDS
2. Anomaly-Based IDS
3. Hybrid IDS


# A. Signature-Based IDS

A **Signature-Based IDS** detects attacks by comparing network traffic with a database of **known attack signatures**.

A **signature** is a unique pattern of a known attack.

If traffic matches a stored signature, the IDS generates an alert.


### How It Works

```text
Incoming Traffic
       │
       ▼
Compare with Signature Database
       │
 ┌─────┴─────┐
 │           │
Match      No Match
 │           │
 ▼           ▼
Alert     Ignore
```


### Advantages

* Fast detection.
* Very accurate for known attacks.
* Low false positives.


### Disadvantages

* Cannot detect unknown attacks.
* Cannot detect Zero-Day attacks.
* Requires regular signature updates.


### Example

An attacker launches a known SQL Injection attack.

↓

The attack matches an existing signature.

↓

IDS generates an alert.


# What is a Zero-Day Attack?

A **Zero-Day Attack** exploits a newly discovered vulnerability **before security vendors create a fix or signature**.

Since no signature exists yet, Signature-Based IDS cannot detect it.



# B. Anomaly-Based IDS

An **Anomaly-Based IDS** first learns what **normal system or network behavior** looks like.

This normal behavior is called the **Baseline**.

If current activity differs significantly from the baseline, the IDS generates an alert.


# What is a Baseline?

A **Baseline** is the normal behavior of a system or network.

Examples:

* Normal login times
* Normal network traffic
* Normal CPU usage
* Normal file access

The IDS uses this baseline to identify abnormal activities.


### How It Works

```text
Learn Normal Behavior
         │
         ▼
     Create Baseline
         │
         ▼
 Compare Current Activity
         │
 ┌───────┴────────┐
 │                │
Normal         Abnormal
 │                │
 ▼                ▼
Ignore         Alert
```


### Advantages

* Detects unknown attacks.
* Detects Zero-Day attacks.
* Detects insider threats.


### Disadvantages

* More false positives.
* Higher processing overhead.
* Requires training time.


### Example

Normally:

A user downloads **50 MB/day**.

Today:

The same user downloads **30 GB**.

↓

The IDS detects abnormal behavior and raises an alert.


# What are False Positives?

A **False Positive** occurs when the IDS incorrectly identifies a **normal activity** as malicious.

Example:

A system administrator transfers a large backup file.

↓

IDS thinks it is data theft.

↓

False Positive.


# Fine-Tuning

**Fine-Tuning** means adjusting the IDS configuration to reduce false positives.

This involves teaching the IDS what activities are actually normal.


# C. Hybrid IDS

A **Hybrid IDS** combines both:

* Signature-Based Detection
* Anomaly-Based Detection

It uses whichever method is appropriate.

### How It Works

Known attack

↓

Use Signature Detection

Unknown attack

↓

Use Anomaly Detection


### Advantages

* Detects both known and unknown attacks.
* Better overall security.
* Reduces weaknesses of each individual method.


### Disadvantages

* More complex.
* Higher resource usage.
* More expensive.


# Detection Method Comparison

| Detection Method    | Detects Known Attacks | Detects Unknown Attacks | Detects Zero-Day Attacks |
| ------------------- | :-------------------: | :---------------------: | :----------------------: |
| **Signature-Based** |           ✅           |            ❌            |             ❌            |
| **Anomaly-Based**   |           ✅           |            ✅            |             ✅            |
| **Hybrid**          |           ✅           |            ✅            |             ✅            |


# IDS Comparison

| Type     | Installed On    | Monitors       |
| -------- | --------------- | -------------- |
| **HIDS** | Individual Host | One computer   |
| **NIDS** | Network         | Entire network |


# Which IDS Should You Choose?

| Situation                            | Best Choice         |
| ------------------------------------ | ------------------- |
| Small environment with known threats | Signature-Based IDS |
| Detecting new and unknown attacks    | Anomaly-Based IDS   |
| Enterprise environments              | Hybrid IDS          |
| Monitoring one server                | HIDS                |
| Monitoring an entire network         | NIDS                |

--------

# Snort IDS

**Snort** is one of the most popular **open-source Intrusion Detection Systems (IDS)**.

It was developed in **1998** and is widely used to monitor network traffic and detect malicious activities.

Snort detects attacks using **rules** that contain known attack patterns (signatures).


# Features of Snort

* Open-source IDS.
* Monitors network traffic.
* Detects known attacks.
* Supports custom detection rules.
* Uses signature-based detection.
* Supports anomaly-based detection.
* Generates alerts when suspicious traffic is detected.


# How Snort Works

```text
Network Traffic
       │
       ▼
     Snort
       │
       ▼
Compare with Rules
       │
 ┌─────┴─────┐
 │           │
Match     No Match
 │           │
 ▼           ▼
Alert     Ignore
```

# Snort Rules

Snort detects attacks using **Rule Files**.

A **rule** contains the pattern of a malicious activity.

Whenever network traffic matches a rule, Snort generates an alert.


## Built-in Rules

Snort comes with many **pre-installed rule files**.

These rules already contain signatures for many common attacks.

Examples include:

* Port Scanning
* SQL Injection
* Malware Traffic
* Buffer Overflow
* Web Attacks

Advantages:

* Ready to use.
* Detects many known attacks.
* Saves configuration time.


## Custom Rules

Sometimes an organization wants to detect specific traffic that isn't covered by the default rules.

In this case, administrators can create **Custom Rules**.

Example:

Detect whenever someone tries to access:

```text
/admin
```

or

Detect traffic coming from a suspicious IP address.


## Disabling Rules

Not every built-in rule is useful.

Sometimes a rule generates too many **False Positives**.

In that case, administrators can:

* Disable unnecessary rules.
* Enable only required rules.
* Create better custom rules.


# Modes of Snort

Snort can work in **three different modes**:

1. Packet Sniffer Mode
2. Packet Logging Mode
3. Network Intrusion Detection System (NIDS) Mode

# 1. Packet Sniffer Mode

This mode simply **captures and displays network packets**.

It does **not analyze** the traffic.

It is mainly used for:

* Network monitoring
* Troubleshooting
* Viewing traffic

### Purpose

Read network packets only.


### Example

The network is slow.

The administrator wants to see what traffic is flowing through the network.

They start Snort in **Packet Sniffer Mode** to view the packets.

### Characteristics

* Displays packets.
* No detection.
* No alerts.
* Useful for troubleshooting.


# 2. Packet Logging Mode

This mode captures network traffic and **stores it in a file**.

The traffic is saved in **PCAP (Packet Capture)** format.

A PCAP file contains all captured network packets.

These files can later be analyzed using tools like:

* Wireshark
* Snort
* Tcpdump


### Purpose

Capture and save network traffic.


### Example

A company experienced a cyber attack yesterday.

The security team wants to investigate it.

They analyze the previously saved **PCAP** files to find the root cause.

### Characteristics

* Captures traffic.
* Saves packets.
* Useful for forensic investigations.
* Supports later analysis.


# What is PCAP?

**PCAP (Packet Capture)** is the standard file format used to store captured network traffic.

It contains:

* Source IP
* Destination IP
* Protocol
* Ports
* Packet contents


# 3. Network Intrusion Detection System (NIDS) Mode

This is **Snort's primary operating mode**.

In this mode, Snort continuously monitors network traffic.

Every packet is compared against Snort's rule files.

If a rule matches,

↓

Snort generates an alert.


### Purpose

Detect network attacks in real time.


### Example

An attacker launches a Port Scan.

↓

Snort matches the traffic with its Port Scan rule.

↓

An alert is generated.


### Characteristics

* Real-time monitoring.
* Uses rule files.
* Detects attacks.
* Generates alerts.


# Snort Modes Comparison

| Mode               | What It Does                 | Generates Alerts | Saves Traffic |
| ------------------ | ---------------------------- | ---------------- | ------------- |
| **Packet Sniffer** | Displays packets             | ❌                | ❌             |
| **Packet Logging** | Captures and saves packets   | ❌                | ✅             |
| **NIDS Mode**      | Detects attacks in real time | ✅                | Optional      |


# When to Use Each Mode

| Situation                          | Best Mode           |
| ---------------------------------- | ------------------- |
| View live network traffic          | Packet Sniffer Mode |
| Save traffic for forensic analysis | Packet Logging Mode |
| Detect attacks in real time        | NIDS Mode           |


# Snort Workflow

```text
Network Traffic
       │
       ▼
     Snort
       │
       ▼
Rule Matching
       │
 ┌─────┴─────┐
 │           │
Match     No Match
 │           │
 ▼           ▼
Alert     Ignore
```

---------

# Snort Configuration and Rule Creation

Before using Snort, it must know:

* Which **network interface** to monitor.
* Which **network range** belongs to your organization.

During installation, these settings are configured.


# Promiscuous Mode

Normally, a network interface only receives packets sent to **its own computer**.

If you want Snort to monitor the **entire network**, you must enable **Promiscuous Mode**.

## Normal Mode

Receives only packets meant for your computer.

```text
Network
   │
   ▼
Your Computer
   ▲
Only receives its own traffic
```


## Promiscuous Mode

Receives **all packets** passing through the network.

```text
Network
   │
   ▼
Snort
   ▲
Receives all network traffic
```

This allows Snort to detect attacks across the network.


# Snort Directory

Snort stores its configuration files and rules inside:

```bash
/etc/snort
```

View the directory:

```bash
ls /etc/snort
```

Example:

```text
classification.config
rules/
snort.conf
snort.lua
threshold.conf
reference.config
```


# Important Files

| File/Folder     | Purpose                                    |
| --------------- | ------------------------------------------ |
| **snort.lua**   | Main configuration file (Snort 3).         |
| **rules/**      | Stores all Snort rule files.               |
| **local.rules** | Custom rules created by the administrator. |
| **snort.conf**  | Older configuration file (Snort 2).        |


# snort.lua

This is the **main configuration file** in Snort 3.

It defines:

* Network range (`HOME_NET`)
* Enabled rule files
* Detection settings
* Logging configuration

Whenever Snort starts, it loads this configuration.


# Snort Rule Format

A Snort rule has two parts:

1. **Rule Header**
2. **Rule Options (Metadata)**

Example:

```text
alert icmp any any -> $HOME_NET any (msg:"Ping Detected"; sid:10001; rev:1;)
```

# Rule Breakdown

```text
alert icmp any any -> $HOME_NET any
```

This is the **Rule Header**.

```text
(msg:"Ping Detected"; sid:10001; rev:1;)
```

This is the **Rule Options**.

# Rule Components

## 1. Action

Specifies what Snort should do.

Example:

```text
alert
```

Meaning:

Generate an alert.


## 2. Protocol

Defines the protocol to inspect.

Example:

```text
icmp
```

ICMP is used by the **ping** command.


## 3. Source IP

Defines where traffic originates.

```text
any
```

Means:

Traffic from **any IP address**.


## 4. Source Port

Defines the sender's port.

```text
any
```

Means:

Any source port.


## 5. Direction Operator

```text
->
```

Means:

Traffic moving from source to destination.

## 6. Destination IP

```text
$HOME_NET
```

`$HOME_NET` is a variable defined inside **snort.lua**.

It represents your internal network.

Example:

```text
HOME_NET = 192.168.1.0/24
```

## 7. Destination Port

```text
any
```

Matches every destination port.


# Rule Metadata

Everything inside parentheses is called **Rule Metadata**.


## msg

```text
msg:"Ping Detected"
```

Displayed when the rule triggers.


## sid (Signature ID)

```text
sid:10001
```

Every Snort rule has a **unique ID**.

This identifies the rule.


## rev (Revision)

```text
rev:1
```

Indicates the version of the rule.

Whenever you modify a rule:

```text
rev:1
↓

rev:2
↓

rev:3
```

# Complete Example Rule

```text
alert icmp any any -> $HOME_NET any (msg:"Ping Detected"; sid:10001; rev:1;)
```

Meaning:

> Generate an alert whenever any ICMP (Ping) packet is sent to the HOME_NET.


# Creating a Custom Rule

Open the custom rule file:

```bash
sudo nano /etc/snort/rules/local.rules
```

Add the rule:

```text
alert icmp any any -> 127.0.0.1 any (msg:"Loopback Ping Detected"; sid:10003; rev:1;)
```

Save the file.


# What Does This Rule Do?

It generates an alert whenever someone pings:

```text
127.0.0.1
```

(The loopback address.)


# Starting Snort

Run Snort:

```bash
sudo snort -q -l /var/log/snort -i lo -A alert_fast -c /etc/snort/snort.lua
```


# Command Breakdown

| Option                    | Purpose                              |
| ------------------------- | ------------------------------------ |
| `sudo`                    | Run as administrator.                |
| `snort`                   | Start Snort.                         |
| `-q`                      | Quiet mode (less output).            |
| `-l /var/log/snort`       | Store logs in this folder.           |
| `-i lo`                   | Monitor interface **lo** (Loopback). |
| `-A alert_fast`           | Display alerts in fast format.       |
| `-c /etc/snort/snort.lua` | Load the Snort configuration file.   |


# Testing the Rule

Ping the loopback address:

```bash
ping 127.0.0.1
```

# Alert Generated

Example:

```text
07/24-10:46:52
[**] Loopback Ping Detected [**]
{ICMP}
127.0.0.1 -> 127.0.0.1
```

This confirms the custom rule is working correctly.


# Running Snort on PCAP Files

Snort can also analyze **previously captured network traffic**.

This is useful for:

* Digital Forensics
* Incident Response
* Historical investigations

Instead of monitoring live traffic, Snort reads packets from a **PCAP** file.


# What is a PCAP File?

A **PCAP (Packet Capture)** file stores captured network packets.

It records:

* Source IP
* Destination IP
* Ports
* Protocols
* Packet contents

# Analyze a PCAP File

```bash
sudo snort -q -l /var/log/snort -r Task.pcap -A alert_fast -c /etc/snort/snort.lua
```

Replace:

```text
Task.pcap
```

with your PCAP filename.

# Command Breakdown

| Option          | Purpose                        |
| --------------- | ------------------------------ |
| `-r Task.pcap`  | Read packets from a PCAP file. |
| `-c`            | Load configuration file.       |
| `-A alert_fast` | Display alerts quickly.        |
| `-l`            | Save logs.                     |


# Live Traffic vs PCAP Analysis

| Live Traffic                      | PCAP File                             |
| --------------------------------- | ------------------------------------- |
| Monitors current network traffic. | Analyzes previously captured traffic. |
| Used for real-time detection.     | Used for forensic investigations.     |
| Uses `-i` option.                 | Uses `-r` option.                     |

--------


