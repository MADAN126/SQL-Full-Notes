# 10-OrderBy-Nulls-Alias.md

# ORDER BY Clause

## Purpose

The `ORDER BY` clause is used to retrieve data in a sorted order.

Without `ORDER BY`, rows are returned in an unspecified order.

---

# Key Points

- Used for sorting query results.
- Can sort data in:
  - Ascending order (`ASC`)
  - Descending order (`DESC`)
- Default sorting order is `ASC`.
- Can be applied to:
  - Numeric columns
  - Character columns
  - Date columns
- Can sort using multiple columns.
- Commonly used while generating reports.

---

# Syntax

```sql
SELECT *
FROM table_name
ORDER BY column_name [ASC | DESC];
```

---

# Ascending Order

## Default Behavior

```sql
SELECT *
FROM emp
ORDER BY ename;
```

Equivalent to:

```sql
SELECT *
FROM emp
ORDER BY ename ASC;
```

---

## Example

Display employees alphabetically.

```sql
SELECT *
FROM emp
ORDER BY ename ASC;
```

---

# Descending Order

## Syntax

```sql
SELECT *
FROM emp
ORDER BY ename DESC;
```

---

## Example

Display employee names in reverse alphabetical order.

```sql
SELECT ename
FROM emp
ORDER BY ename DESC;
```

---

# Sorting Numeric Columns

## Example

Display employees by salary from highest to lowest.

```sql
SELECT empno,
       ename,
       sal
FROM emp
ORDER BY sal DESC;
```

---

# ORDER BY with WHERE Clause

Filtering happens first.

Sorting happens later.

---

## Example

Display all SALESMAN employees sorted by name.

```sql
SELECT *
FROM emp
WHERE job = 'SALESMAN'
ORDER BY ename;
```

---

## Descending Order

```sql
SELECT *
FROM emp
WHERE job = 'SALESMAN'
ORDER BY ename DESC;
```

---

# Execution Flow

```text
FROM
 ↓
WHERE
 ↓
SELECT
 ↓
ORDER BY
```

---

# Multiple Column Sorting

## Syntax

```sql
SELECT *
FROM emp
ORDER BY deptno, sal DESC;
```

---

## Processing

```text
1. Sort by deptno
2. Within same department sort by salary descending
```

---

# ORDER BY Quick Examples

```sql
SELECT * FROM emp ORDER BY ename;
```

```sql
SELECT * FROM emp ORDER BY ename DESC;
```

```sql
SELECT * FROM emp ORDER BY sal;
```

```sql
SELECT * FROM emp ORDER BY sal DESC;
```

```sql
SELECT * FROM emp WHERE deptno = 10 ORDER BY ename;
```

---

# Understanding NULL Values

## What is NULL?

NULL represents:

```text
Missing Information
Unknown Information
Not Applicable Information
```

---

## Examples

Employee commission not assigned.

```text
COMM = NULL
```

Customer mobile number not provided.

```text
MOBILE = NULL
```

---

# Important Facts About NULL

NULL is NOT:

```text
0
''
False
```

NULL means:

```text
Value does not exist / unknown
```

---

# Invalid Comparisons

Never use:

```sql
WHERE comm = NULL
```

```sql
WHERE comm != NULL
```

These do not work correctly.

---

# NULL Conditions

Oracle provides:

```sql
IS NULL
IS NOT NULL
```

---

# IS NULL

## Purpose

Find rows where a column contains NULL.

---

## Syntax

```sql
SELECT *
FROM table_name
WHERE column_name IS NULL;
```

---

## Example

Display employees without commission.

```sql
SELECT *
FROM emp
WHERE comm IS NULL;
```

---

## Example

Display products without price.

```sql
SELECT *
FROM products
WHERE product_price IS NULL;
```

---

# IS NOT NULL

## Purpose

Find rows where values exist.

---

## Syntax

```sql
SELECT *
FROM table_name
WHERE column_name IS NOT NULL;
```

---

## Example

Display employees earning commission.

```sql
SELECT *
FROM emp
WHERE comm IS NOT NULL;
```

---

## Example

Display products having price.

```sql
SELECT *
FROM products
WHERE product_price IS NOT NULL;
```

---

# NULL Summary

| Condition | Meaning |
|------------|----------|
| IS NULL | Missing Value |
| IS NOT NULL | Existing Value |
| = NULL | Invalid |
| != NULL | Invalid |

