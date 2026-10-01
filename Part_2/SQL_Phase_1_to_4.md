```
|id |  name  |age | department |    city   | cgpa |
|--:|--------|---:|------------|-----------|-----:|
| 1 | Rahul  | 20 | IT         | Mangalore | 8.50 |
| 2 | Ananya | 21 | CSE        | Bangalore | 9.10 |
| 3 | Amit   | 20 | ECE        | Mysore    | 7.80 |
| 4 | Priya  | 22 | IT         | Bangalore | 8.90 |
| 5 | Rohan  | 21 | CSE        | Mangalore | 8.20 |
| 6 | Sneha  | 20 | EEE        | Mysore    | 9.30 |
| 7 | Arjun  | 23 | IT         | Udupi     | 7.50 |
| 8 | Neha   | 21 | CSE        | Bangalore | 8.70 |
| 9 | Kiran  | 22 | ECE        | Mangalore | 8.10 |
|10 | Pooja  | 20 | IT         | Udupi     | 9.00 |
```

# PHASE 1 — FOUNDATIONS

# 1. DATABASE CONCEPTS

-> A database is an organized collection of data that can be stored, managed, searched, and updated efficiently.

```text
Database
│
├── Tables
│   ├── students
│   ├── courses
│   └── departments
│
└── Other database objects
```

### DBMS

-> A Database Management System (DBMS) is software used to create, store, organize, retrieve, update, and manage data.

Examples:

```text
PostgreSQL
MySQL
```

Both PostgreSQL and MySQL are Relational Database Management Systems (RDBMS).

### RDBMS

-> An RDBMS stores data primarily in tables and allows relationships between tables.

Think:

```text
Database
    ↓
Tables
    ↓
Rows + Columns
    ↓
Relationships
```

---

# 2. TABLES

-> A table stores related data in rows and columns.

Example:

```text
students

| id | name   | age | department | city      | cgpa |
|---:|--------|----:|------------|-----------|-----:|
| 1  | Rahul  | 20  | IT         | Mangalore | 8.50 |
| 2  | Ananya | 21  | CSE        | Bangalore | 9.10 |
| 3  | Amit   | 20  | ECE        | Mysore    | 7.80 |
```

Think of a table like a spreadsheet, but with database rules and capabilities.

---

# 3. ROWS / COLUMNS

## Row

-> A row represents one record.

Example:

```text
| 1 | Rahul | 20 | IT | Mangalore | 8.50 |
```

This represents one student.

## Column

-> A column represents one attribute/property of the data.

```text
id
name
age
department
city
cgpa
```

### Mental model

```text
Table
│
├── Columns → what information is stored
│
└── Rows    → individual records
```

---

# 4. DATA TYPES

-> A data type defines what kind of value a column can store.

Common SQL data types:

```text
INT
VARCHAR
DECIMAL
DATE
BOOLEAN
```

Example:

```
CREATE TABLE students (
    id INT,
    name VARCHAR(100),
    age INT,
    department VARCHAR(50),
    city VARCHAR(50),
    cgpa DECIMAL(3,2)
);
```

### Common data types

| Data Type | Purpose | Example |
|---|---|---|
| INT | Whole numbers | `20` |
| VARCHAR(n) | Variable-length text | `'Rahul'` |
| DECIMAL(p,s) | Exact decimal values | `8.50` |
| DATE | Calendar date | `'2026-10-01'` |
| BOOLEAN | True/False | `TRUE` |

---

# 5. PRIMARY KEY

-> A primary key uniquely identifies each row in a table.

Example:

```
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    department VARCHAR(50),
    city VARCHAR(50),
    cgpa DECIMAL(3,2)
);
```

Here:

```text
id
↓
PRIMARY KEY
```

### Important properties

```text
- Unique
- Cannot be NULL
- Identifies a row
```

Example:

```text
| id | name   |
|---:|--------|
| 1  | Rahul  |
| 2  | Ananya |
| 3  | Amit   |
```

Two rows cannot have the same primary-key value.

---

# 6. CREATE OUR FIRST TABLE

```
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    age INT,
    department VARCHAR(50),
    city VARCHAR(50),
    cgpa DECIMAL(3,2)
);
```

---

# 7. INSERT DATA

