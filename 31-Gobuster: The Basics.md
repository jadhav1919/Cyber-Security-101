# Gobuster Overview

## Overview

**Gobuster** is a fast, open-source command-line tool written in **Go (Golang)** that performs **content enumeration** by brute-forcing targets with a **wordlist**.

It is widely used by penetration testers, bug bounty hunters, and security professionals to discover hidden resources that are not directly linked on a website.


# What is Gobuster?

Gobuster is an **enumeration tool** that discovers hidden resources by sending requests generated from a wordlist.

It can enumerate:

* Web directories
* Files
* DNS subdomains
* Virtual Hosts (vHosts)
* Amazon S3 buckets
* Google Cloud Storage buckets
* TFTP servers
* Fuzzable parameters


# Where Does Gobuster Fit in Ethical Hacking?

Gobuster is mainly used during the **Reconnaissance** and **Scanning** phases.

```text
Reconnaissance
       │
       ▼
Enumeration (Gobuster)
       │
       ▼
Scanning
       │
       ▼
Exploitation
       │
       ▼
Post Exploitation
```

### Explanation

* **Reconnaissance** → Gather target information.
* **Enumeration** → Discover hidden directories, files, subdomains, and services.
* **Scanning** → Analyze discovered resources for vulnerabilities.
  
# Enumeration

## Definition

**Enumeration** is the process of identifying and listing all available resources on a target system.

These resources may or may not be publicly accessible.

### Examples

A website may contain:

```text
/
├── /login
├── /admin
├── /uploads
├── /backup
└── /config
```

Even if only `/` is linked on the homepage, Gobuster can discover the hidden directories.


# Brute Force

## Definition

A **brute-force** attack systematically tries every possibility until a match is found.

Gobuster uses this technique with **wordlists**.

### Simple Analogy

Imagine having **10 keys** and trying each one in a locked door.

```text
Key 1 
Key 2 
Key 3 
Key 4 
```

Gobuster does the same with directory names, file names, or subdomains.


# How Gobuster Works

```text
Wordlist
     │
     ▼
Gobuster
     │
     ▼
Target Website
     │
     ▼
Hidden Resources Found
```

For every word in the wordlist, Gobuster creates a request.

Example wordlist:

```text
admin
images
backup
uploads
```

Requests sent:

```text
http://example.com/admin
http://example.com/images
http://example.com/backup
http://example.com/uploads
```

# Gobuster Help

Display the help page:

```bash
gobuster --help
```

### Explanation

| Part       | Meaning                                 |
| ---------- | --------------------------------------- |
| `gobuster` | Launches Gobuster                       |
| `--help`   | Displays available commands and options |


# Help Page Sections

## 1. Usage

Shows the general command syntax.

Example:

```text
gobuster [command]
```

## 2. Available Commands

Each command performs a different type of enumeration.

### `dir`

Directory and file enumeration.

Example:

```text
/admin
/uploads
/images
```


### `dns`

Subdomain enumeration.

Example:

```text
blog.example.com
mail.example.com
dev.example.com
```


### `vhost`

Virtual Host (vHost) enumeration.

Example:

```text
shop.example.com
api.example.com
test.example.com
```


### `fuzz`

Fuzzes URLs, headers, or request bodies by replacing the keyword `FUZZ`.

Example:

```text
http://example.com/FUZZ
```


### `gcs`

Enumerates Google Cloud Storage buckets.

### `s3`

Enumerates Amazon S3 buckets.

### `tftp`

Enumerates TFTP resources.

### `version`

Displays the installed Gobuster version.


# Common Flags

Flags customize how Gobuster runs.


## `-t` / `--threads`

### Purpose

Sets the number of concurrent threads.

Example:

```bash
-t 64
```

### Explanation

More threads mean more requests are sent simultaneously.

```text
Thread 1
Thread 2
Thread 3
...
Thread 64
```

### Benefit

* Faster scans.

### Drawback

* Higher resource usage.
* May trigger rate limiting or detection.


## `-w` / `--wordlist`

### Purpose

Specifies the wordlist used during enumeration.

Example:

```bash
-w /usr/share/wordlists/dirb/small.txt
```

### Explanation

Gobuster reads each line from the file and appends it to the target URL.

Example:

Wordlist:

```text
admin
images
backup
```

Requests:

```text
/admin
/images
/backup
```

## `--delay`

### Purpose

Adds a delay between requests.

Example:

```bash
--delay 1s
```

### Why Use It?

Some servers detect rapid requests.

Adding a delay makes enumeration appear more like normal user activity.


## `--debug`

### Purpose

Displays detailed debugging information.

Useful for:

* Troubleshooting
* Configuration errors
* Unexpected responses

## `-o` / `--output`

### Purpose

Writes scan results to a file.

Example:

```bash
-o results.txt
```

Useful for:

* Documentation
* Later analysis
* Reporting


----------
# Gobuster `dir` Mode (Directory & File Enumeration)

## Overview

The **`dir` mode** in Gobuster is used to discover **hidden directories and files** on a web server by performing **wordlist-based enumeration**.

Many websites follow common directory structures, making it possible to find hidden resources by trying directory and file names from a wordlist.


# What is `dir` Mode?

The `dir` mode tells Gobuster to enumerate:

* Directories
* Files
* Hidden web content

It works by appending each word from a wordlist to the target URL and checking the server's response.

 
# Why is Directory Enumeration Important?

Many sensitive resources are not linked on the website.

Example website:

```text
http://example.thm/
```

Visible:

```text
/
```

Hidden:

```text
/admin
/uploads
/backup
/config
/login
```

Gobuster helps discover these hidden paths.


# Example Website Structure

A typical **WordPress** installation looks like:

```text
html/
└── wordpress/
    ├── wp-admin
    ├── wp-content
    └── wp-includes
```