---

# Oracle Alias

## What is an Alias?

Alias is a temporary alternate name given to:

- Columns
- Tables
- Expressions

---

## Why Use Alias?

Improves readability of reports.

Instead of:

```text
EMPNO
ENAME
```

Display:

```text
Employee No
Employee Name
```

---

# Types of Alias

1. Column Alias
2. Table Alias
3. Expression Alias

---

# Column Alias

## Purpose

Provide meaningful names to columns.

---

# Syntax

```sql
SELECT column_name AS alias_name
FROM table_name;
```

---

# Example

```sql
SELECT empno AS "Employee No",
       ename AS "Employee Name"
FROM emp;
```

---

# AS Keyword Optional

These are equivalent:

```sql
SELECT empno AS "Employee No"
FROM emp;
```

```sql
SELECT empno "Employee No"
FROM emp;
```

```sql
SELECT empno EmployeeNo
FROM emp;
```

---

# Multiple Column Aliases

```sql
SELECT empno AS "Employee No",
       ename AS "Employee Name",
       sal AS "Salary"
FROM emp;
```

---

# Table Alias

## Purpose

Provide short names for tables.

Very useful in joins.

---

# Syntax

```sql
SELECT *
FROM table_name alias_name;
```

---

# Example

Without alias:

```sql
SELECT *
FROM emp;
```

---

With alias:

```sql
SELECT *
FROM emp e;
```

---

# Accessing Columns Through Alias

```sql
SELECT e.empno,
       e.ename,
       e.sal
FROM emp e;
```

---

# Selecting Entire Table

```sql
SELECT e.*
FROM emp e;
```

---

# Why Table Alias?

Reduces typing.

Instead of:

```sql
SELECT emp.empno,
       emp.ename
FROM emp;
```

Use:

```sql
SELECT e.empno,
       e.ename
FROM emp e;
```

---

# Expression Alias

## Purpose

Provide alias names to calculated values.

---

# Example

Annual Salary Calculation

```sql
SELECT empno,
       ename,
       sal,
       sal * 12 AS "Annual Salary"
FROM emp;
```

---

# Output

```text
EMPNO   ENAME    Annual Salary
--------------------------------
7369    SMITH      9600
7499    ALLEN     19200
```

---

# More Examples

## Monthly to Yearly Salary

```sql
SELECT ename,
       sal,
       sal * 12 AS "Annual Salary"
FROM emp;
```

---

## Bonus Calculation

```sql
SELECT ename,
       sal,
       sal * 0.10 AS "Bonus"
FROM emp;
```

---

## Salary After Increment

```sql
SELECT ename,
       sal,
       sal + 5000 AS "Updated Salary"
FROM emp;
```

---

# Alias Rules

## Allowed

```sql
SELECT empno AS EmployeeNo
FROM emp;
```

```sql
SELECT empno "Employee No"
FROM emp;
```

---

## Recommended for Spaces

```sql
SELECT empno AS "Employee No"
FROM emp;
```

---

# Real-Time Usage

## Reporting

```sql
SELECT empno AS "Employee ID",
       ename AS "Employee Name",
       sal AS "Monthly Salary"
FROM emp;
```

Produces user-friendly reports.

---

# Interview Questions

## What is ORDER BY?

Used to sort query results.

---

## What is the default sorting order?

```text
ASC (Ascending)
```

---

## Which keyword is used for descending order?

```text
DESC
```

---

## Can ORDER BY be applied to multiple columns?

```text
Yes
```

---

## What is NULL?

Represents missing or unknown information.

---

## How to find NULL values?

```sql
IS NULL
```

---

## How to find non-NULL values?

```sql
IS NOT NULL
```

---

## What is an Alias?

Temporary alternate name for a column, table, or expression.

---

## Types of Alias?

```text
1. Column Alias
2. Table Alias
3. Expression Alias
```

---

## Is AS keyword mandatory?

```text
No
```

---

# Quick Revision

```text
ORDER BY
 ├─ ASC (Default)
 └─ DESC

NULL
 ├─ Missing Value
 ├─ IS NULL
 └─ IS NOT NULL

ALIAS
 ├─ Column Alias
 ├─ Table Alias
 └─ Expression Alias

Column Alias
 └─ Better Repor
