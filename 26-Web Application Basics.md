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



-----------

# HTTP Requests

## What is an HTTP Request?

An **HTTP Request** is a message sent from a client (usually a web browser) to a web server asking it to perform an action.

Every time you:

* Open a webpage
* Log in to a website
* Search for information
* Upload a file
* Submit a form

your browser sends an HTTP request to the server.

 
# Request Flow

```text
+-----------+          HTTP Request          +-------------+
|  Browser  | -----------------------------> | Web Server  |
+-----------+                                +-------------+
```

Example:

```text
User visits:
https://example.com/login
```

The browser sends an HTTP request to retrieve the login page.

  

# Structure of an HTTP Request

An HTTP request consists of:

```text
Request Line
Headers
Blank Line
Body (Optional)
```

Example:

```http
POST /login HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0
Content-Type: application/x-www-form-urlencoded

username=admin&password=Password123
```

  

# Request Line

The **Request Line** (also called the Start Line) is the first line of an HTTP request.

Format:

```text
METHOD /path HTTP/version
```

Example:

```http
GET /profile HTTP/1.1
```

The request line contains three parts:

| Component | Example  | Purpose                 |
| --------- | -------- | ----------------------- |
| Method    | GET      | Action to perform       |
| Path      | /profile | Resource being accessed |
| Version   | HTTP/1.1 | HTTP protocol version   |

  

# HTTP Methods

HTTP methods define what action the client wants the server to perform.

 

## GET

Used to retrieve data from a server.

### Example

```http
GET /products HTTP/1.1
Host: example.com
```

### Common Uses

* Open webpages
* Search products
* View profiles
* Retrieve API data

### Security Considerations

Avoid sending:

* Passwords
* Tokens
* Sensitive information

inside URLs because URLs can be logged and stored in browser history.

 

## POST

Used to send data to the server.

### Example

```http
POST /login HTTP/1.1
Host: example.com

username=admin&password=password123
```

### Common Uses

* User login
* Registration forms
* Uploading data
* Creating records

### Security Considerations

Always:

* Validate input
* Sanitize user data
* Use HTTPS

to prevent attacks like SQL Injection and XSS.

 

## PUT

Used to create or completely replace an existing resource.

### Example

```http
PUT /api/users/101 HTTP/1.1
```

### Common Uses

* Updating user profiles
* Replacing records
* Updating API resources

### Security Considerations

Verify that users are authorized before allowing updates.

 

## DELETE

Used to remove resources.

### Example

```http
DELETE /api/users/101 HTTP/1.1
```

### Common Uses

* Delete accounts
* Remove files
* Delete records

### Security Considerations

Only authorized users should be allowed to perform delete operations.

 

## PATCH

Used to partially update a resource.

### Example

```http
PATCH /api/users/101 HTTP/1.1
```

### Difference Between PUT and PATCH

| PUT                      | PATCH                        |
| ------------------------ | ---------------------------- |
| Replaces entire resource | Updates only selected fields |

Example:

PUT:

```json
{
  "name": "Alex",
  "age": 25
}
```

PATCH:

```json
{
  "age": 26
}
```

 

## HEAD

Similar to GET but returns only headers.

### Example

```http
HEAD /index.html HTTP/1.1
```

### Common Uses

* Check if a file exists
* Verify content size
* Inspect metadata

 

## OPTIONS

Shows which HTTP methods are supported.

### Example

```http
OPTIONS /api/users HTTP/1.1
```

### Example Response

```http
Allow: GET, POST, PUT, DELETE
```

### Common Uses

* API testing
* Browser preflight requests
* Capability discovery

 

## TRACE

Returns the received request for debugging purposes.

### Example

```http
TRACE / HTTP/1.1
```

### Security Consideration

TRACE is often disabled because it can assist attackers during reconnaissance.

 

## CONNECT

Used to establish a secure tunnel between client and server.

### Example

```http
CONNECT example.com:443 HTTP/1.1
```

### Common Uses

* HTTPS communication
* Proxy servers
* Secure tunneling

 

# URL Path

The URL Path identifies the resource being requested.

Example:

```text
https://example.com/api/users/123
```

