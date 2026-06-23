# SQL Notes - 23. Inner Join, Left Join & Right Join

## Sample Tables

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

# INNER JOIN (EQUI JOIN)

## Definition

- Uses `JOIN` or `INNER JOIN`.
- Returns only matching rows from both tables.
- Requires a common column.
- Unmatched records are ignored.

### Syntax

```sql
SELECT columns
FROM table1 t1
JOIN table2 t2
ON t1.column = t2.column;
```

### Example

```sql
SELECT ae.emp_id,
       ae.emp_name,
       ae.dept_id,
       ad.dept_id,
       ad.dept_name
FROM ashokit_emp ae
JOIN ashokit_dept ad
ON ae.dept_id = ad.dept_id
ORDER BY ae.emp_id;
```

### Output

| Emp ID | Emp Name | Dept Name |
|---------|----------|-----------|
| E1 | Anil | SALES |
| E2 | Avinash | IT |
| E3 | Raju | HR |
| E4 | Raghavendra | ADMIN |
| E5 | Abdul | MARKETING |
| E6 | Gupta | IT |
| E7 | Bhavya | SALES |

### Observation

- E8 and E9 are not displayed.
- Their departments (D11, D12) do not exist in Department table.

---

# LEFT JOIN (LEFT OUTER JOIN)

## Definition

Returns:

```text
Inner Join Result
+
All Remaining Rows From Left Table
```

### Process

1. Performs Inner Join.
2. Adds unmatched rows from Left Table.
3. Missing values from Right Table become NULL.

### Syntax

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON condition;
```

### Example

```sql
SELECT ae.emp_id,
       ae.emp_name,
       ae.dept_id,
       ad.dept_id,
       ad.dept_name
FROM ashokit_emp ae
LEFT JOIN ashokit_dept ad
ON ae.dept_id = ad.dept_id
ORDER BY ae.emp_id;
```

### Output

| Emp ID | Emp Name | Dept Name |
|---------|----------|-----------|
| E1 | Anil | SALES |
| E2 | Avinash | IT |
| E3 | Raju | HR |
| E4 | Raghavendra | ADMIN |
| E5 | Abdul | MARKETING |
| E6 | Gupta | IT |
| E7 | Bhavya | SALES |
| E8 | Sunil | NULL |
| E9 | Abhi | NULL |

### Observation

- All employees are displayed.
- E8 and E9 have invalid departments.
- Department columns become NULL.

### Important Point

```text
Left Join = Inner Join + Unmatched Rows From Left Table
```

Left table data is important.

---

# RIGHT JOIN (RIGHT OUTER JOIN)

## Definition

Returns:

```text
Inner Join Result
+
All Remaining Rows From Right Table
```

### Process

1. Performs Inner Join.
2. Adds unmatched rows from Right Table.
3. Missing values from Left Table become NULL.

### Syntax

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON condition;
```

### Example

```sql
SELECT ae.emp_id,
       ae.emp_name,
       ae.dept_id,
       ad.dept_id,
       ad.dept_name
FROM ashokit_emp ae
RIGHT JOIN ashokit_dept ad
ON ae.dept_id = ad.dept_id
ORDER BY ae.emp_id;
```

### Output

| Emp ID | Emp Name | Dept Name |
|---------|----------|-----------|
| E1 | Anil | SALES |
| E2 | Avinash | IT |
| E3 | Raju | HR |
| E4 | Raghavendra | ADMIN |
| E5 | Abdul | MARKETING |
| E6 | Gupta | IT |
| E7 | Bhavya | SALES |
| NULL | NULL | NON-ADMIN |
| NULL | NULL | FINANCE |

### Observation

Departments D3 and D5 have no employees.

Therefore:

```text
Employee Columns = NULL
Department Columns = Displayed
```

### Important Point

```text
Right Join = Inner Join + Unmatched Rows From Right Table
```

Right table data is important.

---

# Comparison

| Join Type | Returns |
|------------|----------|
| Inner Join | Only matching records |
| Left Join | Matching records + unmatched rows from Left table |
| Right Join | Matching records + unmatched rows from Right table |

### Memory Trick

```text
INNER JOIN
→ Common records only

LEFT JOIN
→ Keep everything from Left table

RIGHT JOIN
→ Keep everything from Right table
```

---

# Multi-Table Join Example

## Requirement

Display:

- Employee ID
- Employee Name
- Department Name
- Manager Name
- Project Name

### Query

```sql
SELECT ae.emp_id,
       ae.emp_name,
       ad.dept_name,
       am.manager_name,
       ap.project_name
FROM ashokit_emp ae
LEFT JOIN ashokit_dept ad
       ON ae.dept_id = ad.dept_id
LEFT JOIN ashokit_managers am
       ON am.manager_id = ae.manager_id
LEFT JOIN ashokit_projects ap
       ON ap.team_member_id = ae.emp_id
ORDER BY ap.project_name;
```

### Sample Output

| Employee | Department | Manager | Project |
|-----------|-----------|----------|----------|
| Gupta | IT | MAHESH | BANKING PROJECT |
| Raju | HR | SURESH | BANKING PROJECT |
| Anil | SALES | ASHOK | SPRING PROJECT |
| Avinash | IT | MAHESH | SPRING PROJECT |
| Abdul | MARKETING | RAJESH | WEBSITE PROJECT |
| Raghavendra | ADMIN | NARESH | NULL |
| Bhavya | SALES | ASHOK | NULL |
| Sunil | NULL | ASHOK | NULL |
| Abhi | NULL | MAHESH | NULL |

---

# Observations

### Employees Without Projects

```text
E4 - Raghavendra
E7 - Bhavya
E8 - Sunil
E9 - Abhi
```

Total:

```text
4 Employees
```

### Employees With Invalid Departments

```text
E8 - D11
E9 - D12
```

Department names become NULL because those departments do not exist.

---

# Interview Questions

### What is the difference between INNER JOIN and LEFT JOIN?

```text
INNER JOIN → Returns only matching rows.

LEFT JOIN → Returns matching rows +
            unmatched rows from Left table.
```

### What is the difference between LEFT JOIN and RIGHT JOIN?

```text
LEFT JOIN
→ Left table is important.

RIGHT JOIN
→ Right table is important.
```

### Which join is used most in projects?

```text
INNER JOIN
LEFT JOIN
```

Most real-world applications rarely use RIGHT JOIN because tables can simply be swapped and a LEFT JOIN used instead.
