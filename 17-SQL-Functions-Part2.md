# 17-SQL-Functions-Part2.md

# SQL Functions - Part 2

## Single Row Functions

Single Row Functions work on each row individually and return one result per row.

This session covers:

1. String Functions (Advanced)
2. Math Functions
3. Date Functions
4. Conversion Functions

---

# String Functions

---

## 14. REPLACE()

Replaces a string or substring with another string.

### Syntax

```sql
REPLACE(string, search_string, replace_string)
```

### Examples

```sql
SELECT REPLACE('This is a test','is','IS')
FROM dual;
```

Output:

```text
ThIS IS a test
```

---

```sql
SELECT REPLACE('Welcome To Hyd',
               'Hyd',
               'Hyderabad')
FROM dual;
```

Output:

```text
Welcome To Hyderabad
```

---

### REPLACE vs TRANSLATE

#### TRANSLATE

Works character by character.

```sql
SELECT TRANSLATE('JACK',
                 'J',
                 'B')
FROM dual;
```

Output:

```text
BACK
```

---

#### REPLACE

Works with complete words or substrings.

```sql
SELECT REPLACE('Welcome To Hyd',
               'Hyd',
               'Hyderabad')
FROM dual;
```

Output:

```text
Welcome To Hyderabad
```

---

## 15. INSTR()

Searches for a substring and returns its position.

### Syntax

```sql
INSTR(string, substring)
```

---

### Example 1

```sql
SELECT INSTR('This is a playlist',
             'is')
FROM dual;
```

Output:

```text
3
```

---

### Example 2

Find Second Occurrence

```sql
SELECT INSTR('This is a playlist',
             'is',
             1,
             2)
FROM dual;
```

Output:

```text
6
```

---

### Example 3

Find Third Occurrence

```sql
SELECT INSTR('This is a playlist',
             'is',
             1,
             3)
FROM dual;
```

Output:

```text
16
```

---

### Example 4

Substring Not Found

```sql
SELECT INSTR('This is a playlist',
             'are')
FROM dual;
```

Output:

```text
0
```

---

# Math Functions

---

## 1. ABS()

Converts negative values into positive values.

### Syntax

```sql
ABS(number)
```

### Example

```sql
SELECT ABS(-19)
FROM dual;
```

Output:

```text
19
```

---

## 2. ROUND()

Rounds to the nearest integer.

### Syntax

```sql
ROUND(number)
```

### Examples

```sql
SELECT ROUND(9.5)
FROM dual;
```

Output:

```text
10
```

---

```sql
SELECT ROUND(9.4)
FROM dual;
```

Output:

```text
9
```

---

## 3. FLOOR()

Returns the smallest integer less than or equal to the number.

### Syntax

```sql
FLOOR(number)
```

### Examples

```sql
SELECT FLOOR(9.5)
FROM dual;
```

Output:

```text
9
```

---

```sql
SELECT FLOOR(9.9)
FROM dual;
```

Output:

```text
9
```

---

## 4. CEIL()

Returns the largest integer greater than or equal to the number.

### Syntax

```sql
CEIL(number)
```

### Examples

```sql
SELECT CEIL(9.1)
FROM dual;
```

Output:

```text
10
```

---

```sql
SELECT CEIL(9.95)
FROM dual;
```

Output:

```text
10
```

---

## Difference Between ROUND, FLOOR and CEIL

| Function | 9.1 | 9.5 | 9.9 |
|-----------|------|------|------|
| ROUND() | 9 | 10 | 10 |
| FLOOR() | 9 | 9 | 9 |
| CEIL() | 10 | 10 | 10 |

---

## 5. GREATEST()

Returns the largest value.

### Example

```sql
SELECT GREATEST(5,7,3,2,6,1)
FROM dual;
```

Output:

```text
7
```

---

```sql
SELECT GREATEST(10.25,
                25.68,
                89.47,
                25.14)
FROM dual;
```

Output:

```text
89.47
```

---

## 6. LEAST()

Returns the smallest value.

### Example

```sql
SELECT LEAST(5,7,3,2,6,1)
FROM dual;
```

Output:

```text
1
```

---

```sql
SELECT LEAST(10.25,
             25.68,
             89.47,
             25.14)
FROM dual;
```

Output:

```text
10.25
```

---

## 7. MOD()

Returns the remainder.

### Syntax

```sql
MOD(dividend, divisor)
```

### Examples

```sql
SELECT MOD(10,2)
FROM dual;
```

Output:

```text
0
```

---

```sql
SELECT MOD(16,5)
FROM dual;
```

Output:

```text
1
```

---

## 8. SQRT()

Returns square root.

### Example

```sql
SELECT SQRT(100)
FROM dual;
```

Output:

```text
10
```

---

## 9. POWER()

Returns exponent value.

### Example

```sql
SELECT POWER(5,3)
FROM dual;
```

Output:

```text
125
```

Because:

```text
5 × 5 × 5 = 125
```

---

## 10. LOG()

Returns logarithmic value.

### Example

```sql
SELECT LOG(10,10)
FROM dual;
```

Output:

```text
1
```

---

## 11. SIGN()

Returns the sign of a number.

| Input | Output |
|---------|---------|
| Positive | 1 |
| Zero | 0 |
| Negative | -1 |

### Examples

```sql
SELECT SIGN(50)
FROM dual;
```

Output:

```text
1
```

---

```sql
SELECT SIGN(-50)
FROM dual;
```