```
INSERT INTO students
(id, name, age, department, city, cgpa)
VALUES
(1, 'Rahul', 20, 'IT', 'Mangalore', 8.50),
(2, 'Ananya', 21, 'CSE', 'Bangalore', 9.10),
(3, 'Amit', 20, 'ECE', 'Mysore', 7.80),
(4, 'Priya', 22, 'IT', 'Bangalore', 8.90),
(5, 'Rohan', 21, 'CSE', 'Mangalore', 8.20),
(6, 'Sneha', 20, 'EEE', 'Mysore', 9.30),
(7, 'Arjun', 23, 'IT', 'Udupi', 7.50),
(8, 'Neha', 21, 'CSE', 'Bangalore', 8.70),
(9, 'Kiran', 22, 'ECE', 'Mangalore', 8.10),
(10, 'Pooja', 20, 'IT', 'Udupi', 9.00);
```

---

# PHASE 2 — BASIC QUERIES

# 1. SELECT

-> `SELECT` retrieves data from a table.

### Basic syntax

```
SELECT column_name
FROM table_name;
```

### Example

```
SELECT name
FROM students;
```

This retrieves only the `name` column.

---

# 2. SELECT MULTIPLE COLUMNS

```
SELECT name, age
FROM students;
```

You can select any required columns.

Example:

```
SELECT name, department, cgpa
FROM students;
```

---

# 3. SELECT EVERYTHING

-> `*` means all columns.

```
SELECT *
FROM students;
```

This returns the complete table.

### Important

Use `*` while learning or exploring a small table.

In production queries, selecting only the required columns is often preferable.

---

# 4. SELECT WITH EXPRESSIONS

SQL can also calculate values.

```
SELECT
    name,
    cgpa,
    cgpa + 0.1 AS adjusted_cgpa
FROM students;
```

`AS` creates an alias for the calculated column.

---

# 5. WHERE

-> `WHERE` filters rows.

### Basic syntax

```
SELECT columns
FROM table_name
WHERE condition;
```

### Example

```
SELECT *
FROM students
WHERE department = 'IT';
```

Only IT students are returned.

---

# 6. COMPARISON OPERATORS

| Operator | Meaning |
|---|---|
| `=` | equal |
| `>` | greater than |
| `<` | less than |
| `>=` | greater than or equal |
| `<=` | less than or equal |
| `<>` | not equal |
| `!=` | not equal |

### Example

```
SELECT *
FROM students
WHERE cgpa > 8.5;
```

---

# 7. WHERE + AND

-> `AND` requires all conditions to be true.

```
SELECT *
FROM students
WHERE department = 'IT'
AND cgpa > 8.5;
```

Meaning:

```text
department = IT
        AND
cgpa > 8.5
```

Both must be true.

---

# 8. WHERE + OR

-> `OR` requires at least one condition to be true.

```
SELECT *
FROM students
WHERE department = 'IT'
OR department = 'CSE';
```

This returns students from either IT or CSE.

---

# 9. DISTINCT

-> `DISTINCT` removes duplicate result rows.

### Basic syntax

```
SELECT DISTINCT column_name
FROM table_name;
```

### Example

```
SELECT DISTINCT city
FROM students;
```

Instead of seeing repeated cities, each city appears once.

---

# 10. DISTINCT WITH MULTIPLE COLUMNS

-> DISTINCT applies to the combination of selected columns.

```
SELECT DISTINCT
    department,
    city
FROM students;
```

The combination:

```text
department + city
```

must be unique.

### Important

`DISTINCT department, city` does NOT mean:

```text
unique departments
+
unique cities separately
```

It means:

```text
unique department-city combinations
```

---

# 11. LIKE

-> `LIKE` performs pattern matching.

### Basic syntax

```
SELECT *
FROM students
WHERE name LIKE 'A%';
```

This finds names beginning with `A`.

Example result:

```text
Amit
Ananya
Arjun
```

---

# 12. LIKE WILDCARDS

### `%`

-> Matches zero or more characters.

| Pattern | Meaning |
|---|---|
| `'A%'` | starts with A |
| `'%A'` | ends with A |
| `'%A%'` | contains A |

### `_`

-> Matches exactly one character.

| Pattern | Meaning |
|---|---|
| `'A____'` | A followed by exactly 4 characters |
| `'A_i%'` | A, then any one character, then i, then anything |

