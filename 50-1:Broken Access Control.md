# Broken Access Control

**Broken Access Control** happens when an application fails to properly restrict **who can access data or perform actions**.

In simple words:

> **A user is able to access something they should not be allowed to access.**

For example, imagine a normal user should only access their own profile. Because of weak access control, they can access another user's profile or even an admin page.

The application failed to properly check the user's **permission**.

Broken Access Control may happen because of:

* Poor application design.
* Coding mistakes.
* Wrong security configuration.
* Missing permission checks.

The main impact is **unauthorized access to accounts, files, databases, sensitive information, or administrative functions**.

# What is Access Control?

**Access Control** is a security mechanism that decides:

> **Who can access which resource and what actions they can perform.**

For example:

**Sai → Can view Sai's bank account**

**John → Can view John's bank account**

**Admin → Can manage user accounts**

The server should check the user's permissions before providing access.

Access control protects resources such as:

* Files.
* Directories.
* Databases.
* Web pages.
* User accounts.
* Admin functions.

The primary goal is:

> **Only authorized users should access protected resources.**

# Types of Access Control

There are four important access control models:

| Model    | Access Decided By               | Easy Meaning        |
| -------- | ------------------------------- | ------------------- |
| **DAC**  | Resource owner                  | Owner decides       |
| **MAC**  | System security policy          | System rules decide |
| **RBAC** | User's role                     | Role decides        |
| **ABAC** | User and environment attributes | Conditions decide   |

## Discretionary Access Control (DAC)

**DAC = The resource owner decides who gets access.**

Suppose you create a file.

You are the owner of that file.

You may give another user permission to:

* Read the file.
* Write to the file.
* Execute the file.

The owner controls the permissions.

A simple example is Linux file ownership and permissions.

Think:

> **My resource → I decide who can access it**

## Mandatory Access Control (MAC)

**MAC = The system's predefined security policy decides access.**

Users cannot freely change the access rules.

For example, imagine a government system with security classifications:

**Top Secret**

**Secret**

**Confidential**

A person with **Confidential clearance** cannot simply decide to access Top Secret information.

The system checks the security policy and clearance level.

Think:

> **Strict system rules decide access**

MAC is commonly used in highly secure environments such as:

* Government.
* Military.
* High-security systems.

So:

**MAC = System policy decides access**

## Role-Based Access Control (RBAC)

**RBAC = Access is based on the user's role.**

Users are assigned roles.

Each role has specific permissions.

For example:

| Role     | Permission                  |
| -------- | --------------------------- |
| Employee | View own profile            |
| Manager  | View team information       |
| HR       | Manage employee information |
| Admin    | Manage the system           |

Suppose Sai has the role:

**Employee**

Sai receives Employee permissions.

If Sai becomes a Manager, the system assigns the Manager role and related permissions.

RBAC is very common in companies and enterprise applications.

Think:

> **Your job role decides your access**

So:

**RBAC = Role decides access**

## Attribute-Based Access Control (ABAC)

**ABAC = Access is decided using multiple attributes or conditions.**

Attributes may include:

* User role.
* Location.
* Time.
* Device.
* Department.
* Security level.

For example:

**User Role = Manager**

**Location = Company Office**

**Time = 9 AM to 6 PM**

**Device = Company Laptop**

The application may allow access only when all required conditions are satisfied.

For example:

> Allow access if the user is a Manager AND uses a company laptop AND connects during working hours.

ABAC is more flexible than RBAC.

Think:

> **Multiple conditions decide access**

So:

**ABAC = Attributes and conditions decide access**


# Easy Way to Remember Access Control Models

**DAC → Owner decides**

**MAC → System policy decides**

**RBAC → Role decides**

**ABAC → Attributes decide**

# What is Broken Access Control?

Access control becomes **broken** when the application does not correctly enforce permissions.

Suppose:

**Sai is User ID 100**

Sai accesses:

`/profile?id=100`

The server returns Sai's profile.

Now Sai changes the ID to `101`.

`/profile?id=101`

If the server returns John's profile without checking permission, access control is broken.

The server should check:

> **Does Sai have permission to access User 101's profile?**

If the server does not perform this check, the attacker may gain unauthorized access.


# Horizontal Privilege Escalation

**Horizontal Privilege Escalation** means accessing another user's resources at the **same privilege level**.

Example:

**Normal User Sai → Normal User John's account**

Sai and John are both normal users.

Sai should only access his own account.

But Sai changes the user ID and accesses John's account.

The privilege level did not increase.

The attacker simply moved **sideways to another user's data**.

Think:

> **Same level → Different user**


# Vertical Privilege Escalation

**Vertical Privilege Escalation** means accessing resources or functions belonging to a **higher privilege level**.