Output:

```text
-1
```

---

## 12. SIN()

Returns sine value.

```sql
SELECT SIN(0)
FROM dual;
```

Output:

```text
0
```

---

## 13. COS()

Returns cosine value.

```sql
SELECT COS(0)
FROM dual;
```

Output:

```text
1
```

---

## 14. TAN()

Returns tangent value.

```sql
SELECT TAN(0)
FROM dual;
```

Output:

```text
0
```

---

# Date Functions

Date Functions are heavily used in Banking, Finance, Insurance and Reporting applications.

---

## 1. ADD_MONTHS()

Adds months to a date.

### Syntax

```sql
ADD_MONTHS(date, number_of_months)
```

### Example

```sql
SELECT SYSDATE
FROM dual;
```

---

```sql
SELECT ADD_MONTHS(SYSDATE,12)
FROM dual;
```

Adds 1 year.

---

## 2. MONTHS_BETWEEN()

Returns number of months between two dates.

### Example

```sql
SELECT MONTHS_BETWEEN(
       SYSDATE,
       '22-DEC-2023')
FROM dual;
```

---

## 3. LAST_DAY()

Returns the last day of a month.

### Example

```sql
SELECT LAST_DAY(SYSDATE)
FROM dual;
```

Output Example:

```text
31-DEC-2022
```

---

## 4. NEXT_DAY()

Returns the next specified weekday.

### Example

```sql
SELECT NEXT_DAY(
       SYSDATE,
       'SUNDAY')
FROM dual;
```

---

## 5. EXTRACT()

Extracts specific parts from a date.

---

### Extract Year

```sql
SELECT EXTRACT(YEAR FROM SYSDATE)
FROM dual;
```

---

### Extract Month

```sql
SELECT EXTRACT(MONTH FROM SYSDATE)
FROM dual;
```

---

### Extract Day

```sql
SELECT EXTRACT(DAY FROM SYSDATE)
FROM dual;
```

---

# Banking Domain Example

Historical Data:

```text
01-Jan-2022 → 31-Dec-2022
```

Current Year Data:

```text
01-Jan-2023 → 31-Dec-2023
```

Banks often perform a Roll Forward process to move from one financial year to another.

---

# Conversion Functions

Used to convert one datatype into another.

---

## TO_CHAR()

Converts Date or Number into Character format.

### Syntax

```sql
TO_CHAR(date,'FORMAT')
```

---

## Convert Date to DD/MM/YYYY

```sql
SELECT TO_CHAR(
       SYSDATE,
       'DD/MM/YYYY')
FROM dual;
```

Output:

```text
22/12/2022
```

---

## Convert Date to DD-MON-YYYY

```sql
SELECT TO_CHAR(
       SYSDATE,
       'DD-MON-YYYY')
FROM dual;
```

Output:

```text
22-DEC-2022
```

---

## Display Day Name

```sql
SELECT TO_CHAR(
       SYSDATE,
       'DAY')
FROM dual;
```

Output:

```text
THURSDAY
```

---

## Display Month Name

```sql
SELECT TO_CHAR(
       SYSDATE,
       'MONTH')
FROM dual;
```

Output:

```text
DECEMBER
```

---

## Display Full Date & Time

```sql
SELECT TO_CHAR(
       SYSDATE,
       'DD-MON-YYYY HH:MI:SS')
FROM dual;
```

Output:

```text
22-DEC-2022 10:30:15
```

---

## Display Only Year

```sql
SELECT TO_CHAR(
       SYSDATE,
       'YYYY')
FROM dual;
```

Output:

```text
2022
```

---

# Interview Questions

## Difference Between ROUND(), FLOOR() and CEIL()

```text
ROUND() → Nearest integer
FLOOR() → Lowest integer
CEIL()  → Highest integer
```

---

## Difference Between TRANSLATE() and REPLACE()

```text
TRANSLATE() → Character replacement
REPLACE()   → String replacement
```

Example:

```sql
TRANSLATE('JACK','J','B')
```

Output:

```text
BACK
```

---

```sql
REPLACE('Welcome To Hyd',
        'Hyd',
        'Hyderabad')
```

Output:

```text
Welcome To Hyderabad
```

---

# Quick Revision

| Function | Purpose |
|-----------|----------|
| REPLACE() | Replace substring |
| INSTR() | Find position of substring |
| ABS() | Convert negative to positive |
| ROUND() | Nearest integer |
| FLOOR() | Lowest integer |
| CEIL() | Highest integer |
| GREATEST() | Maximum value |
| LEAST() | Minimum value |
| MOD() | Remainder |
| SQRT() | Square root |
| POWER() | Exponent |
| LOG() | Logarithm |
| SIGN() | Returns sign |
| SIN() | Sine value |
| COS() | Cosine value |
| TAN() | Tangent value |
| ADD_MONTHS() | Add months |
| MONTHS_BETWEEN() | Month difference |
| LAST_DAY() | Last day of month |
| NEXT_DAY() | Next weekday |
| EXTRACT() | Extract year/month/day |
| TO_CHAR() | Convert date/number to string |

# Key Takeaways

- REPLACE works with strings; TRANSLATE works with characters.
- INSTR returns substring position.
- ROUND, FLOOR and CEIL are common interview questions.
- Date functions are heavily used in reporting systems.
- TO_CHAR is one of the most frequently used Oracle functions.
- Conversion functions help transform data into required formats.
