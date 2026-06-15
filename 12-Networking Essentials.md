# Topic: DHCP (Dynamic Host Configuration Protocol)

## Simple Idea

Imagine you go to a coffee shop and connect to its WiFi.

You don't manually enter:

* IP Address
* Gateway (Router)
* DNS Server

Yet your laptop works on the internet immediately.

**Question:** How does your laptop get all these settings automatically?

**Answer:** DHCP

DHCP is like a **receptionist** that gives network information to every device that joins the network.

---

# Why DHCP is Needed

Every device needs:

| Setting        | Purpose                                |
| -------------- | -------------------------------------- |
| IP Address     | Device's unique network address        |
| Subnet Mask    | Identifies local network               |
| Gateway/Router | Path to the Internet                   |
| DNS Server     | Converts website names to IP addresses |

Without DHCP, you would have to enter all these manually every time you join a new network.

---

# Real-Life Example

Imagine a hotel.

When a guest arrives:

1. Guest asks for a room.
2. Reception checks available rooms.
3. Reception offers a room.
4. Guest accepts.
5. Reception confirms and gives the key.

DHCP works exactly the same way.

---

# DORA Process

DHCP uses **4 steps** called **DORA**.

## D = Discover

Laptop joins WiFi and says:

> "Is there any DHCP server here?"

This message is sent to everyone on the network.

### Packet

```
DHCP Discover
```

---

## O = Offer

DHCP Server replies:

> "Yes! You can use IP address 192.168.66.133"

### Packet

```
DHCP Offer
```

---

## R = Request

Laptop replies:

> "Great! I want that IP address."

### Packet

```
DHCP Request
```

---

## A = Acknowledge

Server confirms:

> "Done! That IP address is now yours."

### Packet

```
DHCP ACK
```

---

# DORA Diagram

```text
Laptop                          DHCP Server
   |                                 |
   |---- Discover -----------------> |
   |                                 |
   | <----- Offer ------------------ |
   |                                 |
   |---- Request ------------------> |
   |                                 |
   | <------ ACK ------------------- |
   |                                 |
```

After this process, the laptop can access the network and Internet.

---

# Ports Used

DHCP uses UDP.

| Device      | Port   |
| ----------- | ------ |
| DHCP Server | UDP 67 |
| DHCP Client | UDP 68 |

### Easy Memory Trick

```text
Server = 67
Client = 68
```

---

# Why 0.0.0.0 is Used?

Before getting an IP address, the laptop has no identity on the network.

So it sends packets from:

```text
Source IP = 0.0.0.0
```

Meaning:

> "I don't have an IP yet."

---

# Why 255.255.255.255 is Used?

The laptop doesn't know where the DHCP server is.

So it sends the message to everyone:

```text
Destination IP = 255.255.255.255
```

This is called a **broadcast address**.

Meaning:

> "Everybody listen! Is there a DHCP server here?"

---

# MAC Address Broadcast

At Layer 2 (Data Link Layer), the laptop sends to:

```text
ff:ff:ff:ff:ff:ff
```

Meaning:

> "Send this frame to all devices."

---

# What Does DHCP Finally Give?

After DORA completes, the laptop receives:

### 1. IP Address

Example:

```text
192.168.66.133
```

Used to identify the device.

---

### 2. Gateway

Example:

```text
192.168.66.1
```

Used to reach the Internet.

---

### 3. DNS Server

Example:

```text
8.8.8.8
```

Used to convert:

```text
google.com
```

into

```text
142.250.x.x
```

---



# Topic: ARP (Address Resolution Protocol)

## Simple Idea

Computers communicate using **IP addresses**, but when sending data on the same local network (same WiFi/LAN), they actually need **MAC addresses**.

### Think of it like this:

* **IP Address** = House Address
* **MAC Address** = Person's Name inside the house

You may know the house address, but to deliver a package, you need to know who lives there.

ARP helps find the MAC address when we already know the IP address.

---

# Why ARP is Needed

Suppose:

```text
Your PC IP      = 192.168.66.89
Router IP       = 192.168.66.1
```

Your PC wants to send data to the router.

It knows:

```text
Router IP = 192.168.66.1
```

But Ethernet frames require:

```text
Destination MAC Address
```

Problem:

```text
Know IP ❌
Don't know MAC ❌
```

Solution:

```text
Use ARP
```

---

# What Does ARP Do?

ARP translates:

```text
IP Address  →  MAC Address
```

Example:

```text
192.168.66.1
        ↓
44:df:65:d8:fe:6c
```

---

# ARP Process

## Step 1: ARP Request

Your computer asks everyone:

> "Who has IP 192.168.66.1?"

This is sent as a broadcast.

```text
Who has 192.168.66.1?
Tell 192.168.66.89
```

### Packet

```text
cc:5e:f8:02:21:a7 → ff:ff:ff:ff:ff:ff
```

Notice:

```text
ff:ff:ff:ff:ff:ff
```

This is the broadcast MAC address.

Meaning:

> "Everyone on the network listen!"

---

## Step 2: ARP Reply

The router replies:

> "I am 192.168.66.1"

and sends its MAC address.

```text
192.168.66.1 is at 44:df:65:d8:fe:6c
```

### Packet

```text
44:df:65:d8:fe:6c → cc:5e:f8:02:21:a7
```

Now your PC knows:

```text
192.168.66.1
      ↓
44:df:65:d8:fe:6c
```

---

# Simple Diagram

```text
Your PC                          Router
192.168.66.89                    192.168.66.1

      ARP Request
"Who has 192.168.66.1?"
---------------------------------->

      ARP Reply
"I am 192.168.66.1
My MAC is 44:df:65:d8:fe:6c"
<----------------------------------

Now communication can start
```

---

# What Happens After ARP?

Before ARP:

```text
Know IP Address ✔
Know MAC Address ❌
Cannot send Ethernet frame
```

After ARP:

```text
Know IP Address ✔
Know MAC Address ✔
Can send Ethernet frame ✔
```

---

# Ethernet Frame

An Ethernet frame contains:

```text
+-------------------+
| Destination MAC   |
+-------------------+
| Source MAC        |
+-------------------+
| Type (IPv4)       |
+-------------------+
| IP Packet         |
+-------------------+
```

Example:

```text
Destination MAC = 44:df:65:d8:fe:6c
Source MAC      = cc:5e:f8:02:21:a7
Type            = IPv4
```

---

# Important Difference

### DHCP

Used to get:

```text
IP Address
Gateway
DNS Server
```

### ARP

Used to get:

```text
MAC Address
```

---

# Is ARP Inside an IP Packet?

### No

ARP is special.

Normal communication:

```text
Ethernet Frame
    ↓
IP Packet
    ↓
TCP/UDP
```

But ARP works like this:

```text
Ethernet Frame
    ↓
ARP Message
```

There is NO IP packet involved.

---

# Easy Memory Trick

### DHCP

```text
IP → Configuration
```

### DNS

```text
Domain Name → IP
```

### ARP

```text
IP → MAC
```

---

# Topic: ICMP (Internet Control Message Protocol)

## Simple Idea

ICMP is a protocol used for:

* Checking whether a device is reachable
* Finding network problems
* Discovering the path packets take through the Internet

Think of ICMP as the **network's messenger** that sends status and error messages.

---

# What is ICMP Used For?

The two most common commands that use ICMP are:

| Command                                | Purpose                     |
| -------------------------------------- | --------------------------- |
| ping                                   | Checks if a device is alive |
| traceroute (Linux) / tracert (Windows) | Shows the path packets take |

---

# 1. Ping

## Real-Life Example

Imagine shouting:

> "Hello! Are you there?"

If someone replies:

> "Yes, I'm here!"

you know they are reachable.

Ping works the same way.

---

## How Ping Works

### Step 1: Echo Request

Your computer sends:

```text
ICMP Echo Request
(Type 8)
```

Meaning:

> "Are you there?"

---

### Step 2: Echo Reply

The target replies:

```text
ICMP Echo Reply
(Type 0)
```

Meaning:

> "Yes, I'm here!"

---

## Ping Diagram

```text
Your PC                     Target

Echo Request (Type 8)
---------------------->

Echo Reply (Type 0)
<----------------------
```

---

## Example Command

```bash
ping 192.168.11.1 -c 4
```

