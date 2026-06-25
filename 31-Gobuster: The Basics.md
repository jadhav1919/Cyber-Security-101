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

-------------

# Gobuster `dns` Mode (Subdomain Enumeration)

## Overview

The **`dns` mode** in Gobuster is used to discover **subdomains** of a target domain through **DNS brute forcing**.

Organizations often host multiple applications or services on different subdomains. Even if the main website is secure, another subdomain may still contain vulnerabilities, making subdomain enumeration an essential step during web application reconnaissance.

> **Example:** A company may secure `example.thm`, but `dev.example.thm` or `shop.example.thm` could still expose sensitive information or outdated software.


# What is a Subdomain?

A **subdomain** is an extension of a main domain used to organize different services or applications.

Example:

```text
example.thm              ← Main Domain
│
├── www.example.thm
├── mail.example.thm
├── shop.example.thm
├── blog.example.thm
└── api.example.thm
```

### Explanation

| Subdomain | Purpose                |
| --------- | ---------------------- |
| **www**   | Main website           |
| **mail**  | Email services         |
| **shop**  | E-commerce application |
| **blog**  | Company blog           |
| **api**   | API endpoints          |

Each subdomain can host a completely different application.


# Why Enumerate Subdomains?

Finding subdomains can reveal:

* Hidden applications
* Development servers
* Staging environments
* Admin portals
* APIs
* Legacy systems

Sometimes these systems are less secure than the primary website.

Example:

```text
example.thm
```

Secure website.

However,

```text
dev.example.thm
```

may contain:

* Default credentials
* Debug pages
* Old software
* Sensitive files

This is why subdomain enumeration is an important part of reconnaissance.


# How Gobuster `dns` Works

Gobuster reads each entry from a wordlist and prepends it to the target domain.

```text
Wordlist
     │
     ▼
Gobuster
     │
     ▼
DNS Server
     │
     ▼
Checks if Subdomain Exists
```

Example wordlist:

```text
www
mail
shop
admin
api
```

Gobuster queries:

```text
www.example.thm
mail.example.thm
shop.example.thm
admin.example.thm
api.example.thm
```

If the DNS server returns an IP address, Gobuster reports the subdomain.


# View Help

Display all available options:

```bash
gobuster dns --help
```

This shows every available flag for DNS enumeration.


# Important Flags

## `-d` / `--domain`

Specifies the target domain.

### Syntax

```bash
-d example.thm
```

Gobuster appends every word from the wordlist before this domain.

Example:

```text
admin + example.thm
```

becomes:

```text
admin.example.thm
```


## `-w`

Specifies the wordlist.

Example:

```bash
-w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```

Gobuster reads each word and generates DNS queries.


## `-i` / `--show-ips`

Displays the IP address associated with each discovered subdomain.

Example:

```bash
-i
```

Output:

```text
shop.example.thm     192.168.1.15
```

Useful when identifying which server hosts a particular subdomain.


## `-c` / `--show-cname`

Displays the **Canonical Name (CNAME)** record.

A **CNAME** points one domain name to another domain name.

Example:

```text
shop.example.thm
      │
      ▼
store.example.net
```

Instead of pointing directly to an IP address, the subdomain points to another hostname.

> **Note:** `--show-cname` cannot be used together with `--show-ips`.


## `-r` / `--resolver`

Uses a custom DNS server.

Example:

```bash
-r 8.8.8.8
```

Instead of using the system DNS server, Gobuster sends DNS requests to the specified resolver.

Useful in:

* Labs
* Internal networks
* Custom DNS environments


# Basic Syntax

```bash
gobuster dns -d example.thm -w /path/to/wordlist
```


# Required Parameters

## `dns`

Enables DNS subdomain enumeration mode.


## `-d`

Specifies the target domain.

Example:

```bash
-d example.thm
```

Gobuster will enumerate subdomains under:

```text
example.thm
```


## `-w`

Specifies the wordlist.

Example:

```bash
-w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```

Each entry becomes a DNS query.


# Complete Example

```bash
gobuster dns \
-d example.thm \
-w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```

### What this command does

