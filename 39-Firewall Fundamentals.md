# Introduction to Firewalls

Every device connected to the Internet sends and receives network traffic.

Without protection, attackers could try to access your device or network.

A **Firewall** acts as a security guard between your trusted network and untrusted networks (such as the Internet).

It inspects all incoming and outgoing traffic and decides whether to **allow** or **block** it based on predefined security rules.

# What is a Firewall?

A **Firewall** is a security device or software that monitors and filters network traffic according to security rules.

Its main purpose is to prevent **unauthorized access** while allowing legitimate communication.

# How a Firewall Works

Whenever network traffic reaches your computer or network:

1. The traffic first reaches the firewall.
2. The firewall checks its security rules.
3. It decides whether to:

   * **Allow** the traffic.
   * **Block** the traffic.

Only traffic that satisfies the rules is allowed.


# Why Do We Need a Firewall?

A firewall helps protect systems by:

* Blocking unauthorized access.
* Filtering malicious traffic.
* Allowing legitimate communication.
* Protecting devices from network attacks.
* Enforcing security policies.

# Example

A hacker tries to connect to your computer using a blocked port.

The firewall checks its rules.

Since the connection is not allowed, the firewall blocks it before it reaches your computer.

----------

# Types of Firewalls

Different firewalls provide different levels of protection.

Some only check basic network information, while others inspect the actual contents of the traffic.

Firewalls also operate at different layers of the **OSI Model**.

The four common types are:

1. Stateless Firewall
2. Stateful Firewall
3. Proxy Firewall
4. Next-Generation Firewall (NGFW)


# 1. Stateless Firewall

**OSI Layers:** **Layer 3 (Network)** and **Layer 4 (Transport)**

A **Stateless Firewall** checks every packet **independently**.

It compares each packet against firewall rules but **does not remember previous connections**.

Every packet is treated as a completely new request.


## Characteristics

* Fast packet filtering.
* No memory of previous traffic.
* Uses predefined rules only.
* Cannot identify ongoing sessions.

## Example

A client sends 100 packets to a server.

The firewall checks **all 100 packets individually** because it doesn't remember previous packets.

## Advantages

* Fast performance.
* Low resource usage.
* Suitable for high-speed networks.

## Disadvantages

* Cannot recognize ongoing connections.
* Less secure than stateful firewalls.
* Cannot apply complex security policies.

# 2. Stateful Firewall

**OSI Layers:** **Layer 3** and **Layer 4**

A **Stateful Firewall** not only checks firewall rules but also remembers previous network connections.

It stores active connections in a **State Table**.

Future packets belonging to the same connection are handled using this stored information.

## What is a State Table?

A **State Table** is a memory table that stores information about active network connections.

It helps the firewall determine whether incoming packets belong to an existing trusted session.

## Characteristics

* Tracks active connections.
* Uses firewall rules and connection history.
* Recognizes ongoing sessions.
* More secure than stateless firewalls.

## Example

A user opens a website.

The firewall allows the first connection and stores it in the **State Table**.

All future packets belonging to that connection are automatically allowed without checking every rule again.

## Advantages

* Better security.
* Faster processing for existing sessions.
* Supports more advanced firewall policies.

## Disadvantages

* Uses more memory.
* Slightly slower than stateless firewalls.


# Stateless vs Stateful

| Stateless Firewall                  | Stateful Firewall                     |
| ----------------------------------- | ------------------------------------- |
| Does not remember previous packets. | Remembers previous connections.       |
| Checks every packet independently.  | Uses a state table to track sessions. |
| Faster.                             | More secure.                          |
| Basic filtering.                    | Intelligent filtering.                |


# 3. Proxy Firewall

**OSI Layer:** **Layer 7 (Application Layer)**

A **Proxy Firewall** acts as an **intermediary** between users and the Internet.

Instead of users connecting directly to websites, they first connect to the proxy firewall.

The proxy examines the request and then forwards it to the destination.