### Meaning

```text
ping          = Check connectivity
192.168.11.1  = Target IP
-c 4          = Send only 4 packets
```

---

## Understanding the Output

```text
64 bytes from 192.168.11.1:
icmp_seq=1 ttl=63 time=11.2 ms
```

### Meaning

| Field        | Meaning               |
| ------------ | --------------------- |
| 64 bytes     | Size of reply         |
| icmp_seq=1   | Packet number         |
| ttl=63       | Remaining TTL         |
| time=11.2 ms | Round Trip Time (RTT) |

---

# RTT (Round Trip Time)

RTT means:

```text
Time taken for:
Your PC → Target → Your PC
```

Example:

```text
time=11.2 ms
```

means:

The packet went to the target and returned in:

```text
11.2 milliseconds
```

---

# Packet Loss

Example:

```text
4 packets transmitted
4 received
0% packet loss
```

Meaning:

```text
Sent = 4
Received = 4
Lost = 0
```

Perfect connection.

---

## If Ping Fails

Possible reasons:

### 1. Target is OFF

```text
Computer shut down
```

---

### 2. Firewall Blocks ICMP

```text
Ping request blocked
```

---

### 3. Network Problem

```text
Cable issue
Router issue
WiFi issue
```

---

# 2. Traceroute

## Purpose

Traceroute shows:

```text
Which routers your packet passes through
```

before reaching the destination.

---

## Real-Life Example

Imagine travelling:

```text
Home
 ↓
Bus Stop
 ↓
Railway Station
 ↓
Airport
 ↓
Destination
```

Traceroute shows every stop along the journey.

---

# TTL (Time To Live)

Every IP packet contains a field called:

```text
TTL
```

TTL limits how many routers a packet can cross.

---

## Example

Suppose:

```text
TTL = 3
```

### Router 1

```text
TTL = 2
```

---

### Router 2

```text
TTL = 1
```

---

### Router 3

```text
TTL = 0
```

Router drops the packet.

Then sends:

```text
ICMP Time Exceeded
(Type 11)
```

back to your computer.

---

# How Traceroute Uses TTL

Traceroute sends packets with different TTL values.

---

### First Packet

```text
TTL = 1
```

Dies at Router 1.

Router 1 replies:

```text
ICMP Time Exceeded
```

Now traceroute learns:

```text
Router 1 exists
```

---

### Second Packet

```text
TTL = 2
```

Dies at Router 2.

Router 2 replies.

Traceroute learns:

```text
Router 2 exists
```

---

### Third Packet

```text
TTL = 3
```

Dies at Router 3.

And so on...

---

# Traceroute Diagram

```text
Your PC
   |
   | TTL=1
   v
Router 1
   X Packet dies
   |
   | ICMP Time Exceeded
   |
Your PC learns Router 1

--------------------------

Your PC
   |
   | TTL=2
   v
Router 1
   |
   v
Router 2
   X Packet dies
   |
   | ICMP Time Exceeded
   |
Your PC learns Router 2
```

This continues until the destination is reached.

---

# Why Do We See * * * ?

Example:

```text
5  * * *
6  * * *
```

Means:

```text
Router did not reply
```

Possible reasons:

* Firewall blocks ICMP
* Router configured not to answer
* Packet lost

---

# ICMP Message Types to Remember

| Type | Meaning       |
| ---- | ------------- |
| 0    | Echo Reply    |
| 8    | Echo Request  |
| 11   | Time Exceeded |

---

# Relationship Between DHCP, ARP, and ICMP

### DHCP

```text
Gets IP address automatically
```

---

### ARP

```text
Finds MAC address from IP address
```

---

### ICMP

```text
Checks connectivity and reports network errors
```

---

# Exam Shortcut

### ICMP Full Form

```text
Internet Control Message Protocol
```

### Ping Uses

```text
ICMP Echo Request (Type 8)
ICMP Echo Reply   (Type 0)
```

### Traceroute Uses

```text
ICMP Time Exceeded (Type 11)
```

### TTL

```text
Decreases by 1 at every router
```

### Purpose of Traceroute

```text
Find route/path to destination
```

---

# Topic: Routing Protocols

