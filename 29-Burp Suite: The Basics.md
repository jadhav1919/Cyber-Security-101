## Burp Suite 

#### What is Burp Suite?

**Burp Suite** is a **Java-based web application security testing framework** used by penetration testers to analyze and attack web applications, mobile applications, and APIs.

It is considered the **industry-standard tool** for manual web application security testing.


### How Burp Suite Works

Burp Suite acts as a **proxy** between your browser and the target web server.

```text
Browser ↔ Burp Suite ↔ Web Server
```

This allows you to:

* Intercept requests before they reach the server
* View HTTP/HTTPS traffic
* Modify requests and responses
* Analyze application behavior
* Test for vulnerabilities


### Why Burp Suite is Important

Burp Suite enables security testers to:

* Inspect web traffic
* Manipulate requests
* Test authentication mechanisms
* Discover vulnerabilities
* Analyze APIs
* Perform manual penetration testing


### Burp Suite Editions

#### 1. Burp Suite Community Edition

**Free version** available for non-commercial use.

##### Features

* Intercept HTTP/HTTPS traffic
* Modify requests and responses
* Manual testing tools
* Basic web application assessment

##### Limitations

* No automated vulnerability scanner
* Rate-limited Intruder (fuzzing tool)
* Limited extension functionality

#### 2. Burp Suite Professional

Paid version with advanced features.

##### Additional Features

* Automated vulnerability scanner
* Faster Intruder (fuzzer/brute-forcer)
* Save projects
* Generate reports
* API integration
* Burp Collaborator support
* Full extension support

##### Common Users

* Professional Penetration Testers
* Security Consultants
* Bug Bounty Hunters
 

#### 3. Burp Suite Enterprise

Designed for continuous automated scanning.

##### Features

* Continuous vulnerability scanning
* Automated assessments
* Runs on a server
* Monitors web applications regularly

##### Similar To

* Vulnerability management tools like:

  * Nessus

##### Common Users

* Large organizations
* Security Operations Teams
* Enterprises


----------
# Burp Suite Community Edition Tools

## Overview

Even though **Burp Suite Community Edition** has fewer features than the Professional version, it still provides several powerful tools for web application security testing.

These tools help security professionals:

* Intercept web traffic
* Modify requests and responses
* Test web applications
* Identify vulnerabilities
* Analyze application behavior

 

# 1. Proxy

## What is Proxy?

The **Proxy** is Burp Suite's most important and commonly used tool.

It sits between your browser and the web server, allowing you to intercept and inspect HTTP/HTTPS traffic.

### How It Works

```text
Browser ↔ Burp Proxy ↔ Web Server
```

### What You Can Do

* Capture requests
* Modify requests before sending
* View server responses
* Modify responses before they reach the browser

### Common Uses

* Testing authentication
* Finding hidden parameters
* Manipulating form submissions
* Web application security testing

### Example

Intercept a login request:

```http
POST /login HTTP/1.1

username=admin
password=password123
```

Before sending it to the server, you can modify the request.

### Interview Tip

> Proxy is the core component of Burp Suite because almost all testing begins with intercepting traffic.

  

# 2. Repeater

## What is Repeater?

Repeater allows you to capture a request, modify it, and send it repeatedly.

### Why Use It?

Instead of refreshing the browser every time, you can manually test different payloads quickly.

### Common Uses

* SQL Injection testing
* XSS testing
* Parameter manipulation
* API testing

### Example

Original Request:

```http
GET /profile?id=1
```

Modified Request:

```http
GET /profile?id=2
```

Then:

```http
GET /profile?id=3
```

And so on...

### Benefits

* Fast testing
* Easy payload modification
* Immediate response analysis

### Interview Tip

> Repeater is primarily used for manual vulnerability testing and payload experimentation.

 

# 3. Intruder

## What is Intruder?

Intruder automates sending multiple requests with different payloads.

### Why Use It?

Manually testing hundreds of payloads would take too long.

Intruder automates the process.

### Common Uses

* Brute force attacks
* Fuzzing
* Parameter discovery
* Testing input validation

### Example

Testing usernames:

```text
admin
administrator
root
test
guest
```

Intruder sends requests automatically using each value.

### Community Edition Limitation

* Rate-limited
* Slower than Professional Edition

### Interview Tip

> Intruder is Burp Suite's fuzzing and brute-force tool.

 

# 4. Decoder

## What is Decoder?

Decoder is used to encode and decode data.

### Why Use It?

Web applications often use encoded data formats.

Examples:

* URL Encoding
* Base64 Encoding
* HTML Encoding

### Example

Encoded Value:

```text
YWRtaW46cGFzc3dvcmQ=
```

Decoded Output:

```text
admin:password
```

### Common Uses

* Decoding cookies
* Decoding JWT components
* Encoding payloads
* Data transformation

### Interview Tip

> Decoder helps convert data between readable and encoded formats.

 
# 5. Comparer

## What is Comparer?

Comparer allows you to compare two pieces of data.

### Comparison Types

* Word-level comparison
* Byte-level comparison

### Common Uses

