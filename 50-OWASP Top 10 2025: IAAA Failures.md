# IAAA and OWASP Top 10:2025

This TryHackMe room focuses on three OWASP Top 10:2025 categories related to **Identity, Authentication, Authorisation, and Accountability (IAAA)**.

The three categories are:

| OWASP Category                       | Problem                                                  |
| ------------------------------------ | -------------------------------------------------------- |
| **A01: Broken Access Control**       | User accesses something they should not                  |
| **A07: Authentication Failures**     | Application fails to correctly verify the user           |
| **A09: Logging & Alerting Failures** | Application fails to properly record or alert on attacks |

The main idea is that all three are related to **how applications manage users and their actions**.

# What is IAAA?

**IAAA** stands for:

**Identity → Authentication → Authorisation → Accountability**

These happen in order. You cannot properly perform a later step if the previous step has not been established.

### Identity

**Identity means: Who are you claiming to be?**

It is the unique account representing a person or service.

Examples are a username, email address, or user ID.

For example:

**Username: sai123**

The application now knows the identity you are claiming.

### Authentication

**Authentication means: Prove that identity is really yours.**

Examples include:

* Password
* OTP
* Passkey
* MFA

For example, you claim:

**I am sai123**

The application asks for your password.

If the password is correct, your identity is authenticated.

### Authorisation

**Authorisation means: What are you allowed to do?**

After the application confirms your identity, it checks your permissions.

For example:

**Normal User → View own account**

**Admin → View and manage all accounts**

Authentication answers:

**Who are you?**

Authorisation answers:

**What can you do?**

### Accountability

**Accountability means: Record who did what, when, and from where.**

For example:

**User:** admin

**Action:** Changed user role

**Time:** 10:30 AM

**Source IP:** 10.10.10.5

Logs help security teams investigate suspicious activity and understand what happened.

The easiest way to remember IAAA is:

> **Identity = Who are you? → Authentication = Prove it → Authorisation = What can you do? → Accountability = Record what you did**

# A01: Broken Access Control

**Broken Access Control** happens when the server fails to properly check whether a user is allowed to access a resource or perform an action.

The important point is:

> **The server must check authorisation on every request.**

Suppose you access your bank account using an `accountID` value.

Your account is `7`.

You change the ID from `7` to `6`.

If the application now shows another user's bank account without checking whether you own account `6`, the access control is broken.

This is a common vulnerability called **IDOR**.

## What is IDOR?

**IDOR** stands for **Insecure Direct Object Reference**.

It happens when an application directly uses a user-controlled object identifier without properly checking authorisation.

For example, you are allowed to access account `7`.

You change the account ID to `6`.

The server should ask:

> **Does this logged-in user have permission to access account 6?**

If the server does not perform this check and returns the account data, the application has an IDOR vulnerability.

The problem is **not simply that the ID can be changed**.

The real problem is:

> **The server failed to verify whether the user is authorised to access the requested object.**

## Horizontal Privilege Escalation

**Horizontal Privilege Escalation** means accessing another user's data while staying at the same privilege level.

For example:

**Normal User Sai → Accesses Normal User John's account**

Both users have the same role, but Sai accesses John's information.

Think:

> **Same level → Different user's data**

## Vertical Privilege Escalation

**Vertical Privilege Escalation** means gaining access to higher-level privileges.

For example:

**Normal User → Admin Functions**

The user moves from a lower privilege level to a higher privilege level.

Think:

> **Low privilege → High privilege**

### Horizontal vs Vertical

| Type           | Simple Meaning                               |
| -------------- | -------------------------------------------- |
| **Horizontal** | Access another user's data at the same level |
| **Vertical**   | Gain higher-level permissions                |


# A07: Authentication Failures

**Authentication Failures** happen when an application cannot correctly verify or securely bind a user to their identity.

This may allow an attacker to log in as another user.

Common authentication problems include:

* Username enumeration.
* Weak or guessable passwords.
* No rate limiting.
* No account lockout.
* Login logic flaws.
* Registration logic flaws.
* Insecure sessions.
* Insecure cookie handling.

---

## Username Enumeration

**Username Enumeration** means discovering whether a username exists.

For example, imagine the login page gives different errors.

**Unknown username:** User does not exist.

**Correct username, wrong password:** Incorrect password.

An attacker can test usernames and identify valid accounts.

A safer application may return a general message such as:

**Invalid username or password.**

## Weak Password Protection

If an application allows weak passwords and has no rate limiting or lockout, an attacker may repeatedly guess passwords.

For example:

**admin123**

**password**

**admin@123**

**123456**

Without proper protection, automated password guessing becomes easier.


## Login and Registration Logic Flaws

Sometimes the authentication code itself contains a logic mistake.

The TryHackMe example uses:

**Existing account: `admin`**

The attacker registers:

**`aDmiN`**

The application may incorrectly treat these usernames differently during registration but treat them as the same during login.

The problem is **inconsistent username handling**.

One part of the application may be case-sensitive while another part may be case-insensitive.

This can cause the wrong account to be authenticated.


## Canonical Form

A **canonical form** means converting input into one consistent format before processing or comparing it.

For example:

**admin**

**Admin**

**aDmiN**

The application could convert all usernames to lowercase.

After conversion, all become:

**admin**

The database should then enforce uniqueness on this canonical form.

This prevents users from creating confusing variations of an existing username.

## Session and Cookie Problems

After successful login, the application usually creates a **session**.

The session tells the server:

**This request belongs to this authenticated user.**

If sessions or cookies are handled insecurely, an attacker may steal, reuse, or manipulate them.

Applications should also rotate sessions after important events such as:

* Login.
* Password changes.
* Privilege changes.

# A09: Logging & Alerting Failures

**Logging & Alerting Failures** happen when an application does not properly record or alert on security-relevant events.

Without good logs, defenders may know that an attack happened but cannot clearly understand:

* Who performed the action?
* What did they do?
* When did it happen?
* Where did the request come from?

This directly affects **Accountability**.

## What Should Applications Log?

Important security events include:

* Successful logins.
* Failed logins.
* Password changes.
* MFA or 2FA changes.
* User role changes.
* Privilege changes.
* Administrator actions.
* Suspicious authentication activity.

For example, imagine this activity:

**100 failed login attempts → Successful admin login → User role changed**

This is highly suspicious.

If the application records and monitors these events, defenders may detect the attack.

If these events are not logged, investigating the attack becomes much harder.

## Logging vs Alerting

**Logging** means recording an event.

**Alerting** means notifying the security team when suspicious behavior is detected.

For example:

**Failed Login → Log the event**

But:

**100 Failed Logins in 1 Minute → Generate Security Alert**

So remember:

> **Logging = Record**

> **Alerting = Notify**


## Centralised Logging

Logs should ideally be sent to a central logging or SIEM system.

They should not only remain on the application server.

Why?

If an attacker compromises the server, they may attempt to modify or delete local logs.

Sending logs to another protected system helps preserve evidence.

Organizations should also define proper **log retention**, meaning how long logs are stored.

# Connecting IAAA to OWASP

| IAAA Concept              | OWASP Failure                   |
| ------------------------- | ------------------------------- |
| Identity / Authentication | A07 Authentication Failures     |
| Authorisation             | A01 Broken Access Control       |
| Accountability            | A09 Logging & Alerting Failures |

This is the main structure of the room.

**Authentication fails → Attacker may become another user**

**Authorisation fails → User accesses unauthorized resources**

**Accountability fails → Defenders cannot properly detect or investigate the attack**

-------------