Example:

**Normal User → Admin**

Suppose a normal user accesses:

`/admin`

The application should check:

**Is this user an administrator?**

If the application allows a normal user to access the admin page, this is vertical privilege escalation.

Another example is manipulating a parameter such as:

`role=user`

and changing it to:

`role=admin`

If the server trusts this value and gives admin permissions, access control is broken.

Think:

> **Lower level → Higher level**


# Horizontal vs Vertical Privilege Escalation

| Horizontal                 | Vertical                             |
| -------------------------- | ------------------------------------ |
| Same privilege level       | Higher privilege level               |
| Access another user's data | Access admin or privileged functions |
| User → Another User        | User → Admin                         |
| Move sideways              | Move upward                          |

Easy memory:

**Horizontal = Sideways**

**Vertical = Upwards**

# Insufficient Access Control Checks

This happens when the application **does not properly or consistently check permissions**.

For example, imagine an application has a sensitive report.

The website hides the report button from normal users.

However, the report is available at:

`/admin/report`

A normal user manually enters this path.

If the server displays the report, the application has insufficient access control checks.

The important concept is:

> **Hiding a button is not access control.**

The **server must verify permission on every request**.

The correct flow should be:

**Request → Identify User → Check Permission → Allow or Deny**

Not:

**Request → Return Sensitive Data**

# Insecure Direct Object Reference (IDOR)

**IDOR = Insecure Direct Object Reference**

IDOR happens when an application exposes a reference to an object and fails to properly verify whether the user is authorized to access that object.

Objects may be:

* User accounts.
* Files.
* Orders.
* Bank accounts.
* Documents.
* Messages.

For example:

`/invoice?id=1001`

The user changes it to:

`/invoice?id=1002`

If invoice `1002` belongs to another user and the server displays it, this is an IDOR vulnerability.

The problem is **not only that the ID is predictable**.

The main problem is:

> **The server failed to perform an authorization check.**

The server should verify:

**Does the logged-in user own invoice 1002 or have permission to access it?**

If no:

**Access Denied**

----------------


# Understanding the Web Application

The objective of this task is to **understand how the web application works before trying to find vulnerabilities**.

As a penetration tester, don't just use the website like a normal user.

Instead, always ask yourself:

* What request is sent to the server?
* What response comes back?
* What is the backend code probably doing?
* Can I modify any value?
* Does the server trust user input too much?

This mindset helps you discover vulnerabilities.

# Assessing the Application

The application has three main pages:

| Page             | Purpose                       |
| ---------------- | ----------------------------- |
| **Registration** | Create a new user account     |
| **Login**        | Log in to an existing account |
| **Dashboard**    | User's main page after login  |

A penetration tester usually follows this process:

1. Register a new account.
2. Login with that account.
3. Observe how the application behaves.
4. Capture HTTP requests and responses.
5. Look for possible vulnerabilities.

The workflow is:

**Register → Login → Capture Traffic → Analyze → Test for Vulnerabilities**

# Think Like a Pentester

Whenever you use a website, don't think like a normal user.

Think like this:

### Registration Page

Ask yourself:

* Can I register the same username twice?
* Can I change hidden values?
* Does the application let me become an admin?
* Is the input properly validated?

### Login Page

Think:

* How are credentials sent?
* Does the server create a session?
* Does the response reveal too much information?
* Can login be bypassed?

### Dashboard

Think:

* Why can I access this page?
* How does the server know I'm logged in?
* Is there an admin check?
* Can I modify anything in the URL?

# Capturing HTTP Traffic

To understand what is happening behind the scenes, we capture the HTTP traffic.

Two popular tools are:

* **Burp Suite**
* **OWASP ZAP**

These tools act as a **proxy**.

Instead of:

```
Browser  →  Server
```

The traffic becomes:

```
Browser
     ↓
Burp Suite (Proxy)
     ↓
Server
```

Every request and response passes through Burp.

This allows us to:

* Read requests
* Read responses
* Modify requests
* Send them again

# Burp Proxy

The **Proxy** module captures HTTP traffic.

Think of it as a checkpoint.

```
Browser
   ↓
Proxy (Burp)
   ↓
Server
```

The proxy lets you inspect every request before it reaches the server.

# Burp Repeater

After capturing a request, Burp lets you send it to **Repeater**.

Repeater allows you to:

* Edit requests
* Send them multiple times
* Observe different responses

Workflow:

```
Capture Request
        ↓
Send to Repeater
        ↓
Modify Request
        ↓
Send Again
        ↓
Analyze Response
```

Repeater is one of the most commonly used Burp tools during penetration testing.


# Understanding the Login Response

After a successful login, the application returns a **JSON response**.

Example fields include:

* `status`
* `message`
* `first_name`
* `last_name`
* `is_admin`
* `redirect_link`

JSON is simply a structured way to exchange data.

For example:

```
{
 status
 message
 first_name
 last_name
 is_admin
 redirect_link
}
```

Each field tells the application something.

## status

Shows whether the login succeeded.

Example:

```
Success
```

or

```
Failed
```

## message

Human-readable message.

Example:

```
Login Successful
```

## first_name

Stores the user's first name.

## last_name

Stores the user's last name.

## is_admin

This is the interesting field.

It tells whether the logged-in user is an administrator.

For example:

```
Normal User
↓

is_admin = false
```

```
Administrator
↓

is_admin = true
```

Whenever you see a value related to permissions, ask:

> **Is the server checking this securely?**


## redirect_link

After login, the server tells the browser where to go next.

Example:

```
dashboard.php
```

The application then redirects the user.

# The isadmin URL Parameter

The room mentions that the user is redirected to:

```
dashboard.php?isadmin=...
```

As a pentester, this immediately attracts attention.

Why?

Because anything in the URL can usually be modified by the client.

The important question becomes:

> **Does the server trust this value?**

A secure application should **not** rely on a client-controlled URL parameter to decide permissions. Instead, it should determine the user's role from trusted server-side data (such as the session or database).

So, seeing a parameter like `isadmin` tells you it is **worth investigating** during an authorized security assessment.


# Information Learned from HTTP Responses

Besides application data, HTTP responses often reveal information about the server.

In this room we learn:

### Operating System

```
Debian Linux
```

### Web Server

```
Apache/2.4.38
```

### Backend Language

```
PHP/8.0.19
```

This combination is called the **technology stack**.

```
Linux
     ↓
Apache
     ↓
PHP
     ↓
Web Application
```

Knowing the stack helps a pentester understand the technologies being used and research any relevant security considerations.

# Missing Security Headers

The room says the application has **no security headers**.

Security headers help browsers defend against certain web attacks.

Think of them as an **extra protective layer**.

If they're missing:

* Browser protection is weaker.
* The application may be missing security best practices.

This doesn't automatically mean the application is vulnerable, but it is something to note during an assessment.

------------

# Testing for Vertical Privilege Escalation

In the previous task, we learned that after login, the application returns a JSON response containing:

* `status`
* `message`
* `first_name`
* `last_name`
* `is_admin`
* `redirect_link`

The interesting field is:

**`redirect_link`**

It contains a URL like:

```text
dashboard.php?isadmin=false
```

As a penetration tester, this immediately raises a question:

> **Does the application trust this URL parameter to decide whether a user is an administrator?**


# Step 1: Capture the Login Response

Using **Burp Suite Proxy**, intercept the login response.

Inside the JSON response, you will find something similar to:

```text
redirect_link:
dashboard.php?isadmin=false
```

Normally, the browser automatically redirects you to the dashboard.

Instead of letting that happen, copy the URL from the response.

# Step 2: Test the Parameter

Paste the URL into your browser.

Now change:

```text
isadmin=false
```

to

```text
isadmin=true
```

The idea is **not to randomly change values**. You're testing whether the application improperly relies on a client-controlled parameter for authorization.

# Step 3: Observe the Response

In this intentionally vulnerable TryHackMe lab:

Instead of opening:

```text
dashboard.php
```

the application redirects to:

```text
admin.php
```

This means a **low-privileged user** can reach an **administrator page** simply by changing a parameter.

This is a **Vertical Privilege Escalation** vulnerability.

# Why Is This a Vulnerability?

Let's see what should happen.

### Secure Application

```text
User requests admin page
          ↓
Server checks session/database
          ↓
Is user an Admin?
      ↓          ↓
    Yes          No
     ↓            ↓
Allow Access   Access Denied
```

The server decides based on trusted information.

### Vulnerable Application

```text
User changes:

isadmin=false
        ↓
isadmin=true
        ↓
Server trusts the parameter
        ↓
Admin Page Opens
```

The application trusts **client-controlled input** instead of verifying the user's actual permissions on the server.

This is the core mistake.

# What is Vertical Privilege Escalation?

Vertical Privilege Escalation means:

> **A lower-privileged user gains higher privileges.**

Example:

```text
Normal User
      ↓
Changes request
      ↓
Gets Admin Access
```

The user moved **upwards** in privilege.

# What Happens on the Admin Page?

After reaching `admin.php`, the lab shows an administrator interface.

The page contains an **Admin Access** checkbox for users.

If you check your own account and click **Save Changes**, the application grants your account administrator privileges.

After becoming an administrator, you can perform administrator-only actions, such as modifying other users' administrative access.

This demonstrates the impact of the authorization flaw.


