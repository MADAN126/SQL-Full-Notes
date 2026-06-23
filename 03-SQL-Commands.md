# 03-SQL-Commands.md

## Interacting with Oracle Database

Oracle databases can be accessed using multiple approaches.

### 1. Command Line Interface (CLI)

Tool:

```text
SQL*Plus
```

Example:

```sql
SQL> SELECT * FROM employees;
```

---

### 2. Web Interface

Browser-based Oracle administration tools.

---

### 3. Graphical User Interface (GUI)

Popular GUI tools:

- Oracle SQL Developer
- Toad For Oracle

These are the most commonly used tools in real-world projects.

---

# Oracle Database Accounts

## DBA Account

### Purpose

Database Administrator account responsible for managing the database.

### Default DBA Accounts

```text
SYS
SYSTEM
```

### Responsibilities

- Create Users
- Grant Permissions
- Revoke Permissions
- Manage Database Objects
- Perform Backup and Recovery

---

## Normal Database User

Examples:

```text
rajesh
mahesh
ramesh
```

Normal users can create and manage objects only if permissions are granted.

---

# Creating a User in Oracle

## Step 1: Create User

Syntax:

```sql
CREATE USER username
IDENTIFIED BY password;
```

Example:

```sql
CREATE USER ramesh
IDENTIFIED BY ashokit;
```

Output:

```text
User created.
```

---

## Step 2: Grant Permissions

A newly created user has no privileges.

Permissions must be granted.

Syntax:

```sql
GRANT privilege
TO username;
```

Example:

```sql
GRANT RESOURCE, CONNECT
TO ramesh;
```

Output:

```text
Grant succeeded.
```

---

## Why Permissions Are Required?

Without permissions, a user cannot create database objects.

Examples:

- Tables
- Sequences
- Indexes
- Views
- Procedures
- Functions

---

## Step 3: Connect as New User

Command:

```sql
CONNECT
```

Example:

```text
Enter user-name : ramesh
Enter password  : ashokit

Connected.
```

---

# Important Rule

## Who Can Create Users?

Only DBA accounts can create users.

Example:

```text
SYS
SYSTEM
```

---

## Can One Normal User Create Another User?

```text
No
```

Only users with administrative privileges can create users.

---

# SQL Commands

## Definition

SQL Commands are SQL Statements or SQL Queries used to perform operations on a database.

Example:

```sql
SELECT * FROM emp;
```

Every SQL statement must end with a semicolon.

```sql
SELECT * FROM emp;
```

---

# Categories of SQL Commands

```text
SQL Commands
      │
      ├── DDL
      ├── DML
      ├── DCL
      ├── DRL
      └── TCL
```

---

# 1. DDL (Data Definition Language)

## Purpose

Used to define and modify the structure of database objects.

DDL affects metadata (structure), not data.

---

## DDL Commands

### CREATE

Creates new database objects.

Example:

```sql
CREATE TABLE student(
    id NUMBER,
    name VARCHAR2(30)
);
```

---

### ALTER

Modifies an existing database object.

Example:

```sql
ALTER TABLE student
ADD age NUMBER;
```

---

### DROP

Permanently removes a database object.

Example:

```sql
DROP TABLE student;
```

---

### TRUNCATE

Removes all rows from a table.

Structure remains.

Example:

```sql
TRUNCATE TABLE student;
```

---

## DDL Summary

| Command | Purpose |
|----------|----------|
| CREATE | Create Object |
| ALTER | Modify Object |
| DROP | Delete Object |
| TRUNCATE | Delete All Rows |

---

# 2. DML (Data Manipulation Language)

## Purpose

Used to manipulate data stored inside database objects.

---

## DML Commands

### INSERT

Adds new records.

Example:

```sql
INSERT INTO student
VALUES(101,'Mahesh');
```

---

### UPDATE

Modifies existing records.

Example:

```sql
UPDATE student
SET name='Rajesh'
WHERE id=101;
```

---

### DELETE

Removes records.

Example:

```sql
DELETE FROM student
WHERE id=101;
```

---

## DML Summary

| Command | Purpose |
|----------|----------|
| INSERT | Add Data |
| UPDATE | Modify Data |
| DELETE | Remove Data |

---

# 3. DCL (Data Control Language)

## Purpose

Used to manage permissions and security.

Usually performed by DBAs.

---

## DCL Commands

### GRANT

Provides privileges.

Example:

```sql
GRANT CONNECT
TO ramesh;
```

---

### REVOKE

Removes privileges.

Example:

```sql
REVOKE CONNECT
FROM ramesh;
```

---

## DCL Summary

| Command | Purpose |
|----------|----------|
| GRANT | Give Permission |
| REVOKE | Remove Permission |

---

# 4. DRL (Data Retrieval Language)

## Purpose

Used to retrieve data from database tables.

---

## DRL Command

### SELECT

Retrieves records.

Example:

```sql
SELECT *
FROM student;
```

---

### Retrieve Specific Columns

```sql
SELECT id,name
FROM student;
```

---

### Retrieve Filtered Data

```sql
SELECT *
FROM student
WHERE id=101;
```

---

## DRL Summary

| Command | Purpose |
|----------|----------|
| SELECT | Retrieve Data |

---

# 5. TCL (Transaction Control Language)

## Purpose

Used for transaction management.

---

## What is a Transaction?

A transaction is a group of SQL operations treated as a single unit.

Example:

```text
Withdraw Money
      +
Deposit Money
```

Both operations must succeed together.

---

## TCL Commands

### COMMIT

Makes changes permanent.

Example:

```sql
COMMIT;
```

---

### ROLLBACK

Undo changes before commit.

Example:

```sql
ROLLBACK;
```

---

## TCL Summary

| Command | Purpose |
|----------|----------|
| COMMIT | Save Changes Permanently |
| ROLLBACK | Undo Changes |

---

# Complete SQL Classification

| Category | Full Form | Commands |
|-----------|-----------|-----------|
| DDL | Data Definition Language | CREATE, ALTER, DROP, TRUNCATE |
| DML | Data Manipulation Language | INSERT, UPDATE, DELETE |
| DCL | Data Control Language | GRANT, REVOKE |
| DRL | Data Retrieval Language | SELECT |
| TCL | Transaction Control Language | COMMIT, ROLLBACK |

---

# Interview Questions

## What are SQL Commands?

SQL statements used to perform operations on a database.

---

## What is DDL?

Commands used to create, modify, and delete database structures.

Commands:

```text
CREATE
ALTER
DROP
TRUNCATE
```

---

## What is DML?

Commands used to manipulate data.

Commands:

```text
INSERT
UPDATE
DELETE
```

---

## What is DCL?

Commands used to control permissions.

Commands:

```text
GRANT
REVOKE
```

---

## What is DRL?

Commands used to retrieve data.

Command:

```text
SELECT
```

---

## What is TCL?

Commands used to manage transactions.

Commands:

```text
COMMIT
ROLLBACK
```

---

## Difference Between DELETE, TRUNCATE, and DROP

| DELETE | TRUNCATE | DROP |
|----------|----------|-------|
| Removes Selected Rows | Removes All Rows | Removes Entire Table |
| DML | DDL | DDL |
| Can Use WHERE | No WHERE | Object Deleted |
| Structure Remains | Structure Remains | Structure Removed |

---

# Quick Revision

```text
DDL -> Structure

CREATE   -> Create Object
ALTER    -> Modify Object
DROP     -> Delete Object
TRUNCATE -> Remove All Rows

DML -> Data

INSERT -> Add Data
UPDATE -> Modify Data
DELETE -> Remove Data

DCL -> Permissions

GRANT  -> Give Permission
REVOKE -> Remove Permission

DRL -> Retrieval

SELECT -> Fetch Data

TCL -> Transactions

COMMIT   -> Save Changes
ROLLBACK -> Undo Changes

SYS/SYSTEM -> DBA Accounts
```
