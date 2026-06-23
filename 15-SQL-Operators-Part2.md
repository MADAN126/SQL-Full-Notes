# 15-SQL-Operators-Part2.md

# SQL Operators - Part 2

## Quick Recap

### What is an Operator?

An operator is a symbol used to perform an operation on data.

### What is an Operand?

Operands are the values or variables on which operators work.

Example:

```sql
a = 10;
b = 20;
c = a + b;
```

- Operands → a, b, c
- Operators → =, +

---

## Types of SQL Operators

### 1. Arithmetic Operators

| Operator | Meaning |
|-----------|----------|
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| % | Modulus |

---

### 2. Relational Operators

| Operator | Meaning |
|-----------|----------|
| > | Greater Than |
| >= | Greater Than or Equal To |
| < | Less Than |
| <= | Less Than or Equal To |
| = | Equal To |
| <> | Not Equal To |
| != | Not Equal To |

---

### 3. Logical Operators

| Operator | Meaning |
|-----------|----------|
| AND | Both conditions must be true |
| OR | At least one condition must be true |

---

### 4. Special Operators

- BETWEEN
- NOT BETWEEN
- IN
- NOT IN
- LIKE

---

# Arithmetic Operator Examples

## Calculate 20% Discount

```sql
SELECT pid,
       pname,
       pcost,
       ((pcost * 20) / 100) AS discount_price
FROM ashokit_products_info;
```

### Output

| Product | Cost | Discount |
|----------|------|----------|
| Mobile | 14000 | 2800 |
| Laptop | 12000 | 2400 |
| Tablet | 11000 | 2200 |
| Camera | 10000 | 2000 |

---

## Calculate Final Price After Discount

```sql
SELECT pid,
       pname,
       pcost,
       (pcost * 0.2) AS discount_price,
       (pcost - (pcost * 0.2)) AS final_price
FROM ashokit_products_info;
```

### Formula

```text
Final Price = Product Cost - Discount
```

---

# Relational Operator Examples

## Products Cost Greater Than 12000

```sql
SELECT *
FROM ashokit_products_info
WHERE pcost > 12000;
```

---

## Products Cost Less Than or Equal To 12000

```sql
SELECT *
FROM ashokit_products_info
WHERE pcost <= 12000
ORDER BY pcost ASC;
```

---

## Products Between 12000 and 14000

```sql
SELECT *
FROM ashokit_products_info
WHERE pcost >= 12000
AND pcost <= 14000
ORDER BY pcost ASC;
```

---

## Warranty Equal To 2 Years

```sql
SELECT *
FROM ashokit_products_info
WHERE pwarranty = '2YEAR';
```

---

## Warranty Not Equal To 2 Years

```sql
SELECT *
FROM ashokit_products_info
WHERE pwarranty <> '2YEAR';
```

OR

```sql
SELECT *
FROM ashokit_products_info
WHERE pwarranty != '2YEAR';
```

---

# NULL Operators

## Employees Not Receiving Commission

```sql
SELECT *
FROM emp
WHERE comm IS NULL;
```

---

## Employees Receiving Commission

```sql
SELECT *
FROM emp
WHERE comm IS NOT NULL;
```

---

# BETWEEN Operator

Used to retrieve values within a range.

---

## Commission Between 100 and 500

### Using Relational Operators

```sql
SELECT *
FROM emp
WHERE comm > 100
AND comm <= 500;
```

### Using BETWEEN

```sql
SELECT *
FROM emp
WHERE comm BETWEEN 100 AND 500;
```

---

## Employees Joined in 1981

```sql
SELECT *
FROM emp
WHERE hiredate BETWEEN
      '01-JAN-1981'
  AND '31-DEC-1981';
```

---

# IN Operator

Used when matching multiple values.

---

## Employees Working as Clerk or Salesman

### Using OR

```sql
SELECT *
FROM emp
WHERE job = 'CLERK'
OR job = 'SALESMAN'
ORDER BY job ASC;
```

### Using IN

```sql
SELECT *
FROM emp
WHERE job IN ('CLERK','SALESMAN')
ORDER BY job ASC;
```

