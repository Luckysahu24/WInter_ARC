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

# PHASE 5 — JOINS

## 1. What is a JOIN?

-> A JOIN combines rows from two or more tables using a related column.

Instead of keeping everything in one table, databases normally split related information into separate tables.

For example:

```text
students
    |
    | department_id
    ↓
departments
```

### Example Tables

``` 
students

| id | name   | department_id |
|---:|--------|--------------:|
| 1  | Rahul  | 101           |
| 2  | Ananya | 102           |
| 3  | Amit   | 103           |
| 4  | Priya  | 101           |
```

```
departments

| department_id | department_name |
|--------------:|-----------------|
| 101           | IT              |
| 102           | CSE             |
| 103           | ECE             |
| 104           | EEE             |
```

The common column is:

```text
students.department_id
        =
departments.department_id
```

### Basic JOIN syntax

```
SELECT columns
FROM table1
JOIN table2
    ON table1.column = table2.column;
```

---

# 2. INNER JOIN

-> Returns only the rows where a matching record exists in BOTH tables.

```text
Table A          Table B

A1 ───────────── B1
A2 ───────────── B2
A3        X      B3

INNER JOIN
    ↓

A1 + B1
A2 + B2
```

### Syntax

```
SELECT
    students.name,
    departments.department_name
FROM students
INNER JOIN departments
    ON students.department_id = departments.department_id;
```

### Result

```
| name   | department_name |
|--------|-----------------|
| Rahul  | IT              |
| Ananya | CSE             |
| Amit   | ECE             |
| Priya  | IT              |
```

### Important

`INNER JOIN` removes rows that do not have a match.

---

# 3. JOIN using aliases

Aliases make JOIN queries much easier to read.

```
SELECT
    s.name,
    d.department_name
FROM students AS s
INNER JOIN departments AS d
    ON s.department_id = d.department_id;
```

You can also omit `AS`:

```
SELECT
    s.name,
    d.department_name
FROM students s
INNER JOIN departments d
    ON s.department_id = d.department_id;
```

### Why aliases?

Instead of writing:

```
students.department_id
departments.department_id
```

we can write:

```
s.department_id
d.department_id
```

---

# 4. LEFT JOIN

-> Returns ALL rows from the LEFT table and matching rows from the RIGHT table.

```text
LEFT TABLE                 RIGHT TABLE

A1 ─────────────────────── B1
A2 ─────────────────────── B2
A3          no match       -
A4 ─────────────────────── B4

LEFT JOIN
    ↓

A1 + B1
A2 + B2
A3 + NULL
A4 + B4
```

### Syntax

```
SELECT
    s.name,
    d.department_name
FROM students s
LEFT JOIN departments d
    ON s.department_id = d.department_id;
```

If a student has no matching department:

```text
department_name = NULL
```

### Main idea

```text
LEFT JOIN
↓
Keep everything from the LEFT table.
```

---

# 5. INNER JOIN vs LEFT JOIN

| INNER JOIN | LEFT JOIN |
|---|---|
| Only matching rows | All left-table rows |
| Unmatched left rows removed | Unmatched left rows kept |
| No-match rows don't appear | No-match right-side columns become NULL |

### Easy memory trick

```text
INNER JOIN
= only matches

LEFT JOIN
= everything on left + matches on right
```

---

# 6. RIGHT JOIN

-> Returns ALL rows from the RIGHT table and matching rows from the LEFT table.

```text
LEFT TABLE                 RIGHT TABLE

A1 ─────────────────────── B1
A2 ─────────────────────── B2
-           no match       B3
A4 ─────────────────────── B4

RIGHT JOIN
    ↓

A1 + B1
A2 + B2
NULL + B3
A4 + B4
```

### Syntax

```
SELECT
    s.name,
    d.department_name
FROM students s
RIGHT JOIN departments d
    ON s.department_id = d.department_id;
```

If a department has no student:

```text
name = NULL
```

### Main idea

```text
RIGHT JOIN
↓
Keep everything from the RIGHT table.
```

### Professional note

A `RIGHT JOIN` can usually be rewritten as a `LEFT JOIN` by swapping the table order.

For example:

```
A RIGHT JOIN B
```

is equivalent in result to:

```
B LEFT JOIN A
```

Many developers prefer `LEFT JOIN` because it is easier to read consistently.

---

# 7. FULL OUTER JOIN

-> Returns ALL rows from BOTH tables.

Matching rows are combined.

Unmatched rows are kept with NULL values on the other side.

```text
Table A                 Table B

A1 ─────────────────── B1
A2 ─────────────────── B2
A3                      B3
                         B4

FULL OUTER JOIN
       ↓

A1 + B1
A2 + B2
A3 + NULL
NULL + B3
NULL + B4
```

### PostgreSQL syntax

```
SELECT
    s.name,
    d.department_name
FROM students s
FULL OUTER JOIN departments d
    ON s.department_id = d.department_id;
```

### Important PostgreSQL / MySQL difference

PostgreSQL supports:

```
FULL OUTER JOIN
```

MySQL does not provide a native `FULL OUTER JOIN` syntax.

In MySQL, a common approach is to combine:

```
LEFT JOIN
UNION
RIGHT JOIN
```

Example:

```
SELECT
    s.name,
    d.department_name
FROM students s
LEFT JOIN departments d
    ON s.department_id = d.department_id

UNION

SELECT
    s.name,
    d.department_name
FROM students s
RIGHT JOIN departments d
    ON s.department_id = d.department_id;
```

---

# 8. JOIN Types — Quick Table

| JOIN | What it returns |
|---|---|
| INNER JOIN | Matching rows from both tables |
| LEFT JOIN | All left rows + matching right rows |
| RIGHT JOIN | All right rows + matching left rows |
| FULL OUTER JOIN | All rows from both tables |

---

# 9. JOIN with WHERE

You can filter the result after joining.

```
SELECT
    s.name,
    d.department_name
FROM students s
INNER JOIN departments d
    ON s.department_id = d.department_id
WHERE d.department_name = 'IT';
```

Logical idea:

```text
FROM
 ↓
JOIN
 ↓
WHERE
 ↓
SELECT
```

---

# 10. JOIN + GROUP BY

JOINs and aggregation are commonly used together.

Question:

-> Count students in every department.

```
SELECT
    d.department_name,
    COUNT(s.id) AS student_count
FROM departments d
LEFT JOIN students s
    ON d.department_id = s.department_id
GROUP BY d.department_name;
```

### Why LEFT JOIN?

Because we also want departments that currently have zero students.

If we used `INNER JOIN`, departments without students would disappear.

---

# 11. JOIN + GROUP BY + HAVING

```
SELECT
    d.department_name,
    COUNT(s.id) AS student_count
FROM departments d
LEFT JOIN students s
    ON d.department_id = s.department_id
GROUP BY d.department_name
HAVING COUNT(s.id) >= 2;
```

Meaning:

```text
JOIN
 ↓
GROUP BY department
 ↓
COUNT students
 ↓
keep departments with >= 2 students
```

---

# 12. Multiple JOINs

Real databases commonly require more than two tables.

Example:

```text
students
    ↓
enrollments
    ↓
courses
```

Query:

```
SELECT
    s.name,
    c.course_name
FROM students s
INNER JOIN enrollments e
    ON s.id = e.student_id
INNER JOIN courses c
    ON e.course_id = c.course_id;
```

### Mental model

```text
students
   ↓
enrollments
   ↓
courses
```

Each JOIN connects another related table.

---

# PHASE 6 — INTERMEDIATE

# 1. SUBQUERIES

-> A subquery is a query written inside another query.

Think:

```text
Outer Query
    |
    └── Inner Query
```

### Basic example

Question:

-> Find students whose CGPA is greater than the average CGPA.

First:

```
SELECT AVG(cgpa)
FROM students;
```

Then use that result:

```
SELECT *
FROM students
WHERE cgpa > (
    SELECT AVG(cgpa)
    FROM students
);
```

The inner query:

```
SELECT AVG(cgpa)
FROM students
```

calculates the average.

The outer query:

```
SELECT *
FROM students
WHERE cgpa > ...
```

uses that result.

---

# 2. Scalar Subquery

-> A scalar subquery returns a single value.

Example:

```
SELECT
    name,
    cgpa
FROM students
WHERE cgpa > (
    SELECT AVG(cgpa)
    FROM students
);
```

The inner query returns one value:

```text
average CGPA
```

---

# 3. Subquery with IN

Question:

-> Find students belonging to departments located in Bangalore.

Assume:

```text
departments

| department_id | department_name | city      |
|--------------:|-----------------|-----------|
| 101           | IT              | Bangalore |
| 102           | CSE             | Bangalore |
| 103           | ECE             | Mysore    |
```

Query:

```
SELECT *
FROM students
WHERE department_id IN (
    SELECT department_id
    FROM departments
    WHERE city = 'Bangalore'
);
```

The inner query returns multiple department IDs.

`IN` checks whether the student's department ID belongs to that result.

---

# 4. Correlated Subquery

-> A correlated subquery depends on the current row of the outer query.

Example:

-> Find students whose CGPA is above the average CGPA of their own department.

```
SELECT
    s.name,
    s.department_id,
    s.cgpa
FROM students s
WHERE s.cgpa > (
    SELECT AVG(s2.cgpa)
    FROM students s2
    WHERE s2.department_id = s.department_id
);
```

The inner query changes according to the outer student's department.

---

# 5. CASE

-> CASE provides conditional logic inside SQL.

Think:

```text
if
else if
else
```

### Syntax

```
CASE
    WHEN condition THEN result
    WHEN condition THEN result
    ELSE result
END
```

### Example

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

### Result

```
| name   | cgpa | performance       |
|--------|-----:|-------------------|
| Rahul  | 8.50 | Good              |
| Ananya | 9.10 | Excellent         |
| Amit   | 7.80 | Needs Improvement |
```

---

# 6. CASE With Multiple Conditions

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

### Important

CASE is evaluated from top to bottom.

The first matching `WHEN` is used.

---

# 7. CASE With NULL

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

# 8. COALESCE

-> `COALESCE()` returns the first non-NULL value.

### Syntax

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

# 9. COALESCE With Multiple Values

```
SELECT
    COALESCE(phone, email, 'No Contact') AS contact
FROM students;
```

SQL checks:

```text
phone
 ↓
if NULL
 ↓
email
 ↓
if NULL
 ↓
'No Contact'
```

---

# 10. CASE vs COALESCE

| CASE | COALESCE |
|---|---|
| Conditional logic | NULL fallback |
| Can test many conditions | Returns first non-NULL value |
| More flexible | Simpler for missing values |

Example:

```
CASE
    WHEN city IS NULL THEN 'Unknown'
    ELSE city
END
```

can often be simplified to:

```
COALESCE(city, 'Unknown')
```

---

# 11. UNION

-> `UNION` combines the result of two or more SELECT queries vertically.

```text
Query 1
---------
A
B
C

UNION

Query 2
---------
D
E

Result
---------
A
B
C
D
E
```

### Syntax

```
SELECT column1
FROM table1

UNION

SELECT column1
FROM table2;
```

### Important rule

Both SELECT statements must return compatible numbers/types of columns.

---

# 12. UNION Removes Duplicates

```
SELECT city
FROM students

UNION

SELECT city
FROM departments;
```

`UNION` removes duplicate rows from the combined result.

---

# 13. UNION ALL

-> `UNION ALL` keeps duplicates.

```
SELECT city
FROM students

UNION ALL

SELECT city
FROM departments;
```

### UNION vs UNION ALL

| UNION | UNION ALL |
|---|---|
| Removes duplicates | Keeps duplicates |
| Usually more work | Usually faster |
| Returns unique combined rows | Returns every combined row |

Use `UNION ALL` when duplicate rows are meaningful or when you know deduplication is unnecessary.

---

# 14. CTEs — Common Table Expressions

-> A CTE gives a temporary name to a query result so the main query becomes easier to read.

Syntax:

```
WITH cte_name AS (
    SELECT ...
)
SELECT ...
FROM cte_name;
```

### Example

```
WITH high_scorers AS (
    SELECT *
    FROM students
    WHERE cgpa >= 8.5
)
SELECT *
FROM high_scorers;
```

Think:

```text
WITH
 ↓
create temporary named result
 ↓
use it in the main query
```

---

# 15. CTE With Aggregation