Path:

```text
/api/users/123
```

The server uses the path to determine which resource should be returned.

 

# Security Risks of URL Paths

Attackers may attempt:

## Directory Traversal

Example:

```text
../../etc/passwd
```

Goal:

Access files outside the intended directory.

 

## Unauthorized Access

Example:

```text
/users/1001
/users/1002
/users/1003
```

Attackers may modify identifiers to access another user's data.

 

## Protection Measures

* Validate paths
* Use access controls
* Restrict file permissions
* Implement authorization checks

 

# HTTP Versions

The HTTP version determines how communication occurs between client and server.

## HTTP/0.9 (1991)

Features:

* GET requests only
* No headers
* Very limited functionality

 

## HTTP/1.0 (1996)

Features:

* Added headers
* Better content handling
* Improved caching

 

## HTTP/1.1 (1997)

Features:

* Persistent connections
* Chunked transfers
* Better caching

Most commonly used version today.

 

## HTTP/2 (2015)

Features:

* Multiplexing
* Header compression
* Faster performance

Benefits:

* Reduced latency
* Improved efficiency

 

## HTTP/3 (2022)

Features:

* Uses QUIC protocol
* Faster connection setup
* Improved security
* Better reliability

 

# Common Request Headers

Headers provide additional information about the request.

 

## Host

Example:

```http
Host: example.com
```

Purpose:

Identifies the destination server.

 

## User-Agent

Example:

```http
User-Agent: Mozilla/5.0
```

Purpose:

Identifies the browser, operating system, or client application.

 

## Referer

Example:

```http
Referer: https://google.com
```

Purpose:

Shows where the request originated.

 

## Cookie

Example:

```http
Cookie: sessionid=abc123
```

Purpose:

Stores session and user information.

 

## Content-Type

Example:

```http
Content-Type: application/json
```

Purpose:

Defines the format of the request body.

 

# Request Body

The request body contains data sent from the client to the server.

Commonly used with:

* POST
* PUT
* PATCH

requests.

 

# URL Encoded Data

Content-Type:

```http
application/x-www-form-urlencoded
```

Example:

```http
name=John&age=25&country=US
```

Characteristics:

* Key-value format
* Simple forms
* Small amounts of data

 
# Form Data

Content-Type:

```http
multipart/form-data
```

Example:

```http
Content-Disposition: form-data; name="file"
```

Characteristics:

* File uploads
* Images
* Documents
* Multiple data sections

 

# JSON Data

Content-Type:

```http
application/json
```

Example:

```json
{
  "name": "John",
  "age": 25,
  "country": "US"
}
```

Characteristics:

* API communication
* Lightweight
* Easy to read

Most common format in modern applications.

 

# XML Data

Content-Type:

```http
application/xml
```

Example:

```xml
<user>
  <name>John</name>
  <age>25</age>
</user>
```

Characteristics:

* Structured data
* Enterprise applications
* Legacy systems

 

# Security Best Practices

Always:

 Validate user input

 Sanitize request data

 Use HTTPS

 Implement authentication

 Implement authorization

 Limit file upload types

 Use secure session management

--------------
-------------


# 06 - HTTP Responses

## What is an HTTP Response?

An **HTTP Response** is a message sent by a web server back to a client (browser, mobile application, API client, etc.) after receiving an HTTP request.

The response tells the client:

* Whether the request was successful
* Whether an error occurred
* Whether the resource has moved
* What data should be displayed

 

# HTTP Communication Flow

```text
+-----------+          HTTP Request          +-------------+
|  Browser  | -----------------------------> | Web Server  |
+-----------+                                +-------------+
      ^                                            |
      |                                            |
      |------------ HTTP Response -----------------|
```

Example:

1. User visits:

```text
https://example.com
```

2. Browser sends:

```http
GET / HTTP/1.1
```

3. Server responds:

```http
HTTP/1.1 200 OK
```

along with the webpage content.

 

# Structure of an HTTP Response

An HTTP response consists of:

```text
Status Line
Headers
Blank Line
Body (Optional)
```

Example:

```http
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 150

<html>
<body>
<h1>Welcome</h1>
</body>
</html>
```

 

