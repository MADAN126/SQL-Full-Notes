# 14-SQL-Operators.md

# SQL Operators

## Foreign Key Recap

### Parent Table

```sql
CREATE TABLE ashokit_companies_info(
    company_code VARCHAR2(10),
    company_name VARCHAR2(30) NOT NULL,
    country VARCHAR2(50) NOT NULL,

    CONSTRAINT ashokit_comp_cde_pk
    PRIMARY KEY(company_code)
);
```

### Child Table

```sql
CREATE TABLE ashokit_products_info(
    pid VARCHAR2(10) PRIMARY KEY,
    pname VARCHAR2(30) NOT NULL,
    pcost NUMBER,
    pmfg_dt DATE NOT NULL,
    pwarranty VARCHAR2(50) NOT NULL,
    company_code VARCHAR2(10),

    CONSTRAINT ashokit_comp_code_fk
    FOREIGN KEY(company_code)
    REFERENCES ashokit_companies_info(company_code)
);
```

---

## Add Foreign Key After Table Creation

```sql
ALTER TABLE ashokit_products_info
ADD CONSTRAINT ASHOKIT_COMP_CODE_FK
FOREIGN KEY(company_code)
REFERENCES ashokit_companies_info(company_code);
```

---

## Drop Foreign Key

```sql
ALTER TABLE ashokit_products_info
DROP CONSTRAINT ASHOKIT_COMP_CODE_FK;
```

---

## Foreign Key Syntax

```sql
CREATE TABLE child_table(
    ...
    CONSTRAINT fk_name
    FOREIGN KEY(col1,col2,...)
    REFERENCES parent_table(col1,col2,...)
    ON DELETE CASCADE
);
```

### ON DELETE Options

#### ON DELETE CASCADE

When a parent row is deleted:

- Parent row deleted
- Related child rows automatically deleted

#### ON DELETE SET NULL

When a parent row is deleted:

- Parent row deleted
- Child foreign key column becomes NULL

---

# Interview Question

## Column Level vs Table Level Constraints

### Column Level Constraint

Oracle automatically generates constraint names.

Example:

```text
SYS_C008975
```

### Table Level Constraint

Programmer provides custom constraint names.

Example:

```text
ASHOKIT_COMP_CODE_FK
```

---

# Viewing Constraints

## View All Constraints

```sql
SELECT *
FROM user_constraints;
```

## View Constraints of Specific Table

```sql
SELECT *
FROM user_constraints
WHERE table_name='ASHOKIT_PRODUCTS_INFO';
```

---

# SQL Operators

## What is an Operator?

An operator is a symbol that performs a specific operation.

### Example

```sql
a = 10;
b = 20;

c = a + b;
```

### Operands

```text
a
b
c
```

### Operators

```text
=
+
```

---

# Types of SQL Operators

## 1. Arithmetic Operators

Used for mathematical calculations.

| Operator | Meaning |
|----------|----------|
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| % | Modulus |

---

## 2. Relational Operators

Used for comparisons.

| Operator | Meaning |
|----------|----------|
| > | Greater Than |
| >= | Greater Than or Equal To |
| < | Less Than |
| <= | Less Than or Equal To |
| = | Equal To |
| <> | Not Equal To |

---

## 3. Logical Operators

Used to combine conditions.

| Operator | Meaning |
|----------|----------|
| AND | Both conditions must be true |
| OR | At least one condition must be true |

---

## 4. Special Operators

Used for advanced filtering.

| Operator | Meaning |
|----------|----------|
| BETWEEN | Range check |
| NOT BETWEEN | Outside range |
| IN | Match from list |
| NOT IN | Exclude list |
| LIKE | Pattern matching |

---

# Sample Data

```sql
SELECT * FROM ashokit_products_info;
```

| PID | PNAME | PCOST | WARRANTY |
|------|--------|--------|----------|
| P001 | Mobile | 14000 | 1YEAR |
| P002 | Laptop | 12000 | 2YEAR |
| P003 | Tablet | 11000 | 3YEAR |
| P004 | Camera | 10000 | 4YEAR |
| P009 | Keyboard | 10000 | 3YEAR |
| P008 | HeadSet | 14000 | 2YEAR |

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

---

## Calculate Discount and Final Price

```sql
SELECT pid,
       pname,
       pcost,
       (pcost * 0.2) AS discount_price,
       (pcost - (pcost * 0.2)) AS final_price
FROM ashokit_products_info;
```

---

# Relational Operator Examples

## Products Costing Above 12000

```sql
SELECT *
FROM ashokit_products_info
WHERE pcost > 12000;
```

---

## Products Costing Less Than or Equal To 12000

```sql
SELECT *
FROM ashokit_products_info
WHERE pcost <= 12000
ORDER BY pcost ASC;
```

---

## Products Costing Between 12000 and 14000

```sql
SELECT *
FROM ashokit_products_info
WHERE pcost >= 12000
  AND pcost <= 14000
ORDER BY pcost ASC;
```

---

# Equality and Inequality Examples

## Products With 2-Year Warranty

```sql
SELECT *
FROM ashokit_products_info
WHERE pwarranty = '2YEAR';
```

---

## Products Without 2-Year Warranty

```sql
SELECT *
FROM ashokit_products_info
WHERE pwarranty <> '2YEAR';
```

---

# Quick Revision

| Category | Operators |
|-----------|-----------|
| Arithmetic | +, -, *, /, % |
| Relational | >, >=, <, <=, =, <> |
| Logical | AND, OR |
| Special | BETWEEN, NOT BETWEEN, IN, NOT IN, LIKE |

---

# Interview Questions

### What is an Operator?

A symbol used to perform an operation on data.

### Difference Between Operator and Operand?

- Operator → Performs operation (`+`, `-`, `>`, `=`).
- Operand → Value on which operation is performed.

### Which Operator is Used for "Not Equal To"?

```sql
<>
```

### Which Logical Operators Are Available in SQL?

```sql
AND
OR
```

### Which Operator is Used for Range Checking?

```sql
BETWEEN
```
