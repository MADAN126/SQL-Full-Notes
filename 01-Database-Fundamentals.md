# Database Fundamentals - Ultra Sharp Notes

## Session Overview

- Course Duration: **1 Month ± 10 Days**
- Prerequisite: **None**
- Timings: **9 PM – 10 PM**

---

# Data

## Definition

Data = Information about a real-world object.

### Examples

- Student
- Employee
- Customer
- Mobile
- Laptop
- Chair

### Student Data Example

| RollNo | Name | Branch | Gender | Age |
|---------|--------|---------|---------|-----|
| 1121 | Mahesh | CSE | Male | 28 |

### Important

A single student's details = **Data**

---

# Database

## Definition

A Database is a collection of related data stored in a structured format.

### Example

| RollNo | Name | Branch |
|---------|---------|---------|
| 1121 | Mahesh | CSE |
| 2255 | Suresh | IT |
| 8989 | Rajesh | ECE |

### Remember

```text
One Student Details  -> Data

Many Student Details -> Database
```

---

# DBMS (Database Management System)

## Definition

A software/technique used to:

- Store Data
- Retrieve Data
- Manage Data
- Update Data
- Delete Data

### Examples

Applications such as:

- Amazon
- Flipkart
- Naukri
- Monster
- College Portals
- Banking Systems

store their information inside databases.

---

# Real World Flow

```text
User
 ↓
Application
 ↓
Server
 ↓
Database
```

### Example

```text
Student Login
      ↓
College Application
      ↓
Server
      ↓
Database
```

Database stores all information permanently.

---

# Evolution of Data Storage

## 1. Traditional Approach (Books / Ledger Books)

### Structure

```text
Book
 ↓
Pages
 ↓
Student Information
```

### Problems

#### 1. Security Issues

Anyone can access or damage data.

#### 2. Backup Problems

If a book is lost, data is lost.

#### 3. Space Problems

Requires physical storage.

#### 4. Costly

Printing and maintaining books costs money.

#### 5. Slow Retrieval

Finding one student among thousands takes time.

---

## 2. File System Approach

After computers were introduced, data was stored in files.

### Examples

```text
Students.txt
Employees.txt
Customers.txt
```

---

# Problems with File System

## 1. Security Challenges

Files can be copied or deleted easily.

---

## 2. Data Redundancy

### Definition

Duplicate storage of the same data.

### Example

#### Students.txt

| StudentId | StudentName |
|------------|--------------|
| 101 | Mahesh |

#### StudentBranch.txt

| StudentId | Branch |
|------------|---------|
| 101 | CSE |

StudentId appears multiple times.

### Interview Definition

```text
Data Redundancy = Duplicate or repetitive storage of data.
```

---

## 3. Data Inconsistency

### Definition

Same data exists in multiple places but values differ.

### Example

#### Students.txt

```text
StudentId = 101
```

#### StudentBranch.txt

```text
StudentId = 201
```

Now both files contain different values.

### Interview Definition

```text
Data Inconsistency occurs when duplicate data is not updated everywhere.
```

---

## 4. Slow Retrieval

Searching data from large files takes time.

---

## 5. Backup Problems

Managing backups manually is difficult.

---

## 6. Limited Storage

Files are not suitable for very large-scale applications.

---

# Database Software

## Why Databases Were Introduced

To solve:

- Security Problems
- Redundancy Problems
- Consistency Problems
- Backup Problems
- Performance Problems

---

# Advantages of Database Software

## 1. Strong Security

Uses:

- Username
- Password
- Roles
- Permissions

---

## 2. Easy Data Storage & Retrieval

Fast insertion, update, deletion, and searching.

---

## 3. Huge Data Storage

Can store:

- Millions of rows
- Terabytes of data

---

## 4. Structured Data Storage

Data is stored inside tables.

### Table Components

#### Table

Represents a real-world entity.

Example:

```text
Student
Employee
Customer
```

---

#### Columns (Fields)

Represent attributes.

Example:

```text
RollNo
Name
Branch
Gender
```

---

#### Rows (Records)

Represent actual values.

Example:

```text
101 | Mahesh | CSE | Male
```

---

## 5. No Data Redundancy

Avoids duplicate storage.

---

## 6. Data Integrity

Ensures data remains:

- Correct
- Valid
- Consistent

### Example

Age cannot be:

```text
-5
500
```

Database constraints prevent invalid values.

---

## 7. Associations

Relationships can be created between tables.

### Example

```text
Student
   ↓
Department
```

One department can have many students.

---

# Database Terminology

| Term | Meaning |
|--------|---------|
| Table | Real-world entity |
| Column | Attribute/Field |
| Row | Record |
| Database | Collection of tables |
| DBMS | Software that manages databases |

---

# Popular Database Softwares

| Database | Company |
|-----------|-----------|
| Oracle Database | Oracle Corporation |
| MySQL | Oracle Corporation |
| DB2 | IBM |
| SQL Server | Microsoft |
| Derby | Sun Microsystems |
| PostgreSQL | PostgreSQL Community |

---

# RDBMS

## Full Form

```text
Relational Database Management System
```

### Examples

- Oracle
- MySQL
- SQL Server
- PostgreSQL
- DB2

---

# Types of Database Software

## 1. RDBMS

### Characteristics

- Data stored in tables
- Rows and columns
- Relationships between tables
- Uses SQL

### Examples

- Oracle
- MySQL
- SQL Server
- PostgreSQL

---

## 2. NRDBMS (Non-Relational DBMS)

### Characteristics

- No table relationships
- Flexible structure
- Designed for massive-scale data

### Examples

- MongoDB
- Cassandra
- Redis
- CouchDB

---

# Interview Questions

## What is Data?

Information about a real-world object.

---

## What is Database?

A collection of related data stored in structured format.

---

## What is DBMS?

Software used to store, manage, retrieve, update, and delete data.

---

## What is Data Redundancy?

Duplicate storage of data.

---

## What is Data Inconsistency?

Mismatch of duplicate data across multiple locations.

---

## Difference Between Data and Database

| Data | Database |
|--------|-----------|
| Single information | Collection of information |
| Example: One Student | Example: All Students |

---

## What are the Advantages of Databases over Files?

- Better Security
- Less Redundancy
- Data Integrity
- Backup Support
- Faster Retrieval
- Huge Storage Capacity
- Relationships Between Data

---

# One-Line Revision

```text
Data → Information

Database → Collection of Data

DBMS → Manages Data

Table → Entity

Column → Attribute

Row → Record

Data Redundancy → Duplicate Data

Data Inconsistency → Mismatched Duplicate Data

RDBMS → Relational Database System using Tables

Oracle/MySQL/PostgreSQL/SQL Server → RDBMS
```