* Uses DNS enumeration mode.
* Targets `example.thm`.
* Reads subdomain names from the specified wordlist.
* Sends DNS queries for each entry.
* Displays discovered subdomains.

# How Gobuster Generates Queries

Suppose the wordlist contains:

```text
www
shop
academy
primary
```

Gobuster automatically creates:

```text
www.example.thm
shop.example.thm
academy.example.thm
primary.example.thm
```

Each hostname is sent to the DNS server.

# Sample Output

```text
=================================================
Starting gobuster in DNS enumeration mode
=================================================

Found: www.example.thm
Found: shop.example.thm
Found: academy.example.thm
Found: primary.example.thm

=================================================
Finished
=================================================
```

### Explanation

Gobuster successfully discovered four valid subdomains:

* `www.example.thm`
* `shop.example.thm`
* `academy.example.thm`
* `primary.example.thm`

Each of these should be investigated further because they may host separate web applications.


# DNS Enumeration Workflow

```text
Target Domain
      │
      ▼
Wordlist
      │
      ▼
Gobuster
      │
      ▼
Generate DNS Queries
      │
      ▼
DNS Server
      │
      ▼
Existing Subdomains Found
```


# Best Practices

* Use large, high-quality subdomain wordlists for better coverage.
* Investigate every discovered subdomain separately.
* Display IP addresses using `-i` when mapping infrastructure.
* Use a custom DNS resolver (`-r`) when working in labs or internal environments.
* Remember that different subdomains may host completely different applications.

--------------

# Gobuster `vhost` Mode (Virtual Host Enumeration)

## Overview

The **`vhost` mode** in Gobuster is used to discover **Virtual Hosts (vHosts)** hosted on the same web server.

A single web server can host multiple websites using the **same IP address**. Instead of relying on different IP addresses, the web server determines which website to serve based on the **Host** header in the HTTP request.

Gobuster brute-forces this **Host** header to discover hidden virtual hosts.

> **Example:** A server with IP `192.168.1.10` may host:
>
> * `www.example.thm`
> * `blog.example.thm`
> * `shop.example.thm`
> * `admin.example.thm`

Although all websites share the **same IP**, they are different websites.

  
# Virtual Host vs Subdomain

Many beginners confuse **Virtual Hosts** with **Subdomains**, but they are not the same.

| Virtual Host                                           | Subdomain                         |
| ------------------------------------------------------ | --------------------------------- |
| Configured on the **Web Server** (Apache, Nginx, IIS). | Configured in the **DNS Server**. |
| Uses the **HTTP Host header**.                         | Uses **DNS records**.             |
| Multiple websites can share one IP.                    | Requires DNS resolution.          |
| Found using **Gobuster vhost**.                        | Found using **Gobuster dns**.     |

  

# Example

Imagine a web server with IP:

```text
192.168.1.20
```

The server hosts:

```text
www.example.thm
blog.example.thm
shop.example.thm
admin.example.thm
```

All of them point to:

```text
192.168.1.20
```

The web server decides which website to display by reading:

```http
Host: blog.example.thm
```

or

```http
Host: shop.example.thm
```

  

# Difference Between `dns` and `vhost`

## Gobuster DNS Mode

```text
Wordlist
     │
     ▼
DNS Query
     │
     ▼
DNS Server
     │
     ▼
Returns IP Address
```

Gobuster asks:

> Does `blog.example.thm` exist in DNS?

 

## Gobuster vHost Mode

```text
Wordlist
     │
     ▼
HTTP Request
     │
     ▼
Host Header Changes
     │
     ▼
Web Server
```

Gobuster asks:

> Does the web server respond differently if I send:

```http
Host: blog.example.thm
```

  
# View Help

Display all available options:

```bash
gobuster vhost --help
```

This displays every flag supported by the Virtual Host enumeration mode.

 
# Important Flags

## `-u` / `--url`

Specifies the target web server.

Example

```bash
-u http://10.10.10.15
```

Gobuster sends requests to this server.

 

## `-w`

Specifies the wordlist.

Example

```bash
-w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```

Each word becomes a possible virtual host.

 

## `--domain`

Specifies the base domain.

Example

```bash
--domain example.thm
```

Gobuster combines every word with this domain.

Example

```text
blog
```