Example:

```
SELECT *
FROM students
WHERE name LIKE 'A_i%';
```

---

# 13. PostgreSQL — ILIKE

-> PostgreSQL provides `ILIKE` for case-insensitive pattern matching.

```
SELECT *
FROM students
WHERE name ILIKE 'a%';
```

This can match names beginning with either uppercase or lowercase `A`.

---

# 14. ORDER BY

-> `ORDER BY` sorts the result.

### Basic syntax

```
SELECT *
FROM students
ORDER BY cgpa;
```

Default ordering:

```text
ASC
```

Ascending means:

```text
7.50
7.80
8.10
...
9.30
```

---

# 15. ORDER BY ASC

```
SELECT *
FROM students
ORDER BY cgpa ASC;
```

`ASC` means ascending.

---

# 16. ORDER BY DESC

```
SELECT *
FROM students
ORDER BY cgpa DESC;
```

`DESC` means descending.

Result begins with the highest CGPA.

---

# 17. ORDER BY MULTIPLE COLUMNS

```
SELECT *
FROM students
ORDER BY department ASC, cgpa DESC;
```

Meaning:

```text
1. Sort by department
2. Inside each department, sort CGPA from highest to lowest
```

---

# 18. LIMIT

-> `LIMIT` restricts the number of rows returned.

```
SELECT *
FROM students
LIMIT 3;
```

This returns at most 3 rows.

### LIMIT + ORDER BY

To find the top 3 students by CGPA:

```
SELECT *
FROM students
ORDER BY cgpa DESC
LIMIT 3;
```

### Important

Without `ORDER BY`, "first 3" is not necessarily a meaningful ranking.

---

# 19. OFFSET

-> `OFFSET` skips rows before returning the requested number.

```
SELECT *
FROM students
ORDER BY cgpa DESC
LIMIT 3 OFFSET 3;
```

Conceptually:

```text
Sort by CGPA
    ↓
Skip first 3
    ↓
Return next 3
```

---

# PHASE 3 — CONDITIONS

# 1. AND

-> All conditions must be true.

```
SELECT *
FROM students
WHERE department = 'IT'
AND cgpa >= 8.5;
```

---

# 2. OR

-> At least one condition must be true.

```
SELECT *
FROM students
WHERE department = 'IT'
OR department = 'CSE';
```

---

# 3. NOT

-> Reverses a condition.

```
SELECT *
FROM students
WHERE NOT department = 'IT';
```

Equivalent common forms:

```
SELECT *
FROM students
WHERE department <> 'IT';
```

or:

```
SELECT *
FROM students
WHERE department != 'IT';
```

---

# 4. IN

-> `IN` checks whether a value belongs to a list.

Instead of:

```
WHERE department = 'IT'
OR department = 'CSE'
```

you can write:

```
SELECT *
FROM students
WHERE department IN ('IT', 'CSE');
```

### Mental model

```text
IN
↓
Is this value one of these?
```

---

# 5. NOT IN

-> Finds values that are not in the specified list.

```
SELECT *
FROM students
WHERE department NOT IN ('IT', 'CSE');
```

---

# 6. BETWEEN

-> `BETWEEN` checks whether a value falls within an inclusive range.

```
SELECT *
FROM students
WHERE cgpa BETWEEN 8.0 AND 9.0;
```

This means:

```text
cgpa >= 8.0
AND
cgpa <= 9.0
```

### Important

`BETWEEN` is inclusive.

---

# 7. NOT BETWEEN

-> Finds values outside the specified range.

```
SELECT *
FROM students
WHERE cgpa NOT BETWEEN 8.0 AND 9.0;
```

---

# 8. NULL

-> `NULL` represents a missing, unknown, or not-provided value depending on the data context.

Important:

```text
NULL is not the same as:
0
''
'NULL'
```

---

# 9. IS NULL

-> Use `IS NULL` to find NULL values.

```
SELECT *
FROM students
WHERE city IS NULL;
```

### IS NOT NULL

```
SELECT *
FROM students
WHERE city IS NOT NULL;
```

### Never do this

```
WHERE city = NULL
```

or:

```
WHERE city != NULL
```

Use:

```
IS NULL
IS NOT NULL
```

---

# 10. OPERATOR PRECEDENCE

