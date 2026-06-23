# 07-DDL-Commands-Deep-Dive.md

# DDL (Data Definition Language)

## Definition

DDL commands are used to define and modify the structure of database objects.

### Database Objects

- Tables
- Views
- Sequences
- Indexes
- Stored Procedures
- Stored Functions
- Synonyms

---

## DDL Commands

```text
CREATE
ALTER
TRUNCATE
DROP
RENAME
```

---

# DDL vs DML

| DDL | DML |
|------|------|
| Works on Structure | Works on Data |
| CREATE | INSERT |
| ALTER | UPDATE |
| DROP | DELETE |
| TRUNCATE | - |
| RENAME | - |

---

# 1. CREATE Command

## Purpose

Used to create database objects.

### Objects That Can Be Created

```text
Table
View
Sequence
Index
Procedure
Function
Synonym
```

---

## Table Creation Syntax

```sql
CREATE TABLE table_name(
    column1 datatype,
    column2 datatype,
    column3 datatype
);
```

---

## Example

```sql
CREATE TABLE ashokit_users(
    username VARCHAR2(50),
    user_password VARCHAR2(100)
);
```

---

## Result

```text
Table Created
```

---

# 2. ALTER Command

## Purpose

Used to modify an existing database object's structure.

---

## Operations Supported

```text
ALTER
│
├── ADD Column
├── DROP Column
├── RENAME Column
├── MODIFY Datatype
└── RENAME Table
```

---

# ALTER ADD

## Purpose

Add new columns to an existing table.

---

## Syntax

```sql
ALTER TABLE table_name
ADD(
    column_name datatype
);
```

---

## Add Single Column

```sql
ALTER TABLE ashokit_users
ADD(
    gender CHAR(1)
);
```

---

## Add Multiple Columns

```sql
ALTER TABLE ashokit_users
ADD(
    gender CHAR(1),
    city_name VARCHAR2(50)
);
```

---

## Before

| USERNAME | USER_PASSWORD |
|-----------|---------------|
| Mahesh | xyz123 |

---

## After

| USERNAME | USER_PASSWORD | GENDER | CITY_NAME |
|-----------|---------------|---------|------------|
| Mahesh | xyz123 | NULL | NULL |

---

## Important Rule

New columns are always added at the end.

### Not Possible

```text
USERNAME
GENDER
USER_PASSWORD
```

Oracle does not allow insertion of a column at a specific position.

---

# ALTER DROP

## Purpose

Remove columns from an existing table.

---

## Drop One Column

### Syntax

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

---

### Example

```sql
ALTER TABLE ashokit_employees
DROP COLUMN created_dt;
```

---

## Drop Multiple Columns

### Syntax

```sql
ALTER TABLE table_name
DROP(
    column1,
    column2
);
```

---

### Example

```sql
ALTER TABLE ashokit_employees
DROP(
    created_dt,
    dob
);
```

---

## Before

| EMPID | EMPNAME | DOB | CREATED_DT |
|--------|---------|------|------------|

---

## After

| EMPID | EMPNAME |
|--------|---------|

---

# ALTER RENAME COLUMN

## Purpose

Rename an existing column.

---

## Syntax

```sql
ALTER TABLE table_name
RENAME COLUMN old_name
TO new_name;
```

---

## Example

```sql
ALTER TABLE ashokit_employees
RENAME COLUMN empname
TO employee_name;
```

---

## Before

| EMPNAME |
|----------|

---

## After

| EMPLOYEE_NAME |
|----------------|

---

## Limitation

Only one column can be renamed at a time.

---

# ALTER RENAME TABLE

## Purpose

Rename an existing table.

---

## Syntax

```sql
ALTER TABLE old_table_name
RENAME TO new_table_name;
```

---

## Example

```sql
ALTER TABLE ashokit_employees
RENAME TO maheshit_employees;
```

---

## Result

```text
Table altered.
```

---

## What Happens Internally?

Old table name disappears.

### Before

```text
ashokit_employees
```

### After

```text
maheshit_employees
```

---

## Query Using Old Name

```sql
SELECT *
FROM ashokit_employees;
```

Output:

```text
ORA-00942:
table or view does not exist
```

---

## Query Using New Name

```sql
SELECT *
FROM maheshit_employees;
```

Works successfully.

---

# ALTER MODIFY

## Purpose

Modify datatype or datatype size.

---

## Syntax

```sql
ALTER TABLE table_name
MODIFY column_name datatype(size);
```

---

## Example

```sql
ALTER TABLE maheshit_employees
MODIFY employee_name VARCHAR2(100);
```

---

## Before

```sql
employee_name VARCHAR2(50)
```

---

## After

```sql
employee_name VARCHAR2(100)
```

---

## Modify Multiple Columns

### Syntax

```sql
ALTER TABLE table_name
MODIFY(
    column1 datatype,
    column2 datatype
);
```

---

### Example