becomes

```text
blog.example.thm
```

 

## `--append-domain`

Automatically appends the domain to every wordlist entry.

Without this option:

```text
blog
shop
admin
```

Gobuster sends:

```http
Host: blog
Host: shop
Host: admin
```

These are invalid hostnames.

With:

```bash
--append-domain
```

Gobuster sends:

```http
Host: blog.example.thm
Host: shop.example.thm
Host: admin.example.thm
```

This produces valid requests.

 

## `-m` / `--method`

Specifies the HTTP method.

Example

```bash
-m GET
```

or

```bash
-m POST
```

Normally, **GET** is sufficient.

 

## `--exclude-length`

Filters responses based on response size.

Example

```bash
--exclude-length 250-320
```

Responses whose body size falls between **250** and **320 bytes** will be ignored.

Useful for removing false positives.

 
## `-r` / `--follow-redirect`

Automatically follows HTTP redirects.

Useful when virtual hosts redirect users to another page.

 

# Basic Syntax

```bash
gobuster vhost \
-u http://example.thm \
-w /path/to/wordlist
```

 

# Complete Example

```bash
gobuster vhost \
-u http://10.48.142.170 \
--domain example.thm \
-w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt \
--append-domain \
--exclude-length 250-320
```

 

# Breaking Down the Command

## `gobuster vhost`

Uses Virtual Host enumeration mode.

 

## `-u http://10.48.142.170`

Specifies the target web server.

Gobuster connects directly to:

```text
10.48.142.170
```

 

## `--domain example.thm`

Appends:

```text
example.thm
```

to every word.

Example:

```text
blog
```

becomes

```text
blog.example.thm
```

 

## `-w`

Specifies the wordlist used for brute forcing.

Example entries:

```text
www
shop
academy
blog
```

## `--append-domain`

Ensures Gobuster creates valid hostnames.

Without it:

```http
Host: blog
```

With it:

```http
Host: blog.example.thm
```


## `--exclude-length 250-320`

Filters pages whose response size falls between:

```text
250
```

and

```text
320
```

This removes many false positives.


# How Gobuster Changes the Host Header

Suppose the wordlist contains:

```text
www
shop
academy
blog
```

Gobuster generates:

```http
GET / HTTP/1.1
Host: www.example.thm
```

Next request:

```http
GET / HTTP/1.1
Host: shop.example.thm
```

Next:

```http
GET / HTTP/1.1
Host: academy.example.thm
```

The only thing changing is the **Host** header.


# Understanding the Host Header

Example request:

```http
GET / HTTP/1.1
Host: www.example.thm
User-Agent: gobuster/3.6
Accept: text/html
Connection: keep-alive
```

The Host header has three parts.

```text
www.example.thm
```

| Part        | Meaning                               |
| ----------- | ------------------------------------- |
| **www**     | Subdomain generated from the wordlist |
| **example** | Second-Level Domain                   |
| **thm**     | Top-Level Domain (TLD)                |

Gobuster changes only the first part.


# Sample Output

```text
Found: blog.example.thm Status: 200 [Size: 1493]

Found: shop.example.thm Status: 200 [Size: 2983]

Found: www.example.thm Status: 200 [Size: 84352]

Found: academy.example.thm Status: 200 [Size: 434]
```

### Explanation

Gobuster discovered four valid virtual hosts:

* blog.example.thm
* shop.example.thm
* [www.example.thm](http://www.example.thm)
* academy.example.thm

Each should be investigated because it may host a different application.


# Why Use `--exclude-length`?

Sometimes every request returns:

```text
404 Page Not Found
```

but with different Host headers.

Example:

```text
test.example.thm
```

returns

```text
404
Size: 279
```

Another:

```text
random.example.thm
```

returns

```text
404
Size: 278
```

Gobuster may mistakenly report these as found.

By excluding:

```bash
--exclude-length 250-320
```

these false positives disappear.


# Best Practices

* Always use `--append-domain` when required.
* Use `--exclude-length` to filter false positives.
* Investigate every discovered virtual host individually.
* Remember that virtual hosts are configured on the web server, not in DNS.
* Compare response status codes and page sizes to identify valid hosts.

---