When mixing `AND` and `OR`, use parentheses to make the intended logic explicit.

Example:

```
SELECT *
FROM students
WHERE department = 'IT'
AND (cgpa >= 8.5 OR city = 'Udupi');
```

Think carefully about:

```text
AND
OR
()
```

Parentheses make complex conditions easier to understand and avoid logic mistakes.

---

# 11. NOT LIKE

-> Finds values that do not match a pattern.

```
SELECT *
FROM students
WHERE name NOT LIKE 'A%';
```

---

# PHASE 4 — AGGREGATION

# 1. WHAT IS AGGREGATION?

-> Aggregation means taking multiple rows and calculating a single summarized result.

Example:

```text
10 student rows
      ↓
   AVG(cgpa)
      ↓
one average value
```

### Common aggregate functions

```text
COUNT()
SUM()
AVG()
MIN()
MAX()
```

---

# 2. COUNT()

-> `COUNT()` counts rows or non-NULL values depending on how it is used.

## COUNT(*)

-> Counts rows.

```
SELECT COUNT(*)
FROM students;
```

Result:

```text
10
```

---

## COUNT(column)

-> Counts non-NULL values in that column.

```
SELECT COUNT(city)
FROM students;
```

If some city values are NULL, those rows are not counted.

---

## COUNT with WHERE

```
SELECT COUNT(*)
FROM students
WHERE department = 'IT';
```

This counts only IT students.

---

## COUNT(DISTINCT)

-> Counts unique non-NULL values.

```
SELECT COUNT(DISTINCT department)
FROM students;
```

This gives the number of unique departments.

---

# 3. SUM()

-> Adds numeric values.

```
SELECT SUM(cgpa)
FROM students;
```

Think:

```text
CGPA values
    ↓
SUM()
    ↓
total
```

---

# 4. AVG()

-> Calculates the average of non-NULL numeric values.

```
SELECT AVG(cgpa)
FROM students;
```

Conceptually:

```text
SUM(cgpa)
---------
COUNT(cgpa)
```

---

# 5. MIN()

-> Returns the smallest value.

```
SELECT MIN(cgpa)
FROM students;
```

---

# 6. MAX()

-> Returns the largest value.

```
SELECT MAX(cgpa)
FROM students;
```

---

# 7. MULTIPLE AGGREGATIONS IN ONE QUERY

You can calculate several summaries at once.

```
SELECT
    COUNT(*) AS total_students,
    SUM(cgpa) AS total_cgpa,
    AVG(cgpa) AS average_cgpa,
    MIN(cgpa) AS minimum_cgpa,
    MAX(cgpa) AS maximum_cgpa
FROM students;
```

Result structure:

```text
| total_students | total_cgpa | average_cgpa | minimum_cgpa | maximum_cgpa |
|---------------:|------------:|-------------:|-------------:|-------------:|
| 10             | ...         | ...          | 7.50         | 9.30         |
```

---

# 8. GROUP BY

-> `GROUP BY` divides rows into groups and calculates aggregate results for each group.

This is the BIG concept in aggregation.

Example:

```
SELECT
    department,
    AVG(cgpa)
FROM students
GROUP BY department;
```

Result:

```text
| department | avg  |
|------------|-----:|
| CSE        | 8.67 |
| ECE        | 7.95 |
| EEE        | 9.30 |
| IT         | 8.48 |
```

Mental model:

```text
students
   ↓
GROUP BY department
   ↓
IT group
CSE group
ECE group
EEE group
   ↓
calculate AVG for each group
```

---

# 9. GROUP BY + COUNT

Question:

-> How many students are in each department?

```
SELECT
    department,
    COUNT(*) AS student_count
FROM students
GROUP BY department;
```

Result:

```text
| department | student_count |
|------------|--------------:|
| CSE        | 3             |
| ECE        | 2             |
| EEE        | 1             |
| IT         | 4             |
```

---

# 10. GROUP BY + AVG

```
SELECT
    department,
    AVG(cgpa) AS average_cgpa
FROM students
GROUP BY department;
```

Each department gets its own average.

---

# 11. GROUP BY + SUM

```
SELECT
    department,
    SUM(cgpa) AS total_cgpa
FROM students
GROUP BY department;
```

Each department gets its own total.

---

