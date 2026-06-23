# 11-SQL-Constraints-Part-1.md

# SQL Constraints

## Introduction

Without constraints:

- Duplicate records can be inserted.
- NULL values can be stored where they should not be.
- Invalid data can enter the database.
- Data becomes unreliable.

To enforce business rules, Oracle provides **Constraints**.

---

# What are Constraints?

Constraints are rules applied on table columns to ensure only valid data is stored.

They help maintain:

```text
Data Accuracy
Data Integrity
Data Consistency
```

---

# Why Constraints?

Constraints ensure:

- Duplicate values are prevented.
- Mandatory fields are enforced.
- Invalid values are rejected.
- Business rules are followed.

---

# Levels of Constraints

## 1. Column Level Constraint

Constraint is defined immediately after a column definition.

### Example

```sql
client_id NUMBER UNIQUE
```

---

## 2. Table Level Constraint

Constraint is defined after all column definitions.

### Example

```sql
CONSTRAINT unique_client UNIQUE(client_id)
```

---

# Types of Constraints

```text
1. UNIQUE
2. NOT NULL
3. CHECK
4. DEFAULT
5. PRIMARY KEY
6. FOREIGN KEY
```

---

# UNIQUE Constraint

## Purpose

Prevents duplicate values in a column.

---

## Features

### Advantages

- Prevents duplicate values.
- Can be applied to multiple columns.

### Disadvantage

- Allows NULL values.

---

# UNIQUE Constraint Syntax

## Column Level

```sql
CREATE TABLE clients (
    client_id NUMBER UNIQUE,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50)
);
```

---

## Table Level

```sql
CREATE TABLE clients (
    client_id NUMBER,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50),
    CONSTRAINT unique_client_id
    UNIQUE(client_id)
);
```

---

# UNIQUE Constraint With Custom Name

```sql
CREATE TABLE clients (
    client_id NUMBER,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50),
    CONSTRAINT ashokit_unique_id
    UNIQUE(client_id)
);
```

---

# Composite UNIQUE Constraint

Multiple columns together must be unique.

```sql
CREATE TABLE clients (
    client_id NUMBER,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50),

    CONSTRAINT unique_client
    UNIQUE(client_id, first_name, last_name)
);
```

---

# Add UNIQUE After Table Creation

```sql
ALTER TABLE clients
ADD CONSTRAINT ashokit_first_name
UNIQUE(first_name);
```

---

# Disable UNIQUE Constraint

```sql
ALTER TABLE clients
DISABLE CONSTRAINT unique_constraint_name;
```

---

# Enable UNIQUE Constraint

```sql
ALTER TABLE clients
ENABLE CONSTRAINT unique_constraint_name;
```

---

# Drop UNIQUE Constraint

```sql
ALTER TABLE clients
DROP CONSTRAINT unique_constraint_name;
```

---

# UNIQUE Constraint Example

## Create Table

```sql
CREATE TABLE clients (
    client_id NUMBER UNIQUE,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50)
);
```

---

## Valid Inserts

```sql
INSERT INTO clients
VALUES(1,'Mahesh','Kumar');
```

```sql
INSERT INTO clients
VALUES(NULL,'Mahesh','Kumar');
```

```sql
INSERT INTO clients
VALUES(2,'Ashok','Kumar');
```

---

## Invalid Insert

```sql
INSERT INTO clients
VALUES(1,'Sarath','Kumar');
```

---

## Error

```text
ORA-00001:
unique constraint violated
```

---

# UNIQUE Constraint Summary

| Property | Supported |
|-----------|------------|
| Duplicate Values | ❌ No |
| NULL Values | ✅ Yes |
| Multiple Columns | ✅ Yes |

---

# NOT NULL Constraint

## Purpose

Prevents NULL values.

A value must be provided.

---

## Features

### Advantages

- Mandatory field.
- Prevents NULL values.

### Disadvantage

- Allows duplicate values.

---

# NOT NULL Syntax

```sql
CREATE TABLE clients (
    client_id NUMBER NOT NULL,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50)
);
```

---

# UNIQUE + NOT NULL

Most commonly used together.

```sql
CREATE TABLE clients (
    client_id NUMBER UNIQUE NOT NULL,
    first_name VARCHAR2(50),
    last_name VARCHAR2(50)
);
```

---

# Add NOT NULL After Table Creation

```sql
ALTER TABLE clients
MODIFY(client_id NOT NULL);
```

---

# Important Requirement

Before adding NOT NULL:

```text
Column must not contain NULL values.
```

Otherwise Oracle throws an error.

---

# Remove NOT NULL Constraint

Allow column to accept NULL values again.

```sql
ALTER TABLE clients
MODIFY(client_id NULL);
```

---

# NOT NULL Summary

| Property | Supported |
|-----------|------------|
| Duplicate Values | ✅ Yes |
| NULL Values | ❌ No |
| Mandatory Field | ✅ Yes |

---

# UNIQUE vs NOT NULL

