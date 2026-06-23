# 08-SQL-Commands-DML-DRL-TCL.md

# SQL Command Categories

SQL commands are classified into five major categories.

```text
SQL Commands
│
├── DDL
├── DML
├── DCL
├── DRL / DQL
└── TCL
```

| Category | Purpose | Commands |
|-----------|----------|----------|
| DDL | Structure Management | CREATE, ALTER, DROP, TRUNCATE, RENAME |
| DML | Data Manipulation | INSERT, UPDATE, DELETE |
| DCL | Access Control | GRANT, REVOKE |
| DRL/DQL | Data Retrieval | SELECT |
| TCL | Transaction Control | COMMIT, ROLLBACK, SAVEPOINT |

---

# DDL Commands

## Purpose

Used to manage the structure of database objects.

### Commands

```sql
CREATE
ALTER
DROP
TRUNCATE
RENAME
FLASHBACK
PURGE
```

---

## Auto Commit Behavior

All DDL commands are automatically committed.

```text
Execute DDL
      ↓
Automatic Commit
      ↓
Cannot Rollback
```

Example:

```sql
DROP TABLE employees;
```

The change is committed immediately.

---

# DML Commands

## Purpose

Used to manipulate data inside tables.

### Commands

```sql
INSERT
UPDATE
DELETE
```

---

## Auto Commit Behavior

DML commands are NOT auto committed.

```text
Execute DML
      ↓
Temporary Transaction
      ↓
COMMIT or ROLLBACK Required
```

---

# WHERE Clause

Used to apply conditions.

---

## UPDATE Without WHERE

```sql
UPDATE employees
SET salary = 50000;
```

Effect:

```text
All rows updated
```

---

## UPDATE With WHERE

```sql
UPDATE employees
SET salary = 50000
WHERE emp_id = 101;
```

Effect:

```text
Only matching row updated
```

---

## DELETE Without WHERE

```sql
DELETE FROM employees;
```

Effect:

```text
All rows deleted
```

---

## DELETE With WHERE

```sql
DELETE FROM employees
WHERE emp_id = 101;
```

Effect:

```text
Only matching row deleted
```

---

# DRL / DQL Commands

## Full Forms

```text
DRL = Data Retrieval Language

DQL = Data Query Language
```

---

## SELECT Command

Used to retrieve data from existing tables.

---

# Retrieve All Rows

## Syntax

```sql
SELECT *
FROM table_name;
```

---

## Example

```sql
SELECT *
FROM emp;
```

---

## Meaning of *

```text
* = All Columns
```

---

# Retrieve Rows Using Conditions

## Syntax

```sql
SELECT *
FROM table_name
WHERE condition;
```

---

## Example

```sql
SELECT *
FROM emp
WHERE deptno = 10;
```

---

## Flow

```text
EMP Table
     ↓
Apply Condition
     ↓
Return Matching Rows
```

---

# Selection

## Definition

Retrieving rows completely or partially based on a condition.

---

### Examples

Retrieve all rows:

```sql
SELECT *
FROM emp;
```

---

Retrieve employees from department 10:

```sql
SELECT *
FROM emp
WHERE deptno = 10;
```

---

## Key Idea

Selection focuses on:

```text
ROWS
```

---

# Projection

## Definition

Retrieving specific columns from a table.

---

### Examples

```sql
SELECT empno, ename
FROM emp;
```

---

```sql
SELECT empno, ename, job
FROM emp;
```

---

```sql
SELECT empno
FROM emp;
```

---

```sql
SELECT empname
FROM emp;
```

---

## Key Idea

Projection focuses on:

```text
COLUMNS
```

---

# Selection vs Projection

| Feature | Selection | Projection |
|----------|-----------|------------|
| Focus | Rows | Columns |
| Uses WHERE | Usually Yes | Not Required |
| Returns | Specific Records | Specific Fields |

---

## Selection Example

```sql
SELECT *
FROM emp
WHERE deptno = 10;
```

Returns:

```text
Selected Rows
```

---

## Projection Example

```sql
SELECT empno, ename
FROM emp;
```

Returns:

```text
Selected Columns
```

---

# TCL Commands

## Full Form

```text
Transaction Control Language
```

---

## Commands

```sql
COMMIT
ROLLBACK
SAVEPOINT
```

---

# Transaction

## Definition

Any DML operation performed on database tables.

### DML Operations

```sql
INSERT
UPDATE
DELETE
```

---

## Example

```sql
INSERT INTO emp VALUES(...);

UPDATE emp SET sal=5000;

DELETE FROM emp WHERE empno=101;
```

Each operation is part of a transaction.

---

# Session

## Definition

The time period between login and logout.

```text
Login
   ↓
Transactions
   ↓
Logout
```

---

## Example

```text
User Login
      ↓
INSERT
UPDATE
DELETE
      ↓
User Logout
```

This entire duration is one session.

---

# Types of Session Termination

## 1. Normal Termination

User exits properly.

Examples:

```sql
EXIT;
```

```sql
QUIT;
```

---

### Result

```text
Transactions Saved Successfully
```

---

# 2. Abnormal Termination

