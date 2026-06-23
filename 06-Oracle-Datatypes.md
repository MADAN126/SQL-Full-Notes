# 06-Oracle-Datatypes.md

# Oracle Datatypes

## What is a Datatype?

A datatype defines the type of value that can be stored in a database column.

```text
Column
   ↓
Datatype
   ↓
Allowed Values
```

Example:

```sql
age NUMBER
```

Only numeric values can be stored.

---

# Why Datatypes Are Important

Datatypes help Oracle:

- Validate Data
- Allocate Memory
- Improve Performance
- Maintain Data Integrity

Example:

```sql
age NUMBER
```

Valid:

```text
25
30
45
```

Invalid:

```text
Mahesh
Hyderabad
```

---

# Categories of Oracle Datatypes

```text
Oracle Datatypes
│
├── Number
├── Character
├── Date
├── Timestamp
└── Large Objects
```

---

# 1. NUMBER Datatype

Used to store numeric values.

Examples:

```text
10
25
500
1000
```

and

```text
10.25
25.36
500.75
```

---

## NUMBER(size)

Stores integer values.

### Syntax

```sql
column_name NUMBER(size)
```

### Meaning

```text
size = maximum number of digits
```

---

### Example

```sql
student_no NUMBER(4)
```

Maximum value:

```text
9999
```

Valid:

```text
1
25
999
9999
```

Invalid:

```text
10000
```

Because it exceeds 4 digits.

---

### Real-Time Uses

```text
Student Roll Number
Employee ID
Customer ID
Invoice Number
```

---

## NUMBER(precision, scale)

Used for decimal values.

### Syntax

```sql
column_name NUMBER(precision, scale)
```

---

## Precision

Total number of digits.

---

## Scale

Digits after decimal point.

---

### Example

```sql
salary NUMBER(6,2)
```

Precision:

```text
6
```

Scale:

```text
2
```

Maximum value:

```text
9999.99
```

---

### Example Breakdown

```sql
NUMBER(8,3)
```

Maximum:

```text
12345.678
```

Explanation:

```text
Total Digits = 8
Decimal Digits = 3
```

---

### Real-Time Uses

```text
Salary
Interest Rate
Bill Amount
Average Marks
Tax Percentage
```

---

# NUMBER Datatype Summary

| Datatype | Purpose |
|-----------|----------|
| NUMBER(5) | Integer Values |
| NUMBER(8,2) | Decimal Values |

---

# 2. Character Datatypes

Used to store text values.

Examples:

```text
Mahesh
Ashok
Hyderabad
Male
```

---

# CHAR(size)

Stores fixed-length character data.

### Syntax

```sql
column_name CHAR(size)
```

---

### Characteristics

- Fixed Length Storage
- Maximum Length = 2000 Characters
- Memory allocated statically

---

### Example

```sql
gender CHAR(1)
```

Values:

```text
M
F
```

---

### Example

```sql
student_name CHAR(25)
```

Stored Value:

```text
Mahesh
```

Oracle reserves all 25 characters.

---

### Fixed Length Illustration

```text
CHAR(10)

Value Stored:
Mahesh

Actual Storage:
Mahesh____
```

(remaining spaces are reserved)

---

# VARCHAR / VARCHAR2

Stores variable-length character data.

### Syntax

```sql
column_name VARCHAR2(size)
```

---

### Characteristics

- Variable Length Storage
- Dynamic Memory Allocation
- Maximum Length = 4000 Characters

---

### Example

```sql
student_name VARCHAR2(30)
```

Stored:

```text
Ashok
```

Only required memory is used.

---

### Variable Length Illustration

```text
VARCHAR2(30)

Value:
Ashok

Storage:
Ashok
```

Unused memory is not reserved.

---

# VARCHAR vs VARCHAR2

| VARCHAR | VARCHAR2 |
|----------|-----------|
| SQL Standard | Oracle Specific |
| Rarely Used | Most Common |
| Supported for Compatibility | Recommended by Oracle |

---

## Interview Point

Always prefer:

```sql
VARCHAR2
```

instead of

```sql
VARCHAR
```

in Oracle.

---

# CHAR vs VARCHAR2

| CHAR | VARCHAR2 |
|--------|----------|
| Fixed Length | Variable Length |
| Static Memory | Dynamic Memory |
| Wastes Space | Efficient Storage |
| Suitable for Fixed Values | Suitable for Variable Values |

---

### Example

```sql
gender CHAR(1)
```

Good choice because values are fixed.

---

```sql
employee_name VARCHAR2(50)
```

Good choice because names vary in length.

---

# 3. DATE Datatype

Used to store date values.

---

