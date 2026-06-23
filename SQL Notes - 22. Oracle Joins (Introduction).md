# SQL Notes - 22. Oracle Joins (Introduction)

## Why Joins?

- Joins are used to retrieve data from multiple tables.
- Tables must have a common column.
- Usually:
  - Parent Table → Primary Key
  - Child Table → Foreign Key
- Join condition connects related rows.

### Example

```sql
SELECT *
FROM emp e, dept d
WHERE e.deptno = d.deptno;
```

Join Condition:

```sql
e.deptno = d.deptno
```

---

## Types of Joins

1. Inner Join
2. Left Join
3. Right Join
4. Full Outer Join
5. Cross Join
6. Self Join
7. Natural Join

---

## Office Database Used for Join Examples

### Department Table

| Dept ID | Dept Name |
|----------|-----------|
| D1 | IT |
| D2 | HR |
| D3 | FINANCE |
| D4 | ADMIN |
| D5 | NON-ADMIN |
| D6 | MARKETING |
| D7 | SALES |

---

### Managers Table

| Manager ID | Manager Name | Dept ID |
|------------|-------------|---------|
| M1 | ASHOK | D4 |
| M2 | MAHESH | D1 |
| M3 | SURESH | D2 |
| M4 | RAMESH | D2 |
| M5 | RAJESH | D6 |
| M6 | NARESH | D7 |
| M7 | YAGNESH | D5 |
| M8 | GANESH | D1 |
| M9 | RAGHU | D1 |
| M10 | CHANTI | D4 |

---

### Employee Table

| Emp ID | Emp Name | Salary | Dept ID | Manager ID |
|---------|----------|---------|---------|------------|
| E1 | Anil | 18000 | D7 | M1 |
| E2 | Avinash | 28000 | D1 | M2 |
| E3 | Raju | 38000 | D2 | M3 |
| E4 | Raghavendra | 48000 | D4 | M6 |
| E5 | Abdul | 58000 | D6 | M5 |
| E6 | Gupta | 68000 | D1 | M2 |
| E7 | Bhavya | 78000 | D7 | M1 |
| E8 | Sunil | 88000 | D11 | M1 |
| E9 | Abhi | 98000 | D12 | M2 |

---

### Projects Table

| Project ID | Project Name | Team Member |
|------------|-------------|-------------|
| P1 | SPRING PROJECT | E1 |
| P1 | SPRING PROJECT | E2 |
| P1 | SPRING PROJECT | M1 |
| P2 | BANKING PROJECT | E3 |
| P2 | BANKING PROJECT | E6 |
| P2 | BANKING PROJECT | M2 |
| P3 | WEBSITE PROJECT | M3 |
| P3 | WEBSITE PROJECT | E5 |

---

# INNER JOIN (EQUI JOIN)

## Definition

- Returns only matching rows from both tables.
- Rows without matching values are ignored.
- Common column is mandatory.

---

## Method 1: Using WHERE Clause

### Syntax

```sql
SELECT column_list
FROM table1, table2
WHERE table1.column = table2.column;
```

### Example

```sql
SELECT e.empno, e.ename, d.dname
FROM emp e, dept d
WHERE e.deptno = d.deptno;
```

---

## Method 2: Using ON Clause (Recommended)

### Syntax

```sql
SELECT column_list
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### Example

```sql
SELECT e.empno, e.ename, d.dname
FROM emp e
JOIN dept d
ON e.deptno = d.deptno;
```

---

## Why ON Clause is Preferred?

- Better readability.
- Easier to maintain.
- Separates:
  - Join conditions → `ON`
  - Filtering conditions → `WHERE`
- Most commonly used in real-world projects.

---

## Key Interview Points

### Physical Join

Relationship created using:

```text
Primary Key ↔ Foreign Key
```

Example:

```text
dept.deptno  → Primary Key
emp.deptno   → Foreign Key
```

---

### Logical Join

Data retrieval using SQL JOIN statements.

Example:

```sql
SELECT *
FROM emp e
JOIN dept d
ON e.deptno = d.deptno;
```

---

## Important Notes

- No common column → No join possible.
- Inner Join returns only matched records.
- Unmatched rows are discarded.
- ON clause is preferred over WHERE clause for join conditions.
- Most frequently used join in projects is INNER JOIN.