# 12. GROUP BY + MIN / MAX

```
SELECT
    department,
    MIN(cgpa) AS minimum_cgpa,
    MAX(cgpa) AS maximum_cgpa
FROM students
GROUP BY department;
```

This gives the lowest and highest CGPA in every department.

---

# 13. GROUP BY MULTIPLE COLUMNS

You can group by more than one column.

```
SELECT
    department,
    city,
    COUNT(*) AS student_count
FROM students
GROUP BY department, city;
```

The groups are based on:

```text
department + city
```

---

# 14. WHERE + GROUP BY

`WHERE` filters rows before grouping.

```
SELECT
    department,
    AVG(cgpa) AS average_cgpa
FROM students
WHERE department IN ('IT', 'CSE')
GROUP BY department;
```

Logical flow:

```text
FROM
 ↓
WHERE       ← filter rows
 ↓
GROUP BY    ← make groups
 ↓
aggregate
```

---

# 15. HAVING

-> `HAVING` filters groups after aggregation.

Example:

-> Show departments having more than 2 students.

```
SELECT
    department,
    COUNT(*) AS student_count
FROM students
GROUP BY department
HAVING COUNT(*) > 2;
```

Result conceptually:

```text
| department | student_count |
|------------|--------------:|
| CSE        | 3             |
| IT         | 4             |
```

---

# 16. WHERE vs HAVING

| WHERE | HAVING |
|---|---|
| Filters rows | Filters groups |
| Before grouping | After grouping |
| Commonly filters individual values | Commonly filters aggregate results |
| `WHERE cgpa > 8` | `HAVING AVG(cgpa) > 8` |

### Logical order

```text
FROM
 ↓
WHERE       ← filter rows
 ↓
GROUP BY    ← make groups
 ↓
HAVING      ← filter groups
 ↓
SELECT
 ↓
ORDER BY
 ↓
LIMIT
```

---

# 17. GROUP BY + HAVING + ORDER BY

Example:

-> Show departments with at least 2 students, sorted by average CGPA from highest to lowest.

```
SELECT
    department,
    COUNT(*) AS student_count,
    AVG(cgpa) AS average_cgpa
FROM students
GROUP BY department
HAVING COUNT(*) >= 2
ORDER BY average_cgpa DESC;
```

This combines the major aggregation concepts.

---

# 18. NULL HANDLING IN AGGREGATION

Most aggregate functions ignore NULL values.

For example:

```
AVG(cgpa)
```

calculates using non-NULL CGPA values.

Similarly:

```text
SUM(column)
AVG(column)
MIN(column)
MAX(column)
COUNT(column)
```

generally operate on non-NULL values.

But:

```
COUNT(*)
```

counts rows, including rows where particular columns contain NULL.

---

# 19. COALESCE

-> `COALESCE()` returns the first non-NULL value.

### Basic syntax

```
COALESCE(value1, value2, value3, ...)
```

Example:

```
SELECT
    name,
    COALESCE(city, 'Unknown') AS city
FROM students;
```

If:

```text
city = Bangalore
```

result:

```text
Bangalore
```

If:

```text
city = NULL
```

result:

```text
Unknown
```

---

# 20. CASE WHEN

-> `CASE` provides conditional logic inside SQL.

Think:

```text
if
else if
else
```

### Basic syntax

```
CASE
    WHEN condition THEN result
    WHEN condition THEN result
    ELSE result
END
```

---

# 21. CASE WITH CGPA

```
SELECT
    name,
    cgpa,
    CASE
        WHEN cgpa >= 9 THEN 'Excellent'
        WHEN cgpa >= 8 THEN 'Good'
        ELSE 'Needs Improvement'
    END AS performance
FROM students;
```

Result conceptually:

```text
| name   | cgpa | performance       |
|--------|-----:|-------------------|
| Rahul  | 8.50 | Good              |
| Ananya | 9.10 | Excellent         |
| Amit   | 7.80 | Needs Improvement |
```

### Important

CASE is evaluated from top to bottom.

The first matching `WHEN` is used.

---

# 22. CASE WITH CATEGORIES

```
SELECT
    name,
    age,
    CASE
        WHEN age < 21 THEN 'Young'
        WHEN age <= 22 THEN 'Adult'
        ELSE 'Senior'
    END AS age_group
FROM students;
```

