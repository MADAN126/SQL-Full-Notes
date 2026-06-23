# 12-SQL-Constraints-Check-Default.md

# SQL Constraints: CHECK & DEFAULT

## CHECK Constraint

### Definition
A CHECK constraint restricts the values that can be inserted or updated in a column based on a specified condition.

### Key Points

- Prevents invalid data from being stored.
- Can be applied at both column level and table level.
- Can be applied to one or multiple columns.
- Allows NULL values unless combined with NOT NULL.
- A column can have multiple CHECK constraints.

---

## Column-Level CHECK Constraint

### Syntax

```sql
CREATE TABLE table_name (
    column_name datatype CHECK(condition)
);
```

### Example

```sql
CREATE TABLE parts (
    part_id NUMBER UNIQUE NOT NULL,
    part_name VARCHAR2(255) NOT NULL,
    buy_price NUMBER(9,2) CHECK(buy_price > 0)
);
```

### Valid Inserts

```sql
INSERT INTO parts VALUES(1,'Engine',2500);
INSERT INTO parts VALUES(2,'Horn',3500);
INSERT INTO parts VALUES(3,'Mirror',1500);
```

### Invalid Insert

```sql
INSERT INTO parts VALUES(1,'Engine',0);
```

**Output**

```text
ORA-02290: check constraint violated
```

---

## CHECK Constraint Using BETWEEN

### Example

```sql
CREATE TABLE parts_1 (
    part_id NUMBER UNIQUE NOT NULL,
    part_name VARCHAR2(255) NOT NULL,
    buy_price NUMBER(9,2)
        CHECK(buy_price BETWEEN 5000 AND 99999)
);
```

### Valid Inserts

```sql
INSERT INTO parts_1 VALUES(1,'Engine',25000);
INSERT INTO parts_1 VALUES(2,'Horn',35000);
INSERT INTO parts_1 VALUES(3,'Mirror',15000);
```

### Invalid Inserts

```sql
INSERT INTO parts_1 VALUES(4,'Mirror',4500);

INSERT INTO parts_1 VALUES(5,'Mirror',4999);
```

**Output**

```text
ORA-02290: check constraint violated
```

---

## Table-Level CHECK Constraint

### Syntax

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    CONSTRAINT constraint_name CHECK(condition)
);
```

### Example

```sql
CREATE TABLE parts (
    part_id NUMBER UNIQUE NOT NULL,
    part_name VARCHAR2(255) NOT NULL,
    buy_price NUMBER(9,2),

    CONSTRAINT check_constraint
    CHECK(buy_price > 0)
);
```

---

## CHECK Constraint Using IN

### Example

```sql
CREATE TABLE parts_3 (
    part_id NUMBER UNIQUE NOT NULL,

    part_name VARCHAR2(255)
        NOT NULL
        CHECK(
            part_name IN
            ('HORN','MIRRORS','SCREWS','TOOLS')
        ),

    buy_price NUMBER(9,2)
);
```

### Valid Inserts

```sql
INSERT INTO parts_3 VALUES(1,'MIRRORS',3500);

INSERT INTO parts_3 VALUES(2,'HORN',3500);
```

### Invalid Insert

```sql
INSERT INTO parts_3 VALUES(3,'ENGINE',3500);
```

**Output**

```text
ORA-02290: check constraint violated
```

---

## Add CHECK Constraint After Table Creation

### Syntax

```sql
ALTER TABLE table_name
ADD CONSTRAINT constraint_name
CHECK(condition);
```

### Example

```sql
ALTER TABLE parts
ADD CONSTRAINT check_positive_cost
CHECK(cost > 0);
```

---

## Add New Column

```sql
ALTER TABLE parts
ADD cost NUMBER(9,2);
```

---

## Drop CHECK Constraint

```sql
ALTER TABLE table_name
DROP CONSTRAINT constraint_name;
```

### Example

```sql
ALTER TABLE parts
DROP CONSTRAINT check_positive_cost;
```

---

## Disable CHECK Constraint

```sql
ALTER TABLE table_name
DISABLE CONSTRAINT constraint_name;
```

### Example

```sql
ALTER TABLE parts
DISABLE CONSTRAINT check_positive_cost;
```

---

## Enable CHECK Constraint

```sql
ALTER TABLE table_name
ENABLE CONSTRAINT constraint_name;
```

### Example

```sql
ALTER TABLE parts
ENABLE CONSTRAINT check_positive_cost;
```

---

# DEFAULT Constraint

## Definition

A DEFAULT constraint automatically inserts a predefined value when the user does not provide a value for that column.

### Key Points

- Automatically supplies a value.
- Useful for status, country, created date, etc.
- Can be applied to multiple columns.
- Reduces unnecessary NULL values.

---

## Syntax

```sql
CREATE TABLE table_name (
    column_name datatype DEFAULT value
);
```

---

## Example

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

### Insert Without Country and DOJ

```sql
INSERT INTO Employee(ID, Name, Age)
VALUES(1, 'Mahesh', 25);
```

### Stored Result

| ID | Name | Age | Country | DOJ |
|----|------|-----|---------|-----|
| 1 | Mahesh | 25 | INDIA | Current System Date |

---

## Add DEFAULT Constraint After Table Creation

### Syntax

```sql
ALTER TABLE table_name
MODIFY column_name DEFAULT value;
```

### Example

```sql
ALTER TABLE Employee
MODIFY Country DEFAULT 'INDIA';
```

---

## Remove DEFAULT Value

### Syntax

```sql
ALTER TABLE table_name
MODIFY column_name DEFAULT NULL;
```

### Example

```sql
ALTER TABLE Employee
MODIFY Country DEFAULT NULL;
```

---

# Quick Revision

| Constraint | Duplicate Allowed | NULL Allowed | Purpose |
|------------|------------------|--------------|----------|
| UNIQUE | ❌ No | ✅ One NULL | Prevent duplicates |
| NOT NULL | ✅ Yes | ❌ No | Prevent NULL values |
| CHECK | Depends on condition | ✅ Yes | Restrict values |
| DEFAULT | Depends | Uses default value | Auto-fill values |

---

# Interview Questions

## Can CHECK Constraint Allow NULL?

Yes.

```sql
salary NUMBER CHECK(salary > 0)
```

The constraint validates only non-NULL values. NULL is allowed unless NOT NULL is also specified.

---

## Difference Between CHECK and DEFAULT

| CHECK | DEFAULT |
|---------|---------|
| Validates data | Supplies data |
| Rejects invalid values | Inserts predefined value |
| Used for rules | Used for automatic values |

Example:

```sql
salary NUMBER CHECK(salary > 0)
```

```sql
country VARCHAR2(20) DEFAULT 'INDIA'
```
