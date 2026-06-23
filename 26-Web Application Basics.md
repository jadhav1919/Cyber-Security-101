## What is a Web Application?

A **Web Application** is software that runs on a web server and is accessed through a web browser.

Examples:

* Gmail
* Facebook
* YouTube
* Amazon
* Online Banking Portals

When a user visits a website, the browser communicates with a web server using HTTP/HTTPS protocols to request and receive content.

# Planet Analogy

Think of a web application as a **planet**.

* The **surface** of the planet represents what users can see and interact with.
* The **inside of the planet** represents the hidden systems that make everything work.

| Planet                 | Web Application      |
| ---------------------- | -------------------- |
| Surface                | Front End            |
| Internal Systems       | Back End             |
| Atmosphere             | Security Controls    |
| Library/Records        | Database             |
| Roads & Infrastructure | Servers & Networking |


# Front End

The **Front End** is everything the user sees and interacts with inside a web browser.

## HTML (HyperText Markup Language)

HTML provides the structure of a webpage.

Example:

```html
<h1>Welcome to My Website</h1>
<p>This is a paragraph.</p>
```

### Purpose

* Creates webpage structure
* Defines headings, paragraphs, buttons, forms, images, etc.

### Analogy

HTML is like the DNA or skeleton of an organism.


## CSS (Cascading Style Sheets)

CSS controls the appearance of a webpage.

Example:

```css
h1 {
    color: blue;
}
```

### Purpose

* Colors
* Fonts
* Layouts
* Spacing
* Animations

### Analogy

CSS is like the appearance of an organism:

* Colour
* Shape
* Size
* Texture


## JavaScript (JS)

JavaScript adds interactivity and logic.

Example:

```javascript
alert("Welcome!");
```

### Purpose

* Dynamic content
* Form validation
* Interactive menus
* API communication
* User actions

### Analogy

JavaScript is the brain that makes decisions.


# Back End

The **Back End** contains components that users cannot directly see.

It processes requests and provides data to the front end.


## Database

A database stores information.

Examples:

* User accounts
* Passwords (hashed)
* Product information
* Orders
* Preferences

### Popular Databases

* MySQL
* PostgreSQL
* MongoDB
* Microsoft SQL Server

### Analogy

A database is like:

* A library
* Filing cabinet
* Record storage system


## Infrastructure

Infrastructure includes:

* Web Servers
* Application Servers
* Storage Systems
* Networking Devices
* Operating Systems

### Examples

| Component          | Example           |
| ------------------ | ----------------- |
| Web Server         | Apache, Nginx     |
| Application Server | Tomcat, Node.js   |
| Database Server    | MySQL, PostgreSQL |

### Analogy

Infrastructure is like:

* Roads
* Vehicles
* Fuel systems

that keep the planet functioning.


## Web Application Firewall (WAF)

A WAF filters malicious traffic before it reaches the web server.

### Functions

* Blocks malicious requests
* Detects attacks
* Protects applications

### Common Threats Blocked

* SQL Injection
* Cross-Site Scripting (XSS)
* Malicious Bots

### Popular WAFs

* Cloudflare WAF
* AWS WAF
* Imperva WAF

### Analogy

A WAF is like a planet's atmosphere that protects inhabitants from harmful radiation.


--------------

# URL Structure

## What is a URL?

A **URL (Uniform Resource Locator)** is the address used to locate and access resources on the Internet.

Resources can include:

* Web Pages
* Images
* Videos
* Documents
* APIs
* Downloads

### Example URL

```text
https://admin:password@example.com:443/products/search?q=laptop#reviews
```

A URL consists of several components, each serving a specific purpose.

 
# Anatomy of a URL

```text
https://admin:password@example.com:443/products/search?q=laptop#reviews
│       │              │           │        │          │
│       │              │           │        │          └── Fragment
│       │              │           │        └──────────── Query String
│       │              │           └───────────────────── Path
│       │              └──────────────────────────────── Port
│       └─────────────────────────────────────────────── User Information
└────────────────────────────────────────────────────── Scheme
```

 

# 1. Scheme (Protocol)

The **Scheme** tells the browser which protocol to use when communicating with the server.

### Common Schemes

| Scheme | Description                   |
| ------ | ----------------------------- |
| HTTP   | HyperText Transfer Protocol   |
| HTTPS  | Secure HTTP (Encrypted)       |
| FTP    | File Transfer Protocol        |
| SFTP   | Secure File Transfer Protocol |

### Example

