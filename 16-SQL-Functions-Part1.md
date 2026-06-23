# 16-SQL-Functions-Part1.md

# SQL Functions - Part 1

## What is a Function?

A Function is a self-contained block of statements that performs a specific task.

### Advantages

- Code Reusability
- Reduces complexity
- Improves readability
- Returns a value after processing input

### Important Point

Every function returns only one value.

---

# Types of Functions

## 1. System Defined Functions

Functions provided by Oracle itself.

Examples:

- LENGTH()
- UPPER()
- LOWER()
- TRIM()
- SYSDATE()

---

## 2. User Defined Functions (UDF)

Functions created by programmers to satisfy business requirements.

Example:

```sql
CREATE FUNCTION calculate_bonus(...)
```

---

# Categories of Oracle Functions

## 1. Single Row Functions

- Work on each row individually.
- Return one result for every row.

Example:

```sql
SELECT ename,
       LENGTH(ename)
FROM emp;
```

Output:

```text
SMITH   5
ALLEN   5
WARD    4
```

---

## 2. Multiple Row (Aggregate) Functions

- Work on the entire table.
- Return only one value.

Examples:

```sql
SUM()
AVG()
COUNT()
MAX()
MIN()
```

Example:

```sql
SELECT AVG(sal)
FROM emp;
```

Returns a single value.

---

## 3. Miscellaneous Functions

Used mainly for handling NULL values.

Examples:

```sql
NVL()
NVL2()
COALESCE()
NULLIF()
```

---

# Types of Tables in Oracle

## 1. Database Tables

Tables that store actual business data.

Examples:

```text
EMP
DEPT
CUSTOMERS
PRODUCTS
ORDERS
```

Example:

```sql
SELECT *
FROM emp;
```

---

## 2. Non-Database Tables

Tables that do not store actual business data.

Oracle provides one special table:

```text
DUAL
```

---

# DUAL Table

DUAL is a special one-row, one-column table provided by Oracle.

Used for:

1. Evaluating expressions
2. Evaluating pseudo columns
3. Executing functions

---

## Example 1: Mathematical Expressions

```sql
SELECT (2 + 3 + 4 + 5) / 2
FROM dual;
```

Output:

```text
7
```

---

### With Alias

```sql
SELECT (2 + 3 + 4 + 5) / 2 AS "Division Operation"
FROM dual;
```

Output:

```text
Division Operation
------------------
7
```

---

## Example 2: Current Date

```sql
SELECT SYSDATE
FROM dual;
```

Output:

```text
21-DEC-22
```

---

## Example 3: Execute Functions

```sql
SELECT LENGTH('Welcome To Ashok IT')
FROM dual;
```

Output:

```text
19
```

---

# Single Row Functions

These functions process one row at a time and return one result per row.

---

# 1. LENGTH()

Returns the number of characters in a string.

### Syntax

```sql
LENGTH(string)
```

### Examples

```sql
SELECT LENGTH('Welcome To Hyderabad')
FROM dual;
```

Output:

```text
20
```

---

```sql
SELECT ename,
       LENGTH(ename)
FROM emp;
```

Output:

```text
SMITH   5
WARD    4
ALLEN   5
```

---

# 2. INITCAP()

Converts the first letter of every word to uppercase.

### Syntax

```sql
INITCAP(string)
```

### Example

```sql
SELECT INITCAP('welcome to ashok it hyderabad')
FROM dual;
```

Output:

```text
Welcome To Ashok It Hyderabad
```

---

# 3. CHR()

Returns a character corresponding to an ASCII value.

### Syntax

```sql
CHR(number)
```

### Example

```sql
SELECT CHR(122)
FROM dual;
```

Output:

```text
z
```

---

```sql
SELECT CHR(65)
FROM dual;
```

Output:

```text
A
```

---

# 4. ASCII()

Returns the ASCII value of a character.

### Syntax

```sql
ASCII(character)
```

### Example

```sql
SELECT ASCII('a')
FROM dual;
```

Output:

```text
97
```

---

```sql
SELECT ASCII('A')
FROM dual;
```

Output:

```text
65
```

---

# 5. UPPER()

Converts text into uppercase.

### Syntax

```sql
UPPER(string)
```

### Example