```
WITH department_stats AS (
    SELECT
        department,
        AVG(cgpa) AS average_cgpa,
        COUNT(*) AS student_count
    FROM students
    GROUP BY department
)
SELECT *
FROM department_stats
WHERE average_cgpa > 8.5;
```

This is much easier to understand than putting everything into one giant nested query.

---

# 16. Multiple CTEs

```
WITH department_stats AS (
    SELECT
        department,
        AVG(cgpa) AS average_cgpa
    FROM students
    GROUP BY department
),
high_performing AS (
    SELECT *
    FROM department_stats
    WHERE average_cgpa >= 8.5
)
SELECT *
FROM high_performing;
```

CTEs can be chained using commas.

---

# 17. Views

-> A view is a stored query that behaves like a virtual table.

### Create a view

```
CREATE VIEW high_cgpa_students AS
SELECT
    id,
    name,
    department,
    cgpa
FROM students
WHERE cgpa >= 8.5;
```

Now:

```
SELECT *
FROM high_cgpa_students;
```

You can query it like a table.

---

# 18. Why use Views?

Views are useful for:

```text
- Reusing complex queries
- Simplifying reporting
- Hiding unnecessary columns
- Providing controlled access to data
```

### Remove a view

```
DROP VIEW high_cgpa_students;
```

---

# PHASE 7 — ADVANCED

# 1. WINDOW FUNCTIONS

-> A window function performs a calculation across related rows while keeping the individual rows.

This is the BIG difference:

```text
GROUP BY
→ combines rows into one row per group

WINDOW FUNCTION
→ keeps individual rows
```

Example:

```text
GROUP BY

IT     → 8.48
CSE    → 8.67
ECE    → 7.95
```

Window function:

```text
Rahul   8.50   IT    8.48
Priya   8.90   IT    8.48
Arjun   7.50   IT    8.48
Pooja   9.00   IT    8.48
```

The individual students remain visible.

---

# 2. Basic Window Function

```
SELECT
    name,
    department,
    cgpa,
    AVG(cgpa) OVER () AS overall_average
FROM students;
```

Every row remains visible.

The overall average is repeated for every row.

---

# 3. PARTITION BY

-> `PARTITION BY` divides rows into logical groups for a window function.

### Example

```
SELECT
    name,
    department,
    cgpa,
    AVG(cgpa) OVER (
        PARTITION BY department
    ) AS department_average
FROM students;
```

Conceptually:

```text
IT
├── Rahul
├── Priya
├── Arjun
└── Pooja

CSE
├── Ananya
├── Rohan
└── Neha

ECE
├── Amit
└── Kiran
```

Each department gets its own average.

---

# 4. GROUP BY vs PARTITION BY

| GROUP BY | PARTITION BY |
|---|---|
| Collapses rows | Keeps rows |
| Produces one row per group | Produces a value for every row |
| Used with aggregation | Used with window functions |

Example:

```
GROUP BY
```

```
SELECT
    department,
    AVG(cgpa)
FROM students
GROUP BY department;
```

Result:

```text
IT   8.48
CSE  8.67
ECE  7.95
EEE  9.30
```

Window:

```
SELECT
    name,
    department,
    cgpa,
    AVG(cgpa) OVER (
        PARTITION BY department
    ) AS department_average
FROM students;
```

Result keeps every student.

---

# 5. ROW_NUMBER()

-> Assigns a unique sequential number to rows inside a window.

### Syntax

```
ROW_NUMBER() OVER (
    ORDER BY cgpa DESC
)
```

### Example

```
SELECT
    name,
    cgpa,
    ROW_NUMBER() OVER (
        ORDER BY cgpa DESC
    ) AS row_num
FROM students;
```

Result conceptually:

```text
| name   | cgpa | row_num |
|--------|-----:|--------:|
| Sneha  | 9.30 | 1       |
| Ananya | 9.10 | 2       |
| Pooja  | 9.00 | 3       |
| Priya  | 8.90 | 4       |
```

Every row receives a unique number.

---

# 6. ROW_NUMBER() With PARTITION BY

Question:

-> Rank students separately within each department.