# Status Line

The **Status Line** is the first line of every HTTP response.

Format:

```text
HTTP-Version Status-Code Reason-Phrase
```

Example:

```http
HTTP/1.1 200 OK
```

 

## Components of the Status Line

| Component     | Example  | Purpose                    |
| ------------- | -------- | -------------------------- |
| HTTP Version  | HTTP/1.1 | Protocol version           |
| Status Code   | 200      | Response result            |
| Reason Phrase | OK       | Human-readable description |

 

# Status Codes

Status codes are three-digit numbers that indicate the result of the request.

They are divided into five categories:

| Range   | Category      |
| ------- | ------------- |
| 100–199 | Informational |
| 200–299 | Success       |
| 300–399 | Redirection   |
| 400–499 | Client Errors |
| 500–599 | Server Errors |

 

# 1xx - Informational Responses

These responses indicate that the request has been received and processing is continuing.

 

## 100 Continue

Example:

```http
HTTP/1.1 100 Continue
```

Meaning:

* Server received the initial request
* Client can continue sending remaining data

Commonly used during large file uploads.

 

# 2xx - Successful Responses

These responses indicate that the request was successfully processed.

 

## 200 OK

Example:

```http
HTTP/1.1 200 OK
```

Meaning:

* Request completed successfully
* Requested resource returned

Most common success response.

 

## 201 Created

Example:

```http
HTTP/1.1 201 Created
```

Meaning:

* New resource created successfully

Common in APIs when creating:

* Users
* Products
* Orders

 

## 204 No Content

Example:

```http
HTTP/1.1 204 No Content
```

Meaning:

* Request succeeded
* No response body returned

Often used for DELETE requests.

 

# 3xx - Redirection Responses

These responses tell the client that the resource has moved.

 

## 301 Moved Permanently

Example:

```http
HTTP/1.1 301 Moved Permanently
Location: https://newsite.com
```

Meaning:

* Resource permanently moved
* Browser should use the new URL

Useful for:

* Website migrations
* SEO optimization

 

## 302 Found (Temporary Redirect)

Example:

```http
HTTP/1.1 302 Found
Location: https://example.com/login
```

Meaning:

* Resource temporarily located elsewhere
* Original URL may be used again later

 

## 304 Not Modified

Example:

```http
HTTP/1.1 304 Not Modified
```

Meaning:

* Cached version is still valid
* Browser can use local copy

Improves performance and reduces bandwidth.

 

# 4xx - Client Error Responses

These errors occur because of problems with the client's request.

 

## 400 Bad Request

Example:

```http
HTTP/1.1 400 Bad Request
```

Meaning:

* Invalid request format
* Missing parameters
* Malformed syntax

 

## 401 Unauthorized

Example:

```http
HTTP/1.1 401 Unauthorized
```

Meaning:

* Authentication required
* User has not logged in

 

## 403 Forbidden

Example:

```http
HTTP/1.1 403 Forbidden
```

Meaning:

* User is authenticated
* User lacks permission

Difference:

| Code | Meaning           |
| ---- | ----------------- |
| 401  | Login required    |
| 403  | Permission denied |

 

## 404 Not Found

Example:

```http
HTTP/1.1 404 Not Found
```

Meaning:

* Requested resource does not exist

Common causes:

* Incorrect URL
* Deleted page
* Missing file

 

## 405 Method Not Allowed

Example:

```http
HTTP/1.1 405 Method Not Allowed
```

Meaning:

* HTTP method is not permitted

Example:

```http
DELETE /users/1
```

when only GET is allowed.

 

# 5xx - Server Error Responses

These errors indicate problems on the server side.

 

## 500 Internal Server Error

Example:

```http
HTTP/1.1 500 Internal Server Error
```

Meaning:

* Unexpected server failure
* Application crash
* Programming error

 

## 502 Bad Gateway

Example:

```http
HTTP/1.1 502 Bad Gateway
```

Meaning:

* Gateway received an invalid response from another server

Common in reverse proxy environments.

 

## 503 Service Unavailable

Example:

```http
HTTP/1.1 503 Service Unavailable
```