* Comparing HTTP responses
* Comparing cookies
* Comparing API outputs
* Identifying differences between requests

### Example

Response 1:

```json
{
  "role":"user"
}
```

Response 2:

```json
{
  "role":"admin"
}
```

Comparer highlights the differences.

### Benefits

* Quick identification of changes
* Useful during privilege escalation testing

### Interview Tip

> Comparer helps identify differences between requests and responses.

 

# 6. Sequencer

## What is Sequencer?

Sequencer analyzes the randomness of generated tokens.

### What Does It Test?

Whether tokens are truly random and unpredictable.

### Common Targets

* Session IDs
* Authentication tokens
* Password reset tokens
* CSRF tokens

### Example

If a website generates:

```text
1001
1002
1003
1004
```

instead of random values, an attacker may predict future tokens.

### Security Risk

Poor randomness can lead to:

* Session hijacking
* Account takeover
* Authentication bypass

### Interview Tip

> Sequencer is used to test the randomness and quality of token generation.

 

# Burp Suite Extensions

## What are Extensions?

Extensions add new functionality to Burp Suite.

### Supported Languages

* Java
* Python (Jython)
* Ruby (JRuby)

### Loading Extensions

Using:

```text
Extender Module
```

### Downloading Extensions

Using:

```text
BApp Store
```
 

# Popular Extension

## Logger++

### Purpose

Extends Burp Suite's logging capabilities.

### Benefits

* Better request logging
* Better response logging
* Easier traffic analysis

 ---------

# Burp Suite Installation Guide

## Overview

Before using Burp Suite for web application security testing, it must be installed on your system.

Burp Suite is available for:

* Linux
* Windows
* macOS
* Kali Linux (pre-installed)

> **Note:** If you are using a TryHackMe AttackBox or a standard Kali Linux installation, Burp Suite is usually already installed.

 

# Why Install Burp Suite?

Burp Suite is widely used for:

* Web Application Penetration Testing
* Mobile Application Testing
* API Security Testing
* Bug Bounty Hunting
* Security Research
* Web Development Debugging

 

# Downloading Burp Suite

## Official Source

Burp Suite should always be downloaded from the official PortSwigger website:

**Official Website**

