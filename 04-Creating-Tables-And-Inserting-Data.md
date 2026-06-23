# 04-Creating-Tables-And-Inserting-Data.md

# Database Objects

Database objects are logical structures stored inside a database.

## Common Database Objects

- Tables
- Views
- Sequences
- Indexes
- Stored Procedures
- Stored Functions

---

# Table

## Definition

A table is a database object used to store data in rows and columns.

### Example

| Customer_ID | Customer_Name | Gender | Age | Location |
|------------|---------------|---------|-----|-----------|
| 101 | Mahesh | Male | 35 | Hyderabad |
| 102 | Ashok | Male | 35 | Hyderabad |

---

# Life Cycle of Working With a Table

```text
Create Table
      ↓
Insert Data
      ↓
Retrieve Data
```

Commands Used:

```text
CREATE  -> Create Table

INSERT  -> Add Data

SELECT  -> Retrieve Data
```

---

# CREATE TABLE Command

## Purpose

Used to create a new table.

### Category

```text
DDL (Data Definition Language)
```

---

## General Syntax

```sql
CREATE TABLE table_name(
    column1 datatype,
    column2 datatype,
    column3 datatype
);
```

---

# Oracle Naming Conventions

Every database object name should follow these rules.

---

## Rule 1

Name must start with an alphabet.

### Valid

```text
customer
student
emp1
```

### Invalid

```text
1customer
9student
```

---

## Rule 2

Allowed Characters

```text
a-z
A-Z
0-9
@
$
#
_
```

### Valid

```text
customer_1
emp$
student#
```

---

## Rule 3

Names are Case Insensitive

```sql
CUSTOMERS
customers
Customers
```

All are treated as the same name.

---

## Rule 4

Reserved Keywords Cannot Be Used

### Invalid

```sql
CREATE TABLE SELECT
```

```sql
CREATE TABLE WHERE
```

```sql
CREATE TABLE INSERT
```

These are SQL keywords.

---

## Rule 5

Spaces Are Not Allowed

### Invalid

```text
customer table
student info
```

### Valid

```text
customer_table
student_info
```

---

# Datatypes Used

## NUMBER

Stores numeric values.

Examples:

```text
10
25
1000
50000
```

---

## VARCHAR

Stores character data.

Examples:

```text
Mahesh
Hyderabad
Male
```

---

## Syntax

```sql
VARCHAR(size)
```

Example:

```sql
VARCHAR(50)
```

Maximum 50 characters.

---

# Creating Customer Table

## Requirement

Store:

- Customer ID
- Customer Name
- Gender
- Age
- Location

---

## Query

```sql
CREATE TABLE ashokit_customers(
    customer_id NUMBER,
    customer_name VARCHAR(50),
    gender VARCHAR(15),
    age NUMBER,
    location VARCHAR(50)
);
```

---

## Output

```text
Table Created.
```

---

# Understanding the Table

```sql
CREATE TABLE ashokit_customers(
    customer_id NUMBER,
    customer_name VARCHAR(50),
    gender VARCHAR(15),
    age NUMBER,
    location VARCHAR(50)
);
```

| Column | Datatype |
|----------|----------|
| customer_id | NUMBER |
| customer_name | VARCHAR(50) |
| gender | VARCHAR(15) |
| age | NUMBER |
| location | VARCHAR(50) |

---

# INSERT Command

## Purpose

Used to insert records into a table.

### Category

```text
DML (Data Manipulation Language)
```

---

# Method 1: Insert Using Column Names

## Syntax

```sql
INSERT INTO table_name(
    column1,
    column2,
    column3
)
VALUES(
    value1,
    value2,
    value3
);
```

---

## Example

```sql
INSERT INTO ashokit_customers(
    customer_id,
    customer_name,
    gender,
    age,
    location
)
VALUES(
    1,
    'Mahesh',
    'Male',
    35,
    'Hyderabad'
);
```

---

## Another Example

```sql
INSERT INTO ashokit_customers(
    customer_id,
    customer_name,
    gender,
    age,
    location
)
VALUES(
    2,
    'Ashok',
    'Male',
    35,
    'Hyderabad'
);
```

---

# Method 2: Insert Without Column Names

## Syntax

```sql
INSERT INTO table_name
VALUES(
    value1,
    value2,
    value3
);
```

### Important

Values must follow the exact column order defined during table creation.

---

## Example

```sql
INSERT INTO ashokit_customers
VALUES(
    3,
    'Rajesh',
    'Male',
    40,
    'Mumbai'
);
```

---

# Method 3: Runtime Input

## Syntax

```sql
INSERT INTO table_name
VALUES(
    &customerId,
    &customerName,
    &gender,
    &age,
    &location
);
```

---

## What Happens?

Oracle prompts for values at runtime.

Example:

```text
Enter value for customerId : 101
Enter value for customerName : Mahesh
Enter value for gender : Male
Enter value for age : 35
Enter value for location : Hyderabad
```

---

# SELECT Command

## Purpose

Used to retrieve data from a table.

### Category

```text
DRL (Data Retrieval Language)
```

---

# Select All Records

## Syntax

```sql
SELECT *
FROM table_name;
```

---

## Example

```sql
SELECT *
FROM ashokit_customers;
```

---

## Output

| Customer_ID | Customer_Name | Gender | Age | Location |
|------------|---------------|---------|-----|-----------|
| 1 | Mahesh | Male | 35 | Hyderabad |
| 2 | Ashok | Male | 35 | Hyderabad |
| 3 | Rajesh | Male | 40 | Mumbai |

---

# Meaning of *

The asterisk (*) means:

```text
All Columns
```

Example:

```sql
SELECT *
FROM ashokit_customers;
```

Returns every column from the table.

---

# SQL Execution Flow

```text
CREATE TABLE
      ↓
INSERT INTO TABLE
      ↓
SELECT DATA
      ↓
Verify Results
```

---

# SQL Categories Used So Far

| Command | Category | Purpose |
|----------|----------|----------|
| CREATE | DDL | Create Table |
| INSERT | DML | Insert Data |
| SELECT | DRL | Retrieve Data |

---

# Interview Questions

## What is a Table?

A database object used to store data in rows and columns.

---

## Which SQL Command Creates a Table?

```sql
CREATE TABLE
```

---

## Which SQL Command Inserts Data?

```sql
INSERT INTO
```

---

## Which SQL Command Retrieves Data?

```sql
SELECT
```

---

## What is the Difference Between NUMBER and VARCHAR?

| NUMBER | VARCHAR |
|----------|----------|
| Stores Numbers | Stores Characters |
| 100 | Mahesh |
| 5000 | Hyderabad |

---

## Can We Omit Column Names During INSERT?

Yes.

```sql
INSERT INTO table_name
VALUES(...);
```

But values must match the table column order exactly.

---

## What Does SELECT * Mean?

Retrieve all columns from a table.

---

# Quick Revision

```text
Table -> Stores Data

CREATE TABLE -> Create Table

INSERT INTO -> Add Data

SELECT -> Retrieve Data

NUMBER -> Numeric Data

VARCHAR -> Character Data

* -> All Columns

DDL -> CREATE

DML -> INSERT

DRL -> SELECT

Table = Rows + Columns
```