Meaning:

* Server temporarily unavailable
* Maintenance mode
* Server overload

 

# Response Headers

Response headers provide additional information about the server and response.

Format:

```text
Header: Value
```

 

## Date

Example:

```http
Date: Fri, 23 Aug 2024 10:43:21 GMT
```

Purpose:

Shows when the response was generated.

 

## Content-Type

Example:

```http
Content-Type: text/html
```

Purpose:

Specifies the format of the response body.

Common values:

| Content Type     | Description  |
| ---------------- | ------------ |
| text/html        | HTML webpage |
| application/json | JSON data    |
| application/xml  | XML data     |
| image/png        | PNG image    |
| text/plain       | Plain text   |

 

## Content-Length

Example:

```http
Content-Length: 2048
```

Purpose:

Indicates response size in bytes.

 

## Server

Example:

```http
Server: nginx
```

Purpose:

Shows server software handling the request.

Examples:

* Apache
* Nginx
* IIS

### Security Note

Attackers may use this information during reconnaissance.

Many organizations hide or modify this header.

 

## Set-Cookie

Example:

```http
Set-Cookie: sessionid=abc123
```

Purpose:

Stores cookies in the browser.

Used for:

* Authentication
* Sessions
* User preferences

 

## Cache-Control

Example:

```http
Cache-Control: max-age=3600
```

Purpose:

Controls browser caching behavior.

 

## Location

Example:

```http
Location: https://example.com/home
```

Purpose:

Used during redirects.

Common with:

* 301 responses
* 302 responses

 

# Response Body

The Response Body contains the actual data returned by the server.

Examples:

* HTML pages
* JSON data
* Images
* Videos
* PDFs

 
## HTML Response Body Example

```html
<html>
<head>
<title>Welcome</title>
</head>
<body>
<h1>Hello User</h1>
</body>
</html>
```
 

## JSON Response Body Example

```json
{
  "id": 101,
  "username": "alex",
  "role": "student"
}
```

Commonly used by APIs.

 

# Security Considerations

 

## Information Disclosure

Avoid exposing:

* Internal server names
* Software versions
* Stack traces
* Database errors

Bad Example:

```text
MySQL Error:
Access denied for user root
```

Attackers can use this information for exploitation.

 

## Cross-Site Scripting (XSS)

Never return unsanitized user input.

Vulnerable Example:

```html
<h1>Welcome USER_INPUT</h1>
```

Attackers may inject malicious JavaScript.


## Secure Cookies

Cookies should use:

```http
Set-Cookie: sessionid=abc123; HttpOnly; Secure
```

Benefits:

* Prevent JavaScript access
* HTTPS-only transmission

---
----------


# HTTP Headers

## What are HTTP Headers?

HTTP Headers are **key-value pairs** included in HTTP requests and responses that provide additional information about the communication between a client and a server.

Headers help control:

* Authentication
* Sessions
* Caching
* Content Types
* Security Policies
* Browser Behavior

### Header Format

```http
Header-Name: Value
```

Example:

```http
Content-Type: application/json
```

 

# Why Are Headers Important?

Headers allow clients and servers to exchange important information without placing it directly in the message body.

### Uses of Headers

* Identify the destination server
* Identify the client browser
* Define content formats
* Manage sessions
* Control caching
* Improve security

 

# Types of HTTP Headers

There are two main categories:

## Request Headers

Sent from:

```text
Client → Server
```

Purpose:

Provide information about the request.

 

## Response Headers

Sent from:

```text
Server → Client
```

Purpose:

Provide information about the response.

 

# Request Headers

Request headers give additional information about the client's request.

 

## Host Header

### Example

```http
Host: tryhackme.com
```

### Purpose

Identifies the destination website or server.

### Example Request

```http
GET / HTTP/1.1
Host: tryhackme.com
```

### Security Note

Incorrect handling of the Host header can lead to:

* Host Header Injection
* Password Reset Poisoning
* Cache Poisoning

 

## User-Agent Header

### Example

```http
User-Agent: Mozilla/5.0
```

### Purpose

Identifies:

* Browser
* Operating System
* Device Type