[PortSwigger Burp Suite Downloads](https://portswigger.net/burp/releases?utm_source=chatgpt.com)

 

# Installation by Operating System

## Kali Linux

### Pre-installed Version

Most Kali Linux distributions already include Burp Suite.

### Verify Installation

Open a terminal and run:

```bash
burpsuite
```

Or search:

```bash
which burpsuite
```

 
### Install Using APT

If Burp Suite is missing:

```bash
sudo apt update
sudo apt install burpsuite -y
```

### Verify Installation

```bash
burpsuite
```

 

## Windows

### Step 1: Download

Download the Community Edition installer from the PortSwigger website.

### Step 2: Run Installer

Double-click:

```text
burpsuite_community_windows.exe
```

### Step 3: Follow Setup Wizard

Recommended:

* Accept license agreement
* Keep default installation location
* Continue with default settings

### Step 4: Launch Burp Suite

Open:

```text
Start Menu → Burp Suite Community Edition
```

 

## Linux (Ubuntu, Debian, Parrot OS, etc.)

### Step 1: Download Installer

Download the Linux installer script.

Example:

```text
burpsuite_community_linux_v2025.sh
```

 

### Step 2: Make Executable

```bash
chmod +x burpsuite_community_linux.sh
```

 

### Step 3: Run Installer

Using sudo:

```bash
sudo ./burpsuite_community_linux.sh
```

Without sudo:

```bash
./burpsuite_community_linux.sh
```

 

### Installation Location

If installed without sudo:

```text
~/BurpSuiteCommunity/BurpSuiteCommunity
```

Meaning:

```text
/home/username/BurpSuiteCommunity/BurpSuiteCommunity
```

 

### PATH Consideration

Without sudo:

* Burp Suite is installed locally.
* It is NOT automatically added to PATH.

You may need to launch it manually:

```bash
~/BurpSuiteCommunity/BurpSuiteCommunity
```

 

## macOS

### Step 1: Download

Download the macOS installer from PortSwigger.

### Step 2: Open Installer

Double-click the downloaded file.

### Step 3: Follow Installation Wizard

Accept default options unless customization is required.

### Step 4: Launch

Open Burp Suite from:

```text
Applications → Burp Suite Community Edition
```

 

# Installation Wizard

## Recommended Settings

For beginners, the default settings are usually sufficient.

### Recommended Choices

 Default installation directory

 Default shortcuts

 Default components

 Standard configuration

 

## Best Practice

Always review:

* Installation path
* Permissions requested
* Additional software options

before clicking **Next**.

 

# Verifying Installation

After installation, launch Burp Suite.

If successful, you should see:

```text
Burp Suite Community Edition
```

followed by:

```text
Project Options
Temporary Project
```

on startup.

 

# Common Linux Commands

## Make Installer Executable

```bash
chmod +x burpsuite_community_linux.sh
```

### Explanation

| Part     | Meaning                 |
| -------- | ----------------------- |
| chmod    | Change file permissions |
| +x       | Add execute permission  |
| filename | Installer script        |

 

## Run Installer

```bash
sudo ./burpsuite_community_linux.sh
```

### Explanation

| Part      | Meaning              |
| --------- | -------------------- |
| sudo      | Run as administrator |
| ./        | Current directory    |
| script.sh | Installation script  |

 

# Troubleshooting

## Permission Denied

Error:

```bash
Permission denied
```

Solution:

```bash
chmod +x burpsuite_community_linux.sh
```
 

## Command Not Found

Error:

```bash
burpsuite: command not found
```

Possible Causes:

* Not installed
* Not added to PATH

Solution:

Run directly:

```bash
~/BurpSuiteCommunity/BurpSuiteCommunity
```

-----------


# Burp Suite Initial Setup and Dashboard

## Overview

After installing and launching Burp Suite for the first time, you must complete a simple setup process before accessing the main interface.

This setup only takes a few clicks and prepares Burp Suite for web application testing.


# Launching Burp Suite

## Step 1: Start Burp Suite

Open Burp Suite Community Edition.

When Burp starts for the first time, you will be asked to:

* Accept the License Agreement
* Select a Project Type
* Choose Configuration Settings


# Project Selection

## What is a Project?

A project stores:

* Requests
* Responses
* Scan results
* Configuration settings
* Session information


## Community Edition Setup

In Burp Suite Community Edition, the options are limited.

### Recommended Action

Simply click:

```text
Next
```

to continue.


# Configuration Settings

## Purpose

Burp Suite allows users to load custom configurations.

For beginners and most testing scenarios, the default configuration is sufficient.


## Recommended Option

Select:

```text
Use Burp Defaults
```

Then click:

```text
Start Burp
```


## Why Use Default Settings?

The default configuration already includes:

* Proxy Listener
* Browser Integration
* Standard Interface Layout
* Default Project Settings

These settings work well for most web application assessments.

# Training Screen

## First Launch Experience

Some Burp Suite versions display a training or tutorial screen when launched for the first time.

### Benefits

The training materials help you learn:

* Burp Interface
* Proxy Usage
* Request Interception
* Security Testing Workflows

### Recommendation

Spend some time reviewing these materials if you are new to Burp Suite.


# Burp Dashboard

## What is the Dashboard?

The Dashboard is the central workspace of Burp Suite.

It provides:

* Activity monitoring
* Task management
* Event tracking
* Vulnerability information

At first glance, it may look overwhelming, but it becomes easy to navigate with practice.


# Dashboard Layout

The Dashboard is divided into four main sections.


## 1. Tasks

### Purpose

The Tasks panel manages background tasks performed by Burp Suite.

### Community Edition

By default, Burp runs:

```text
Live Passive Crawl
```

### What Does It Do?

It automatically:

* Records visited pages
* Maps application content
* Tracks browsing activity

### Benefits

Helps build a site map while testing.


### Professional Edition

Additional features include:

* Active vulnerability scans
* On-demand scans
* Automated assessments


## 2. Event Log

### Purpose

Displays activities performed by Burp Suite.

### Examples

* Proxy started
* New connections established
* Requests intercepted
* Extensions loaded

### Why It Matters

Useful for:

* Troubleshooting
* Monitoring activity
* Tracking Burp actions


## 3. Issue Activity

### Purpose

Displays vulnerabilities discovered by Burp's automated scanner.

### Availability

 Not available in Community Edition

 Available in Professional Edition


### Information Displayed

* Vulnerability Name
* Severity
* Confidence Level
* Affected URLs

### Example

```text
High     SQL Injection
Medium   Cross-Site Scripting
Low      Information Disclosure
```


## 4. Advisory

### Purpose

Provides detailed information about detected vulnerabilities.

### Information Included

* Vulnerability Description
* Technical Details
* References
* Remediation Advice

### Example

For SQL Injection:

```text
Description:
Application fails to sanitize user input.

Remediation:
Use parameterized queries.
```

### Community Edition

Since no automated scanner exists:

```text
Advisory Section = Usually Empty
```


# Help Icons

## What Are the Question Mark Icons?

Throughout Burp Suite you will notice:

```text
?
```

icons.


## Purpose

They open context-sensitive help documentation.

### Benefits

Provides:

* Feature explanations
* Usage instructions
* Troubleshooting guidance

### Recommendation

Always check the help icon when learning a new Burp feature.


# Why the Help System is Useful

Instead of searching online every time:

```text
Click ? → Read Explanation → Continue Testing
```

This saves time and improves learning.

----------------


# Burp Suite Navigation

## Overview

Burp Suite provides an organized interface that allows users to quickly switch between different tools (called **modules**) and their settings (called **sub-tabs**).

Understanding the navigation system makes web application testing much faster and more efficient.

# Burp Suite Interface Layout

The Burp Suite interface mainly consists of:

```text
+----------------------------------------------------+
| Main Menu (File, Edit, Project, Window, Help...)   |
+----------------------------------------------------+
| Module Bar (Dashboard | Target | Proxy | ...)      |
+----------------------------------------------------+
| Sub-Tab Bar (Intercept | HTTP History | Options)   |
+----------------------------------------------------+
|                Working Area                         |
+----------------------------------------------------+
```


# 1. Module Selection

## What is a Module?

A **module** is a major tool within Burp Suite that performs a specific security testing task.

Each module has its own functionality.

### Common Modules

* Dashboard
* Target
* Proxy
* Intruder
* Repeater
* Decoder
* Comparer
* Sequencer
* Extender


## Purpose

The **Module Bar** (top navigation bar) lets you switch between Burp Suite's different tools.

### Example

Selecting the **Proxy** module opens all features related to intercepting HTTP/HTTPS traffic.

```text
Dashboard | Target | Proxy | Intruder | Repeater
```

## Why is it Useful?

Allows quick access to different testing tools without leaving the application.


# 2. Sub-Tabs

## What are Sub-Tabs?

Some modules contain additional sections called **sub-tabs**.

These provide more specific features within that module.


## Example

When you open the **Proxy** module, you may see:

```text
Intercept | HTTP History | WebSockets | Options
```

Each sub-tab has a different purpose.


### Proxy → Intercept

Used to:

* Capture requests
* Modify requests
* Forward requests
* Drop requests


### Proxy → HTTP History

Displays every HTTP request and response that passes through Burp Suite.

Useful for:

* Reviewing traffic
* Finding hidden endpoints
* Analyzing application behavior


### Proxy → WebSockets

Used for analyzing WebSocket communication between the client and server.


### Proxy → Options

Contains configuration settings for the Proxy module.

Examples:

* Proxy Listener
* Interception Rules
* Match & Replace Rules


# 3. Detaching Tabs

## What is Tab Detaching?

Burp Suite allows modules or tabs to be opened in separate windows.

This feature is useful when working with multiple tools at the same time.


## Why Use Detached Windows?

Example:

Keep:

* Proxy on one monitor
* Repeater on another monitor

This improves productivity during testing.


## How to Detach a Tab

1. Click **Window** from the application menu.
2. Select **Detach**.
3. The selected tab opens in a separate window.


## Reattaching Tabs

To move the window back into Burp Suite:

1. Open **Window**.
2. Select **Attach** (or the equivalent reattach option).


# Keyboard Shortcuts

## Why Use Shortcuts?

Keyboard shortcuts allow faster navigation between commonly used modules.

Instead of clicking through menus, you can instantly switch tabs.


## Default Shortcuts

| Shortcut             | Opens     |
| -------------------- | --------- |
| **Ctrl + Shift + D** | Dashboard |
| **Ctrl + Shift + T** | Target    |
| **Ctrl + Shift + P** | Proxy     |
| **Ctrl + Shift + I** | Intruder  |
| **Ctrl + Shift + R** | Repeater  |


# Shortcut Explanation

## Ctrl + Shift + D

Opens:

```text
Dashboard
```

Used for:

* Viewing tasks
* Monitoring events
* Checking Burp activity


## Ctrl + Shift + T

Opens:

```text
Target
```

Used for:

* Viewing Site Map
* Managing Scope
* Organizing discovered content


## Ctrl + Shift + P

Opens:

```text
Proxy
```

Used for:

* Intercepting HTTP requests
* Modifying requests
* Viewing HTTP History


## Ctrl + Shift + I

Opens:

```text
Intruder
```

Used for:

* Brute-force attacks
* Fuzzing
* Payload testing


## Ctrl + Shift + R

Opens:

```text
Repeater
```

Used for:

* Modifying requests
* Resending requests
* Manual vulnerability testing


# Navigation Workflow

A typical workflow in Burp Suite might look like:

```text
Dashboard
      ↓
Target
      ↓
Proxy
      ↓
Repeater
      ↓
Intruder
```

Each module supports a different stage of the security testing process.


# Tips for Efficient Navigation

* Learn the keyboard shortcuts for frequently used modules.
* Use **sub-tabs** to access module-specific settings.
* Detach tabs if working with multiple monitors or comparing data side by side.
* Explore the **Window** menu to manage detached tabs.

-------------


# Burp Suite Settings

## Overview

Burp Suite provides a wide range of configuration options that allow you to customize how the application behaves during security testing.

There are **two main types of settings**:

* **User (Global) Settings**
* **Project Settings**

Understanding the difference between them is important because some settings are permanent, while others only apply to the current testing session.
 

# Types of Settings

## 1. User (Global) Settings

### What are User Settings?

User Settings (also called **Global Settings**) affect the **entire Burp Suite installation**.

These settings are automatically loaded every time Burp Suite starts.

### Characteristics

* Apply to all future projects
* Saved permanently
* Available every time Burp is launched

### Examples

* Interface preferences
* Proxy defaults
* Display options
* Keyboard shortcuts
* Default browser configuration

### Best Use

Configure options that you want Burp Suite to remember across all projects.


## 2. Project Settings

### What are Project Settings?

Project Settings only affect the **currently opened project**.

They are intended for configuring settings specific to a particular penetration test.

### Characteristics

* Temporary
* Apply only to the current project
* Can be different for every project

### Community Edition Limitation

Since **Burp Suite Community Edition cannot save projects**, all Project Settings are lost when Burp Suite is closed.

### Examples

* Proxy configuration
* Scope settings
* Session handling rules
* Target-specific options

# User Settings vs Project Settings

| Feature             | User Settings                  | Project Settings               |
| ------------------- | ------------------------------ | ------------------------------ |
| Scope               | Entire Burp Suite installation | Current project only           |
| Saved after restart |  Yes                           | No (Community Edition)         |
| Purpose             | Default configuration          | Project-specific configuration |
| Persistence         | Permanent                      | Temporary                      |


# Opening the Settings Window

## Step 1

Launch Burp Suite.

## Step 2

Click the **Settings** button located in the **top navigation bar**.

```text
Top Navigation
----------------------------------------
Dashboard | Proxy | Target | Settings ⚙
```

## Step 3

A separate **Settings Window** opens.

This window contains all configurable options in Burp Suite.


# Settings Window Layout

The Settings window is divided into two main sections:

```text
+----------------------+---------------------------+
| Navigation Menu      | Settings Panel            |
|                      |                           |
| Search               | Configuration Options     |
| Type Filter          |                           |
| User Settings        |                           |
| Project Settings     |                           |
| Categories           |                           |
+----------------------+---------------------------+
```


# Search

## Purpose

The **Search** feature helps you quickly locate a specific setting.

### Why Use It?

Instead of manually browsing dozens of categories, simply type a keyword.

### Example Searches

```text
Proxy
Certificate
TLS
Intercept
Browser
Theme
```

### Benefit

Saves time when configuring Burp Suite.


# Type Filter

## Purpose

The **Type Filter** allows you to filter settings based on their type.

### Available Filters

* User Settings
* Project Settings

### Benefit

Makes it easier to find only the settings you need.


# User Settings Section

## Purpose

Displays all settings that affect the **entire Burp Suite installation**.

### Examples

* User Interface
* Display Preferences
* Proxy Defaults
* Keyboard Shortcuts

### Best Practice

Use this section for settings that should remain the same across all projects.


# Project Settings Section

## Purpose

Displays settings related only to the **current project**.

### Examples

* Scope
* Sessions
* Proxy Rules
* Logging
* Target Configuration

### Important Note

In **Burp Suite Community Edition**, these settings disappear after closing Burp because projects cannot be saved.


# Categories

## Purpose

Groups settings into logical categories.

Instead of searching manually, you can browse categories such as:

* Proxy
* Target
* Intruder
* Repeater
* Connections
* TLS
* Sessions

### Benefit

Makes navigation much easier when configuring a specific Burp component.


# Settings Shortcuts

## What are Settings Shortcuts?

Many Burp Suite modules provide a shortcut button that opens the Settings window directly to the relevant configuration page.


## Example

Inside the **Proxy** module you will find:

```text
Proxy Settings
```

Clicking this button opens:

```text
Settings
    ↓
Proxy Category
```

instead of opening the main Settings page.

### Benefit

Faster access to frequently used settings.


# Why the Search Feature is Useful

Imagine trying to locate the **TLS Certificate** settings.

Without Search:

```text
Settings
   ↓
Browse Categories
      ↓
Find TLS
```

With Search:

```text
Search
   ↓
Type "TLS"
   ↓
Instant Results
```

The search feature significantly reduces the time spent navigating through settings.


# Best Practices

* Keep **User Settings** for permanent preferences.
* Use **Project Settings** for target-specific configurations.
* Use the **Search** bar to quickly locate options.
* Take advantage of **Settings Shortcuts** inside modules.
* Review settings before starting a penetration test.

-------------

# Burp Proxy

## Overview

The **Burp Proxy** is the **core component** of Burp Suite and one of the most important tools used during **web application penetration testing**.

It acts as an **intermediary (proxy)** between your browser and the target web server, allowing you to intercept, inspect, modify, and forward HTTP/HTTPS requests and responses.


# How Burp Proxy Works

Normally, a browser communicates directly with a web server.

```text
Browser  ───────────────►  Web Server
```

When Burp Proxy is enabled, the traffic passes through Burp Suite first.

```text
Browser
     │
     ▼
Burp Proxy
     │
     ▼
Web Server
```

This gives you complete control over the communication before it reaches the server.

# Why Use Burp Proxy?

Burp Proxy allows security testers to:

* Capture HTTP/HTTPS requests
* Inspect request contents
* Modify request parameters
* Forward requests manually
* Drop unwanted requests
* Analyze server responses
* Send requests to other Burp tools


# Intercepting Requests

## What is Request Interception?

When **Intercept** is enabled, every request sent by your browser is **paused** before reaching the web server.

Instead of going directly to the server, the request appears in the **Proxy → Intercept** tab.

```text
Browser
     │
     ▼
Burp Proxy (Intercept)
     │
     ✖ Waiting...
```

This allows you to inspect and modify the request.


## Available Actions

Once a request is intercepted, you can:

### Forward

Sends the request to the web server.

```text
Browser
     │
     ▼
Burp Proxy
     │
     ▼
Web Server
```

**Use Case**

Continue normal browsing after inspecting the request.

### Drop

Deletes the intercepted request.

The server never receives it.

```text
Browser
     │
     ▼
Burp Proxy
     │
   Request Dropped 
```

**Use Case**

* Testing error handling
* Blocking unwanted requests


### Edit

Modify any part of the request before forwarding it.

Example:

Original Request

```http
GET /profile?id=1 HTTP/1.1
```

Modified Request

```http
GET /profile?id=2 HTTP/1.1
```

**Use Case**

* Parameter manipulation
* Authentication testing
* SQL Injection testing
* IDOR testing

### Send to Other Modules

Instead of forwarding immediately, the request can be sent to:

* Repeater
* Intruder
* Comparer
* Decoder

for further analysis.


# Intercept Toggle

At the top of the Intercept tab you will see:

```text
Intercept is on
```


## Intercept ON

Requests stop inside Burp.

You manually decide what happens next.

```text
Browser
     │
     ▼
Burp (Paused)
```


## Intercept OFF

Requests pass through Burp automatically.

Traffic is still captured and logged.

```text
Browser
     │
     ▼
Burp
     │
     ▼
Server
```

No manual intervention is required.


# Taking Control of Web Traffic

The Burp Proxy gives testers complete control over HTTP communication.

You can:

* Change URLs
* Modify cookies
* Edit headers
* Change request methods
* Modify POST data
* Remove parameters
* Add parameters

This is one of the main reasons Burp Suite is so powerful.


# Request Logging

## Automatic Logging

Even if **Intercept** is turned **OFF**, Burp still records every request.

This allows you to review traffic later.


## Benefits

You don't need to intercept every request manually.

Burp automatically builds a history of all communication.


# HTTP History

## What is HTTP History?

The **HTTP History** tab stores every HTTP request and response that passes through Burp Proxy.


### Information Stored

* URL
* Method (GET, POST, etc.)
* Status Code
* Host
* MIME Type
* Request
* Response

### Uses

* Review previous requests
* Replay requests
* Find hidden endpoints
* Analyze application behavior


# WebSocket History

## What are WebSockets?

WebSockets allow **real-time, two-way communication** between a client and server without repeatedly creating new HTTP requests.

Examples include:

* Chat applications
* Live notifications
* Online games
* Stock market dashboards


## Burp Support

Burp Proxy automatically captures WebSocket traffic.

You can inspect:

* Messages
* Frames
* Payloads


# Proxy Settings

Click:

```text
Proxy Settings
```

to configure Burp Proxy behavior.


# Important Proxy Settings

## 1. Response Interception

### Default Behavior

Burp only intercepts **requests**.

Responses pass directly back to the browser.


### Enable Response Interception

You can configure Burp to intercept responses as well.

```text
Browser
     │
     ▼
Request
     │
     ▼
Server
     │
Response
     ▼
Burp (Intercept Response)
     ▼
Browser
```


### Why Use It?

Useful for:

* Viewing server responses
* Modifying HTML
* Testing client-side security
* Debugging


# 2. Match and Replace

## What is Match and Replace?

Automatically modifies requests or responses using predefined rules.

Instead of manually editing every request, Burp performs the changes automatically.


## Example 1

Replace one User-Agent with another.

Original

```http
User-Agent: Chrome
```

Automatically becomes

```http
User-Agent: Firefox
```

## Example 2

Replace cookies.

Original

```http
Cookie: user=guest
```

Automatically becomes

```http
Cookie: user=admin
```

## Uses

* Change User-Agent
* Modify Cookies
* Replace Headers
* Modify Parameters
* Testing Input Validation


## Regular Expressions (Regex)

Match and Replace supports **Regular Expressions (Regex)**.

Regex allows matching patterns instead of exact text.

Example:

```text
session=[A-Za-z0-9]+
```

Matches:

```text
session=abc123
session=xyz987
session=qwerty45
```

# Burp Proxy Workflow

```text
Browser
      │
      ▼
Burp Proxy
      │
      ├── Intercept
      ├── Edit
      ├── Drop
      ├── Forward
      ├── Send to Repeater
      ├── Send to Intruder
      └── Log Traffic
      │
      ▼
Target Server
```


# Best Practices

* Keep **Intercept OFF** during normal browsing.
* Enable **Intercept** only when you want to inspect or modify requests.
* Use **HTTP History** to review previous requests instead of intercepting everything.
* Send interesting requests to **Repeater** for manual testing.
* Use **Match and Replace** to automate repetitive modifications.

-------

# Configuring Burp Suite Proxy with FoxyProxy (Firefox)

## Overview

To intercept web traffic using **Burp Suite**, your web browser must send all HTTP/HTTPS requests through Burp Suite instead of directly to the web server.

This is achieved by configuring a **proxy** in the browser. In Firefox, the easiest way is to use the **FoxyProxy** extension.

> **Note:** If you are using the **TryHackMe AttackBox**, **FoxyProxy is already installed**.


# What is FoxyProxy?

## Definition

**FoxyProxy** is a Firefox browser extension that allows you to easily switch between different proxy configurations.

Instead of manually changing Firefox's network settings each time, you can enable or disable a proxy with a single click.


## Why Use FoxyProxy?

Without FoxyProxy:

```text
Firefox
    ↓
Manual Network Settings
    ↓
Edit Proxy Every Time
```

With FoxyProxy:

```text
Firefox
     ↓
Click FoxyProxy Icon
     ↓
Enable / Disable Proxy
```

### Benefits

* Quick proxy switching
* Easy configuration
* No manual browser settings
* Ideal for penetration testing


# Network Flow

### Without Burp Proxy

```text
Browser
     │
     ▼
Target Web Server
```

Traffic goes directly to the website.



### With Burp Proxy

```text
Browser
     │
     ▼
FoxyProxy
     │
     ▼
Burp Suite (127.0.0.1:8080)
     │
     ▼
Target Web Server
```

Now every request passes through Burp Suite.


# Step 1 – Install FoxyProxy

If using your own Firefox installation:

Install the **FoxyProxy Basic** extension from the Firefox Add-ons store.

> **AttackBox Users:** Skip this step because FoxyProxy is pre-installed.


# Step 2 – Open FoxyProxy

Click the **FoxyProxy icon** in the upper-right corner of Firefox.

This opens the proxy management menu.


# Step 3 – Open FoxyProxy Options

Click:

```text
Options
```

This opens the FoxyProxy configuration page in a new browser tab.


# Step 4 – Add a New Proxy

Click:

```text
Add
```

to create a new proxy profile.


# Step 5 – Configure Burp Proxy

Fill in the following values:

| Setting      | Value     |
| ------------ | --------- |
| **Title**    | Burp      |
| **Proxy IP** | 127.0.0.1 |
| **Port**     | 8080      |


## Explanation of Each Value

### Title

```text
Burp
```

A friendly name for your proxy profile.

You may use any name.


### Proxy IP

```text
127.0.0.1
```

#### What is 127.0.0.1?

This is the **localhost** (loopback) address.

It tells Firefox:

> "Send traffic to the Burp Suite running on this same computer."


### Port

```text
8080
```

#### Why Port 8080?

By default, Burp Suite listens for browser traffic on **TCP port 8080**.

Browser traffic sent to:

```text
127.0.0.1:8080
```

will be received by Burp Suite.


# Step 6 – Save Configuration

Click:

```text
Save
```

Your Burp proxy profile is now created.


# Step 7 – Activate the Proxy

Click the FoxyProxy icon again.

Select:

```text
Burp
```

Firefox now routes all traffic through Burp Suite.


# Browser Traffic Flow

Once activated:

```text
Firefox
      │
      ▼
127.0.0.1:8080
      │
      ▼
Burp Suite
      │
      ▼
Target Website
```


# Step 8 – Enable Intercept

Open Burp Suite.

Navigate to:

```text
Proxy
      ↓
Intercept
```

Ensure the button displays:

```text
Intercept is ON
```

This means Burp will pause requests before forwarding them.


# Step 9 – Test the Proxy

Open Firefox.

Visit the target website.

Example:

```text
http://<Target-IP>/
```

Instead of loading immediately:

* Firefox appears to "hang"
* Burp Suite captures the request

Example intercepted request:

```http
GET / HTTP/1.1
Host: target-ip
User-Agent: Mozilla/5.0
```

Congratulations! You have successfully intercepted your first HTTP request.


# Why Does the Browser Hang?

When **Intercept** is ON:

```text
Browser
     │
     ▼
Burp Suite
     │
Waiting...
```

Burp pauses the request.

The browser waits until you decide what to do.


# Available Actions

When a request is intercepted, you can:

### Forward

Send the request to the server.

```text
Browser
     │
     ▼
Burp
     │
Forward
     ▼
Server
```


### Drop

Delete the request.

The server never receives it.

### Edit

Modify:

* URL
* Parameters
* Cookies
* Headers
* Request Body

before forwarding.


### Send to Other Tools

You can send requests to:

* Repeater
* Intruder
* Decoder
* Comparer

for further analysis.

# Right-Click Menu

Right-clicking an intercepted request provides quick access to many actions.

Common options include:

* Send to Repeater
* Send to Intruder
* Send to Decoder
* Send to Comparer
* Copy URL
* Copy Request
* Save Request

This saves time during testing.

# Important Notes

## Intercept ON

```text
Browser
     │
     ▼
Burp
     │
Waiting...
```

Every request pauses.

## Intercept OFF

```text
Browser
     │
     ▼
Burp
     │
     ▼
Server
```

Traffic flows automatically while still being logged in **HTTP History**.

## Remember

Leaving **Intercept ON** accidentally can make your browser appear frozen because every request waits for your approval.

If browsing stops unexpectedly, check whether **Intercept** is enabled.

# WebSocket Requests

If other browser tabs are open, Burp may intercept WebSocket traffic instead of requests to your target application.

### Recommendation

Before beginning a lab:

* Close unnecessary tabs.
* Keep only the target website open.

This reduces background traffic and makes intercepted requests easier to analyze.

# Best Practices

* Enable FoxyProxy only when testing.
* Keep Burp running while FoxyProxy is enabled.
* Turn **Intercept OFF** after capturing the request you need.
* Use **HTTP History** to review previous traffic.
* Close unnecessary browser tabs before testing.

-------------

# Burp Suite Target Tab

## Overview

The **Target** tab is one of the most useful modules in Burp Suite. While many users think it is only for defining the testing scope, it also helps you:

* Discover website pages
* Build a site map automatically
* View discovered API endpoints
* Manage testing scope
* Learn about common web vulnerabilities

The Target tab contains **three sub-tabs**:

* **Site Map**
* **Issue Definitions**
* **Scope Settings**


# Target Tab Structure

```text
Target
│
├── Site Map
├── Issue Definitions
└── Scope Settings
```

# 1. Site Map

## What is the Site Map?

The **Site Map** automatically records every webpage and resource you visit while your browser traffic passes through Burp Proxy.

Instead of manually documenting pages, Burp builds a tree structure of the target website.

## How It Works

When Burp Proxy is active:

```text
Browser
      │
      ▼
Burp Proxy
      │
      ▼
Target Website
```

Every request is automatically added to the Site Map.


## Example

Suppose you browse:

```text
/
```

Then:

```text
/login
```

Then:

```text
/dashboard
```

Then:

```text
/profile
```

The Site Map becomes:

```text
example.com
│
├── /
├── /login
├── /dashboard
└── /profile
```


## Information Stored

Each endpoint includes:

* URL
* Request
* Response
* Status Code
* Parameters
* Headers


## Why is it Useful?

The Site Map helps testers:

* Discover hidden pages
* Understand website structure
* Identify APIs
* Locate admin panels
* Find upload pages
* Review previously visited pages


## API Discovery

One major advantage is **API enumeration**.

If a webpage communicates with an API like:

```text
/api/login
/api/profile
/api/users
```

those endpoints are automatically added to the Site Map.

This makes API testing much easier.


## Burp Professional Feature

Burp Suite Professional can automatically crawl websites.

Crawler:

```text
Homepage
     │
     ▼
Discovers Links
     │
     ▼
Visits Pages
     │
     ▼
Updates Site Map
```
## Community Edition

Although automatic crawling is unavailable, the Site Map is still populated while you manually browse the application.


# 2. Issue Definitions

## What are Issue Definitions?

Burp Suite Community does **not** include the automated vulnerability scanner found in Burp Suite Professional.

However, it still includes a library of vulnerability descriptions.


## Purpose

Issue Definitions provide:

* Vulnerability descriptions
* Risk information
* Technical explanations
* References
* Suggested remediation


## Example Vulnerabilities

You may find information about:

* SQL Injection
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Directory Traversal
* XML External Entity (XXE)
* Remote Code Execution (RCE)

## Why is it Useful?

Issue Definitions help you:

* Understand vulnerabilities
* Write penetration testing reports
* Learn web security concepts
* Reference official descriptions


## Example

If you discover an SQL Injection manually:

Instead of writing your own explanation,

you can use Burp's Issue Definition as a reference.


# 3. Scope Settings

## What is Scope?

The **Scope** determines which websites Burp Suite should focus on during testing.


## Why Use Scope?

Without a scope:

Burp captures traffic from:

* Google
* Firefox updates
* Background browser requests
* Extensions
* Target application

Result:

```text
Too Much Noise
```


With Scope enabled:

```text
Target Website Only
```

Burp ignores unrelated traffic.


## Example

Include:

```text
example.com
```

Exclude:

```text
google.com
```

Burp will only capture:

```text
example.com/*
```


## Benefits

* Cleaner Site Map
* Easier Traffic Analysis
* Faster Testing
* Better Organization


# Practical Workflow

Typical workflow:

```text
Start Burp
      │
      ▼
Enable Proxy
      │
      ▼
Browse Website
      │
      ▼
Target → Site Map
      │
      ▼
Review Pages
      │
      ▼
Analyze Interesting Endpoints
```

# Site Map Challenge

## Objective

Browse the entire target website.

Visit:

* Homepage
* Every linked page

Then open:

```text
Target
     ↓
Site Map
```

Look for an endpoint that appears unusual.


## Why?

Sometimes applications expose:

* Hidden files
* Backup files
* Debug pages
* API endpoints
* Configuration files

These often stand out in the Site Map.


## Next Step

Open the unusual endpoint.

You can:

* Visit it directly in Firefox

OR

* View its response inside Burp:

```text
Target
     ↓
Site Map
     ↓
Select Endpoint
     ↓
Response
```


# Best Practices

* Always browse the entire application before testing.
* Review the Site Map for hidden content.
* Set the Scope to reduce unnecessary traffic.
* Use Issue Definitions when documenting vulnerabilities.
* Pay attention to unusual file names and API endpoints.

---