## Real-Time Examples

```text
Date Of Birth
Joining Date
Purchase Date
Hire Date
Booking Date
```

---

## Syntax

```sql
dob DATE
```

---

## Oracle Default Date Format

```text
DD-MON-YY
```

Example:

```text
12-FEB-13
```

---

### Sample Values

```text
24-APR-04
18-APR-02
14-APR-03
```

---

# 4. TIMESTAMP Datatype

Stores both date and time.

---

## Syntax

```sql
created_dt TIMESTAMP
```

---

## Oracle Default Format

```text
DD-MON-YY HH:MI:SS
```

Example:

```text
12-FEB-13 18:20:35
```

---

## Real-Time Uses

```text
Created Date
Login Time
Order Time
Audit Logs
Transaction Time
```

---

# DATE vs TIMESTAMP

| DATE | TIMESTAMP |
|--------|----------|
| Stores Date | Stores Date + Time |
| Less Information | More Information |
| Birth Date | Transaction Time |

---

# 5. Large Object Datatypes

Used for very large data.

---

# CLOB

## Full Form

```text
Character Large Object
```

Stores very large text data.

---

### Size

```text
1 GB - 4 GB
```

---

### Examples

```text
Articles
Books
Reports
Documents
```

---

# BLOB

## Full Form

```text
Binary Large Object
```

Stores binary data.

---

### Size

```text
1 GB - 4 GB
```

---

### Examples

```text
Images
Videos
Audio Files
PDF Files
```

---

# BFILE

## Full Form

```text
Binary File
```

Stores references to external binary files.

---

### Examples

```text
External Images
External Videos
External Documents
```

---

# Employee Table Example

## Table Creation

```sql
CREATE TABLE ashokit_employees(
    empId NUMBER(5),
    empName VARCHAR2(50),
    gender CHAR(1),
    dob DATE,
    created_dt TIMESTAMP
);
```

---

# Understanding the Design

| Column | Datatype | Reason |
|----------|----------|----------|
| empId | NUMBER(5) | Employee Number |
| empName | VARCHAR2(50) | Variable Length Name |
| gender | CHAR(1) | Fixed Value (M/F) |
| dob | DATE | Birth Date |
| created_dt | TIMESTAMP | Date + Time |

---

# Inserting Records

## Example

```sql
INSERT INTO ashokit_employees
VALUES(
    5656,
    'Rani',
    'F',
    '24-APR-2004',
    SYSDATE
);
```

---

## SYSDATE

Returns current system date and time.

Example:

```sql
SYSDATE
```

Output:

```text
Current Date and Time
```

---

# Viewing Table Data

```sql
SELECT *
FROM ashokit_employees;
```

---

# Describe Command (DESC)

Used to view table structure.

### Syntax

```sql
DESC table_name;
```

---

### Example

```sql
DESC ashokit_employees;
```

Output:

```text
EMPID        NUMBER(5)
EMPNAME      VARCHAR2(50)
GENDER       CHAR(1)
DOB          DATE
CREATED_DT   TIMESTAMP(6)
```

---

# Interview Questions

## What is a Datatype?

A datatype defines the type of value allowed in a column.

---

## Difference Between NUMBER(5) and NUMBER(5,2)

| NUMBER(5) | NUMBER(5,2) |
|------------|------------|
| Integer Values | Decimal Values |
| 99999 | 999.99 |

---

## Difference Between CHAR and VARCHAR2

| CHAR | VARCHAR2 |
|--------|----------|
| Fixed Length | Variable Length |
| Static Memory | Dynamic Memory |
| More Space Usage | Efficient Storage |

---

## Which Character Datatype Is Recommended in Oracle?

```text
VARCHAR2
```

---

## Difference Between DATE and TIMESTAMP

| DATE | TIMESTAMP |
|--------|----------|
| Date Only | Date + Time |
| Less Precision | More Precision |

---

## What is CLOB?

Character Large Object used to store huge text data.

---

## What is BLOB?

Binary Large Object used to store images, videos, and files.

---

## What is BFILE?

Stores references to external binary files.

---

## What Does DESC Command Do?

Displays table structure.

Example:

```sql
DESC ashokit_employees;
```

---

# Quick Revision

```text
NUMBER(size)
    → Integers

NUMBER(p,s)
    → Decimals

CHAR
    → Fixed Length Characters

VARCHAR2
    → Variable Length Characters

DATE
    → Date Only

TIMESTAMP
    → Date + Time

CLOB
    → Large Text Data

BLOB
    → Binary Data

BFILE
    → External Binary Files

DESC
    → Display Table Structure

SYSDATE
    → Current System Date & Time
```
