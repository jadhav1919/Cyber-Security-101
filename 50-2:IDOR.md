# Insecure Direct Object Reference (IDOR)

**IDOR (Insecure Direct Object Reference)** is a type of **Broken Access Control** vulnerability.

It happens when:

> **The application allows users to access an object by changing its identifier, but the server does not verify whether the user is authorized to access that object.**

In simple words:

> **The server trusts the object ID instead of checking who owns it.**

---

# Why Does IDOR Happen?

Every web application stores objects such as:

* User profiles
* Orders
* Invoices
* Documents
* Messages
* Support tickets

Each object has a unique identifier (ID).

Example:

| Object         | ID   |
| -------------- | ---- |
| Sai's Profile  | 1305 |
| John's Profile | 1306 |
| Invoice        | 201  |
| Document       | 555  |

When you open your profile, the application may send:

```text
/profile?user_id=1305
```

The server uses **1305** to find your profile.

---

# How IDOR Works

Imagine you log in as Sai.

The browser requests:

```text
/profile?user_id=1305
```

The server returns:

* Sai's Name
* Sai's Email
* Sai's Profile

Everything is normal.

Now suppose you change:

```text
1305
```

to

```text
1000
```

Result:

```text
/profile?user_id=1000
```

If the server now shows another user's profile, the application has an **IDOR vulnerability**.

---

# Why Is This Vulnerable?

The application correctly authenticated you.

The server knows:

> **You are Sai.**

But it never asks:

> **Is Sai allowed to view profile 1000?**

Instead it simply does:

```text
User requested:

1000

↓

Retrieve Profile 1000

↓

Return Data
```

The missing step is:

```text
Is this profile owned by the logged-in user?
```

That missing check is the vulnerability.

---

# Authentication vs Authorization

This is one of the most important concepts.

### Authentication

Answers:

> **Who are you?**

Example:

You log in successfully.

The server knows you are Sai.

---

### Authorization

Answers:

> **What are you allowed to access?**

Example:

Can Sai access profile 1000?

If the server never checks this,

IDOR occurs.

---

# Authentication is NOT the Problem

Many beginners think:

> "The user is logged in, so authentication failed."

No.

Authentication worked perfectly.

The problem is:

**Authorization failed.**

The server authenticated the user,

but failed to verify ownership.

---

# Why is IDOR Dangerous?

Changing a single ID may allow access to:

* User profiles
* Orders
* Bank accounts
* Messages
* Medical records
* Documents
* Admin resources

Sometimes attackers can even:

* Modify another user's profile
* Change email address
* Reset passwords
* Delete data
* Take over accounts

A single missing authorization check can become a full account takeover.

---

# Plaintext IDOR

The simplest IDOR uses normal numbers.

Example:

```text
/profile?id=15
```

Change it to

```text
/profile?id=14
```

If another profile appears,

the application is vulnerable.

---

# Encoded IDOR

Sometimes developers hide IDs using **Base64 Encoding**.

Example:

Instead of:

```text
123
```

they send

```text
MTIz
```

This looks different,

but it is **NOT secure**.

---

## Base64 Workflow

An attacker simply does:

```text
Encoded Value

↓

Decode

↓

Modify

↓

Encode Again

↓

Send Request
```

Example:

```text
MTIz

↓

123

↓

124

↓

MTI0

↓

Send Request
```

If another user's data appears,

IDOR still exists.

---

## Important

Base64 is **Encoding**

NOT

**Encryption**

Encoding only changes the format.

Anyone can reverse it.

Think:

> **Encoding hides data from computers, not from attackers.**

---

# Hashed IDOR

Some applications use hashes instead of IDs.

Example:

Instead of:

```text
123
```

They send:

```text
202cb962ac59075b964b07152d234b70
```

This is an **MD5 hash**.

---

## Is Hashing Secure?

Hashing is better than encoding because it cannot simply be reversed.

However,

if developers hash predictable values like:

```text
1
2
3
4
5
```

An attacker can simply hash:

```text
1

↓

MD5

↓

Compare
```

Then:

```text
2

↓

MD5

↓

Compare
```

Eventually they discover the pattern.

Once they know:

```text
MD5(UserID)
```

they can generate hashes for every user.

So hashing alone **does not prevent IDOR**.

---

# Hash Lengths

You can often identify the hashing algorithm by length.

| Algorithm | Length        |
| --------- | ------------- |
| MD5       | 32 Characters |
| SHA-1     | 40 Characters |
| SHA-256   | 64 Characters |

Kali tools:

* hashid
* hash-identifier

help identify hashes.

---

# UUIDs and Random IDs

Some applications use random identifiers.

Example:

```text
d3b07384-d9a0-4e9b-8b3c-2f1a6c7e4a90
```

This is much harder to guess.

Random IDs prevent:

**Enumeration**

They do NOT automatically prevent IDOR.

---

# Two-Account Technique

If IDs cannot be guessed,

security testers use two accounts.

Example:

### Account A

Owns:

```text
Document XYZ
```

### Account B

Logs in separately.

Replace Account B's identifier with Account A's identifier.

If Account B receives Account A's data,

the application has IDOR.

The important idea:

> **Can another authenticated user access someone else's object?**

---

# Where Can Object References Be Found?

Many beginners only look at URLs.

This misses many IDOR vulnerabilities.

You should inspect **every request**.

---

## 1. URL Parameters

Example:

```text
/profile?id=5
```

---

## 2. POST Body

Example:

```text
user_id=5
```

---

## 3. Cookies

Example:

```text
user_id=5
```

---

## 4. HTTP Headers

Sometimes IDs appear inside custom headers.

---

## 5. REST API Paths

Example:

```text
/api/users/5/orders
```

---

## 6. AJAX / Background Requests

Modern websites load data silently.

Example:

```text
/api/v1/customer?id=15
```

You won't see this in the address bar.

You must inspect:

* Browser Network Tab
* Burp Suite

---

## 7. JavaScript Files

JavaScript often contains:

* Hidden API endpoints
* Parameter names
* Internal URLs

These may reveal hidden IDOR opportunities.

---

## 8. Parameter Mining

Sometimes developers leave hidden parameters.

Normal request:

```text
/user/details
```

Hidden feature:

```text
/user/details?user_id=5
```

The frontend never sends this parameter,

but the backend still accepts it.

Finding these hidden parameters is called:

> **Parameter Mining**

---

# Practical Lab

The lab demonstrates this vulnerability.

Steps:

### Step 1

Create an account.

---

### Step 2

Login.

---

### Step 3

Open:

**Your Account**

---

### Step 4

Open:

Developer Tools (F12)

↓

Network Tab

↓

Refresh Page

---

### Step 5

Observe a request like:

```text
/api/v1/customer?id=YOUR_ID
```

The server returns JSON:

```text
{
id
username
email
}
```

Notice:

The returned data depends entirely on:

```text
id=
```

---

### Step 6

Replay the request using:

* Browser "Edit and Resend"
* Burp Suite
* curl

Change:

```text
id=YourID
```

to

```text
id=1
```

If another user's information appears,

the application has an **IDOR vulnerability**.

Repeat with:

```text
id=3
```

to answer the TryHackMe question.

---

# How to Prevent IDOR

Developers should:

* Authenticate users.
* Authorize every request.
* Verify object ownership.
* Never trust user-controlled IDs.
* Use server-side authorization.
* Use RBAC/ABAC.
* Log unauthorized access attempts.

Correct flow:

```text
User Requests Object

↓

Authenticate User

↓

Check Ownership

↓

Allowed?

↓

Yes → Return Data

No → Access Denied
```

---

