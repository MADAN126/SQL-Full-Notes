# 18-SQL-Functions-Session3.md

# SQL Functions - Session 3

**Date:** 23/12/2022  
**Session:** 23

---

# SQL Functions Overview

## Types of SQL Functions

### 1. Single Row Functions
Works on each row individually and returns one result per row.

- String Functions
- Math Functions
- Date Functions
- Conversion Functions

### 2. Multi Row Functions (Aggregate Functions)
Works on an entire column/table and returns a single result.

- SUM()
- AVG()
- MAX()
- MIN()
- COUNT()

### 3. Miscellaneous Functions
Used mainly for handling NULL values.

- NVL()
- NVL2()
- NULLIF()
- COALESCE()

---

# Conversion Functions

## 1. TO_CHAR()

Converts Oracle Date → Character/String format.

### Syntax

```sql
TO_CHAR(date,'FORMAT')
```

### Examples

```sql
SELECT TO_CHAR(SYSDATE,'DD/MM/YYYY') FROM dual;
-- 23/12/2022

SELECT TO_CHAR(SYSDATE,'DD-MON-YYYY') FROM dual;
-- 23-DEC-2022

SELECT TO_CHAR(SYSDATE,'YYYY/MM/DD') FROM dual;
-- 2022/12/23

SELECT TO_CHAR(SYSDATE,'DAY') FROM dual;
-- FRIDAY

SELECT TO_CHAR(SYSDATE,'MONTH') FROM dual;
-- DECEMBER

SELECT TO_CHAR(SYSDATE,'DD-MON-YYYY HH:MM:SS') FROM dual;
-- 23-DEC-2022 09:12:55

SELECT TO_CHAR(SYSDATE,'YYYY') FROM dual;
-- 2022

SELECT TO_CHAR(SYSDATE,'DD-MONTH-YYYY') FROM dual;
-- 23-DECEMBER-2022

SELECT TO_CHAR(SYSDATE,'DD-MONTH-YYYY-DAY') FROM dual;
-- 23-DECEMBER-2022-FRIDAY
```

### Important Formats

| Format | Meaning |
|----------|----------|
| DD | Day |
| MM | Month Number |
| MON | Month Short Name |
| MONTH | Full Month Name |
| YYYY | 4 Digit Year |
| DAY | Week Day |
| HH | Hour |
| MI | Minutes |
| SS | Seconds |

---

## 2. TO_DATE()

Converts Character Format Date → Oracle Date Format.

### Syntax

```sql
TO_DATE('date_string','format')
```

### Examples

```sql
SELECT TO_DATE('22/03/2015','DD/MM/YYYY')
FROM dual;
```

Output:

```text
22-MAR-15
```

```sql
SELECT TO_DATE('2015:03:12','YYYY:MM:DD')
FROM dual;
```

Output:

```text
12-MAR-15
```

### Use Cases

- User input dates
- Data migration
- Date comparisons

---

# Multi Row Functions (Aggregate Functions)

Aggregate Functions work on a complete column and return only one value.

---

## 1. SUM()

Returns total of all values.

### Syntax

```sql
SELECT SUM(column_name)
FROM table_name;
```

### Example

```sql
SELECT SUM(sal)
FROM emp;
```

Output:

```text
29025
```

---

## 2. AVG()

Returns average value.

### Syntax

```sql
SELECT AVG(column_name)
FROM table_name;
```

### Example

```sql
SELECT AVG(sal)
FROM emp;
```

Output:

```text
2073.2142...
```

---

## 3. MAX()

Returns highest value.

### Example

```sql
SELECT MAX(sal)
FROM emp;
```

Output:

```text
5000
```

---

## 4. MIN()

Returns lowest value.

### Example

```sql
SELECT MIN(sal)
FROM emp;
```

Output:

```text
800
```

---

## 5. COUNT()

Counts records.

---

### COUNT(*)

Counts all rows.

Includes:

- Duplicate values
- NULL values

```sql
SELECT COUNT(*)
FROM emp;
```

Output:

```text
14
```

---

### COUNT(column_name)

Counts:

- Duplicate values ✔
- NULL values ✘

```sql
SELECT COUNT(mgr)
FROM emp;
```

---

### COUNT(DISTINCT column_name)

Counts:

- Unique values ✔
- Duplicate values ✘
- NULL values ✘

```sql
SELECT COUNT(DISTINCT mgr)
FROM emp;
```

---

# Miscellaneous Functions

Used for NULL handling.

---

## 1. NVL()

Replaces NULL with specified value.

### Syntax

```sql
NVL(column,replacement_value)
```

### Working

```text
If NULL      → replacement value
If Not NULL  → original value
```

### Example

```sql
SELECT empno,
       sal,
       comm,
       sal + NVL(comm,1000) total_sal
FROM emp;
```

### Example

```sql
SELECT empno,
       ename,
       sal,
       comm,
       NVL(comm,100),
       sal + NVL(comm,100) AS total_salary
FROM emp
ORDER BY empno;
```

---

## 2. NVL2()

Checks whether value is NULL or NOT NULL.

### Syntax

```sql
NVL2(column,value_if_not_null,value_if_null)
```

### Working

```text
If NOT NULL → second argument
If NULL     → third argument
```

### Examples

```sql
SELECT NVL2(NULL,1,2)
FROM dual;
```

Output:

```text
2
```

```sql
SELECT NVL2(10,'ABC','XYZ')
FROM dual;
```

Output:

```text
ABC
```

```sql
SELECT empno,
       ename,
       sal,
       comm,
       NVL2(comm,comm,sal)
FROM emp;
```

---

## 3. NULLIF()

Converts value into NULL when two expressions are equal.

### Syntax

```sql
NULLIF(a,b)
```

### Working

```text
a = b  → NULL
a ≠ b  → a
```

### Example

```sql
SELECT ename,
       LENGTH(ename),
       job,
       LENGTH(job),
       NULLIF(LENGTH(ename), LENGTH(job))
FROM emp;
```

---

## 4. COALESCE()

Returns first non-null value.

### Syntax

```sql
COALESCE(value1,value2,value3,...)
```

### Example

```sql
SELECT COALESCE(NULL,NULL,123,NULL,5332)
FROM dual;
```

Output:

```text
123
```

### Example

```sql
SELECT empno,
       ename,
       sal,
       comm,
       COALESCE(comm,sal)
FROM emp;
```

---

# Interview Questions

## Difference Between NVL and NVL2

| NVL | NVL2 |
|-------|-------|
| Takes 2 arguments | Takes 3 arguments |
| Replaces NULL value | Checks NULL or NOT NULL |
| Simpler | More flexible |

---

## Difference Between COUNT(*) and COUNT(column)

| COUNT(*) | COUNT(column) |
|-----------|---------------|
| Counts all rows | Ignores NULL values |
| Includes NULL | Excludes NULL |

---

## Difference Between TO_CHAR and TO_DATE

| TO_CHAR | TO_DATE |
|----------|----------|
| Date → String | String → Date |
| Formatting output | Converting input |

---

# Quick Revision

### Conversion Functions

```sql
TO_CHAR()
TO_DATE()
```

### Aggregate Functions

```sql
SUM()
AVG()
MAX()
MIN()
COUNT()
```

### NULL Functions

```sql
NVL()
NVL2()
NULLIF()
COALESCE()
```

### Most Asked Interview Functions

```sql
COUNT(*)
COUNT(column)
COUNT(DISTINCT column)

NVL()
NVL2()

TO_CHAR()
TO_DATE()

SUM()
AVG()
MAX()
MIN()
```