## Characteristics

* Inspects packet contents.
* Hides internal IP addresses.
* Supports content filtering.
* Controls application access.


## Example

A user requests:

```text id="7dzkj2"
https://example.com
```

The request goes to the **Proxy Firewall** first.

The proxy:

* Inspects the request.
* Applies security policies.
* Forwards the request using its own IP address.

The website never sees the user's real internal IP address.

## Advantages

* Strong security.
* Hides internal network.
* Supports content filtering.
* Can block malicious websites.

## Disadvantages

* Slower because every request is inspected.
* Requires more system resources.

# 4. Next-Generation Firewall (NGFW)

**OSI Layers:** **Layer 3 to Layer 7**

A **Next-Generation Firewall (NGFW)** is the most advanced firewall.

It combines traditional firewall capabilities with modern security features.

## Characteristics

* Deep Packet Inspection (DPI)
* Intrusion Prevention System (IPS)
* SSL/TLS inspection
* Threat Intelligence integration
* Application awareness
* Heuristic attack detection

## Example

An attacker sends encrypted malware.

The NGFW:

* Decrypts SSL traffic.
* Inspects the contents.
* Detects malware.
* Blocks the connection before it reaches the network.

## Advantages

* Highest level of protection.
* Detects modern attacks.
* Blocks threats in real time.
* Inspects encrypted traffic.


## Disadvantages

* More expensive.
* Requires higher processing power.
* More complex to configure.


# Firewall Comparison

| Firewall      | OSI Layer | Main Feature                                                                |
| ------------- | --------- | --------------------------------------------------------------------------- |
| **Stateless** | Layer 3–4 | Filters each packet independently.                                          |
| **Stateful**  | Layer 3–4 | Tracks active network connections.                                          |
| **Proxy**     | Layer 7   | Acts as an intermediary and inspects packet contents.                       |
| **NGFW**      | Layer 3–7 | Advanced protection with DPI, IPS, SSL inspection, and threat intelligence. |

# Firewall Selection Guide

| Use Case                        | Best Firewall                   |
| ------------------------------- | ------------------------------- |
| High-speed basic filtering      | Stateless Firewall              |
| Secure enterprise network       | Stateful Firewall               |
| Content filtering and web proxy | Proxy Firewall                  |
| Advanced enterprise security    | Next-Generation Firewall (NGFW) |

-----------

# Firewall Rules

A firewall uses **rules** to decide whether network traffic should be **allowed, blocked, or forwarded**.

These rules help organizations customize how incoming and outgoing traffic is handled based on their security requirements.

# Why Are Firewall Rules Needed?

Every organization has different security requirements.

For example:

* One company may **block SSH (Port 22)** completely.
* Another company may **allow SSH only from trusted IP addresses**.

Firewall rules make these custom security policies possible.

# Components of a Firewall Rule

Every firewall rule consists of several components.

| Component               | Description                                               |
| ----------------------- | --------------------------------------------------------- |
| **Source Address**      | The IP address sending the traffic.                       |
| **Destination Address** | The IP address receiving the traffic.                     |
| **Port**                | The port number used for communication.                   |
| **Protocol**            | The communication protocol (TCP, UDP, ICMP, etc.).        |
| **Action**              | What the firewall should do (Allow, Deny, Forward).       |
| **Direction**           | Whether the rule applies to incoming or outgoing traffic. |

# Example Firewall Rule

| Action | Source       | Destination | Protocol | Port | Direction |
| ------ | ------------ | ----------- | -------- | ---- | --------- |
| Allow  | 192.168.1.10 | Web Server  | TCP      | 80   | Outbound  |

Meaning:

> Allow computer **192.168.1.10** to send **HTTP (Port 80)** traffic to the web server.


# Firewall Actions

A firewall can perform three main actions.

## 1. Allow

The firewall **permits** matching traffic.

### Example

Allow all HTTP traffic leaving the network.

