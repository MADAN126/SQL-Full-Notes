# 09-TCL-and-DCL-Commands.md

# Transaction Control Language (TCL)

## Purpose

TCL commands are used to control and manage transactions in a database.

---

## TCL Commands

```text
COMMIT
ROLLBACK
SAVEPOINT
```

---

# What is a Transaction?

A transaction is any operation performed on a database using DML commands.

### DML Commands

```sql
INSERT
UPDATE
DELETE
```

---

## Example

```sql
INSERT INTO employees VALUES(101,'Mahesh');

UPDATE employees
SET salary=50000
WHERE empid=101;

DELETE FROM employees
WHERE empid=101;
```

Each operation is considered a transaction.

---

# What is a Session?

A session is the time period between user login and logout.

```text
Login
  ↓
Transactions
  ↓
Logout
```

---

## Session Example

```text
User Login
    ↓
Insert Records
    ↓
Update Records
    ↓
Delete Records
    ↓
Logout
```

Everything performed between login and logout belongs to the same session.

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
Transactions handled properly.
```

---

## 2. Abnormal Termination

Unexpected session termination.

Examples:

```text
Power Failure
System Crash
CPU Shutdown
Force Closing Application
```

---

### Result

```text
Unsaved transactions are lost.
```

---

# COMMIT Command

## Purpose

Used to save transactions permanently into the database.

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
INSERT INTO employees
VALUES(101,'Mahesh');

COMMIT;
```

Result:

```text
Data permanently stored.
```

---

# ROLLBACK Command

## Purpose

Used to undo transactions before a COMMIT.

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
DELETE FROM employees
WHERE empid=101;

ROLLBACK;
```

Result:

```text
Deleted record restored.
```

---

# COMMIT vs ROLLBACK

| COMMIT | ROLLBACK |
|----------|----------|
| Saves Changes | Undoes Changes |
| Permanent | Temporary Undo |
| Cannot Be Reversed Easily | Restores Previous State |

---

# SAVEPOINT Command

## Purpose

Used to save a group of transactions under a name.

Acts like a checkpoint within a transaction.

---

## Syntax

```sql
SAVEPOINT savepoint_name;
```

---

## Example

```sql
SAVEPOINT insertSavePoint;
```

---

# Savepoint Flow

```text
Login
  ↓
Insert(2)
  ↓
SAVEPOINT insertSavePoint
  ↓
Update(2)
  ↓
SAVEPOINT updateSavePoint
```

---

# Scenario

```text
Insert 2 Records
      ↓
Savepoint A
      ↓
Update 2 Records
      ↓
Savepoint B
```

---

# Rollback Entire Transaction

```sql
ROLLBACK;
```

Result:

```text
Insert(2) Removed
Update(2) Removed
```

---

# Rollback To Specific Savepoint

## Syntax

```sql
ROLLBACK TO savepoint_name;
```

---

## Example

```sql
ROLLBACK TO updateSavePoint;
```

Result:

```text
Operations after updateSavePoint removed.
```

---

## Example

```sql
ROLLBACK TO insertSavePoint;
```

Result:

```text
Everything after insertSavePoint removed.
```

---

# Savepoint Visualization

```text
Login
  ↓
Insert(2)
  ↓
SAVEPOINT A
  ↓
Update(2)
  ↓
SAVEPOINT B
  ↓