```sql
SELECT UPPER('mahesh')
FROM dual;
```

Output:

```text
MAHESH
```

---

# 6. LOWER()

Converts text into lowercase.

### Syntax

```sql
LOWER(string)
```

### Example

```sql
SELECT LOWER('MAHESH')
FROM dual;
```

Output:

```text
mahesh
```

---

# 7. REVERSE()

Reverses a string.

### Syntax

```sql
REVERSE(string)
```

### Example

```sql
SELECT REVERSE('Mahesh')
FROM dual;
```

Output:

```text
hsehaM
```

---

# 8. TRIM()

Removes spaces from both left and right sides.

### Syntax

```sql
TRIM(string)
```

### Example

```sql
SELECT TRIM('   Welcome To Ashok IT   ')
FROM dual;
```

Output:

```text
Welcome To Ashok IT
```

---

### Length Comparison

```sql
SELECT LENGTH('   Welcome To Ashok IT   '),
       LENGTH(TRIM('   Welcome To Ashok IT   '))
FROM dual;
```

Output:

```text
26   19
```

---

# 9. LTRIM()

Removes spaces only from the left side.

### Syntax

```sql
LTRIM(string)
```

### Example

```sql
SELECT LTRIM('      Welcome To Ashok IT')
FROM dual;
```

Output:

```text
Welcome To Ashok IT
```

---

# 10. RTRIM()

Removes spaces only from the right side.

### Syntax

```sql
RTRIM(string)
```

### Example

```sql
SELECT RTRIM('Welcome To Ashok IT      ')
FROM dual;
```

Output:

```text
Welcome To Ashok IT
```

---

# 11. LPAD()

Pads characters on the left side.

### Syntax

```sql
LPAD(string, total_length, pad_character)
```

### Example

```sql
SELECT LPAD('Ashok IT',15,'*')
FROM dual;
```

Output:

```text
*******Ashok IT
```

---

# 12. RPAD()

Pads characters on the right side.

### Syntax

```sql
RPAD(string, total_length, pad_character)
```

### Example

```sql
SELECT RPAD('Ashok IT',15,'*')
FROM dual;
```

Output:

```text
Ashok IT*******
```

---

# 13. TRANSLATE()

Replaces characters in a string.

### Syntax

```sql
TRANSLATE(source, from_char, to_char)
```

### Example

```sql
SELECT TRANSLATE('JACKJ','J','B')
FROM dual;
```

Output:

```text
BACKB
```

---

# Interview Questions

## Difference Between UPPER() and INITCAP()

### UPPER()

```sql
SELECT UPPER('welcome to ashok it')
FROM dual;
```

Output:

```text
WELCOME TO ASHOK IT
```

---

### INITCAP()

```sql
SELECT INITCAP('welcome to ashok it')
FROM dual;
```

Output:

```text
Welcome To Ashok It
```

---

## Difference Between TRIM, LTRIM, RTRIM

### TRIM()

Removes spaces from both sides.

```text
|    TEXT    |
```

↓

```text
TEXT
```

---

### LTRIM()

Removes spaces from left side only.

```text
|    TEXT|
```

↓

```text
TEXT|
```

---

### RTRIM()

Removes spaces from right side only.

```text
|TEXT    |
```

↓

```text
|TEXT
```

---

# Quick Revision

| Function | Purpose |
|-----------|----------|
| LENGTH() | Counts characters |
| INITCAP() | Capitalizes first letter of every word |
| CHR() | ASCII value → Character |
| ASCII() | Character → ASCII value |
| UPPER() | Converts to uppercase |
| LOWER() | Converts to lowercase |
| REVERSE() | Reverses string |
| TRIM() | Removes spaces from both sides |
| LTRIM() | Removes left spaces |
| RTRIM() | Removes right spaces |
| LPAD() | Adds characters to left |
| RPAD() | Adds characters to right |
| TRANSLATE() | Replaces characters |

# Key Takeaways

- Functions improve code reusability.
- DUAL table is used for expressions, functions, and pseudo columns.
- Single Row Functions return one result for each row.
- LENGTH counts spaces as characters.
- UPPER and LOWER change text case.
- TRIM family removes unwanted spaces.
- LPAD and RPAD are useful for formatting output.
- CHR and ASCII convert between characters and ASCII codes.