| Feature | UNIQUE | NOT NULL |
|----------|---------|---------|
| Prevent Duplicate Values | ✅ Yes | ❌ No |
| Prevent NULL Values | ❌ No | ✅ Yes |
| Multiple Columns | ✅ Yes | ✅ Yes |
| Most Commonly Combined | ✅ Yes | ✅ Yes |

---

# CHECK Constraint

## Purpose

Allows only values that satisfy a condition.

Invalid values are rejected.

---

# Features

### Advantages

- Enforces business rules.
- Validates data before insertion.

### Disadvantage

- Allows NULL values.

---

# CHECK Constraint Syntax

## Column Level

```sql
CREATE TABLE parts (
    buy_price NUMBER(9,2)
    CHECK(buy_price > 0)
);
```

---

## Table Level

```sql
CREATE TABLE parts (
    buy_price NUMBER(9,2),

    CONSTRAINT check_positive_price
    CHECK(buy_price > 0)
);
```

---

# Example

```sql
CREATE TABLE parts (
    part_id NUMBER UNIQUE NOT NULL,
    part_name VARCHAR2(255) NOT NULL,
    buy_price NUMBER(9,2)
    CHECK(buy_price > 0)
);
```

---

# Valid Insert

```sql
INSERT INTO parts
VALUES(1,'HDD',5000);
```

---

# Invalid Insert

```sql
INSERT INTO parts
VALUES(2,'Screen',0);
```

---

## Error

```text
ORA-02290:
check constraint violated
```

---

# Another Invalid Insert

```sql
INSERT INTO parts
VALUES(3,'Monitor',-100);
```

---

## Reason

```text
-100 > 0  → FALSE
```

Rejected.

---

# Add CHECK Constraint

```sql
ALTER TABLE parts
ADD CONSTRAINT check_positive_cost
CHECK(cost > 0);
```

---

# Add New Column

```sql
ALTER TABLE parts
ADD cost NUMBER(9,2);
```

---

# Disable CHECK Constraint

```sql
ALTER TABLE parts
DISABLE CONSTRAINT check_positive_cost;
```

---

# Enable CHECK Constraint

```sql
ALTER TABLE parts
ENABLE CONSTRAINT check_positive_cost;
```

---

# Drop CHECK Constraint

```sql
ALTER TABLE parts
DROP CONSTRAINT check_positive_cost;
```

---

# CHECK Constraint Summary

| Property | Supported |
|-----------|------------|
| Custom Validation | ✅ Yes |
| Duplicate Values | ✅ Yes |
| NULL Values | ✅ Yes |
| Business Rules | ✅ Yes |

---

# DEFAULT Constraint

## Purpose

Assigns a value automatically when the user does not provide one.

---

# Features

- Provides automatic values.
- Reduces NULL values.
- Improves data consistency.

---

# Syntax

```sql
CREATE TABLE table_name (
    column_name datatype
    DEFAULT value
);
```

---

# Example

```sql
CREATE TABLE Employee (
    ID NUMBER NOT NULL,
    Name VARCHAR2(20) NOT NULL,
    Age NUMBER,

    Country VARCHAR2(10)
    DEFAULT 'INDIA',

    DOJ DATE
    DEFAULT SYSDATE
);
```

---

# Insert Without Country

```sql
INSERT INTO Employee
(ID, Name, Age)
VALUES
(1,'Mahesh',25);
```

---

# Stored Data

```text
Country = INDIA
DOJ     = Current System Date
```

---

# Add DEFAULT After Table Creation

```sql
ALTER TABLE Employee
MODIFY Country DEFAULT 'INDIA';
```

---

# Remove DEFAULT Value

```sql
ALTER TABLE Employee
MODIFY Country DEFAULT NULL;
```

---

# DEFAULT Constraint Summary

| Property | Supported |
|-----------|------------|
| Automatic Value | ✅ Yes |
| Prevents Missing Data | ✅ Yes |
| Allows User Override | ✅ Yes |

---

# Constraint Quick Revision

```text
UNIQUE
 └─ No Duplicate Values
 └─ Allows NULL

NOT NULL
 └─ No NULL Values
 └─ Allows Duplicates

CHECK
 └─ Validates Condition
 └─ Allows NULL

DEFAULT
 └─ Auto Value
 └─ Used When No Value Supplied
```

---

# Interview Questions

## What are Constraints?

Rules applied on table columns to maintain valid data.

---

## Types of Constraints?

```text
UNIQUE
NOT NULL
CHECK
DEFAULT
PRIMARY KEY
FOREIGN KEY
```

---

## Which Constraint Prevents Duplicate Values?

```text
UNIQUE
```

---

## Which Constraint Prevents NULL Values?

```text
NOT NULL
```

---

## Can UNIQUE Allow NULL?

```text
Yes
```

---

## Can NOT NULL Allow Duplicates?

```text
Yes
```

---

## Which Constraint Validates Business Rules?

```text
CHECK
```

---

## Which Constraint Automatically Inserts Values?

```text
DEFAULT
```

---

## Which Constraint Is Commonly Used With UNIQUE?

```text
NOT NULL
```

Because UNIQUE alone still allows NULL values.