```text
https://tryhackme.com
```

Here:

```text
https
```

is the scheme.

 

## Security Note

 Always prefer HTTPS over HTTP.

HTTPS:

* Encrypts data
* Protects credentials
* Prevents eavesdropping
* Improves website security

 

# 2. User Information

A URL can contain authentication details.

### Example

```text
https://admin:password@example.com
```

Where:

```text
admin
```

= Username

```text
password
```

= Password

 

## Security Risk

Embedding credentials in URLs is considered insecure because:

* URLs may be logged
* URLs may appear in browser history
* Credentials can be exposed

### Modern Practice

Most applications use:

* Login forms
* Session Cookies
* Authentication Tokens

instead of credentials inside URLs.

 

# 3. Host / Domain

The Host identifies the website being accessed.

### Example

```text
https://tryhackme.com
```

Host:

```text
tryhackme.com
```

 

## Domain Examples

| Domain        | Purpose                |
| ------------- | ---------------------- |
| google.com    | Search Engine          |
| github.com    | Code Hosting           |
| tryhackme.com | Cybersecurity Training |
| amazon.com    | E-Commerce             |

 

## Security Risk - Typosquatting

Attackers often register domains similar to legitimate websites.

### Example

Legitimate:

```text
google.com
```

Malicious:

```text
goog1e.com
```

Notice:

```text
1
```

replaces:

```text
l
```

This technique is called **Typosquatting** and is commonly used in phishing attacks.

 

# 4. Port

A Port tells the server which service should handle the request.

### Example

```text
https://example.com:443
```

Port:

```text
443
```

 

## Common Ports

| Port | Service |
| ---- | ------- |
| 80   | HTTP    |
| 443  | HTTPS   |
| 21   | FTP     |
| 22   | SSH     |
| 25   | SMTP    |
| 3306 | MySQL   |

 

## Note

If no port is specified:

* HTTP uses Port 80
* HTTPS uses Port 443

by default.

 

# 5. Path

The Path specifies the exact resource being requested.

### Example

```text
https://example.com/products/laptops
```

Path:

```text
/products/laptops
```

 

## Purpose

The path tells the server:

* Which page to display
* Which file to retrieve
* Which API endpoint to access

 

## Security Risks

Improper path handling can lead to:

### Directory Traversal

Example:

```text
../../etc/passwd
```

Attackers may attempt to access sensitive files outside the intended directory.

### Mitigation

* Validate paths
* Restrict file access
* Implement access controls

 

# 6. Query String

The Query String contains additional parameters.

It begins with:

```text
?
```

### Example

```text
https://example.com/search?q=laptop
```

Query String:

```text
?q=laptop
```

Parameter:

```text
q=laptop
```

 
## Multiple Parameters

```text
https://example.com/search?q=laptop&sort=price
```

Parameters:

```text
q=laptop
sort=price
```

 

## Security Risks

Attackers may manipulate query parameters to perform:

* SQL Injection
* XSS
* Parameter Tampering

### Mitigation

* Validate input
* Sanitize user data
* Use parameterized queries

 

# 7. Fragment

A Fragment points to a specific section within a webpage.

It begins with:

```text
#
```

### Example

```text
https://example.com/tutorial#installation
```

Fragment:

```text
#installation
```

The browser automatically jumps to the Installation section.

 

## Common Uses

* Documentation
* FAQs
* Long articles
* Navigation menus

 
## Security Consideration

Fragments can sometimes contain user-controlled data.

Always validate and sanitize any fragment data used by JavaScript applications.

 

# Complete URL Example

```text
https://admin:password@example.com:443/products/search?q=laptop#reviews
```

| Component    | Value            |
| ------------ | ---------------- |
| Scheme       | https            |
| User         | admin            |
| Password     | password         |
| Host         | example.com      |
| Port         | 443              |
| Path         | /products/search |
| Query String | q=laptop         |
| Fragment     | reviews          |

----------------

# HTTP Messages

## What are HTTP Messages?

HTTP (HyperText Transfer Protocol) messages are the packets of data exchanged between a client and a web server.

They enable communication between users and web applications.

### Example

When you:

1. Open a website
2. Submit a login form
3. Search for a product
4. Upload a file

your browser sends an **HTTP Request**, and the server sends back an **HTTP Response**.


# Client-Server Communication

```text
+-----------+                         +-------------+
|   Client  |                         | Web Server  |
| (Browser) |                         |             |
+-----------+                         +-------------+
      |                                      |
      |------ HTTP Request ----------------->|
      |                                      |
      |<----- HTTP Response -----------------|
      |                                      |
```

