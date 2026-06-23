# 05-Update-And-Delete-Commands.md

# SQL*Plus Utility Commands

## Clear Screen

Used to clear the SQL*Plus screen.

```sql
CL SCR
```

---

## Increase Line Width

Used to display more characters per line.

### Syntax

```sql
SET LINESIZE number;
```

### Example

```sql
SET LINESIZE 300;
```

---

# UPDATE Statement

## Definition

The `UPDATE` statement is used to modify existing data in a table.

### Category

```text
DML (Data Manipulation Language)
```

---

# How UPDATE Works

```text
Existing Record
        ↓
UPDATE Statement
        ↓
Modified Record
```

---

# Updating All Rows

## Syntax

```sql
UPDATE table_name
SET column_name = value;
```

---

## Example

Update location for every customer.

```sql
UPDATE ashokit_customers
SET location='Delhi';
```

### Result

```text
3 rows updated.
```

---

## Before Update

| Customer_ID | Name | Location |
|------------|------|----------|
| 1 | Mahesh | Hyderabad |
| 2 | Ashok | Hyderabad |
| 3 | Rajesh | Mumbai |

---

## After Update

| Customer_ID | Name | Location |
|------------|------|----------|
| 1 | Mahesh | Delhi |
| 2 | Ashok | Delhi |
| 3 | Rajesh | Delhi |

---

# Updating Specific Rows

To update only selected rows, use the `WHERE` clause.

---

## Syntax

```sql
UPDATE table_name
SET column_name=value
WHERE condition;
```

---

# Update Using Customer ID

## Example

```sql
UPDATE ashokit_customers
SET location='Pune'
WHERE customer_id=1;
```

### Result

```text
1 row updated.
```

---

# Update Using Customer Name

## Example

```sql
UPDATE ashokit_customers
SET location='Pune'
WHERE customer_name='Mahesh';
```

### Result

```text
1 row updated.
```

---

# Update Multiple Columns

## Example

```sql
UPDATE ashokit_customers
SET location='Guntur',
    age=40
WHERE customer_name='Mahesh';
```

### Result

```text
1 row updated.
```

---

# Update Using Multiple Conditions

## Example

```sql
UPDATE ashokit_customers
SET location='Guntur',
    age=40
WHERE customer_name='Mahesh'
AND gender='Male';
```

### Result

```text
1 row updated.
```

---

# Understanding WHERE Clause

## Purpose

Filters rows before modification.

Without `WHERE`:

```sql
UPDATE ashokit_customers
SET location='Delhi';
```

All rows are updated.

---

With `WHERE`:

```sql
UPDATE ashokit_customers
SET location='Pune'
WHERE customer_id=1;
```

Only matching rows are updated.

---

# SET Keyword

## Purpose

Specifies columns that need modification.

### Example

```sql
SET location='Pune'
```

---

# WHERE Keyword

## Purpose

Specifies conditions.

### Example

```sql
WHERE customer_id=1
```

---

# Real-Time Best Practice

Always perform updates using a unique column.

Recommended:

```sql
customer_id
```

Reason:

```text
Customer ID is unique.
```

---

## Bad Practice

```sql
UPDATE ashokit_customers
SET location='Pune'
WHERE customer_name='Mahesh';
```

Problem:

There may be multiple customers named Mahesh.

---

## Good Practice

```sql
UPDATE ashokit_customers
SET location='Pune'
WHERE customer_id=1;
```

Only one row is affected.

---

# DELETE Statement

## Definition

Used to remove records from a table.

### Category

```text
DML (Data Manipulation Language)
```

---

# How DELETE Works

```text
Existing Rows
      ↓
DELETE Statement
      ↓
Rows Removed
```

---

# Delete All Rows

## Syntax

```sql
DELETE FROM table_name;
```

---

## Example

```sql
DELETE FROM ashokit_customers;
```

### Result

```text
All rows deleted.
```

### Important

Table structure remains.

Only data is removed.

---

# Before DELETE

| Customer_ID | Name |
|------------|------|
| 1 | Mahesh |
| 2 | Ashok |
| 3 | Rajesh |

---

# After DELETE

```text
No Records Found
```

---

# Delete Specific Rows

## Syntax

```sql
DELETE FROM table_name
WHERE condition;
```

---

# Delete Using Customer ID

## Example

```sql
DELETE FROM ashokit_customers
WHERE customer_id=1;
```

Deletes customer whose ID is 1.

---

# Delete Using Customer Name

## Example

```sql
DELETE FROM ashokit_customers
WHERE customer_name='Ashok';
```

Deletes customers named Ashok.

---

# Delete Using Gender

## Example

```sql
DELETE FROM ashokit_customers
WHERE gender='Male';
```

Deletes all male customers.

---

# Delete Using Multiple Conditions

## Example

```sql
DELETE FROM ashokit_customers
WHERE gender='Male'
AND age>=35;
```

Deletes customers satisfying both conditions.

---

# Common Conditions in WHERE Clause

## Equal To

```sql
WHERE customer_id=1
```

---

## Greater Than

```sql
WHERE age>35
```

---

## Greater Than or Equal To

```sql
WHERE age>=35
```

---

## Less Than

```sql
WHERE age<35
```

---

## Less Than or Equal To

```sql
WHERE age<=35
```

---

## Multiple Conditions

```sql
WHERE age>=35
AND gender='Male'
```

---

# UPDATE vs DELETE

| UPDATE | DELETE |
|----------|----------|
| Modifies Data | Removes Data |
| Data Remains | Data Removed |
| Uses SET | Does Not Use SET |
| Usually Uses WHERE | Usually Uses WHERE |

---

# DELETE vs TRUNCATE vs DROP

| DELETE | TRUNCATE | DROP |
|----------|----------|----------|
| Removes Rows | Removes All Rows | Removes Table |
| DML | DDL | DDL |
| Can Use WHERE | No WHERE | No WHERE |
| Structure Remains | Structure Remains | Structure Removed |
| Slower | Faster | Removes Entire Object |

---

# SQL Commands Learned So Far

| Command | Category | Purpose |
|----------|----------|----------|
| CREATE | DDL | Create Table |
| INSERT | DML | Insert Records |
| SELECT | DRL | Retrieve Records |
| UPDATE | DML | Modify Records |
| DELETE | DML | Remove Records |

---

# Interview Questions

## What is UPDATE?

Used to modify existing records in a table.

---

## What is DELETE?

Used to remove records from a table.

---

## What is the Purpose of SET?

Used to specify columns that should be modified.

Example:

```sql
SET location='Pune'
```

---

## What is the Purpose of WHERE?

Used to filter rows.

Example:

```sql
WHERE customer_id=1
```

---

## What Happens If WHERE Is Omitted in UPDATE?

All rows are updated.

---

## What Happens If WHERE Is Omitted in DELETE?

All rows are deleted.

---

## Which Is Preferred for Updates?

```text
Primary Key / Unique Column
```

Example:

```sql
customer_id
```

---

# Quick Revision

```text
UPDATE -> Modify Existing Data

DELETE -> Remove Existing Data

SET -> Specifies Modified Columns

WHERE -> Filters Rows

UPDATE without WHERE -> Updates All Rows

DELETE without WHERE -> Deletes All Rows

Best Practice:
Use customer_id for UPDATE and DELETE operations.

UPDATE -> DML

DELETE -> DML
```