Example:

```http
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
```

### Common Uses

* Browser compatibility
* Analytics
* Logging

### Security Note

Attackers can easily modify User-Agent values.

Never trust User-Agent headers for authentication.

 

## Referer Header

### Example

```http
Referer: https://google.com
```

### Purpose

Indicates where the request originated.

Example:

```text
Google → Website
```

### Common Uses

* Analytics
* Traffic tracking
* CSRF protection

### Security Note

Referer values can be spoofed and may expose sensitive URLs.

 

## Cookie Header

### Example

```http
Cookie: sessionid=abc123
```

### Purpose

Stores information previously provided by the server.

Common Data:

* Session IDs
* User Preferences
* Authentication Tokens

### Example

```http
Cookie: sessionid=abc123; theme=dark
```

### Security Risks

Poor cookie security may lead to:

* Session Hijacking
* Session Fixation
* Account Takeover

 

## Content-Type Header

### Example

```http
Content-Type: application/json
```

### Purpose

Specifies the format of the request body.

 

### Common Content Types

| Content-Type                      | Purpose      |
| --------------------------------- | ------------ |
| text/html                         | HTML Page    |
| application/json                  | JSON Data    |
| application/xml                   | XML Data     |
| text/plain                        | Plain Text   |
| multipart/form-data               | File Uploads |
| application/x-www-form-urlencoded | Form Data    |

 

## Content-Length Header

### Example

```http
Content-Length: 150
```

### Purpose

Specifies the size of the request body in bytes.

### Benefits

* Prevents incomplete transfers
* Helps servers process data correctly


# Response Headers

Response headers provide information about the server's response.

 

## Date Header

### Example

```http
Date: Fri, 23 Aug 2024 10:43:21 GMT
```

### Purpose

Shows when the server generated the response.

 

## Server Header

### Example

```http
Server: nginx
```

### Purpose

Identifies server software.

Common Values:

```text
Apache
Nginx
Microsoft IIS
LiteSpeed
```

### Security Note

Server information can help attackers identify potential vulnerabilities.

Many organizations hide this header.

 

## Content-Type Header

### Example

```http
Content-Type: text/html
```

### Purpose

Defines the type of data returned.

Example:

```http
Content-Type: application/json
```

means the response contains JSON data.

 

## Content-Length Header

### Example

```http
Content-Length: 2048
```

### Purpose

Shows the size of the response body.

 

## Set-Cookie Header

### Example

```http
Set-Cookie: sessionid=abc123
```

### Purpose

Instructs the browser to store cookies.

 

### Secure Cookie Example

```http
Set-Cookie: sessionid=abc123; HttpOnly; Secure; SameSite=Strict
```

 

### Security Flags

| Flag     | Purpose                    |
| -------- | -------------------------- |
| HttpOnly | Prevents JavaScript access |
| Secure   | HTTPS Only                 |
| SameSite | Protects against CSRF      |

 

## Cache-Control Header

### Example

```http
Cache-Control: max-age=3600
```

### Purpose

Controls how long content can be cached.

 

### Common Directives

| Directive | Purpose                    |
| --------- | -------------------------- |
| no-cache  | Must revalidate before use |
| no-store  | Do not store data          |
| max-age   | Cache lifetime             |
| public    | Anyone can cache           |
| private   | Only browser can cache     |

 

### Security Note

Sensitive pages should use:

```http
Cache-Control: no-store
```

Examples:

* Banking portals
* Admin dashboards
* Payment pages

 

## Location Header

### Example

```http
Location: https://example.com/login
```

### Purpose

Specifies where the client should redirect.

Usually seen with:

* 301 Moved Permanently
* 302 Found

 

### Example

```http
HTTP/1.1 302 Found
Location: /login
```

The browser automatically redirects the user.

### Security Note

Improper validation may lead to:

* Open Redirect Vulnerabilities
* Phishing Attacks

 

# Request Header Example

```http
GET /profile HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0
Referer: https://google.com
Cookie: sessionid=abc123
```

### Breakdown

| Header     | Purpose             |
| ---------- | ------------------- |
| Host       | Destination Server  |
| User-Agent | Browser Information |
| Referer    | Previous Page       |
| Cookie     | Session Data        |

 

