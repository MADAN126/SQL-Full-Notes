# 02-Introduction-To-Oracle-And-SQL.md

## Recap

### Purpose of a Database

A database stores application data.

```text
Application
     ↓
Database
```

Examples:

- Internet Banking
- E-Commerce Applications
- Hospital Management Systems
- College Management Systems

All user activities generate data that is stored in a database.

---

# Types of Database Softwares

## 1. SQL Databases (RDBMS)

### Definition

RDBMS stands for **Relational Database Management System**.

### Examples

- Oracle Database
- MySQL
- SQL Server
- PostgreSQL
- DB2
- Derby

### Characteristics

#### Data Stored in Tables

```text
Student
+-------+--------+--------+
| Id    | Name   | Branch |
+-------+--------+--------+
| 101   | Mahesh | CSE    |
+-------+--------+--------+
```

---

#### Two-Dimensional Storage

Data is organized using:

```text
Rows
Columns
```

---

#### Database Terminology

| Term | Meaning |
|--------|---------|
| Table | Relation |
| Column | Field / Attribute |
| Row | Tuple / Record |

---

#### Structured Data

Every row follows the same structure.

Example:

```text
Student_Id
Student_Name
Branch
```

Every student record follows these columns.

---

#### Real-Time Usage

Commonly used in:

- Banking Applications
- E-Commerce Systems
- ERP Systems
- Finance Systems

---

## 2. NoSQL Databases (NRDBMS)

### Definition

NoSQL databases store data in non-relational formats.

### Examples

- MongoDB
- Cassandra
- Redis
- HBase
- DynamoDB

---

### Storage Formats

#### Document Databases

```json
{
  "id":101,
  "name":"Mahesh",
  "branch":"CSE"
}
```

---

#### Key-Value Databases

```text
101 -> Mahesh
```

---

#### Column Databases

Store data column-wise.

---

#### Graph Databases

Store nodes and relationships.

---

### Characteristics

- Flexible Schema
- Semi-Structured Data
- Unstructured Data
- High Scalability

---

# SQL

## Full Form

```text
Structured Query Language
```

---

## Definition

SQL is used to communicate with relational databases.

SQL allows users to:

- Insert Data
- Retrieve Data
- Update Data
- Delete Data
- Manage Database Objects

---

# Why SQL?

Without SQL:

```text
Data Exists
      ↓
Cannot Access Efficiently
```

With SQL:

```text
Data Exists
      ↓
SQL Query
      ↓
Required Result
```

---

# SQL Characteristics

## SQL is a Query Language

Used to retrieve information from databases.

Example:

```sql
SELECT * FROM customers;
```

---

## SQL is a Database Programming Language

Used to perform operations on data.

---

## SQL Statements are Human Readable

Example:

```sql
SELECT * FROM customers;
```

Easy to understand.

---

## SQL is Case Insensitive

All are valid:

```sql
SELECT * FROM customers;
```

```sql
select * from customers;
```

```sql
SeLeCt * FrOm customers;
```

### Best Practice

```sql
SELECT * FROM customers;
```

Use uppercase for SQL keywords.

---

## SQL is ANSI Standard

### ANSI

```text
American National Standards Institute
```

ANSI standardization makes SQL common across databases.

Examples:

- Oracle
- MySQL
- SQL Server
- PostgreSQL

---

## Every SQL Statement Ends With Semicolon

Correct:

```sql
SELECT * FROM customers;
```

Wrong:

```sql
SELECT * FROM customers
```

---

## SQL Executes One Statement at a Time

Example:

```sql
SELECT * FROM customers;
```

Only one statement executes at a time.

---

## Multiple Statements Require PL/SQL

SQL handles individual statements.

PL/SQL handles program logic and multiple statements.

---

# Customer Table Example

## Customers

| Customer_Id | Customer_Name | Customer_Location |
|------------|--------------|------------------|
| 1025 | Mahesh | Hyderabad |
| 1026 | Suresh | Delhi |
| 1027 | Rajesh | Bangalore |
| 1028 | Nagesh | Chennai |
| 1029 | Naresh | Pondicherry |

---

# Query Examples

## Retrieve Customers From Hyderabad

```sql
SELECT *
FROM customers
WHERE customer_location = 'Hyderabad';
```

### Output

| Customer_Id | Customer_Name | Customer_Location |
|------------|--------------|------------------|
| 1025 | Mahesh | Hyderabad |

---

## Retrieve All Customers

```sql
SELECT *
FROM customers;
```

### Output

Returns all rows.

---

## Retrieve Customer ID By Name

```sql
SELECT customer_id
FROM customers
WHERE customer_name = 'Mahesh';
```

### Output

| Customer_Id |
|------------|
| 1025 |

---

# Understanding SQL Query Structure

## SELECT

Used to retrieve data.

```sql
SELECT customer_name
FROM customers;
```

---

## FROM

Specifies the table.

```sql
FROM customers
```

---

## WHERE

Filters records.

```sql
WHERE customer_location='Hyderabad'
```

---

# PL/SQL

## Full Form

```text
Procedural Language / SQL
```

Oracle's extension of SQL.

---

## Why PL/SQL?

SQL Limitations:

- No Variables
- No Loops
- No Conditions
- Executes One Statement

PL/SQL Adds:

- Variables
- Conditions
- Loops
- Procedures
- Functions
- Multiple SQL Statements

---

## Simple Comparison

| SQL | PL/SQL |
|------|---------|
| Query Language | Procedural Language |
| One Statement | Multiple Statements |
| No Loops | Supports Loops |
| No Variables | Supports Variables |
| Data Manipulation | Business Logic |

---

# Oracle Database

## About Oracle

Oracle Database is an enterprise-level relational database software.

### Developed By

Oracle Corporation

---

## Features

- High Security
- High Performance
- Reliability
- Scalability
- Large Data Handling

---

## Oracle Express Edition (XE)

### Full Form

```text
Oracle Express Edition
```

### Purpose

Free lightweight Oracle database for:

- Learning
- Development
- Practice

---

## Oracle Learning Flow

```text
Database Concepts
        ↓
RDBMS Concepts
        ↓
SQL
        ↓
Oracle Installation
        ↓
Connecting To Oracle
        ↓
Tables
        ↓
Queries
        ↓
Functions
        ↓
Joins
        ↓
Subqueries
        ↓
PL/SQL
```

---

# Interview Questions

## What is SQL?

Structured Query Language used to communicate with relational databases.

---

## Why is SQL Called a Query Language?

Because it is used to query and manipulate database data.

---

## Is SQL Case Sensitive?

No.

```sql
SELECT
select
SeLeCt
```

All are valid.

---

## What is ANSI?

```text
American National Standards Institute
```

Provides SQL standards.

---

## What is PL/SQL?

Oracle's procedural extension to SQL that supports programming constructs such as variables, loops, conditions, procedures, and functions.

---

## Difference Between SQL and NoSQL

| SQL | NoSQL |
|------|--------|
| Table Based | Non-Table Based |
| Structured Data | Flexible Data |
| Fixed Schema | Dynamic Schema |
| Uses SQL | Different Query Models |
| Oracle, MySQL | MongoDB, Redis |

---

# Quick Revision

```text
RDBMS  -> Relational Database Management System

SQL    -> Structured Query Language

Table  -> Relation

Column -> Field / Attribute

Row    -> Tuple / Record

SQL    -> Query Language

ANSI   -> American National Standards Institute

PL/SQL -> Procedural Language / SQL

Oracle -> RDBMS

MySQL  -> RDBMS

MongoDB -> NoSQL

Redis  -> NoSQL
```