```sql
ALTER TABLE maheshit_employees
MODIFY(
    employee_id NUMBER(6),
    employee_name VARCHAR2(140)
);
```

---

# 3. TRUNCATE Command

## Purpose

Delete all records permanently from a table.

---

## Category

```text
DDL
```

---

## Syntax

```sql
TRUNCATE TABLE table_name;
```

---

## Example

```sql
TRUNCATE TABLE maheshit_employees;
```

---

## Result

```text
Table truncated.
```

---

## Before

| EMPID | EMPNAME |
|--------|---------|
| 101 | Mahesh |
| 102 | Rani |
| 103 | Suresh |

---

## After

```text
No Rows
```

---

## Structure After TRUNCATE

Table still exists.

```text
Rows      → Deleted
Columns   → Remain
Table     → Remains
```

---

# 4. DROP Command

## Purpose

Remove an entire database object.

---

## Syntax

```sql
DROP TABLE table_name;
```

---

## Example

```sql
DROP TABLE maheshit_employees;
```

---

## Result

```text
Table dropped.
```

---

## Before DROP

```text
Table Exists
Rows Exist
Columns Exist
```

---

## After DROP

```text
Table Removed
Rows Removed
Columns Removed
```

---

## Query After DROP

```sql
SELECT *
FROM maheshit_employees;
```

Output:

```text
ORA-00942:
table or view does not exist
```

---

# 5. RENAME Command

## Purpose

Rename a table directly.

---

## Syntax

```sql
RENAME old_table_name
TO new_table_name;
```

---

## Example

```sql
RENAME ashokit_users
TO maheshit_users;
```

---

## Result

```text
Table renamed.
```

---

# TRUNCATE vs DROP

| TRUNCATE | DROP |
|-----------|------|
| Deletes Rows | Deletes Table |
| Structure Remains | Structure Removed |
| Table Exists | Table Removed |
| Faster | Complete Removal |

---

## Example

### TRUNCATE

```sql
TRUNCATE TABLE employees;
```

After execution:

```text
Employees Table Exists
No Records
```

---

### DROP

```sql
DROP TABLE employees;
```

After execution:

```text
Employees Table Does Not Exist
```

---

# Oracle Recycle Bin

## Concept

Dropped tables are not immediately destroyed.

Oracle stores them in the Recycle Bin.

---

## View Recycle Bin

```sql
SELECT *
FROM recyclebin;
```

---

## Why Recycle Bin Exists?

To recover accidentally dropped tables.

---

# Flashback Table

## Purpose

Restore a dropped table.

---

## Syntax

```sql
FLASHBACK TABLE table_name
TO BEFORE DROP;
```

---

## Example

```sql
FLASHBACK TABLE maheshit_employees
TO BEFORE DROP;
```

---

## Result

```text
Dropped table restored.
```

---

# View All Tables

## Syntax

```sql
SELECT *
FROM tab;
```

---

## Purpose

Displays all tables owned by the current user.

---

# DDL Command Summary

| Command | Purpose |
|----------|----------|
| CREATE | Create Object |
| ALTER ADD | Add Column |
| ALTER DROP | Remove Column |
| ALTER RENAME COLUMN | Rename Column |
| ALTER MODIFY | Change Datatype |
| ALTER RENAME TO | Rename Table |
| TRUNCATE | Remove All Rows |
| DROP | Remove Table |
| RENAME | Rename Table |
| FLASHBACK | Restore Dropped Table |

---

# Interview Questions

## What is DDL?

Data Definition Language used to manage database object structure.

---

## Which Command Adds New Columns?

```sql
ALTER TABLE
ADD(...)
```

---

## Which Command Removes Columns?

```sql
ALTER TABLE
DROP COLUMN
```

---

## Which Command Changes Datatype?

```sql
ALTER TABLE
MODIFY
```

---

## Difference Between DROP and TRUNCATE?

| DROP | TRUNCATE |
|--------|---------|
| Deletes Table | Deletes Rows |
| Structure Removed | Structure Remains |
| Cannot Query Table | Can Query Table |

---

## What is Oracle Recycle Bin?

A storage area where dropped tables are kept temporarily.

---

## How to Restore a Dropped Table?

```sql
FLASHBACK TABLE table_name
TO BEFORE DROP;
```

---

## How to See All Tables?

```sql
SELECT * FROM tab;
```

---

# Quick Revision

```text
DDL → Structure

CREATE
    → Create Object

ALTER ADD
    → Add Column

ALTER DROP
    → Remove Column

ALTER RENAME COLUMN
    → Rename Column

ALTER MODIFY
    → Change Datatype

ALTER RENAME TO
    → Rename Table

TRUNCATE
    → Delete All Rows
    → Table Exists

DROP
    → Delete Entire Table

RENAME
    → Rename Table

RECYCLEBIN
    → Stores Dropped Tables

FLASHBACK
    → Restore Dropped Table

TAB
    → Show All Tables
```