| Action | Source         | Destination | Protocol | Port | Direction |
| ------ | -------------- | ----------- | -------- | ---- | --------- |
| Allow  | 192.168.1.0/24 | Any         | TCP      | 80   | Outbound  |

**Meaning**

* Devices inside the network can browse websites using **HTTP (Port 80)**.

## 2. Deny

The firewall **blocks** matching traffic.

This is used to stop unwanted or malicious connections.

### Example

Block all SSH connections coming into the network.

| Action | Source | Destination    | Protocol | Port | Direction |
| ------ | ------ | -------------- | -------- | ---- | --------- |
| Deny   | Any    | 192.168.1.0/24 | TCP      | 22   | Inbound   |

**Meaning**

* Nobody can remotely connect to internal devices using **SSH (Port 22)**.


## 3. Forward

The firewall **redirects** traffic to another device.

This is commonly used in **port forwarding**.

### Example

Forward HTTP traffic to the internal web server.

| Action  | Source | Destination | Protocol | Port | Direction |
| ------- | ------ | ----------- | -------- | ---- | --------- |
| Forward | Any    | 192.168.1.8 | TCP      | 80   | Inbound   |

**Meaning**

* Anyone accessing **Port 80** is automatically redirected to the web server **192.168.1.8**.

# Rule Directions

Firewall rules are also categorized based on the direction of traffic.

## 1. Inbound Rules

These rules control **incoming traffic**.

Traffic flow:

```text
Internet
    │
    ▼
 Firewall
    │
 Internal Network
```

### Example

Allow users from the Internet to access a web server on **Port 80**.

## 2. Outbound Rules

These rules control **outgoing traffic**.

Traffic flow:

```text
Internal Network
      │
      ▼
   Firewall
      │
   Internet
```

### Example

Block all devices except the mail server from sending emails using **SMTP (Port 25)**.


## 3. Forward Rules

These rules redirect traffic to another system.

Traffic flow:

```text
Internet
    │
    ▼
 Firewall
    │
    ▼
Web Server
```

### Example

Forward all incoming **HTTP (Port 80)** requests to an internal web server.

# Common Ports

| Port    | Protocol | Purpose                |
| ------- | -------- | ---------------------- |
| **22**  | SSH      | Remote login           |
| **25**  | SMTP     | Email sending          |
| **53**  | DNS      | Domain name resolution |
| **80**  | HTTP     | Websites               |
| **443** | HTTPS    | Secure websites        |

# Example Rule Set

| Action  | Source           | Destination      | Protocol | Port | Direction | Purpose                   |
| ------- | ---------------- | ---------------- | -------- | ---- | --------- | ------------------------- |
| Allow   | Internal Network | Internet         | TCP      | 80   | Outbound  | Allow web browsing        |
| Allow   | Internal Network | Internet         | TCP      | 443  | Outbound  | Allow secure web browsing |
| Deny    | Any              | Internal Network | TCP      | 22   | Inbound   | Block SSH access          |
| Forward | Any              | Web Server       | TCP      | 80   | Inbound   | Forward web traffic       |

------

# Windows Defender Firewall

**Windows Defender Firewall** is the built-in firewall in Microsoft Windows.

It protects your computer by monitoring and filtering **incoming** and **outgoing** network traffic based on firewall rules.

You can:

* Allow or block applications.
* Create custom firewall rules.
* Control inbound and outbound traffic.
* Configure different settings for different network types.



# Opening Windows Defender Firewall

Open the Windows Search and type:

```text
Windows Defender Firewall
```

This opens the main firewall dashboard.



# Main Dashboard

The dashboard lets you:

* View network profiles.
* Allow or block applications.
* Turn the firewall on or off.
* Restore default settings.
* Open Advanced Settings to create custom rules.


# Network Profiles

Windows automatically detects the network you are connected to using **Network Location Awareness (NLA)** and applies the appropriate firewall settings.

There are two main profiles.