```
SELECT
    name,
    department,
    cgpa,
    ROW_NUMBER() OVER (
        PARTITION BY department
        ORDER BY cgpa DESC
    ) AS department_row_number
FROM students;
```

Now numbering restarts for each department.

```text
IT
1
2
3
4

CSE
1
2
3

ECE
1
2
```

---

# 7. RANK()

-> Assigns ranks while giving tied rows the same rank.

Example:

```text
CGPA

9.5
9.5
9.0
8.5
```

Using `RANK()`:

```text
1
1
3
4
```

There is a gap after the tie.

### Syntax

```
SELECT
    name,
    cgpa,
    RANK() OVER (
        ORDER BY cgpa DESC
    ) AS rank
FROM students;
```

---

# 8. DENSE_RANK()

-> Gives tied rows the same rank but does NOT leave gaps.

Example:

```text
CGPA

9.5
9.5
9.0
8.5
```

`DENSE_RANK()`:

```text
1
1
2
3
```

### Syntax

```
SELECT
    name,
    cgpa,
    DENSE_RANK() OVER (
        ORDER BY cgpa DESC
    ) AS dense_rank
FROM students;
```

---

# 9. ROW_NUMBER vs RANK vs DENSE_RANK

| Function | Ties get same rank? | Gaps after ties? |
|---|---|---|
| ROW_NUMBER | No | No |
| RANK | Yes | Yes |
| DENSE_RANK | Yes | No |

Example:

```text
Scores: 100, 100, 90, 80
```

```text
ROW_NUMBER
1
2
3
4

RANK
1
1
3
4

DENSE_RANK
1
1
2
3
```

This difference is extremely important.

---

# 10. LAG()

-> `LAG()` accesses a value from a previous row.

Example:

```text
| month | sales |
|-------|------:|
| Jan   | 100   |
| Feb   | 120   |
| Mar   | 150   |
```

Query:

```
SELECT
    month,
    sales,
    LAG(sales) OVER (
        ORDER BY month
    ) AS previous_month_sales
FROM monthly_sales;
```

Result:

```text
| month | sales | previous_month_sales |
|-------|------:|---------------------:|
| Jan   | 100   | NULL                 |
| Feb   | 120   | 100                  |
| Mar   | 150   | 120                  |
```

---

# 11. LAG() With Difference

Very common in analytics.

```
SELECT
    month,
    sales,
    sales - LAG(sales) OVER (
        ORDER BY month
    ) AS sales_change
FROM monthly_sales;
```

Result:

```text
| month | sales | sales_change |
|-------|------:|-------------:|
| Jan   | 100   | NULL         |
| Feb   | 120   | 20           |
| Mar   | 150   | 30           |
```

---

# 12. LEAD()

-> `LEAD()` accesses a value from a future row.

```
SELECT
    month,
    sales,
    LEAD(sales) OVER (
        ORDER BY month
    ) AS next_month_sales
FROM monthly_sales;
```

Result:

```text
| month | sales | next_month_sales |
|-------|------:|-----------------:|
| Jan   | 100   | 120              |
| Feb   | 120   | 150              |
| Mar   | 150   | NULL             |
```

---

# 13. LAG vs LEAD

| Function | Looks at |
|---|---|
| LAG() | Previous row |
| LEAD() | Next row |

Memory trick:

```text
LAG  ← look backward
LEAD → look forward
```

---

# 14. Window Function Syntax Pattern

Most window functions follow:

```
function_name(...) OVER (
    PARTITION BY ...
    ORDER BY ...
)
```

Example:

```
AVG(cgpa) OVER (
    PARTITION BY department
    ORDER BY cgpa
)
```

The two most important pieces are:

```text
PARTITION BY
→ divide into groups

ORDER BY
→ define row order inside each group
```

---

# PHASE 8 — PROFESSIONAL DATABASE SKILLS

# 1. INDEXES

-> An index is a database structure that helps the database find rows faster.

Think of a book.

Without an index:

```text
Read every page
↓
Find the topic
```

With an index:

```text
Look at index
↓
Find page
↓
Go directly there
```

A database index serves a similar purpose.

---

# 2. Create an Index

Suppose we frequently search by department:

```
SELECT *
FROM students
WHERE department = 'IT';
```

Create:

