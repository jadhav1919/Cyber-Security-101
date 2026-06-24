# SQL Fundamentals

## 1. What is a Database?

A **Database** is an organized collection of data that can be:

* Stored
* Accessed
* Updated
* Analyzed

### Examples

* User accounts (username/password)
* Social media posts and comments
* E-commerce orders
* Netflix watch history

 

# 2. Types of Databases

## Relational Database (SQL)

Stores data in **tables** using rows and columns.

### Example

| id | first_name | email                                       |
| -- | ---------- | ------------------------------------------- |
| 1  | John       | [john@example.com](mailto:john@example.com) |

### Features

* Structured data
* Relationships between tables
* High accuracy
* Uses SQL

### Examples

* MySQL
* MariaDB
* Oracle Database
* PostgreSQL

 

## Non-Relational Database (NoSQL)

Stores data in flexible formats such as:

* Documents
* Key-Value pairs
* Collections

### Example

```json
{
  "name": {
    "first": "Thomas",
    "last": "Anderson"
  },
  "occupation": ["The One"]
}
```

### Features

* Flexible structure
* Handles varying data formats
* Highly scalable

### Examples

* MongoDB
* Cassandra
* Redis

 

# 3. Tables, Rows, and Columns

## Table

A collection of related data.

Example:

```text
Books
```

 

## Column

Defines the type of information stored.

```text
id
name
published_date
```

 

## Row

A single record in a table.

| id | name                       | published_date |
| -- | -------------------------- | -------------- |
| 1  | Android Security Internals | 2014-10-14     |

 
# 4. Data Types

| Data Type | Description     |
| --------- | --------------- |
| INT       | Integer numbers |
| VARCHAR   | Text/String     |
| DATE      | Date values     |
| FLOAT     | Decimal numbers |

Example:

```sql
name VARCHAR(255)
price FLOAT
published_date DATE
```

 

# 5. Keys

## Primary Key

Uniquely identifies each record.

### Characteristics

* Must be unique
* Cannot be NULL
* One primary key per table

Example:

```sql
book_id INT PRIMARY KEY
```

 

## Foreign Key

Creates a relationship between tables.

### Example

Books Table:

```text
book_id
book_name
author_id
```

Authors Table:

```text
id
author_name
```

Here:

```text
Books.author_id
```

references

```text
Authors.id
```

 

# 6. DBMS (Database Management System)

Software used to manage databases.

Acts as an interface between:

```text
User ↔ DBMS ↔ Database
```

### Examples

* MySQL
* MariaDB
* Oracle Database
* MongoDB

 

# 7. SQL (Structured Query Language)

SQL is used to:

* Create databases
* Create tables
* Insert data
* Retrieve data
* Update data
* Delete data

 

# 8. Why Learn SQL?

### Fast

Returns large amounts of data quickly.

### Easy

Uses English-like syntax.

### Reliable

Maintains data integrity.

### Flexible

Powerful querying capabilities.

 

# 9. Database Statements

## Create Database

```sql
CREATE DATABASE thm_bookmarket_db;
```

 

## Show Databases

```sql
SHOW DATABASES;
```

 

## Select Database

```sql
USE thm_bookmarket_db;
```

 

## Delete Database

```sql
DROP DATABASE database_name;
```

 

# 10. Table Statements

## Create Table

```sql
CREATE TABLE book_inventory (
    book_id INT AUTO_INCREMENT PRIMARY KEY,
    book_name VARCHAR(255) NOT NULL,
    publication_date DATE
);
```

 

## Show Tables

```sql
SHOW TABLES;
```

 

## Describe Table

```sql
DESCRIBE book_inventory;
```

Shortcut:

```sql
DESC book_inventory;
```

 

## Alter Table

Add a new column:

```sql
ALTER TABLE book_inventory
ADD page_count INT;
```

 

## Drop Table

```sql
DROP TABLE table_name;
```

 

# 11. CRUD Operations

CRUD = Create, Read, Update, Delete

 

## Create (INSERT)

```sql
INSERT INTO books
(id, name, published_date, description)
VALUES
(1, "Android Security Internals",
"2014-10-14",
"Security Architecture Guide");
```

 

## Read (SELECT)

All columns:

```sql
SELECT * FROM books;
```

Specific columns:

```sql
SELECT name, description
FROM books;
```

 

## Update (UPDATE)

```sql
UPDATE books
SET description = "Updated Description"
WHERE id = 1;
```

 