### Example

User visits:

```text
https://example.com
```

The browser sends a request to the server.

The server processes the request and sends back:

* HTML
* CSS
* JavaScript
* Images
* Videos
* API Data


# Types of HTTP Messages

There are two types of HTTP messages:

## 1. HTTP Request

Sent from:

```text
Client → Server
```

Purpose:

* Request data
* Submit forms
* Upload files
* Delete resources
* Update information


## 2. HTTP Response

Sent from:

```text
Server → Client
```

Purpose:

* Return requested data
* Confirm successful actions
* Report errors
* Redirect users


# Structure of an HTTP Message

Every HTTP message follows a standard structure.

```text
Start Line
Headers
Empty Line
Body
```



# 1. Start Line

The Start Line is the first line of an HTTP message.

It tells the recipient what type of message is being sent.

---

## Request Start Line

Example:

```http
GET /login HTTP/1.1
```

Components:

| Part     | Description   |
| -------- | ------------- |
| GET      | HTTP Method   |
| /login   | Resource Path |
| HTTP/1.1 | HTTP Version  |


## Response Start Line

Example:

```http
HTTP/1.1 200 OK
```

Components:

| Part     | Description   |
| -------- | ------------- |
| HTTP/1.1 | HTTP Version  |
| 200      | Status Code   |
| OK       | Reason Phrase |


# 2. Headers

Headers contain additional information about the request or response.

They use a:

```text
Key: Value
```

format.


## Request Header Example

```http
Host: example.com
User-Agent: Mozilla/5.0
Cookie: sessionid=abc123
```


## Response Header Example

```http
Content-Type: text/html
Server: nginx
Content-Length: 1256
```


## Why Headers Matter

Headers provide information such as:

* Browser details
* Content type
* Authentication data
* Session information
* Security policies


# 3. Empty Line

An empty line separates:

```text
Headers
and
Body
```

Without this separator, the server or browser may not correctly understand the message.

Example:

```http
Host: example.com
User-Agent: Mozilla/5.0

username=admin
```

Notice the blank line before the body.


# 4. Body

The Body contains the actual data being transmitted.

Not every HTTP message contains a body.

For example:

* GET requests usually have no body.
* POST requests commonly include a body.


## Request Body Example

```http
POST /login HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded

username=admin&password=password123
```

Body:

```text
username=admin&password=password123
```

## Response Body Example

```http
HTTP/1.1 200 OK
Content-Type: text/html

<html>
<head>
<title>Welcome</title>
</head>
<body>
Hello User
</body>
</html>
```

Body:

```html
<html>
<head>
<title>Welcome</title>
</head>
<body>
Hello User
</body>
</html>
```


# Complete HTTP Request Example

```http
GET /profile HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0
Cookie: sessionid=abc123

```

### Breakdown

| Component   | Value       |
| ----------- | ----------- |
| Method      | GET         |
| Path        | /profile    |
| Version     | HTTP/1.1    |
| Host Header | example.com |
| User-Agent  | Mozilla/5.0 |
| Body        | None        |


# Complete HTTP Response Example

```http
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 85

<html>
<body>
<h1>Welcome</h1>
</body>
</html>
```

### Breakdown

| Component     | Value        |
| ------------- | ------------ |
| Version       | HTTP/1.1     |
| Status Code   | 200          |
| Reason Phrase | OK           |
| Content-Type  | text/html    |
| Body          | HTML Content |


# Why Understanding HTTP Messages is Important

## Web Development

Helps developers:

* Build websites
* Create APIs
* Debug communication issues

## Cybersecurity

Helps security professionals:

* Analyze web traffic
* Detect attacks
* Test applications
* Find vulnerabilities


## Penetration Testing

Most web attacks involve manipulating:

* Requests
* Responses
* Headers
* Parameters

Understanding HTTP messages is essential for:

* Burp Suite
* OWASP ZAP
* API Testing
* Web Application Pentesting


# Security Considerations

Always validate and sanitize user input contained in HTTP messages.

Common attacks include:

| Attack                     | Description                  |
| -------------------------- | ---------------------------- |
| SQL Injection              | Malicious database queries   |
| Cross-Site Scripting (XSS) | Injecting malicious scripts  |
| Command Injection          | Executing system commands    |
| Parameter Tampering        | Modifying request parameters |

Proper handling of HTTP messages helps prevent these attacks.