```
CREATE INDEX idx_students_department
ON students(department);
```

Now the database has an index on:

```text
department
```

---

# 3. Index on Multiple Columns

You can create a composite index:

```
CREATE INDEX idx_students_department_cgpa
ON students(department, cgpa);
```

This can help queries involving those columns, depending on the query and database optimizer.

---

# 4. Drop an Index

PostgreSQL:

```
DROP INDEX idx_students_department;
```

MySQL:

```
DROP INDEX idx_students_department
ON students;
```

---

# 5. Important Index Trade-off

Indexes can make reads faster, but they are not free.

Indexes can:

```text
+ Speed up suitable searches
+ Help sorting/joining in some cases
+ Improve query performance
```

But they also:

```text
- Consume storage
- Add overhead to INSERT
- Add overhead to UPDATE
- Add overhead to DELETE
```

Therefore:

```text
Don't index every column.
```

Create indexes based on actual query patterns and workload.

---

# 6. TRANSACTIONS

-> A transaction is a group of database operations treated as one logical unit.

Example:

```text
Bank transfer

Account A
   ↓
- ₹100

Account B
   ↓
+ ₹100
```

Both operations should succeed together.

If one fails, we want to undo the transaction.

---

# 7. Basic Transaction Syntax

```
BEGIN;

UPDATE accounts
SET balance = balance - 100
WHERE id = 1;

UPDATE accounts
SET balance = balance + 100
WHERE id = 2;

COMMIT;
```

`COMMIT` permanently saves the transaction.

---

# 8. ROLLBACK

If something goes wrong:

```
BEGIN;

UPDATE accounts
SET balance = balance - 100
WHERE id = 1;

ROLLBACK;
```

The changes made inside the transaction are undone according to the database's transaction semantics.

---

# 9. COMMIT vs ROLLBACK

| Command | Purpose |
|---|---|
| COMMIT | Save transaction changes |
| ROLLBACK | Undo uncommitted transaction changes |

Think:

```text
BEGIN
  ↓
operations
  ↓
 ┌───────────────┐
 │               │
COMMIT        ROLLBACK
 │               │
save             undo
```

---

# 10. ACID

-> ACID describes four important properties of reliable database transactions.

```text
A → Atomicity
C → Consistency
I → Isolation
D → Durability
```

---

# 11. Atomicity

-> A transaction happens completely or not at all.

Example:

```text
Transfer ₹100

A - ₹100
B + ₹100
```

We don't want:

```text
A - ₹100
B + nothing
```

Atomicity protects the transaction as one unit.

---

# 12. Consistency

-> A transaction should move the database from one valid state to another valid state while respecting defined rules and constraints.

Example:

If an account cannot have a negative balance according to the application's/database rules, a transaction should not leave the database violating that rule.

---

# 13. Isolation

-> Concurrent transactions should not improperly interfere with one another.

For example:

```text
Transaction A
Transaction B
```

may execute at the same time.

The database's isolation mechanisms control what each transaction can see and how concurrent changes interact.

---

# 14. Durability

-> Once a transaction is successfully committed, its changes should survive failures such as a database restart, subject to the database system's durability guarantees.

```text
COMMIT
  ↓
saved
  ↓
restart
  ↓
data remains
```

---

# 15. ACID Summary

| Property | Meaning |
|---|---|
| Atomicity | All or nothing |
| Consistency | Preserves database rules |
| Isolation | Controls concurrent transaction interaction |
| Durability | Committed data persists |

---

# 16. CONSTRAINTS

-> Constraints are rules enforced by the database to maintain valid data.

Common constraints:

```text
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
CHECK
DEFAULT
```

---

# 17. PRIMARY KEY

-> Uniquely identifies each row.

```
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

Properties:

```text
- Unique
- Cannot be NULL
- Identifies a row
```

---

# 18. FOREIGN KEY

-> Creates a relationship between tables.

```
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(50)
);
```

Then:

```
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,
    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

Relationship:

```text
students.department_id
          ↓
departments.department_id
```

---

# 19. UNIQUE

-> Prevents duplicate values in a column/constraint key.

```
CREATE TABLE users (
    id INT PRIMARY KEY,
    email VARCHAR(255) UNIQUE
);
```