# Why Did This Happen?

The application made an insecure design decision.

Instead of checking:

```text
Who is the logged-in user?
```

it trusted:

```text
What does the URL parameter say?
```

This is dangerous because:

* Users control URLs.
* Users can modify requests.
* Attackers can use proxy tools like Burp Suite to change values.

**Never trust client-controlled data for authorization decisions.**

-------------

# Preventing Broken Access Control

Finding vulnerabilities is only one part of cybersecurity.

The other important part is **preventing them**.

There are several best practices developers should follow to reduce the risk of **Broken Access Control**.

# 1. Role-Based Access Control (RBAC)

One of the best ways to control access is by using **Role-Based Access Control (RBAC)**.

Instead of giving permissions directly to every user, permissions are assigned to **roles**.

Users are then assigned one or more roles.

Example:

| Role       | Permissions                  |
| ---------- | ---------------------------- |
| **Admin**  | Create, Read, Update, Delete |
| **Editor** | Create, Read, Update         |
| **User**   | Read Only                    |

For example:

```text
Admin
   ↓
Create
Read
Update
Delete
```

```text
Editor
   ↓
Create
Read
Update
```

```text
User
   ↓
Read
```

When a user tries to perform an action, the application asks:

> **Does this user's role have permission to perform this action?**

If yes:

**Allow**

If no:

**Deny**

The sample PHP function:

```php
hasPermission()
```

simply checks whether a particular role contains the required permission.

For example:

```
Role = Admin

Permission = Delete

↓

Allowed
```

But

```
Role = User

Permission = Delete

↓

Denied
```

## Why is RBAC Important?

Without RBAC:

Developers may accidentally forget permission checks.

With RBAC:

Permissions are centralized.

Every request checks the user's role before allowing access.

Think:

> **Role decides what the user can do.**


# 2. Parameterized Queries

Parameterized queries help prevent **SQL Injection**.

Suppose the application builds a SQL query like this:

```php
SELECT * FROM users
WHERE username='$username'
```

If the application directly inserts user input into SQL, an attacker may inject SQL commands.

Instead, developers should use **Prepared Statements (Parameterized Queries).**

Prepared statements separate:

* SQL code
* User data

The database treats user input only as **data**, not as SQL commands.

Think:

```
SQL Query
      +
User Input
```

Bad approach:

```
Mix everything together
```

Good approach:

```
SQL Structure
      ↓
Placeholder
      ↓
User Data
```

The database safely inserts the value.


## Why is this Important?

Even though SQL Injection is a different OWASP category, if attackers exploit SQL Injection, they may bypass authentication or retrieve unauthorized data.

So preventing SQL Injection also helps protect access control.


# 3. Proper Session Management

After login, the application creates a **Session**.

The session tells the server:

> **This user has already authenticated.**

Example:

```
User Logs In
      ↓
Server Creates Session
      ↓
Browser Stores Session Cookie
      ↓
Future Requests Use Same Session
```

The PHP example shows:

```php
session_start();
```

This creates or resumes a session.

Then:

```php
$_SESSION['user_id']
```

stores the authenticated user's ID.


## Session Timeout

The code also stores:

```php
last_activity
```

Every request checks:

```
Current Time
-
Last Activity
```

If more than **1800 seconds (30 minutes)** have passed:

```
Session Expired
```

The application destroys the session.

This prevents someone from using an old unattended session.


## Good Session Practices

Proper session management includes:

* Secure cookies
* Session timeout
* Session expiration
* Limiting active sessions
* Regenerating session IDs after login
* Destroying sessions after logout

Think:

> **Sessions prove that a user is still authenticated.**

# 4. Secure Coding Practices

Secure coding means writing code that avoids introducing security vulnerabilities.

Two important practices mentioned are:

## Validate and Sanitize User Input

Users should never be trusted.

The application should check all user input.

Example:

Instead of accepting anything,

the application cleans the input first.

PHP uses:

```php
filter_input()
```

This helps remove unwanted or dangerous input.

Think:

```
User Input
      ↓
Validate
      ↓
Sanitize
      ↓
Use Safely
```

## Secure Password Storage

The room compares two methods.

### Bad

```php
md5()
```

MD5 is an old hashing algorithm.

It is considered **cryptographically broken** for password storage because it is fast and vulnerable to modern password cracking attacks.

### Good

```php
password_hash()
```

`password_hash()` is designed specifically for storing passwords securely.

It automatically uses a modern password hashing algorithm and includes a unique salt.

Think:

```
Password
      ↓
password_hash()
      ↓
Secure Password Hash
```

The original password is **not stored directly**.

When the user logs in later, the application compares the entered password with the stored hash (typically using `password_verify()`).


------------