User disconnects unexpectedly.

Examples:

```text
Power Failure
System Crash
CPU Shutdown
Force Close
```

---

### Result

```text
Unsaved Transactions Lost
```

---

# COMMIT

## Purpose

Saves all pending transactions permanently.

---

## Syntax

```sql
COMMIT;
```

---

## Flow

```text
INSERT
UPDATE
DELETE
     ↓
COMMIT
     ↓
Permanent Save
```

---

## Example

```sql
INSERT INTO emp
VALUES(101,'Mahesh');
```

```sql
COMMIT;
```

Now the record is permanently stored.

---

# ROLLBACK

## Purpose

Undo all uncommitted transactions.

---

## Syntax

```sql
ROLLBACK;
```

---

## Flow

```text
INSERT
UPDATE
DELETE
      ↓
ROLLBACK
      ↓
Undo Changes
```

---

## Example

```sql
DELETE FROM emp
WHERE empno = 101;
```

Mistake detected.

```sql
ROLLBACK;
```

Result:

```text
Delete Operation Reversed
```

---

# COMMIT vs ROLLBACK

| COMMIT | ROLLBACK |
|----------|----------|
| Saves Changes | Undoes Changes |
| Permanent | Temporary Undo |
| Cannot Reverse Easily | Restores Previous State |

---

## Example Scenario

### Step 1

User logs in.

```text
Login Successful
```

---

### Step 2

Performs transactions.

```sql
INSERT 10 Records
UPDATE 10 Records
DELETE 15 Records
```

---

### Current State

```text
Changes Not Yet Permanent
```

---

### Option A

```sql
COMMIT;
```

Result:

```text
All Changes Saved Permanently
```

---

### Option B

```sql
ROLLBACK;
```

Result:

```text
All Changes Discarded
```

---

# SAVEPOINT

## Purpose

Marks a checkpoint within a transaction.

---

## Why Needed?

Instead of rolling back everything, rollback can return to a specific point.

---

## Syntax

```sql
SAVEPOINT point_name;
```

---

## Example

```sql
INSERT INTO emp VALUES(...);

SAVEPOINT A;

UPDATE emp SET salary=50000;

SAVEPOINT B;

DELETE FROM emp WHERE empno=101;
```

---

Current Flow:

```text
INSERT
   ↓
SAVEPOINT A
   ↓
UPDATE
   ↓
SAVEPOINT B
   ↓
DELETE
```

---

Rollback to B:

```sql
ROLLBACK TO B;
```

Only operations after B are removed.

---

Rollback to A:

```sql
ROLLBACK TO A;
```

Everything after A is removed.

---

# User Management Commands

## Drop User

### Syntax

```sql
DROP USER user_name CASCADE;
```

---

### Example

```sql
DROP USER rajesh CASCADE;
```

---

### Result

```text
User Dropped
```

---

### Important

Must be executed using a DBA account.

Examples:

```text
SYS
SYSTEM
```

---

# View All Users

## Syntax

```sql
SELECT *
FROM all_users;
```

---

## Purpose

Displays all database users.

---

# Oracle Recycle Bin

Dropped tables are stored in Oracle Recycle Bin.

---

## View Recycle Bin

```sql
SELECT *
FROM recyclebin;
```

---

# PURGE Command

## Purpose

Permanently remove objects from recycle bin.

---

## Syntax

```sql
PURGE TABLE table_name;
```

---

## Example

```sql
PURGE TABLE maheshit_employees;
```

---

## Result

```text
Table Purged
```

---

# DELETE vs TRUNCATE

| DELETE | TRUNCATE |
|----------|----------|
| DML | DDL |
| Can Use WHERE | Cannot Use WHERE |
| Deletes Specific Rows | Deletes All Rows |
| Can Rollback Before Commit | Auto Commit |
| Slower | Faster |

---

## Example

### DELETE

```sql
DELETE FROM emp
WHERE empno = 101;
```

Deletes one row.

---

### TRUNCATE

```sql
TRUNCATE TABLE emp;
```

Deletes all rows.

---

# TRUNCATE vs DROP

| TRUNCATE | DROP |
|-----------|------|
| Deletes Data | Deletes Table |
| Structure Remains | Structure Removed |
| Table Exists | Table Removed |
| Faster | Complete Removal |

---

# Quick Revision

```text
DDL
 ├─ CREATE
 ├─ ALTER
 ├─ DROP
 ├─ TRUNCATE
 ├─ RENAME
 ├─ FLASHBACK
 └─ PURGE

DML
 ├─ INSERT
 ├─ UPDATE
 └─ DELETE

DRL/DQL
 └─ SELECT

TCL
 ├─ COMMIT
 ├─ ROLLBACK
 └─ SAVEPOINT

Selection
 └─ Retrieves Rows

Projection
 └─ Retrieves Columns

COMMIT
 └─ Save Permanently

ROLLBACK
 └─ Undo Changes

SAVEPOINT
 └─ Transaction Checkpoint

DELETE
 └─ DML

TRUNCATE
 └─ DDL

DROP
 └─ Removes Table Structure
```
