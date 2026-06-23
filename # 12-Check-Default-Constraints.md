# Oracle_Session_12_SQL_Constraints_Check_Default.md

# SQL Constraints – Check Constraint & Default Constraint

## Constraint Types

1. UNIQUE
2. NOT NULL
3. CHECK
4. DEFAULT
5. PRIMARY KEY
6. FOREIGN KEY

---

## Constraint Levels

### Column-Level Constraint

Constraint is defined directly with a column.

```sql
column_name datatype constraint
```

### Table-Level Constraint

Constraint is defined separately after all columns.

```sql
constraint constraint_name constraint_definition
```

---

# CHECK Constraint

A CHECK constraint restricts values that can be inserted or updated into a column.

## Key Points

- Prevents invalid data.
- Allows only values satisfying a condition.
- Can be applied to one or more columns.
- Allows NULL values unless NOT NULL is specified.
- Can be defined at column level or table level.

---

## Column-Level CHECK Constraint

### Syntax

```sql
CREATE TABLE table_name(
    column_name datatype CHECK(condition)
);
```

### Example

```sql
CREATE TABLE parts(
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

### Output

| PART_ID | PART_NAME | BUY_PRICE |
|----------|-----------|------------|
| 1 | Engine | 2500 |
| 2 | Horn | 3500 |
| 3 | Mirror | 1500 |

---

## Invalid CHECK Example

```sql
INSERT INTO parts VALUES(1,'Engine',0);
```

### Error

```text
ORA-02290: check constraint violated
```

Reason:

```sql
buy_price > 0
```

0 does not satisfy the condition.

---

## CHECK Using BETWEEN

### Example

```sql
CREATE TABLE parts_1(
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
INSERT INTO parts_1 VALUES(3,'Mirror',4500);

INSERT INTO parts_1 VALUES(3,'Mirror',4999);
```

### Error

```text
ORA-02290: check constraint violated
```

Because values are less than 5000.

---

## Table-Level CHECK Constraint

### Syntax

```sql
CREATE TABLE table_name(
    column1 datatype,
    column2 datatype,
    CONSTRAINT constraint_name CHECK(condition)
);
```

### Example

```sql
CREATE TABLE parts(
    part_id NUMBER UNIQUE NOT NULL,
    part_name VARCHAR2(255) NOT NULL,
    buy_price NUMBER(9,2),
    CONSTRAINT check_constraint CHECK(buy_price > 0)
);
```

---

## CHECK Using IN Operator

### Example

```sql
CREATE TABLE parts_3(
    part_id NUMBER UNIQUE NOT NULL,
    part_name VARCHAR2(255) NOT NULL
        CHECK(part_name IN
        ('HORN','MIRRORS','SCREWS','TOOLS')),
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

### Error

```text
ORA-02290: check constraint violated
```

Because `ENGINE` is not in:

```sql
('HORN','MIRRORS','SCREWS','TOOLS')
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

## Adding New Column Before CHECK Constraint

```sql
ALTER TABLE parts
ADD cost NUMBER(9,2);
```

---

## Drop CHECK Constraint

### Syntax

```sql
ALTER TABLE table_name
DROP CONSTRAINT constraint_name;
```

---

## Disable CHECK Constraint

### Syntax

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

### Syntax

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

A DEFAULT constraint automatically inserts a predefined value when the user does not provide one.

## Key Points

- Supplies a default value automatically.
- Reduces manual data entry.
- Helps avoid unwanted NULL values.
- Can be applied to multiple columns.
- Commonly used with dates, country names, status columns, etc.

---

## Syntax

```sql
CREATE TABLE table_name(
    column_name datatype DEFAULT value
);
```

---

## Example

```sql
CREATE TABLE Employee(
    ID NUMBER NOT NULL,
    Name VARCHAR2(20) NOT NULL,
    Age NUMBER,
    Country VARCHAR2(10) DEFAULT 'INDIA',
    DOJ DATE DEFAULT SYSDATE
);
```

---

## User Provides All Values

```sql
INSERT INTO Employee
VALUES(1,'Mahesh',25,'USA',SYSDATE);
```

Stored values:

```text
Country = USA
DOJ = Current Date
```

---

## User Omits Default Columns

```sql
INSERT INTO Employee(ID,Name,Age)
VALUES(1,'Mahesh',25);
```

Oracle automatically inserts:

```text
Country = INDIA
DOJ = Current System Date
```

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

# CHECK vs DEFAULT

| Feature | CHECK | DEFAULT |
|----------|---------|----------|
| Purpose | Restricts values | Supplies value automatically |
| Prevents invalid data | Yes | No |
| Inserts value automatically | No | Yes |
| Allows NULL | Yes | Usually avoids NULL indirectly |
| Uses conditions | Yes | No |

### Example

```sql
CHECK(salary > 0)
```

```sql
DEFAULT 'INDIA'
```

---

# Interview Questions

## What is a CHECK constraint?

A constraint that allows only values satisfying a specified condition.

---

## Can CHECK constraint allow NULL values?

Yes. CHECK validates only non-null values unless NOT NULL is also applied.

---

## Difference Between UNIQUE and CHECK

| UNIQUE | CHECK |
|---------|--------|
| Prevents duplicate values | Validates a condition |
| Allows one NULL | Allows multiple NULLs |

---

## What is a DEFAULT constraint?

A constraint that automatically inserts a predefined value when no value is supplied.

---

## Can DEFAULT and NOT NULL be used together?

Yes.

```sql
country VARCHAR2(20)
DEFAULT 'INDIA'
NOT NULL
```

This guarantees that the column always contains a value.