Two users should not have the same email under this constraint.

---

# 20. NOT NULL

-> Requires a value to be provided.

```
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

This prevents `name` from being NULL.

---

# 21. CHECK

-> Enforces a condition.

```
CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    cgpa DECIMAL(3,2),
    CHECK (cgpa >= 0 AND cgpa <= 10)
);
```

Now the database can reject invalid CGPA values outside the specified range.

---

# 22. DEFAULT

-> Provides a default value when no value is supplied.

```
CREATE TABLE users (
    id INT PRIMARY KEY,
    status VARCHAR(20) DEFAULT 'active'
);
```

If status is omitted:

```text
status = active
```

---

# 23. NORMALIZATION

-> Normalization is the process of organizing data to reduce unnecessary duplication and improve data integrity.

### Bad design

```
students

| id | name | department | department_hod |
|----|------|------------|----------------|
| 1  | Rahul| IT         | Dr. X          |
| 2  | Priya| IT         | Dr. X          |
| 3  | Amit | CSE        | Dr. Y          |
```

`Dr. X` is repeated.

Instead:

```text
students
        |
        | department_id
        ↓
departments
```

```
students

| id | name  | department_id |
|----|-------|---------------|
| 1  | Rahul | 101           |
| 2  | Priya | 101           |
| 3  | Amit  | 102           |
```

```
departments

| department_id | department | hod    |
|---------------|------------|--------|
| 101           | IT         | Dr. X  |
| 102           | CSE        | Dr. Y  |
```

---

# 24. Why Normalize?

Normalization helps reduce:

```text
- Duplicate data
- Update anomalies
- Insert anomalies
- Delete anomalies
```

It also helps maintain consistent information.

---

# 25. First Normal Form — 1NF

-> A table should have atomic values and no repeating groups.

Bad:

```
| id | phone_numbers        |
|----|----------------------|
| 1  | 9876, 8765, 7654     |
```

Better:

```
| id | phone |
|----|-------|
| 1  | 9876  |
| 1  | 8765  |
| 1  | 7654  |
```

Each field contains a single logical value.

---

# 26. Second Normal Form — 2NF

-> A table must be in 1NF and non-key attributes should depend on the whole primary key, not only part of a composite key.

This matters mainly when a table has a composite primary key.

Example:

```text
(student_id, course_id)
```

If:

```text
student_id → student_name
```

then `student_name` depends only on part of the composite key.

That dependency should be separated into the appropriate table.

---

# 27. Third Normal Form — 3NF

-> A table should be in 2NF and non-key attributes should not depend on other non-key attributes.

Example:

```text
student_id
department_id
department_name
```

If:

```text
student_id → department_id
department_id → department_name
```

then `department_name` is transitively dependent on `student_id`.

It is better stored in the department table.

---

# 28. Normalization Summary

| Normal Form | Main idea |
|---|---|
| 1NF | Atomic values; no repeating groups |
| 2NF | No partial dependency on part of a composite key |
| 3NF | No transitive dependency between non-key attributes |

Normalization is a design tool, not simply a rule to split every possible table.

---

# 29. QUERY OPTIMIZATION

-> Query optimization means making SQL queries execute efficiently while producing the required result.

A query can be logically correct but inefficient.

Example:

```
SELECT *
FROM students;
```

If a table has millions of rows and you only need two columns, this may retrieve much more data than necessary.

Better:

```
SELECT name, cgpa
FROM students;
```

---

# 30. Common Query Optimization Ideas

```text
- Select only required columns
- Filter early when appropriate
- Use suitable indexes
- Avoid unnecessary joins
- Avoid unnecessary DISTINCT
- Use appropriate JOIN conditions
- Inspect the execution plan
- Avoid repeated expensive calculations
- Understand table size and data distribution
```

---

# 31. SELECT * vs Specific Columns

Instead of:

```
SELECT *
FROM students
WHERE department = 'IT';
```

prefer:

```
SELECT
    id,
    name,
    cgpa