Recommended because it is cleaner and easier to read.

---

## Employees Working as Clerk or Manager

```sql
SELECT *
FROM emp
WHERE job IN ('CLERK','MANAGER');
```

---

## Employees With Salaries 1250, 3000, 5000

```sql
SELECT *
FROM emp
WHERE sal IN (1250,3000,5000);
```

---

# NOT IN Operator

Used to exclude multiple values.

---

## Employees Not Working as Clerk or Salesman

### Using AND

```sql
SELECT *
FROM emp
WHERE job <> 'CLERK'
AND job <> 'SALESMAN';
```

### Using NOT IN

```sql
SELECT *
FROM emp
WHERE job NOT IN ('CLERK','SALESMAN');
```

Recommended approach.

---

# Subquery Example

## Employees Working in Sales Department

### Step 1

```sql
SELECT *
FROM dept
WHERE dname = 'SALES';
```

### Step 2

```sql
SELECT deptno
FROM dept
WHERE dname = 'SALES';
```

### Step 3

```sql
SELECT *
FROM emp
WHERE deptno IN
(
    SELECT deptno
    FROM dept
    WHERE dname = 'SALES'
);
```

---

# LIKE Operator

Used for pattern matching.

---

## Names Starting With A

```sql
SELECT *
FROM emp
WHERE ename LIKE 'A%'
ORDER BY ename ASC;
```

### Matches

```text
ADAMS
ALLEN
```

---

## Names Ending With S

```sql
SELECT *
FROM emp
WHERE ename LIKE '%S'
ORDER BY ename ASC;
```

### Matches

```text
JAMES
JONES
```

---

## Names Starting With A and Ending With S

```sql
SELECT *
FROM emp
WHERE ename LIKE 'A%S';
```

---

## Names Starting With J and Ending With S

```sql
SELECT *
FROM emp
WHERE ename LIKE 'J%S';
```

---

# Wildcards

## % (Percent)

Represents any number of characters.

Examples:

```sql
LIKE 'A%'
```

Starts with A.

```sql
LIKE '%S'
```

Ends with S.

```sql
LIKE '%A%'
```

Contains A.

---

## _ (Underscore)

Represents exactly one character.

---

## Employee Names Having Exactly 5 Characters

```sql
SELECT *
FROM emp
WHERE ename LIKE '_____';
```

Examples:

```text
SMITH
ALLEN
JONES
BLAKE
CLARK
```

---

## Employee Names Having 5 Characters and Ending With S

```sql
SELECT *
FROM emp
WHERE ename LIKE '____S';
```

Examples:

```text
JONES
JAMES
```

---

## Salaries Containing Exactly 3 Digits

```sql
SELECT *
FROM emp
WHERE sal LIKE '___';
```

Examples:

```text
800
950
```

---

# Important Interview Questions

### Difference Between IN and OR

```sql
WHERE job = 'CLERK'
OR job = 'MANAGER'
```

vs

```sql
WHERE job IN ('CLERK','MANAGER')
```

Both give the same result.

`IN` is cleaner and easier to maintain.

---

### Difference Between BETWEEN and AND

```sql
WHERE sal >= 1000
AND sal <= 3000
```

vs

```sql
WHERE sal BETWEEN 1000 AND 3000
```

Both produce the same result.

`BETWEEN` is more readable.

---

### Difference Between NULL and 0

```text
NULL → Value is unknown or missing.
0    → Actual numeric value.
```

Example:

```sql
WHERE comm IS NULL
```

is NOT the same as

```sql
WHERE comm = 0
```

---

# Key Takeaways

- Arithmetic operators perform calculations.
- Relational operators compare values.
- Logical operators combine conditions.
- BETWEEN checks ranges.
- IN checks multiple values.
- NOT IN excludes multiple values.
- LIKE performs pattern matching.
- `%` = any number of characters.
- `_` = exactly one character.
- Use `IS NULL` and `IS NOT NULL` for NULL handling.
- Subqueries can be used inside `IN`.