## Delete (DELETE)

```sql
DELETE FROM books
WHERE id = 1;
```

 

# 12. SQL Clauses

## DISTINCT

Removes duplicate values.

```sql
SELECT DISTINCT name
FROM books;
```

 

## GROUP BY

Groups records together.

```sql
SELECT name, COUNT(*)
FROM books
GROUP BY name;
```

 

## ORDER BY

### Ascending

```sql
SELECT *
FROM books
ORDER BY published_date ASC;
```

### Descending

```sql
SELECT *
FROM books
ORDER BY published_date DESC;
```

 
## HAVING

Filters grouped results.

```sql
SELECT name, COUNT(*)
FROM books
GROUP BY name
HAVING name LIKE '%Hack%';
```

 

# 13. Logical Operators

## LIKE

Pattern matching.

```sql
SELECT *
FROM books
WHERE description LIKE '%guide%';
```

 

## AND

Both conditions must be true.

```sql
SELECT *
FROM books
WHERE category='Offensive Security'
AND name='Bug Bounty Bootcamp';
```

 

## OR

At least one condition must be true.

```sql
SELECT *
FROM books
WHERE name LIKE '%Android%'
OR name LIKE '%iOS%';
```

 

## NOT

Negates a condition.

```sql
SELECT *
FROM books
WHERE NOT description LIKE '%guide%';
```

 

## BETWEEN

Checks range.

```sql
SELECT *
FROM books
WHERE id BETWEEN 2 AND 4;
```

 

# 14. Comparison Operators

## Equal To (=)

```sql
SELECT *
FROM books
WHERE name='Designing Secure Software';
```

 

## Not Equal To (!=)

```sql
SELECT *
FROM books
WHERE category != 'Offensive Security';
```

 

## Less Than (<)

```sql
SELECT *
FROM books
WHERE published_date < '2020-01-01';
```

 

## Greater Than (>)

```sql
SELECT *
FROM books
WHERE published_date > '2020-01-01';
```

 

## Less Than or Equal To (<=)

```sql
SELECT *
FROM books
WHERE published_date <= '2021-11-15';
```

 

## Greater Than or Equal To (>=)

```sql
SELECT *
FROM books
WHERE published_date >= '2021-11-02';
```

 

# 15. String Functions

## CONCAT()

Combines strings.

```sql
SELECT CONCAT(name,
' is a ',
category,
' book')
AS book_info
FROM books;
```

 

## GROUP_CONCAT()

Combines multiple rows into one string.

```sql
SELECT category,
GROUP_CONCAT(name SEPARATOR ', ')
AS books
FROM books
GROUP BY category;
```

 

## SUBSTRING()

Extract part of a string.

```sql
SELECT SUBSTRING(
published_date,
1,
4
)
AS year
FROM books;
```

 

## LENGTH()

Returns string length.

```sql
SELECT LENGTH(name)
AS name_length
FROM books;
```

 

# 16. Aggregate Functions

## COUNT()

Counts rows.

```sql
SELECT COUNT(*)
AS total_books
FROM books;
```

 

## SUM()

Adds values.

```sql
SELECT SUM(price)
AS total_price
FROM books;
```

 

## MAX()

Returns largest value.

```sql
SELECT MAX(published_date)
AS latest_book
FROM books;
```

  

## MIN()

Returns smallest value.

```sql
SELECT MIN(published_date)
AS earliest_book
FROM books;
```

---

# Exam / Interview Questions

### What is SQL?

Structured Query Language used to manage relational databases.

### Difference between SQL and NoSQL?

| SQL                  | NoSQL                          |
| -------------------- | ------------------------------ |
| Structured           | Flexible                       |
| Tables               | Documents/Collections          |
| Uses SQL             | Uses different query methods   |
| Strong relationships | Less emphasis on relationships |

### Difference between Primary Key and Foreign Key?

| Primary Key             | Foreign Key      |
| ----------------------- | ---------------- |
| Uniquely identifies row | Links tables     |
| Unique                  | Can repeat       |
| One per table           | Multiple allowed |

### What does CRUD stand for?

* Create → INSERT
* Read → SELECT
* Update → UPDATE
* Delete → DELETE

### Difference between WHERE and HAVING?

| WHERE              | HAVING                  |
| ------------------ | ----------------------- |
| Filters rows       | Filters grouped results |
| Before aggregation | After aggregation       |

---