# Response Header Example

```http
HTTP/1.1 200 OK
Date: Fri, 23 Aug 2024 10:43:21 GMT
Server: nginx
Content-Type: text/html
Content-Length: 1024
Set-Cookie: sessionid=abc123
```

### Breakdown

| Header         | Purpose         |
| -------------- | --------------- |
| Date           | Response Time   |
| Server         | Server Software |
| Content-Type   | Data Format     |
| Content-Length | Data Size       |
| Set-Cookie     | Store Cookie    |

 

# Security Considerations

  

## Sensitive Information Disclosure

Avoid exposing:

```text
Apache/2.4.58
PHP/8.3.0
MySQL 8.0
```

This information helps attackers identify targets.

 

## Cookie Security

Always use:

```http
Set-Cookie: sessionid=abc123; HttpOnly; Secure; SameSite=Strict
```

Benefits:

* Prevents XSS cookie theft
* Prevents session hijacking
* Reduces CSRF attacks

 

## Cache Security

Never cache:

* Password reset pages
* Banking information
* Session data
* Payment information

Use:

```http
Cache-Control: no-store
```

  

## Content-Type Validation

Always specify the correct Content-Type.

Incorrect content types may lead to:

* MIME Sniffing
* Content Injection
* Browser Misinterpretation

---
---------

# Security Headers

## Introduction

HTTP Security Headers are special response headers that help protect web applications against common attacks such as:

* Cross-Site Scripting (XSS)
* Clickjacking
* MIME-Type Confusion
* Information Disclosure
* Man-in-the-Middle (MITM) Attacks
* Open Redirect Attacks

Security headers provide an additional layer of defense by instructing browsers how to handle website content securely.

 

# Why Security Headers Matter

Without proper security headers, attackers may be able to:

* Inject malicious JavaScript
* Steal user sessions
* Trick users into visiting malicious websites
* Intercept communications
* Load unauthorized resources

Security headers significantly reduce the attack surface of a web application.

 

# Common Security Headers

The most important security headers are:

| Header                           | Purpose                                   |
| -------------------------------- | ----------------------------------------- |
| Content-Security-Policy (CSP)    | Prevent XSS and malicious content loading |
| Strict-Transport-Security (HSTS) | Force HTTPS connections                   |
| X-Content-Type-Options           | Prevent MIME-type sniffing                |
| Referrer-Policy                  | Control referrer information sharing      |

 

# 1. Content-Security-Policy (CSP)

## What is CSP?

Content Security Policy (CSP) helps prevent:

* Cross-Site Scripting (XSS)
* Data Injection Attacks
* Malicious Third-Party Script Execution

It tells the browser which resources are trusted and allowed to load.

 

## Example CSP Header

```http
Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.example.com; style-src 'self'
```

 

## Understanding CSP Directives

### default-src

Defines the default source for all content types.

Example:

```http
default-src 'self'
```

Meaning:

* Only load resources from the same website.

 

### script-src

Controls where JavaScript files can be loaded from.

Example:

```http
script-src 'self' https://cdn.example.com
```

Meaning:

* Allow scripts from:

  * Current website
  * cdn.example.com

 

### style-src

Controls where CSS files can be loaded from.

Example:

```http
style-src 'self'
```

Meaning:

* Only allow stylesheets from the current website.

 

## Common CSP Keywords

| Keyword         | Meaning                                       |
| --------------- | --------------------------------------------- |
| 'self'          | Current website                               |
| 'none'          | Block all sources                             |
| '*'             | Allow all sources                             |
| 'unsafe-inline' | Allow inline scripts/styles (not recommended) |
| 'unsafe-eval'   | Allow JavaScript eval() (not recommended)     |

 

## Security Benefits

CSP helps prevent:

### Cross-Site Scripting (XSS)

Without CSP:

```html
<script>alert('XSS')</script>
```

may execute successfully.

With a properly configured CSP:

```http
Content-Security-Policy: script-src 'self'
```

the browser blocks unauthorized scripts.

 

# 2. Strict-Transport-Security (HSTS)