## Simple Idea

Imagine you want to travel from:

```text
Hyderabad → Kottayam
```

There are many possible routes:

```text
Route 1: Hyderabad → Chennai → Kottayam
Route 2: Hyderabad → Bengaluru → Kottayam
Route 3: Hyderabad → Coimbatore → Kottayam
```

How do you decide which route to take?

You use:

```text
Google Maps
```

Similarly, routers need a way to decide:

```text
Which path should a packet take?
```

This is called **Routing**.

---

# What is Routing?

Routing is the process of finding the best path for data to travel from:

```text
Source Device
      ↓
Destination Device
```

---

## Example

Suppose:

```text
Your Mobile
      ↓
Router A
      ↓
Router B
      ↓
Router C
      ↓
Web Server
```

Every router must decide:

> "Where should I send this packet next?"

---

# Why Routing Protocols Are Needed

The Internet contains:

```text
Billions of devices
Millions of routers
```

No router can manually remember every path.

Therefore routers use **Routing Protocols** to exchange information and learn routes automatically.

---

# Simple Example

Imagine this network:

```text
Network 1
    |
 Router A
    |
Internet
    |
 Router B
    |
Network 2
```

If a packet starts from:

```text
Network 1
```

How does Router A know where Network 2 is?

Answer:

```text
Routing Protocols
```

---

# Main Routing Protocols

For exams and TryHackMe, remember these four:

```text
OSPF
EIGRP
BGP
RIP
```

---

# 1. OSPF

## Full Form

```text
Open Shortest Path First
```

---

## Simple Idea

Every router shares information about its connections.

Eventually every router builds a complete map of the network.

Then it calculates:

```text
Shortest path
```

to the destination.

---

## Real-Life Example

Imagine Google Maps knows every road.

It calculates:

```text
Fastest route
```

for you.

OSPF works similarly.

---

## Easy Memory Trick

```text
OSPF = Open Shortest Path First

Finds shortest path
```

---

# 2. EIGRP

## Full Form

```text
Enhanced Interior Gateway Routing Protocol
```

---

## Simple Idea

Routers share:

```text
Bandwidth
Delay
Reachable Networks
```

Then they choose the best route.

---

## Example

Suppose two routes exist:

```text
Route A = High speed fiber
Route B = Slow connection
```

EIGRP prefers:

```text
Route A
```

because it has lower delay and better bandwidth.

---

## Easy Memory Trick

```text
EIGRP = Smart route selection
```

---

# 3. BGP

## Full Form

```text
Border Gateway Protocol
```

---

## Most Important Protocol

### Why?

Because:

```text
The Internet runs on BGP
```

---

## Simple Idea

Different organizations share routes.

Example:

```text
Jio Network
      ↔
Airtel Network
      ↔
Google Network
      ↔
Amazon Network
```

BGP helps them exchange routing information.

---

## Real-Life Example

Think of countries.

Each country has its own roads.

BGP tells countries:

```text
How to reach each other
```

---

## Easy Memory Trick

```text
BGP = Backbone of Internet
```

If a TryHackMe question asks:

> Which routing protocol is mainly used on the Internet?

Answer:

```text
BGP
```

---

# 4. RIP

## Full Form

```text
Routing Information Protocol
```

---

## Simple Idea

RIP counts:

```text
Number of routers (hops)
```

between source and destination.

Then it chooses the route with the fewest hops.

---

## Example

### Route A

```text
PC → R1 → R2 → Server

2 hops
```

---

### Route B

```text
PC → R1 → R2 → R3 → R4 → Server

4 hops
```

---

RIP chooses:

```text
Route A
```

because:

```text
2 hops < 4 hops
```

---

## Easy Memory Trick

```text
RIP = Route with least hops
```

---

# Comparison Table

| Protocol | Full Form                                  | How It Chooses Route  |
| -------- | ------------------------------------------ | --------------------- |
| OSPF     | Open Shortest Path First                   | Shortest path         |
| EIGRP    | Enhanced Interior Gateway Routing Protocol | Bandwidth + Delay     |
| BGP      | Border Gateway Protocol                    | Internet-wide routing |
| RIP      | Routing Information Protocol               | Fewest hops           |