## 1. Private Network

Used for trusted networks such as:

* Home Wi-Fi
* Office network

Usually allows more communication between devices.



## 2. Public (Guest) Network

Used for untrusted networks such as:

* Coffee shops
* Airports
* Hotels
* Public Wi-Fi

Usually has stricter firewall rules to improve security.

Example:

* Block most incoming connections.
* Allow only essential outgoing traffic.


# Main Firewall Options

## Allow an App

Allows or blocks specific applications through the firewall.

Example:

* Allow Google Chrome.
* Block FTP software.


## Turn Firewall On/Off

Enable or disable Windows Defender Firewall.

> Microsoft recommends **keeping the firewall enabled**.

Instead of turning it off completely, block only the required traffic.


## Restore Defaults

Restores all firewall settings to their original default configuration.

Useful if firewall rules become misconfigured.


# Advanced Settings

**Advanced Settings** allows you to create **custom firewall rules**.

Here you can create:

* Inbound Rules
* Outbound Rules
* Connection Security Rules


# Inbound Rules

Control **incoming traffic**.

Example:

* Allow Remote Desktop (RDP).
* Block SSH connections.


# Outbound Rules

Control **outgoing traffic**.

Example:

* Block access to websites.
* Prevent applications from accessing the Internet.


# Creating a Custom Outbound Rule

In this example, the goal is to **block web browsing** by blocking:

* HTTP → Port **80**
* HTTPS → Port **443**


## Step 1

Open:

```text
Windows Defender Firewall
→ Advanced Settings
```


## Step 2

Select:

```text
Outbound Rules
```

Click:

```text
New Rule
```


## Step 3

Choose:

```text
Custom
```

Click **Next**.


## Step 4

Choose:

```text
All Programs
```

Click **Next**.


## Step 5

Configure:

* Protocol → **TCP**
* Local Port → **All Ports**
* Remote Port → **Specific Ports**

Enter:

```text
80,443
```

Click **Next**.

## Step 6

Keep both:

* Local IP Address → Any
* Remote IP Address → Any

Click **Next**.


## Step 7

Choose:

```text
Block the connection
```

Click **Next**.


## Step 8

Select all profiles:

* Private
* Public

Click **Next**.

## Step 9

Give the rule a name.

Example:

```text
Block HTTP and HTTPS
```

Click:

```text
Finish
```

The rule is now active.

# Testing the Rule

Before creating the rule:

Visit:

```text
http://10.10.10.10
```

The website opens successfully.

After enabling the rule:

Visit the same website again.

Result:

```text
This site can't be reached
```

because traffic on **Ports 80 and 443** is blocked.

-----------
# Linux Firewall

Linux also provides built-in firewall capabilities to control network traffic.

Unlike Windows, Linux offers multiple firewall utilities, all built on the **Netfilter** framework.

These tools allow you to:

* Allow or block traffic.
* Filter packets.
* Configure NAT (Network Address Translation).
* Track network connections.


# Netfilter

**Netfilter** is the core firewall framework inside the Linux kernel.

It provides the basic firewall functions used by different Linux firewall tools.

### Netfilter Features

* Packet Filtering
* Network Address Translation (NAT)
* Connection Tracking

> Think of **Netfilter** as the **engine**, while tools like **iptables**, **nftables**, and **ufw** are different ways to control that engine.


# Linux Firewall Utilities

Several firewall tools use the Netfilter framework.

| Utility       | Description                                              |
| ------------- | -------------------------------------------------------- |
| **iptables**  | Traditional Linux firewall utility.                      |
| **nftables**  | Modern replacement for iptables.                         |
| **firewalld** | Uses zones and predefined rule sets.                     |
| **ufw**       | Beginner-friendly firewall utility with simple commands. |

# 1. iptables

* Most widely used firewall utility.
* Uses Netfilter.
* Supports advanced firewall rules.
* Command syntax is complex.

### Best For

