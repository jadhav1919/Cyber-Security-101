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
