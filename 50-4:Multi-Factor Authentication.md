# Multi-Factor Authentication (MFA)

## What is MFA?

**Multi-Factor Authentication (MFA)** is a security method that requires **two or more verification factors** before a user can access an account or system.

Instead of relying only on a password, MFA adds extra layers of security.

Simple definition:

> **MFA = Verify your identity using multiple authentication factors.**

The goal is:

> **Even if an attacker steals your password, they still cannot log in without the additional authentication factor(s).**

# Why Do We Need MFA?

Suppose your password is:

```text
Password = mypassword123
```

If an attacker steals it through:

* Phishing
* Data breach
* Keylogger
* Password reuse

they can immediately log in.

With MFA:

```text
Password
      +
OTP / Fingerprint / Security Key
```

the attacker needs **both factors**.

This makes account compromise much more difficult.

# 2FA vs MFA

Many people think they're the same.

They are related, but not identical.

## 2FA (Two-Factor Authentication)

Requires **exactly two authentication factors.**

Example:

```text
Password
+
OTP
```

Two factors only.


## MFA (Multi-Factor Authentication)

Requires **two or more authentication factors.**

Example:

```text
Password
+
Fingerprint
+
Security Key
```

Three factors.

This is MFA, but **not** 2FA.

## Easy Way to Remember

```text
All 2FA is MFA

BUT

Not all MFA is 2FA
```


# Authentication Factors

MFA uses factors from different categories.

There are **five major authentication factors**.

---

# 1. Something You Know

This is information stored in your memory.

Examples:

* Password
* PIN
* Security Question

Example:

```text
Password = Sai@123
```

Advantages:

* Easy to use.

Disadvantages:

* Can be guessed.
* Can be stolen.
* Can be phished.

# 2. Something You Have

Something physically owned by the user.

Examples:

* Mobile phone
* Authenticator App
* Smart Card
* Hardware Token
* Client Certificate

Example:

```text
Google Authenticator
```

Even if someone knows your password,

they still need your phone.

# 3. Something You Are

Biometric authentication.

Examples:

* Fingerprint
* Face Recognition
* Iris Scan

Example:

```text
Touch Finger

↓

Phone Unlocks
```

Important:

Biometrics are **not 100% accurate**.

A fingerprint never matches perfectly.

Therefore,

biometrics should be used **together with other factors**, not alone.


# 4. Somewhere You Are

Authentication based on location.

Examples:

* IP Address
* GPS Location
* Country
* Office Network

Example:

```text
Office Network

↓

Normal Login
```

But:

```text
Unknown Country

↓

Require OTP
```

Banks commonly use this.

# 5. Something You Do

Authentication based on behavior.

Examples:

* Typing speed
* Mouse movement
* Touchscreen behavior

This is called **Behavioral Authentication**.

Example:

The application learns how you normally type.

If typing suddenly changes significantly,

it requests additional authentication.

This is the hardest type to implement.

# Summary of Authentication Factors

| Factor             | Example                        |
| ------------------ | ------------------------------ |
| Something You Know | Password, PIN                  |
| Something You Have | Phone, Security Key            |
| Something You Are  | Fingerprint, Face Scan         |
| Somewhere You Are  | Office Network, IP Address     |
| Something You Do   | Typing Pattern, Mouse Movement |


# Common 2FA Methods

## 1. TOTP (Time-Based One-Time Password)

Most common method.

Apps:

* Google Authenticator
* Microsoft Authenticator
* Authy

Every **30 seconds**, a new OTP is generated.

Example:

```text
Current OTP

↓

548731

↓

30 Seconds Later

↓

834125
```

Old OTP becomes invalid.

Advantages:

* Very secure.
* Difficult to reuse.


# 2. Push Notification

Applications send a notification to your phone.

Example:

```text
Login Attempt

↓

Phone Receives Notification

↓

Approve / Deny
```

Apps:

* Duo
* Google Prompt

Only the owner of the phone can approve.


# 3. SMS OTP

Most websites use this.

Flow:

```text
Login

↓

SMS Sent

↓

123456

↓

Enter OTP
```

Advantages:

* Simple.
* Easy for users.

Disadvantages:

* SIM swapping.
* SMS interception.
* Less secure than TOTP.

# 4. Hardware Tokens

Example:

```text
YubiKey
```

These devices generate OTPs or authenticate using NFC/USB.

Advantages:

* Very secure.
* Works offline.
* Cannot easily be copied.

# Conditional Access

Conditional Access changes authentication requirements depending on the situation.

Think of it as:

```text
If Condition Changes

↓

Increase Security
```

## Location-Based

Example:

```text
Office

↓

Password Only
```

But

```text
Different Country

↓

Password + OTP
```

## Time-Based

Example:

```text
Working Hours

↓

Password
```

After office hours:

```text
Password

+

OTP
```

## Behavioral Analysis

Suppose a user suddenly:

* Downloads huge amounts of data.
* Logs in at midnight.
* Opens unusual files.

The application may request additional authentication.

## Device-Based

Example:

```text
Company Laptop

↓

Allowed
```

```text
Personal Laptop

↓

Blocked
```

Many companies only allow trusted devices.


# Where is MFA Used?

## Banking

Bank login usually uses:

```text
Password

+

OTP
```

Even if a password is stolen,

transactions cannot proceed without the OTP.


## Healthcare

Hospitals protect patient records.

Example:

```text
Security Badge

+

Fingerprint
```

Only authorized doctors can access medical records.


## Corporate IT

Companies protect:

* Email
* VPN
* Cloud
* Internal Systems

Typical login:

```text
Corporate Password

+

Authenticator App
```


# Common MFA Vulnerabilities

Even MFA can be implemented incorrectly.


# 1. Weak OTP Generation

If OTPs follow predictable patterns,

attackers can guess them.

Example:

```text
1001

↓

1002

↓

1003
```

This is insecure.

OTPs should be random.



# 2. OTP Leakage

One of the most common implementation mistakes.

After login,

the application requests an OTP.

Instead of only sending:

```text
Success
```

the server accidentally returns:

```json
{
"token":"482931"
}
```

The attacker simply reads the response.

No guessing needed.


## Practical Lab

Workflow:

```text
Login

↓

Open Developer Tools

↓

Network Tab

↓

XHR Request

↓

/token

↓

Response

↓

OTP Found

↓

Enter OTP

↓

Login Successful
```

This is **insecure coding**.

The server should **never** return the generated OTP to the client.

Instead, it should return:

```text
Success
```


# 3. Brute Forcing OTP

Suppose OTP has:

```text
4 Digits
```

Possible values:

```text
0000

↓

9999
```

If unlimited guesses are allowed,

eventually the attacker may find the correct OTP.

# 4. No Rate Limiting

Without rate limiting:

```text
Try OTP

↓

Wrong

↓

Try Again

↓

Wrong

↓

Try Again

↓

Unlimited Attempts
```

Eventually,

the correct OTP may be guessed.

Applications should:

* Limit attempts.
* Lock accounts temporarily.
* Increase delays.


# 5. Evilginx

**Evilginx** is a phishing framework used in authorized security testing and, unfortunately, by attackers.

It works as a **Man-in-the-Middle (MITM) Proxy**.

Flow:

```text
Victim

↓

Fake Login Page

↓

Username

↓

Password

↓

OTP

↓

Evilginx

↓

Real Website
```

The victim logs into what appears to be the legitimate website.

Evilginx forwards everything to the real website while capturing:

* Username
* Password
* Session Cookie

Attackers often don't need the OTP afterward because they can reuse the authenticated session cookie.


# Logic Flaw: MFA Bypass

One of the most dangerous MFA vulnerabilities.

Suppose login works like this:

```text
Username

↓

Password

↓

OTP

↓

Dashboard
```

A secure application should only allow dashboard access **after OTP verification**.

## Secure Flow

```text
Username

↓

Password

↓

OTP

↓

Verify OTP

↓

Session Authenticated

↓

Dashboard
```

## Vulnerable Flow

Suppose the application creates:

```php
$_SESSION['authenticated']=true;
```

immediately after:

```text
Username

↓

Password
```

Instead of waiting until OTP verification.

Then:

```text
Username

↓

Password

↓

Session Created

↓

Attacker Visits Dashboard Directly

↓

Access Granted
```

The attacker completely bypasses MFA.

# Correct Session Management

The room recommends using **two separate authentication states**.

### Session 1

```text
Username

+

Password

↓

Can Access Only MFA Page
```

---

### Session 2

Created **only after successful OTP verification**.

```text
OTP Verified

↓

Authenticated Session

↓

Dashboard Access
```

This prevents MFA bypass.


# Why Some Apps Return to Login After OTP Failure

After several failed OTP attempts,

many applications:

* Destroy the session.
* Force the user to log in again.

Reasons:

* Prevent brute-force attacks.
* Limit repeated OTP guessing.
* Verify credentials again.


# Automation

Attackers often automate repetitive tasks.

Automation helps because it:

* Logs in automatically.
* Handles session expiration.
* Repeats requests consistently.
* Saves time.

In the lab, the Python script repeatedly:

```text
Login

↓

Submit OTP

↓

Logged Out?

↓

Login Again

↓

Retry
```

until it eventually receives a valid authenticated session.

The purpose of the lab is to demonstrate **why applications need strong rate limiting, proper session management, and secure OTP handling**.



# How to Prevent MFA Vulnerabilities

Developers should:

* Generate cryptographically secure random OTPs.
* Never return OTPs in HTTP responses.
* Implement rate limiting.
* Lock accounts after repeated failures.
* Separate pre-MFA and post-MFA sessions.
* Validate OTPs server-side.
* Protect session cookies.
* Use secure authentication flows.
