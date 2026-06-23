# 01-Database-Fundamentals.md

## Data

### Definition

Data is information about a real-world object.

### Examples

- Student
- Employee
- Customer
- Mobile
- Laptop

### Student Data Example

| RollNo | Name | Branch | Gender | Age |
|---------|--------|---------|---------|-----|
| 1121 | Mahesh | CSE | Male | 28 |

**Key Point**

```text
Information about one student = Data
```

---

## Database

### Definition

A database is a collection of related data stored in a structured format.

### Example

| RollNo | Name | Branch |
|---------|---------|---------|
| 1121 | Mahesh | CSE |
| 2255 | Suresh | IT |
| 8989 | Rajesh | ECE |

**Key Point**

```text
One Student Information  -> Data
Many Student Records     -> Database
```

---

## Database Management System (DBMS)

### Definition

A DBMS is software used to store, retrieve, update, delete, and manage data efficiently.

### Responsibilities

- Store data
- Retrieve data
- Update data
- Delete data
- Secure data
- Maintain consistency

### Real-World Flow

```text
User
 ↓
Application
 ↓
Server
 ↓
Database
```

### Example Applications

- Amazon
- Flipkart
- Naukri
- Banking Systems
- College Management Systems

---

## Evolution of Data Storage

### 1. Traditional Approach (Books / Ledgers)

```text
Book
 ↓
Pages
 ↓
Student Information
```

#### Problems

1. Security issues
2. Backup problems
3. Space consumption
4. Costly maintenance
5. Slow data retrieval

---

### 2. File System Approach

Data was stored inside files.

Examples:

```text
Students.txt
Employees.txt
Customers.txt
```

#### Problems

### Security Challenges

Files can be copied, modified, or deleted easily.

### Data Redundancy

#### Definition

Duplicate storage of the same data.

#### Example

**Students.txt**

| StudentId | StudentName |
|------------|--------------|
| 101 | Mahesh |

**StudentBranch.txt**

| StudentId | Branch |
|------------|---------|
| 101 | CSE |

StudentId is stored multiple times.

---

### Data Inconsistency

#### Definition

The same data exists in multiple places but contains different values.

#### Example

**Students.txt**

```text
StudentId = 101
```

**StudentBranch.txt**

```text
StudentId = 201
```

Both files now contain conflicting information.

---

### Slow Retrieval

Searching through large files is time-consuming.

---

### Backup Difficulties

Backup management must be handled manually.

---

### Limited Storage

Files are not suitable for large-scale applications.

---

## Database Software

Database software was introduced to overcome the limitations of file systems.

### Advantages

### Strong Security

Supports:

- Username
- Password
- Roles
- Permissions

---

### Efficient Storage and Retrieval

Data can be inserted, updated, deleted, and searched quickly.

---

### Large Storage Capacity

Can store:

- Millions of records
- Massive datasets

---

### Structured Storage

Data is stored in tables.

---

## Table Structure

### Table

Represents a real-world entity.

Examples:

```text
Student
Employee
Customer
```

---

### Column (Field)

Represents an attribute of an entity.

Examples:

```text
RollNo
Name
Branch
Gender
```

---

### Row (Record)

Represents actual data values.

Example:

```text
101 | Mahesh | CSE | Male
```

---

## No Data Redundancy

Database normalization reduces duplicate data storage.

---

## Data Integrity

Ensures data remains:

- Accurate
- Consistent
- Valid

### Example

Invalid values such as:

```text
Age = -5
Age = 500
```

can be prevented using constraints.

---

## Associations (Relationships)

Databases can establish relationships between tables.

### Example

```text
Department
     ↑
     |
  Student
```

One department can have many students.

---

## Database Terminology

| Term | Meaning |
|--------|---------|
| Data | Information |
| Database | Collection of related data |
| DBMS | Software that manages data |
| Table | Entity |
| Column | Field / Attribute |
| Row | Record |

---

## Popular Database Softwares

| Database | Organization |
|-----------|-------------|
| Oracle Database | Oracle Corporation |
| MySQL | Oracle Corporation |
| DB2 | IBM |
| SQL Server | Microsoft |
| Derby | Sun Microsystems |
| PostgreSQL | PostgreSQL Community |

---

## RDBMS

### Full Form

```text
Relational Database Management System
```

### Characteristics

- Data stored in tables
- Rows and columns
- Relationships between tables
- SQL support
- Reduced redundancy
- Better consistency

### Examples

- Oracle Database
- MySQL
- SQL Server
- PostgreSQL
- DB2

---

## Types of Database Software

### 1. RDBMS

#### Features

- Table-based storage
- Relationships between tables
- Uses SQL
- Structured schema

#### Examples

- Oracle
- MySQL
- SQL Server
- PostgreSQL

---

### 2. NRDBMS (Non-Relational DBMS)

#### Features

- Flexible schema
- No mandatory table relationships
- Suitable for large-scale distributed systems

#### Examples

- MongoDB
- Cassandra
- Redis
- CouchDB

---

## Interview Questions

### What is Data?

Information about a real-world object.

---

### What is a Database?

A collection of related data stored in a structured format.

---

### What is DBMS?

Software used to store, manage, retrieve, update, and delete data.

---

### What is Data Redundancy?

Duplicate storage of the same data.

---

### What is Data Inconsistency?

A situation where duplicate data contains different values in different locations.

---

### Difference Between Data and Database

| Data | Database |
|--------|-----------|
| Single information | Collection of information |
| One student record | All student records |

---

### Advantages of Database Over File System

- Better security
- Reduced redundancy
- Improved consistency
- Backup support
- Faster retrieval
- Large storage capacity
- Relationship management

---

## Quick Revision

```text
Data           -> Information

Database       -> Collection of Data

DBMS           -> Manages Data

Table          -> Entity

Column         -> Attribute

Row            -> Record

Data Redundancy -> Duplicate Data

Data Inconsistency -> Conflicting Duplicate Data

RDBMS          -> Relational Database System

Oracle         -> RDBMS

MySQL          -> RDBMS

SQL Server     -> RDBMS

PostgreSQL     -> RDBMS
```
