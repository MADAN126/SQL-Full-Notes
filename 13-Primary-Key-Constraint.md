# 13-Primary-Key-Constraint.md

# Primary Key Constraint

## Recap of Previous Constraints

### UNIQUE

- Does not allow duplicate values.
- Allows one NULL value.

### NOT NULL

- Does not allow NULL values.
- Allows duplicate values.

### CHECK

- Restricts values based on a condition or expression.

### DEFAULT

- Inserts a default value when no value is supplied.

---

# Primary Key Constraint

A Primary Key is a combination of:

- UNIQUE
- NOT NULL

### Characteristics

- Does not allow duplicate values.
- Does not allow NULL values.
- Can be defined at Column Level.
- Can be defined at Table Level.
- Every table should have only one Primary Key.
- Used to uniquely identify each record in a table.

---

# Column Level Primary Key

## Syntax

```sql
CREATE TABLE table_name (
    column_name1 datatype PRIMARY KEY,
    column_name2 datatype,
    column_name3 datatype
);
```

## Example

```sql
CREATE TABLE ashokit_students(
    student_id NUMBER PRIMARY KEY,
    student_name VARCHAR2(30) NOT NULL,
    courses VARCHAR2(30),
    course_fee NUMBER(7,2),
    contact_no VARCHAR2(10),
    created_dt TIMESTAMP
);
```

---

# Table Level Primary Key

## Syntax

```sql
CREATE TABLE table_name(
    column_name1 datatype,
    column_name2 datatype,
    column_name3 datatype,

    CONSTRAINT constraint_name
    PRIMARY KEY(column_name)
);
```

## Example

```sql
CREATE TABLE students(
    student_id NUMBER,
    student_name VARCHAR2(30),

    CONSTRAINT pk_students
    PRIMARY KEY(student_id)
);
```

---

# Complete Example

```sql
CREATE TABLE ashokit_students(
    student_id NUMBER PRIMARY KEY,
    student_name VARCHAR2(30) NOT NULL,

    courses VARCHAR2(30)
        CHECK(courses IN (
            'Core Java',
            'Advanced Java',
            'Java Full Stack'
        )),

    course_fee NUMBER(7,2)
        CHECK(course_fee BETWEEN 5000 AND 10000),

    contact_no VARCHAR2(10)
        UNIQUE NOT NULL,

    created_dt TIMESTAMP
        DEFAULT SYSDATE
);
```

---

# Insert Records

```sql
INSERT INTO ashokit_students
VALUES(1,'Mahesh','Core Java',5000,'2112112121',SYSDATE);

INSERT INTO ashokit_students
VALUES(2,'Suresh','Advanced Java',6000,'12323232',SYSDATE);

INSERT INTO ashokit_students
VALUES(3,'Nagesh','Java Full Stack',7000,'343434343',SYSDATE);

INSERT INTO ashokit_students
VALUES(4,'Ramesh','Java Full Stack',8000,'545454545',SYSDATE);

INSERT INTO ashokit_students
VALUES(5,'Rajesh','Java Full Stack',9000,'8676767676',SYSDATE);
```

---

# Using DEFAULT Value

Since `created_dt` has a default value:

```sql
DEFAULT SYSDATE
```

We can omit it during insertion.

```sql
INSERT INTO ashokit_students(
    student_id,
    student_name,
    courses,
    course_fee,
    contact_no
)
VALUES(
    11,
    'Suman',
    'Advanced Java',
    9500,
    '454565654'
);
```

---

# View Data

```sql
SELECT * FROM ashokit_students;
```

---

# Viewing Constraints

## All Constraints

```sql
SELECT * FROM user_constraints;
```

## Constraints of a Specific Table

```sql
SELECT *
FROM user_constraints
WHERE table_name = 'ASHOKIT_STUDENTS';
```

---

# Drop Existing Primary Key

```sql
ALTER TABLE ashokit_students
DROP PRIMARY KEY;
```

---

# Add Primary Key to Existing Table

```sql
ALTER TABLE ashokit_students
ADD PRIMARY KEY(student_id);
```

---

# Constraint Information Example

| Constraint Type | Description |
|---------------|-------------|
| Check | STUDENT_NAME IS NOT NULL |
| Check | CONTACT_NO IS NOT NULL |
| Check | Courses validation |
| Check | Course fee range validation |
| Unique | Contact number uniqueness |
| Primary Key | Student ID uniqueness + not null |

---

# Interview Questions

## Why is Primary Key Required?

Primary Key uniquely identifies each row in a table.

## Can a Table Have Multiple Primary Keys?

No. A table can have only one Primary Key.

## Can a Primary Key Contain NULL?

No.

## Can a Primary Key Contain Duplicate Values?

No.

## Difference Between UNIQUE and PRIMARY KEY

| UNIQUE | PRIMARY KEY |
|----------|-------------|
| Allows one NULL value | Does not allow NULL values |
| Prevents duplicates | Prevents duplicates |
| Multiple UNIQUE constraints allowed | Only one PRIMARY KEY allowed per table |

---

# Useful DBA Command

```sql
ALTER USER system
IDENTIFIED BY new_password;
```