---

# Topic: NAT (Network Address Translation)

## Simple Idea

IPv4 provides about:

```text
4 Billion IP Addresses
```

Years ago, this seemed like a lot.

But today we have:

* Computers
* Laptops
* Smartphones
* TVs
* Cameras
* Smart Watches
* IoT Devices

As a result, IPv4 addresses started running out.

---

# Solution: NAT

## What is NAT?

**NAT (Network Address Translation)** allows:

```text
Many Private IP Addresses
           ↓
One Public IP Address
```

to share Internet access.

---

# Real-Life Example

Imagine an apartment building.

### Apartment Number

```text
Flat 101
Flat 102
Flat 103
Flat 104
```

These are like:

```text
Private IP Addresses
```

---

### Building Address

```text
123 Main Road
```

This is like:

```text
Public IP Address
```

People outside only see:

```text
123 Main Road
```

They don't see the individual flat numbers.

Similarly, websites only see your router's public IP.

---

# Without NAT

Suppose a company has:

```text
20 Computers
```

Without NAT:

```text
20 Public IP Addresses Needed
```

Very expensive and wastes IP addresses.

---

# With NAT

```text
20 Computers
       ↓
    Router
       ↓
1 Public IP Address
```

Now:

```text
Only 1 Public IP Needed
```

---

# Example Network

```text
Laptop     192.168.0.129
Phone      192.168.0.130
PC         192.168.0.131
                 |
                 |
             Router
         Public IP:
          212.3.4.5
                 |
              Internet
```

All devices share:

```text
212.3.4.5
```

---

# The Problem

Suppose:

```text
Laptop opens Google
Phone opens YouTube
PC opens TryHackMe
```

All requests appear to come from:

```text
212.3.4.5
```

How does the router know which reply belongs to which device?

---

# NAT Translation Table

The router keeps a table.

Example:

| Internal Device | Internal Port | Public IP | Public Port |
| --------------- | ------------- | --------- | ----------- |
| 192.168.0.129   | 15401         | 212.3.4.5 | 19273       |
| 192.168.0.130   | 15402         | 212.3.4.5 | 19274       |
| 192.168.0.131   | 15403         | 212.3.4.5 | 19275       |

---

# Step-by-Step Example

## Step 1

Laptop sends request.

```text
Source IP   = 192.168.0.129
Source Port = 15401
```

---

## Step 2

Router receives it.

Router changes:

```text
192.168.0.129:15401
```

to

```text
212.3.4.5:19273
```

---

## Step 3

Google receives:

```text
212.3.4.5:19273
```

Google has no idea the laptop exists.

It only sees:

```text
212.3.4.5
```

---

## Step 4

Google replies.

```text
Destination:
212.3.4.5:19273
```

---

## Step 5

Router checks its NAT table.

```text
19273
      ↓
192.168.0.129:15401
```

The router forwards the response to the laptop.

---

# Diagram

```text
Laptop
192.168.0.129:15401
        |
        |
        v

Router (NAT)

192.168.0.129:15401
        ↓
212.3.4.5:19273

        |
        |
        v

Google Server
```

Reply:

```text
Google
    ↓
212.3.4.5:19273
    ↓
Router
    ↓
192.168.0.129:15401
    ↓
Laptop
```

---

# Private IP Addresses

Common private IP ranges:

### Class A

```text
10.0.0.0 - 10.255.255.255
```

---

### Class B

```text
172.16.0.0 - 172.31.255.255
```

---

### Class C

```text
192.168.0.0 - 192.168.255.255
```

---

# Public vs Private IP

| Private IP                  | Public IP          |
| --------------------------- | ------------------ |
| Used inside network         | Used on Internet   |
| Not reachable from Internet | Reachable globally |
| Free to use                 | Assigned by ISP    |

Example:

```text
Private IP = 192.168.0.129
Public IP  = 212.3.4.5
```

---

# Advantages of NAT

### 1. Saves IPv4 Addresses

```text
Many devices
      ↓
One Public IP
```

---

### 2. Cheaper

No need to buy many public IPs.

---

### 3. Extra Security

External users cannot directly see internal devices.

They only see:

```text
Router's Public IP
```

---