### Explanation

| Directory     | Purpose                        |
| ------------- | ------------------------------ |
| `wp-admin`    | WordPress administration panel |
| `wp-content`  | Themes, plugins, uploads       |
| `wp-includes` | Core WordPress files           |

Gobuster can discover these directories even if they are not linked on the homepage.


# How Gobuster Works

```text
Wordlist
      │
      ▼
Gobuster
      │
      ▼
Target Website
      │
      ▼
Checks Response
      │
      ▼
Displays Existing Directories
```

Example wordlist:

```text
admin
uploads
backup
images
```

Gobuster tests:

```text
http://example.thm/admin
http://example.thm/uploads
http://example.thm/backup
http://example.thm/images
```


# Gobuster `dir` Help

Display all options:

```bash
gobuster dir --help
```

This shows all available flags for directory enumeration.


# Commonly Used Flags

## `-c` / `--cookies`

### Purpose

Adds a cookie to every request.

Example:

```bash
-c "PHPSESSID=abcdef123456"
```

### Why Use It?

Some directories are only accessible after authentication.


## `-x` / `--extensions`

### Purpose

Searches for files with specific extensions.

Example:

```bash
-x php,js,txt
```

Gobuster checks:

```text
index.php
login.php
admin.js
config.txt
```


## `-H` / `--headers`

### Purpose

Adds custom HTTP headers.

Example:

```bash
-H "Authorization: Bearer TOKEN"
```

Useful when the application requires authentication headers.


## `-k` / `--no-tls-validation`

### Purpose

Ignores HTTPS certificate validation.

Useful when testing:

* Self-signed certificates
* CTF environments
* Lab machines

Example:

```bash
-k
```


## `-n` / `--no-status`

### Purpose

Hides HTTP status codes from the output.

Produces cleaner output.


## `-U` / `--username`

### Purpose

Specifies a username for authenticated requests.

Example:

```bash
-U admin
```

## `-P` / `--password`

### Purpose

Specifies the corresponding password.

Example:

```bash
-P password123
```

Used together with `-U`.


## `-s` / `--status-codes`

### Purpose

Shows only selected HTTP status codes.

Example:

```bash
-s 200
```

or

```bash
-s 200,301,302
```

Useful when filtering valid responses.


## `-b` / `--status-codes-blacklist`

### Purpose

Hides specific status codes.

Example:

```bash
-b 404
```

Commonly used to suppress "Not Found" responses.

> **Note:** This option overrides `-s`.


## `-r` / `--followredirect`

### Purpose

Automatically follows HTTP redirects.

Example:

```bash
-r
```

Useful when the server responds with:

```text
301 Moved Permanently
302 Found
```

Instead of stopping, Gobuster follows the redirect and continues.



# Basic Syntax

```bash
gobuster dir -u http://example.thm -w /path/to/wordlist
```


# Required Options

## `dir`

Enables **directory enumeration mode**.


## `-u`

Specifies the target URL.

Example:

```bash
-u http://example.thm
```


## `-w`

Specifies the wordlist.

Example:

```bash
-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

# Complete Example

```bash
gobuster dir -u http://www.example.thm -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r
```

# Command Breakdown

## `gobuster dir`

Use directory enumeration mode.


## `-u http://www.example.thm`

Target website.

Gobuster begins scanning from the specified path.

Example:

```text
http://www.example.thm/
```

### Can the URL include a directory?

Yes.

Example:

```text
http://www.example.thm/resources
```

Gobuster will only enumerate inside:

```text
/resources
```

### Why must the protocol be included?

Correct:

```text
http://example.thm
https://example.thm
```

Incorrect:

```text
example.thm
```

Gobuster requires the protocol to determine how to connect.


### IP Address vs Hostname

Using an IP:

```text
http://192.168.1.10
```

Using a hostname:

```text
http://example.thm
```

**Recommendation:** Use the **hostname** whenever possible.

### Why?

A single IP address can host multiple websites using **Virtual Hosting (vHosts)**.

Using the hostname ensures Gobuster scans the intended website.


# Important Limitation

Gobuster **does not scan recursively**.

Example:

Gobuster discovers:

```text
/admin
```

It **will not automatically** continue scanning inside:

```text
/admin/
```

You must run a second scan:

```bash
gobuster dir -u http://example.thm/admin -w wordlist.txt
```


# Enumerating File Extensions

Gobuster can search for specific file types.

Example:

```bash
gobuster dir -u http://example.thm -w wordlist.txt -x php,js
```


### What Happens?

Wordlist:

```text
admin
login
config
```

Gobuster checks:

```text
/admin
/admin.php
/admin.js

/login
/login.php
/login.js

/config
/config.php
/config.js
```

This helps discover hidden application files.


# Scan Workflow

```text
Target URL
      │
      ▼
Wordlist
      │
      ▼
Append Word
      │
      ▼
Send HTTP Request
      │
      ▼
Receive Status Code
      │
      ▼
Display Valid Results
```


# Common HTTP Status Codes

| Status Code | Meaning               | Why It Matters                    |
| ----------- | --------------------- | --------------------------------- |
| **200**     | OK                    | Resource exists                   |
| **301**     | Moved Permanently     | Redirect found                    |
| **302**     | Found                 | Temporary redirect                |
| **403**     | Forbidden             | Resource exists but access denied |
| **404**     | Not Found             | Resource does not exist           |
| **500**     | Internal Server Error | Server-side error                 |


# Best Practices

* Use the hostname instead of the IP when possible.
* Include the correct protocol (`http://` or `https://`).
* Start with a small wordlist for quick reconnaissance.
* Use `-x` when looking for common file types.
* Follow redirects with `-r` if appropriate.
* Re-scan interesting directories manually because Gobuster is not recursive.

---
