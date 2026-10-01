# SQL Fundamentals — PostgreSQL + MySQL
```
Database Management System (DBMS)
│
├── PostgreSQL
└── MySQL
``` 
Both are Relational database management systems (RDBMS).

-----------------------------
### Inside a Database
``` 
Database
│
├── Tables
│   ├── students
│   ├── courses
│   └── departments
│
└── Other database objects
```
### A Table of students look like 
``` 


|  ID  |  Name  |  Age  |  Department  |  CGPA  |
|:----:|:------:|:-----:|:------------:|:------:|
|  1   | Rahul  |  20   |      IT      |  8.5   |
|  2   | Ananya |  21   |     CSE      |  9.1   |
|  3   |  Amit  |  20   |     ECE      |  7.8   |
|  4   | Priya  |  22   |      IT      |  8.9   |
```
---
# Part 1 — Install PostgreSQL
☑ PostgreSQL Server  
☑ pgAdmin 4  
☑ Command Line Tools  
☑ Stack Builder  
password: postgres  
port: 5432

# Part 2 — Understand pgAdmin
```
Servers
└── PostgreSQL ...
    ├── Databases
    ├── Login/Group Roles
    └── Tablespaces  
```

# Part 3 — Install MySQL
Configuration :  
Username: root  
Password: mysql
Port: 3306  

# Part 4 — PostgreSQL vs MySQL
```
PostgreSQL                    SQL
SELECT name                   SELECT name
FROM students;                FROM students;
```
You'll encounter differences later, especially around:
- data types
- auto-increment
- functions
- date/time handling
- JSON
- advanced features
- stored procedures
- administration

# Part 5 — Your First Database
create database sql_learning;
USE sql_learning;

# Part 6 — Create Our First Table
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
# Part 7 — Insert Data
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

|  id  |  name  |  age  |  department  |   city    |  cgpa  |
| :--: | :----: | :--: | :----------: | :-------: | :----: |
|  1   | Rahul  |  20   |      IT      | Mangalore |  8.50  |
|  2   | Ananya |  21   |     CSE      | Bangalore |  9.10  |
|  3   |  Amit  |  20   |     ECE      |  Mysore   |  7.80  |
|  4   | Priya  |  22   |      IT      | Bangalore |  8.90  |
|  5   | Rohan  |  21   |     CSE      | Mangalore |  8.20  |
|  6   | Sneha  |  20   |     EEE      |  Mysore   |  9.30  |
|  7   | Arjun  |  23   |      IT      |   Udupi   |  7.50  |
|  8   |  Neha  |  21   |     CSE      | Bangalore |  8.70  |
|  9   | Kiran  |  22   |     ECE      | Mangalore |  8.10  |
|  10  | Pooja  |  20   |      IT      |   Udupi   |  9.00  |
```
# Part 8 — SELECT
Retrieve data from a table.  
--> SELECT column_name
FROM table_name;

Selecting Multiple Columns  
--> SELECT name, age
FROM students;

Selecting Everything  
--> SELECT *
FROM students;


# Part 9 — WHERE 
filter rows.

SELECT *
FROM students
WHERE department = 'IT';
### Comparison Operators
```
| Operator | Meaning |
|---|---|
| `=` | equal |
| `>` | greater than |
| `<` | less than |
| `>=` | greater than or equal |
| `<=` | less than or equal |
| `<>` | not equal |
| `!=` | not equal |

WHERE + AND
SELECT *
FROM students
WHERE department = 'IT'
AND cgpa > 8.5;

WHERE + OR
SELECT *
FROM students
WHERE department = 'IT'
OR department = 'CSE';
```
# Part 10 — DISTINCT 
### removes duplicate result rows.
SELECT DISTINCT city
FROM students;

### Unique Combination 
SELECT DISTINCT department, city
FROM students;

# Part 11 — LIKE
### pattern matching.
``` 
SELECT *                            Result 
FROM students                       Amit
WHERE name LIKE 'A%';               Ananya
                                    Arjun
What does % mean? Any number of Characters 
| Pattern | Meaning                            |
|---------|------------------------------------|
|  `'A%'` | starts with A                      |
|  `'%A'` | ends with A                        |
| `'%A%'` | contains A                         |
|`'A____'`| A followed by exactly 4 characters |

% vs _ 
% zero or more character
_ means exactly one character 
WHERE name LIKE 'A_i%'
```
# PostgreSQL: ILIKE
``` 
SELECT *
FROM students
WHERE name ILIKE 'a%';
```

# Part 12 — ORDER BY
``` 
SELECT *
FROM students
ORDER BY cgpa;
Explicit ASC ORDERED BY ASC cgpa;
Explicit ASC ORDERED BY DESC cgpa;
--> By default:ASC (Ascending)
```
### ORDER BY Multiple Columns
```
SELECT *
FROM students
ORDER BY department ASC, cgpa DESC;
```
# Part 13 — LIMIT
``` SELECT *
FROM students
LIMIT 3;
```
###  Without ORDER BY, "first 3" is not necessarily a meaningful ranking.
```
SELECT *
FROM students
ORDER BY cgpa DESC
LIMIT 3;```