---

# 23. CASE WITH NULL

```
SELECT
    name,
    CASE
        WHEN city IS NULL THEN 'City Unknown'
        ELSE city
    END AS city_status
FROM students;
```

---

# 24. CASE + AGGREGATE FUNCTIONS

You can combine CASE with aggregate functions for conditional aggregation.

Example:

```
SELECT
    COUNT(CASE WHEN cgpa >= 9 THEN 1 END) AS excellent,
    COUNT(CASE WHEN cgpa >= 8 AND cgpa < 9 THEN 1 END) AS good,
    COUNT(CASE WHEN cgpa < 8 THEN 1 END) AS needs_improvement
FROM students;
```

This produces counts for different CGPA categories.

---

# 25. CASE + SUM

Another common pattern:

```
SELECT
    SUM(CASE
        WHEN cgpa >= 9 THEN 1
        ELSE 0
    END) AS excellent_students
FROM students;
```

Mental model:

```text
Condition true
    ↓
1

Condition false
    ↓
0

SUM()
    ↓
number of matching students
```

---

# 26. CONDITIONAL AGGREGATION BY DEPARTMENT

```
SELECT
    department,
    SUM(
        CASE
            WHEN cgpa >= 9 THEN 1
            ELSE 0
        END
    ) AS excellent_students
FROM students
GROUP BY department;
```

This calculates the number of students with CGPA >= 9 in every department.

---

# 27. COMPLETE AGGREGATION QUERY

A common professional-style pattern:

```
SELECT
    department,
    COUNT(*) AS student_count,
    AVG(cgpa) AS average_cgpa,
    MAX(cgpa) AS highest_cgpa,
    SUM(
        CASE
            WHEN cgpa >= 9 THEN 1
            ELSE 0
        END
    ) AS excellent_student_count
FROM students
WHERE cgpa >= 8
GROUP BY department
HAVING COUNT(*) >= 2
ORDER BY average_cgpa DESC;
```

### Understand the flow

```text
FROM students
      ↓
WHERE cgpa >= 8
      ↓
GROUP BY department
      ↓
COUNT / AVG / MAX / SUM(CASE)
      ↓
HAVING COUNT(*) >= 2
      ↓
ORDER BY average_cgpa DESC
```

This is the structure that should eventually become natural when solving aggregation problems.

---

# 28. AGGREGATION QUICK REFERENCE

| Function / Clause | Purpose |
|---|---|
| `COUNT(*)` | Count rows |
| `COUNT(column)` | Count non-NULL values |
| `COUNT(DISTINCT column)` | Count unique non-NULL values |
| `SUM(column)` | Add values |
| `AVG(column)` | Calculate average |
| `MIN(column)` | Smallest value |
| `MAX(column)` | Largest value |
| `GROUP BY` | Create groups |
| `HAVING` | Filter groups |
| `COALESCE()` | Replace NULL with fallback |
| `CASE` | Conditional logic |

---

# FINAL MENTAL MODEL

```text
PHASE 1 — FOUNDATIONS
│
├── Database concepts
├── Tables
├── Rows / Columns
├── Data types
└── Primary keys
        ↓
PHASE 2 — BASIC QUERIES
│
├── SELECT
├── WHERE
├── DISTINCT
├── LIKE
├── ORDER BY
└── LIMIT
        ↓
PHASE 3 — CONDITIONS
│
├── AND
├── OR
├── NOT
├── IN
├── BETWEEN
└── IS NULL
        ↓
PHASE 4 — AGGREGATION
│
├── COUNT
├── SUM
├── AVG
├── MIN
├── MAX
├── GROUP BY
└── HAVING
```

## The Core Progression

```text
SELECT
→ get data

WHERE
→ filter rows

DISTINCT
→ remove duplicate result rows

LIKE
→ pattern matching

ORDER BY
→ sort results

LIMIT
→ restrict number of rows

AND / OR / NOT
→ combine conditions

IN
→ match against a list

BETWEEN
→ match a range

IS NULL
→ check missing values

COUNT / SUM / AVG / MIN / MAX
→ summarize data

GROUP BY
→ summarize each group

HAVING
→ filter summarized groups

COALESCE
→ provide a fallback for NULL

CASE
→ apply conditional logic
```