Delete(2)
```

### Rollback To B

```sql
ROLLBACK TO B;
```

```text
Delete Removed
```

---

### Rollback To A

```sql
ROLLBACK TO A;
```

```text
Update Removed
Delete Removed
```

---

### Commit

```sql
COMMIT;
```

```text
Current State Saved Permanently
```

---

# DCL (Data Control Language)

## Purpose

DCL commands are used to control user permissions and access rights.

Typically used by Database Administrators (DBAs).

---

## DCL Commands

```text
GRANT
REVOKE
```

---

# GRANT Command

## Purpose

Used to provide permissions to users.

---

## Syntax

```sql
GRANT privileges
TO username;
```

---

## Example

```sql
GRANT resource, connect
TO karthik;
```

---

## Result

```text
Grant succeeded.
```

---

## Meaning

User can now:

```text
Connect to Database
Create Objects
Work With Database Resources
```

---

# REVOKE Command

## Purpose

Used to remove permissions from users.

---

## Syntax

```sql
REVOKE privilege
FROM username;
```

---

## Example

```sql
REVOKE resource
FROM karthik;
```

---

## Result

```text
Revoke succeeded.
```

---

# User Creation (DBA Activity)

## Create User

### Syntax

```sql
CREATE USER username
IDENTIFIED BY password;
```

---

## Example

```sql
CREATE USER karthik
IDENTIFIED BY ashokit;
```

---

## Result

```text
User KARTHIK created.
```

---

# Grant Permissions

```sql
GRANT resource, connect
TO karthik;
```

---

## Why Required?

Newly created users cannot work immediately.

Permissions must be granted.

---

# View All Users

## Syntax

```sql
SELECT *
FROM all_users;
```

---

## Purpose

Displays all users in the database.

---

# View Detailed User Information

## Syntax

```sql
SELECT *
FROM dba_users;
```

---

## Purpose

Displays detailed information about database users.

---

## Requirement

Usually requires DBA privileges.

---

# View Tables In Current Account

## Syntax

```sql
SELECT *
FROM tab;
```

---

## Purpose

Displays all tables owned by the currently connected user.

---

# Display Current User

## Syntax

```sql
SHOW USER;
```

---

## Example Output

```text
USER is "KARTHIK"
```

---

# Change User Password

## Syntax

```sql
ALTER USER username
IDENTIFIED BY new_password;
```

---

## Example

```sql
ALTER USER karthik
IDENTIFIED BY karthik;
```

---

## Result

```text
User altered.
```

---

# Lock User Account

## Purpose

Prevents user login.

---

## Syntax

```sql
ALTER USER username
ACCOUNT LOCK;
```

---

## Example

```sql
ALTER USER karthik
ACCOUNT LOCK;
```

---

## Result

```text
Account Locked
```

---

# Unlock User Account

## Purpose

Allows login again.

---

## Syntax

```sql
ALTER USER username
ACCOUNT UNLOCK;
```

---

## Example

```sql
ALTER USER karthik
ACCOUNT UNLOCK;
```

---

## Result

```text
Account Unlocked
```

---

# Drop User

## Purpose

Remove a user from the database.

---

## Syntax

```sql
DROP USER username CASCADE;
```

---

## Example

```sql
DROP USER karthik CASCADE;
```

---

## Result

```text
User Dropped
```

---

# What Does CASCADE Mean?

Removes:

```text
User
Tables
Views
Indexes
Sequences
Procedures
Functions
```

owned by that user.

---

## When CASCADE Is Required

### User Contains Objects

```sql
DROP USER karthik CASCADE;
```

Required.

---

### Empty User

```sql
DROP USER karthik;
```

Usually sufficient.

---

# DCL Workflow

```text
DBA
 │
 ├── Create User
 │
 ├── Grant Permissions
 │
 ├── User Works
 │
 ├── Revoke Permissions
 │
 ├── Lock/Unlock User
 │
 └── Drop User
```

---

# TCL vs DCL

| TCL | DCL |
|------|------|
| Controls Transactions | Controls Permissions |
| COMMIT | GRANT |
| ROLLBACK | REVOKE |
| SAVEPOINT | User Access Management |

---

# Interview Questions

## What is TCL?

Transaction Control Language used to manage transactions.

---

## What are TCL Commands?

```text
COMMIT
ROLLBACK
SAVEPOINT
```

---

## What is a Transaction?

Any INSERT, UPDATE, or DELETE operation performed on a database.

---

## What is COMMIT?

Saves transactions permanently.

---

## What is ROLLBACK?

Undoes transactions before commit.

---

## What is SAVEPOINT?

A named checkpoint inside a transaction.

---

## What is DCL?

Data Control Language used to manage permissions.

---

## What are DCL Commands?

```text
GRANT
REVOKE
```

---

## Which User Creates New Users?

```text
DBA User
```

Examples:

```text
SYS
SYSTEM
```

---

## How To See Current User?

```sql
SHOW USER;
```

---

## How To Lock A User?

```sql
ALTER USER username ACCOUNT LOCK;
```

---

## How To Unlock A User?

```sql
ALTER USER username ACCOUNT UNLOCK;
```

---

## How To Drop A User?

```sql
DROP USER username CASCADE;
```

---

# Quick Revision

```text
TCL
 ├─ COMMIT
 ├─ ROLLBACK
 └─ SAVEPOINT

COMMIT
 └─ Save Permanently

ROLLBACK
 └─ Undo Changes

SAVEPOINT
 └─ Named Checkpoint

DCL
 ├─ GRANT
 └─ REVOKE

GRANT
 └─ Give Permission

REVOKE
 └─ Remove Permission

SHOW USER
 └─ Current User

ALL_USERS
 └─ View Users

DBA_USERS
 └─ Detailed User Information

ACCOUNT LOCK
 └─ Disable Login

ACCOUNT UNLOCK
 └─ Enable Login

DROP USER ... CASCADE
 └─ Remove User And Objects
```