## What is HSTS?

HSTS forces browsers to always use HTTPS when communicating with a website.

This protects users against:

* Man-in-the-Middle (MITM) Attacks
* SSL Stripping Attacks
* Unencrypted Connections

 

## Example HSTS Header

```http
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
```

 

## HSTS Directives

### max-age

Specifies how long the browser should remember the HTTPS rule.

Example:

```http
max-age=63072000
```

Value:

```text
63072000 seconds = 2 years
```

 

### includeSubDomains

Applies HSTS to all subdomains.

Example:

```http
includeSubDomains
```

Protects:

```text
example.com
blog.example.com
admin.example.com
api.example.com
```

 

### preload

Requests inclusion in browser preload lists.

Example:

```http
preload
```

Benefits:

* Browser enforces HTTPS before first visit.

 

## Security Benefits

Prevents:

### HTTP Downgrade Attacks

Attackers cannot force users to switch from:

```text
HTTPS → HTTP
```

 

### SSL Stripping

Attackers cannot intercept and remove HTTPS protections.

 

# 3. X-Content-Type-Options

## What is X-Content-Type-Options?

This header prevents browsers from guessing file types.

It forces browsers to trust the Content-Type header provided by the server.

 

## Example

```http
X-Content-Type-Options: nosniff
```

 

## What Does "nosniff" Mean?

```http
nosniff
```

tells the browser:

```text
Do not guess file types.
Only trust the Content-Type header.
```

 

## Why Is This Important?

Suppose a malicious file:

```text
evil.js
```

is uploaded but disguised as:

```text
image.jpg
```

Without:

```http
X-Content-Type-Options: nosniff
```

some browsers may attempt to execute it.

With:

```http
X-Content-Type-Options: nosniff
```

the browser respects the declared MIME type.

 

## Security Benefits

Prevents:

* MIME Sniffing Attacks
* File Upload Exploitation
* Content Type Confusion

 

# 4. Referrer-Policy

## What is Referrer-Policy?

This header controls how much information is shared when users move from one website to another.

 

## Example

```http
Referrer-Policy: strict-origin-when-cross-origin
```

 

## Common Referrer Policies

### no-referrer

```http
Referrer-Policy: no-referrer
```

Meaning:

* Never send referrer information.

 

### same-origin

```http
Referrer-Policy: same-origin
```

Meaning:

* Send referrer only within the same website.

 

### strict-origin

```http
Referrer-Policy: strict-origin
```

Meaning:

* Only send the domain name.
* Do not send the full URL path.

 
### strict-origin-when-cross-origin

```http
Referrer-Policy: strict-origin-when-cross-origin
```

Meaning:

* Same-site requests:

  * Send full URL
* Cross-site requests:

  * Send only origin

Example:

```text
https://example.com/profile?id=100
```

External websites receive only:

```text
https://example.com
```

 

## Security Benefits

Prevents leakage of:

* Session Information
* Internal URLs
* Sensitive Query Parameters

Example:

```text
https://example.com/reset?token=abc123
```

Without proper policies, sensitive tokens may be exposed.

 

# SecurityHeaders.io

A useful website for checking security headers:

```text
https://securityheaders.io
```

 

## What It Does

Analyzes websites and reports:

* Missing security headers
* Weak security configurations
* Overall security rating

 

## Typical Ratings

| Grade | Meaning            |
| ----- | ------------------ |
| A+    | Excellent Security |
| A     | Very Good          |
| B     | Good               |
| C     | Average            |
| D     | Weak               |
| F     | Poor               |

 

# Real-World Attack Prevention

| Attack                     | Security Header        |
| -------------------------- | ---------------------- |
| Cross-Site Scripting (XSS) | CSP                    |
| SSL Stripping              | HSTS                   |
| MIME Sniffing              | X-Content-Type-Options |
| Information Leakage        | Referrer-Policy        |

 

# Example Secure Response Headers

```http
HTTP/1.1 200 OK
Content-Security-Policy: default-src 'self'
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
X-Content-Type-Options: nosniff
Referrer-Policy: strict-origin-when-cross-origin
```

---