FROM students
WHERE department = 'IT';
```

when those are the only columns needed.

---

# 32. EXPLAIN

-> `EXPLAIN` shows the query execution plan chosen by the database.

Example:

```
EXPLAIN
SELECT *
FROM students
WHERE department = 'IT';
```

It helps you understand things such as:

```text
- Which scan is being used
- Which indexes may be used
- Join strategy
- Estimated rows
- Estimated cost
```

---

# 33. EXPLAIN ANALYZE — PostgreSQL

-> `EXPLAIN ANALYZE` executes the query and reports actual execution information along with the plan.

```
EXPLAIN ANALYZE
SELECT *
FROM students
WHERE department = 'IT';
```

This is especially useful when investigating real performance.

### Important

Because `EXPLAIN ANALYZE` actually executes the query, be careful with statements that modify data.

For example, don't casually run:

```
EXPLAIN ANALYZE
DELETE FROM students;
```

on production data.

---

# 34. EXPLAIN vs EXPLAIN ANALYZE

| EXPLAIN | EXPLAIN ANALYZE |
|---|---|
| Shows the planned execution strategy | Executes the query and reports actual execution information |
| Uses estimates | Provides actual runtime/row information |
| Useful for inspecting plans | Useful for comparing estimates with reality |
| Does not normally execute the target query | Does execute the target query |

---

# 35. Query Optimization Workflow

A professional workflow:

```text
1. Write a correct query
        ↓
2. Measure the problem
        ↓
3. EXPLAIN the query
        ↓
4. Inspect the execution plan
        ↓
5. Identify bottleneck
        ↓
6. Consider index/query/schema changes
        ↓
7. EXPLAIN ANALYZE
        ↓
8. Compare performance
        ↓
9. Verify the result is still correct
```

Never optimize only because a query "looks complicated."

Measure first.

---

# 36. PHASE 5 → PHASE 8 CONNECTION

```text
PHASE 5 — JOINS
│
├── INNER JOIN
├── LEFT JOIN
├── RIGHT JOIN
└── FULL OUTER JOIN
        ↓
PHASE 6 — INTERMEDIATE
│
├── Subqueries
├── CASE
├── COALESCE
├── UNION
├── CTEs
└── Views
        ↓
PHASE 7 — ADVANCED
│
├── Window Functions
├── PARTITION BY
├── ROW_NUMBER
├── RANK
├── DENSE_RANK
└── LAG / LEAD
        ↓
PHASE 8 — PROFESSIONAL DATABASE SKILLS
│
├── Indexes
├── Transactions
├── ACID
├── Constraints
├── Normalization
├── Query optimization
└── EXPLAIN / EXPLAIN ANALYZE
```

# QUICK REFERENCE

## JOIN

```
INNER JOIN
LEFT JOIN
RIGHT JOIN
FULL OUTER JOIN
```

## INTERMEDIATE

```
Subqueries
CASE
COALESCE
UNION
UNION ALL
CTEs
Views
```

## WINDOW FUNCTIONS

```
OVER()
PARTITION BY
ROW_NUMBER()
RANK()
DENSE_RANK()
LAG()
LEAD()
```

## DATABASE DESIGN

```
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
CHECK
DEFAULT
```

## TRANSACTIONS

```
BEGIN;
COMMIT;
ROLLBACK;
```

## PERFORMANCE

```
CREATE INDEX
DROP INDEX
EXPLAIN
EXPLAIN ANALYZE
```

## FINAL MENTAL MODEL

```text
JOIN
→ combine tables

SUBQUERY
→ query inside query

CASE
→ conditional logic

COALESCE
→ replace NULL with a fallback

UNION
→ combine query results vertically

CTE
→ give a query result a temporary name

VIEW
→ save a query as a virtual table

WINDOW FUNCTION
→ calculate across related rows without collapsing them

PARTITION BY
→ divide window rows into groups

ROW_NUMBER
→ unique sequential numbering

RANK
→ ranking with gaps after ties

DENSE_RANK
→ ranking without gaps after ties

LAG
→ previous row

LEAD
→ next row

INDEX
→ speed up suitable data access

TRANSACTION
→ group operations into one logical unit

ACID
→ reliable transaction properties

CONSTRAINT
→ enforce data rules

NORMALIZATION
→ organize data and reduce unnecessary duplication

EXPLAIN
→ inspect the planned query execution

EXPLAIN ANALYZE
→ execute and inspect actual query performance
```