* Experienced Linux administrators.
* Advanced firewall configurations.

# 2. nftables

* Successor to **iptables**.
* Simpler and more efficient.
* Better packet filtering.
* Better NAT support.

### Best For

* Modern Linux systems.

# 3. firewalld

* Uses **network zones** instead of individual rules.
* Supports dynamic firewall changes.
* Common in Red Hat, CentOS, Fedora.

### Example Zones

* Public
* Home
* Work
* Internal

# 4. UFW (Uncomplicated Firewall)

**UFW** is the easiest Linux firewall for beginners.

Instead of writing long **iptables** commands, you use simple UFW commands.

UFW automatically creates the required Netfilter/iptables rules.


# Checking Firewall Status

Use:

```bash
sudo ufw status
```

Example output:

```text
Status: inactive
```

Shows whether the firewall is enabled.


# Enable Firewall

```bash
sudo ufw enable
```

Example output:

```text
Firewall is active and enabled on system startup
```

This:

* Enables the firewall.
* Starts it automatically after reboot.

# Disable Firewall

```bash
sudo ufw disable
```

Turns off the firewall.

# Default Policy

The **default policy** decides what happens to traffic **when no specific rule matches**.


## Allow All Outgoing Traffic

```bash
sudo ufw default allow outgoing
```

Meaning:

* Outgoing traffic is allowed by default.
* Unless another rule specifically blocks it.

## Allow All Incoming Traffic

```bash
sudo ufw default allow incoming
```

Allows all incoming traffic.

(Not recommended for most systems.)


## Deny All Incoming Traffic

```bash
sudo ufw default deny incoming
```

Blocks all incoming traffic unless explicitly allowed.

This is a common and secure default configuration.

# Blocking SSH

SSH uses:

| Service | Port   |
| ------- | ------ |
| SSH     | 22/TCP |

To block SSH connections:

```bash
sudo ufw deny 22/tcp
```

Example output:

```text
Rule added
Rule added (v6)
```

Meaning:

* All incoming SSH connections are blocked.


# Viewing Firewall Rules

Use:

```bash
sudo ufw status numbered
```

Example:

```text
To                         Action      From
--                         ------      ----
[1] 22/tcp                 DENY IN     Anywhere
[2] 22/tcp (v6)            DENY IN     Anywhere (v6)
```

The numbers make it easy to delete rules.

# Deleting a Rule

Delete rule number **2**:

```bash
sudo ufw delete 2
```

Example output:

```text
Deleting:
deny 22/tcp

Proceed with operation (y|n)? y

Rule deleted
```

# Basic UFW Commands

| Command                           | Purpose                                |
| --------------------------------- | -------------------------------------- |
| `sudo ufw status`                 | Show firewall status.                  |
| `sudo ufw enable`                 | Enable firewall.                       |
| `sudo ufw disable`                | Disable firewall.                      |
| `sudo ufw default allow outgoing` | Allow all outgoing traffic by default. |
| `sudo ufw default deny incoming`  | Block all incoming traffic by default. |
| `sudo ufw deny 22/tcp`            | Block SSH connections.                 |
| `sudo ufw status numbered`        | Display numbered firewall rules.       |
| `sudo ufw delete <rule_number>`   | Delete a firewall rule.                |


# Firewall Workflow

```text
Internet
     │
     ▼
    UFW
     │
     ▼
Netfilter (Kernel Firewall)
     │
     ▼
Linux System
```

UFW sends simple commands to **Netfilter**, which actually filters the network traffic.


# Comparison of Linux Firewall Utilities

| Utility       | Difficulty | Best For                         |
| ------------- | ---------- | -------------------------------- |
| **iptables**  | Hard       | Advanced firewall management     |
| **nftables**  | Medium     | Modern Linux firewall management |
| **firewalld** | Medium     | Enterprise Linux systems         |
| **UFW**       | Easy       | Beginners and Ubuntu users       |

-------------
