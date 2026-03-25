# 🗄️ SQL Complete Course Notes — Beginner to Advanced

> **A complete, well-structured guide to SQL and Databases.**
> Covers everything from basic concepts to advanced queries, window functions, stored procedures, and performance optimization.
> Perfect for quick revision before exams or interviews. 🚀

---

## 📚 Table of Contents

1. [Introduction to Databases](#1-introduction-to-databases)
2. [Introduction to SQL](#2-introduction-to-sql)
3. [Setting Up the Environment](#3-setting-up-the-environment)
4. [SQL Data Types](#4-sql-data-types)
5. [DDL — Creating & Managing Tables](#5-ddl--creating--managing-tables)
6. [DML — Inserting, Updating & Deleting Data](#6-dml--inserting-updating--deleting-data)
7. [DQL — Querying Data (SELECT)](#7-dql--querying-data-select)
8. [Filtering Data — WHERE Clause](#8-filtering-data--where-clause)
9. [Sorting Data — ORDER BY](#9-sorting-data--order-by)
10. [Aggregate Functions](#10-aggregate-functions)
11. [GROUP BY & HAVING](#11-group-by--having)
12. [JOINS](#12-joins)
13. [Subqueries](#13-subqueries)
14. [Set Operators — UNION, INTERSECT, EXCEPT](#14-set-operators--union-intersect-except)
15. [SQL Functions — String, Date, Numeric](#15-sql-functions--string-date-numeric)
16. [NULL Handling](#16-null-handling)
17. [Views](#17-views)
18. [Indexes](#18-indexes)
19. [Stored Procedures](#19-stored-procedures)
20. [Triggers](#20-triggers)
21. [Transactions & ACID Properties](#21-transactions--acid-properties)
22. [Window Functions (Advanced)](#22-window-functions-advanced)
23. [CTEs — Common Table Expressions](#23-ctes--common-table-expressions)
24. [Database Design & Normalization](#24-database-design--normalization)
25. [Constraints & Keys](#25-constraints--keys)
26. [DCL — User Permissions & Security](#26-dcl--user-permissions--security)
27. [Performance Optimization](#27-performance-optimization)
28. [Interview Questions Cheatsheet](#28-interview-questions-cheatsheet)

---

## 1. Introduction to Databases

### What is a Database?
A **database** is an organized collection of structured data stored electronically so it can be easily accessed, managed, and updated.

**Real-life examples:**
- A hospital stores patient records in a database.
- Amazon stores product listings, orders, and user data in databases.
- A school stores student grades and attendance in a database.

### Types of Databases

| Type | Description | Example |
|------|-------------|---------|
| **Relational (RDBMS)** | Data stored in tables with rows & columns | MySQL, PostgreSQL, SQL Server, Oracle |
| **NoSQL** | Data stored as documents, key-value pairs, graphs | MongoDB, Redis, Cassandra |
| **In-Memory** | Data stored in RAM for speed | Redis, Memcached |
| **Cloud** | Hosted on cloud platforms | Amazon RDS, Google BigQuery |

### What is an RDBMS?
**Relational Database Management System (RDBMS)** stores data in **tables** that are related to each other through **keys**.

```
Database
 └── Tables (like spreadsheets)
       └── Rows    = Records / Data entries
       └── Columns = Fields / Attributes
```

---

## 2. Introduction to SQL

### What is SQL?
**SQL (Structured Query Language)** is the standard language used to communicate with a relational database. It lets you:
- **Create** databases and tables
- **Read** (retrieve) data
- **Update** existing data
- **Delete** data

> 💡 SQL is pronounced **"sequel"** or **"S-Q-L"** — both are correct!

### SQL Sub-languages

| Category | Full Name | Purpose | Commands |
|----------|-----------|---------|----------|
| **DDL** | Data Definition Language | Define/modify structure | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| **DML** | Data Manipulation Language | Modify data | `INSERT`, `UPDATE`, `DELETE` |
| **DQL** | Data Query Language | Retrieve data | `SELECT` |
| **DCL** | Data Control Language | Manage permissions | `GRANT`, `REVOKE` |
| **TCL** | Transaction Control Language | Manage transactions | `COMMIT`, `ROLLBACK`, `SAVEPOINT` |

### SQL Execution Order (Important for Interviews!)

```
FROM       → Which table(s)?
JOIN       → Combine tables
WHERE      → Filter rows (before grouping)
GROUP BY   → Group rows
HAVING     → Filter groups (after grouping)
SELECT     → Choose columns
DISTINCT   → Remove duplicates
ORDER BY   → Sort results
LIMIT      → Limit number of rows
```

> ⚠️ **Pro Tip:** Even though you write `SELECT` first, SQL processes `FROM` first! This is why you can't use aliases in a `WHERE` clause.

---

## 3. Setting Up the Environment

### Installing MySQL (Recommended for Beginners)

1. Download **MySQL Community Server** from [mysql.com](https://mysql.com)
2. Install **MySQL Workbench** (GUI tool)
3. Or use online tools: [db-fiddle.com](https://www.db-fiddle.com), [sqlfiddle.com](http://sqlfiddle.com)

### Popular SQL Tools

| Tool | Description |
|------|-------------|
| **MySQL Workbench** | GUI for MySQL |
| **pgAdmin** | GUI for PostgreSQL |
| **DBeaver** | Universal DB tool (works with any DB) |
| **VS Code** + SQL Extension | Lightweight option |
| **DB Browser for SQLite** | Great for learning |

### Your First SQL Query

```sql
SELECT 'Hello, World!' AS greeting;
```

**Output:**
```
+---------------+
| greeting      |
+---------------+
| Hello, World! |
+---------------+
```

---

## 4. SQL Data Types

### Common Data Types

```
TEXT / STRING Types:
├── CHAR(n)       → Fixed-length string. e.g., CHAR(10) always 10 chars
├── VARCHAR(n)    → Variable-length string. e.g., VARCHAR(255) up to 255 chars
└── TEXT          → Long text (no size limit)

NUMERIC Types:
├── INT / INTEGER → Whole numbers. e.g., 1, 100, -50
├── BIGINT        → Very large whole numbers
├── FLOAT         → Decimal numbers (less precise)
├── DECIMAL(p,s)  → Exact decimal. e.g., DECIMAL(10,2) for money
└── BOOLEAN       → TRUE or FALSE

DATE / TIME Types:
├── DATE          → YYYY-MM-DD  e.g., 2024-01-15
├── TIME          → HH:MM:SS   e.g., 14:30:00
├── DATETIME      → Date + Time
└── TIMESTAMP     → Date + Time (auto-updates)
```

### Choosing the Right Data Type

| Use Case | Data Type |
|----------|-----------|
| Name, Email | `VARCHAR(255)` |
| Age, Count | `INT` |
| Price, Salary | `DECIMAL(10, 2)` |
| Yes/No flag | `BOOLEAN` |
| Birth date | `DATE` |
| Long description | `TEXT` |
| Phone number | `VARCHAR(20)` (not INT — no math needed) |

> 💡 **Pro Tip:** Always use `DECIMAL` for money — never `FLOAT`, because floating-point math can cause tiny rounding errors!

---

## 5. DDL — Creating & Managing Tables

### Creating a Database

```sql
CREATE DATABASE school;

-- Switch to the database
USE school;
```

### Creating a Table

```sql
CREATE TABLE students (
    student_id   INT          PRIMARY KEY AUTO_INCREMENT,
    first_name   VARCHAR(50)  NOT NULL,
    last_name    VARCHAR(50)  NOT NULL,
    email        VARCHAR(100) UNIQUE,
    date_of_birth DATE,
    grade        CHAR(2),
    enrolled_at  TIMESTAMP    DEFAULT CURRENT_TIMESTAMP
);
```

**Explanation:**
- `PRIMARY KEY` → Unique identifier for each row
- `AUTO_INCREMENT` → Automatically increases the ID (1, 2, 3…)
- `NOT NULL` → This column cannot be empty
- `UNIQUE` → No two rows can have the same value
- `DEFAULT` → Value used if no value is provided

### Viewing Table Structure

```sql
DESCRIBE students;
-- or
DESC students;
```

### Modifying a Table (ALTER)

```sql
-- Add a new column
ALTER TABLE students ADD phone VARCHAR(20);

-- Rename a column
ALTER TABLE students RENAME COLUMN phone TO mobile;

-- Change column data type
ALTER TABLE students MODIFY COLUMN grade VARCHAR(5);

-- Drop a column
ALTER TABLE students DROP COLUMN mobile;
```

### Deleting Tables

```sql
-- Delete the table AND all its data permanently
DROP TABLE students;

-- Delete all data but keep the table structure
TRUNCATE TABLE students;
```

### Renaming a Table

```sql
RENAME TABLE students TO learners;
```

> ⚠️ **Pro Tip:** `DROP` removes the table entirely. `TRUNCATE` removes data but keeps the structure. `DELETE` (DML) removes rows one-by-one and can be rolled back!

---

## 6. DML — Inserting, Updating & Deleting Data

### INSERT — Add New Rows

```sql
-- Insert one row
INSERT INTO students (first_name, last_name, email, date_of_birth, grade)
VALUES ('Alice', 'Johnson', 'alice@email.com', '2000-05-15', 'A');

-- Insert multiple rows at once
INSERT INTO students (first_name, last_name, email, grade)
VALUES
    ('Bob',   'Smith',   'bob@email.com',   'B'),
    ('Carol', 'White',   'carol@email.com', 'A'),
    ('David', 'Brown',   'david@email.com', 'C');
```

### UPDATE — Modify Existing Rows

```sql
-- Update one student's grade
UPDATE students
SET grade = 'A+'
WHERE student_id = 2;

-- Update multiple columns at once
UPDATE students
SET grade = 'B', email = 'newemail@email.com'
WHERE student_id = 3;
```

> ⚠️ **ALWAYS use WHERE with UPDATE!** Without it, you'll update ALL rows in the table!

### DELETE — Remove Rows

```sql
-- Delete a specific student
DELETE FROM students
WHERE student_id = 4;

-- Delete all students with grade 'F'
DELETE FROM students
WHERE grade = 'F';
```

> ⚠️ **ALWAYS use WHERE with DELETE!** `DELETE FROM students;` (without WHERE) deletes ALL data!

---

## 7. DQL — Querying Data (SELECT)

### Basic SELECT

```sql
-- Get all columns and all rows
SELECT * FROM students;

-- Get specific columns only
SELECT first_name, last_name, grade FROM students;
```

### Column Aliases (AS)

```sql
SELECT
    first_name AS "First Name",
    last_name  AS "Last Name",
    grade      AS "Score"
FROM students;
```

**Output:**
```
+------------+-----------+-------+
| First Name | Last Name | Score |
+------------+-----------+-------+
| Alice      | Johnson   | A     |
| Bob        | Smith     | B     |
+------------+-----------+-------+
```

### DISTINCT — Remove Duplicates

```sql
-- Get unique grades (no repeats)
SELECT DISTINCT grade FROM students;
```

### LIMIT — Control Number of Rows

```sql
-- Get only the first 5 students
SELECT * FROM students LIMIT 5;

-- Get students 6 to 10 (skip first 5)
SELECT * FROM students LIMIT 5 OFFSET 5;
```

---

## 8. Filtering Data — WHERE Clause

### Comparison Operators

```sql
SELECT * FROM students WHERE grade = 'A';     -- Equal
SELECT * FROM students WHERE grade != 'F';    -- Not equal
SELECT * FROM students WHERE student_id > 3;  -- Greater than
SELECT * FROM students WHERE student_id >= 3; -- Greater than or equal
SELECT * FROM students WHERE student_id < 10; -- Less than
```

### Logical Operators (AND, OR, NOT)

```sql
-- Students with grade A AND enrolled in 2024
SELECT * FROM students
WHERE grade = 'A' AND YEAR(enrolled_at) = 2024;

-- Students with grade A OR grade B
SELECT * FROM students
WHERE grade = 'A' OR grade = 'B';

-- Students who are NOT grade F
SELECT * FROM students
WHERE NOT grade = 'F';
```

### BETWEEN — Range Filter

```sql
-- Students with IDs between 5 and 10
SELECT * FROM students
WHERE student_id BETWEEN 5 AND 10;

-- Students born in the 2000s
SELECT * FROM students
WHERE date_of_birth BETWEEN '2000-01-01' AND '2009-12-31';
```

### IN — Multiple Values

```sql
-- Students with grade A, B, or C (cleaner than multiple OR)
SELECT * FROM students
WHERE grade IN ('A', 'B', 'C');

-- Students NOT in grade D or F
SELECT * FROM students
WHERE grade NOT IN ('D', 'F');
```

### LIKE — Pattern Matching

```sql
-- Names starting with 'A'
SELECT * FROM students WHERE first_name LIKE 'A%';

-- Names ending with 'son'
SELECT * FROM students WHERE last_name LIKE '%son';

-- Names with exactly 5 characters
SELECT * FROM students WHERE first_name LIKE '_____';

-- Names containing 'ar' anywhere
SELECT * FROM students WHERE first_name LIKE '%ar%';
```

**Pattern symbols:**
- `%` → Matches any number of characters (including zero)
- `_` → Matches exactly one character

---

## 9. Sorting Data — ORDER BY

```sql
-- Sort by last name A to Z (ascending is default)
SELECT * FROM students ORDER BY last_name ASC;

-- Sort by grade Z to A (descending)
SELECT * FROM students ORDER BY grade DESC;

-- Sort by grade first, then by name
SELECT * FROM students ORDER BY grade ASC, last_name ASC;
```

---

## 10. Aggregate Functions

Aggregate functions perform a **calculation on a group of rows** and return a **single value**.

| Function | Description | Example |
|----------|-------------|---------|
| `COUNT()` | Count number of rows | `COUNT(*)` |
| `SUM()` | Add up values | `SUM(salary)` |
| `AVG()` | Calculate average | `AVG(score)` |
| `MIN()` | Find smallest value | `MIN(price)` |
| `MAX()` | Find largest value | `MAX(age)` |

```sql
-- How many students are there?
SELECT COUNT(*) AS total_students FROM students;

-- What is the average grade score?
SELECT AVG(score) AS avg_score FROM results;

-- Highest and lowest scores
SELECT MAX(score) AS highest, MIN(score) AS lowest FROM results;

-- Total salary bill
SELECT SUM(salary) AS total_payroll FROM employees;
```

> 💡 **Pro Tip:** `COUNT(*)` counts all rows including NULLs. `COUNT(column_name)` skips NULL values.

---

## 11. GROUP BY & HAVING

### GROUP BY — Group Rows Together

```sql
-- Count students per grade
SELECT grade, COUNT(*) AS num_students
FROM students
GROUP BY grade;
```

**Output:**
```
+-------+--------------+
| grade | num_students |
+-------+--------------+
| A     | 12           |
| B     | 18           |
| C     | 7            |
+-------+--------------+
```

```sql
-- Average salary per department
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

### HAVING — Filter Groups

`WHERE` filters **rows** before grouping. `HAVING` filters **groups** after grouping.

```sql
-- Only show grades that have more than 5 students
SELECT grade, COUNT(*) AS num_students
FROM students
GROUP BY grade
HAVING COUNT(*) > 5;

-- Departments with average salary above 50000
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

### WHERE vs HAVING

```
WHERE  → Filters individual rows → Runs BEFORE GROUP BY
HAVING → Filters groups         → Runs AFTER  GROUP BY
```

```sql
-- WHERE + GROUP BY + HAVING together
SELECT department, AVG(salary) AS avg_salary
FROM employees
WHERE hire_date > '2020-01-01'   -- Only recent hires
GROUP BY department
HAVING AVG(salary) > 60000;      -- Only high-paying departments
```

---

## 12. JOINS

**JOINs** are used to combine rows from two or more tables based on a related column.

### Sample Tables

**employees**
```
+----+-------+--------+---------------+
| id | name  | salary | department_id |
+----+-------+--------+---------------+
|  1 | Alice | 70000  |       1       |
|  2 | Bob   | 55000  |       2       |
|  3 | Carol | 80000  |       1       |
|  4 | David | 60000  |    NULL       |
+----+-------+--------+---------------+
```

**departments**
```
+----+-------------+
| id | dept_name   |
+----+-------------+
|  1 | Engineering |
|  2 | Marketing   |
|  3 | HR          |
+----+-------------+
```

---

### INNER JOIN — Only Matching Rows

Returns rows that have matching values **in both tables**.

```sql
SELECT e.name, e.salary, d.dept_name
FROM employees e
INNER JOIN departments d ON e.department_id = d.id;
```

**Result:** Alice, Carol → Engineering | Bob → Marketing | David → **excluded** (no dept)

---

### LEFT JOIN — All Left + Matching Right

Returns **all rows from the left table**, and matching rows from the right. Non-matching right rows get NULL.

```sql
SELECT e.name, d.dept_name
FROM employees e
LEFT JOIN departments d ON e.department_id = d.id;
```

**Result:** All 4 employees shown. David gets NULL for dept_name. HR is excluded.

---

### RIGHT JOIN — All Right + Matching Left

Returns **all rows from the right table**, and matching rows from the left.

```sql
SELECT e.name, d.dept_name
FROM employees e
RIGHT JOIN departments d ON e.department_id = d.id;
```

**Result:** HR appears with NULL name (no employee is in HR).

---

### FULL OUTER JOIN — All Rows From Both

Returns all rows from both tables. NULLs where there's no match.

```sql
SELECT e.name, d.dept_name
FROM employees e
FULL OUTER JOIN departments d ON e.department_id = d.id;
```

> ⚠️ **MySQL does not support FULL OUTER JOIN directly.** Use UNION of LEFT JOIN + RIGHT JOIN:

```sql
SELECT e.name, d.dept_name
FROM employees e LEFT JOIN departments d ON e.department_id = d.id
UNION
SELECT e.name, d.dept_name
FROM employees e RIGHT JOIN departments d ON e.department_id = d.id;
```

---

### SELF JOIN — Join Table with Itself

Useful for hierarchical data (e.g., employees and their managers).

```sql
-- Find each employee and their manager's name
SELECT
    e.name AS employee,
    m.name AS manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.id;
```

---

### JOIN Type Diagram

```
INNER JOIN:      LEFT JOIN:       RIGHT JOIN:      FULL JOIN:
  [A ∩ B]       [All A + B∩A]   [All B + A∩B]    [All A + All B]
  ┌──┬──┐        ┌──┬──┐          ┌──┬──┐           ┌──┬──┐
  │  │██│        │██│██│          │  │██│           │██│██│
  │  │██│        │██│██│          │  │██│           │██│██│
  └──┴──┘        └──┴──┘          └──┴──┘           └──┴──┘
```

> 💡 **Pro Tip:** Always use table **aliases** (`e`, `d`) to make JOIN queries shorter and more readable.

---

## 13. Subqueries

A **subquery** is a query inside another query. The inner query runs first.

### Subquery in WHERE

```sql
-- Find employees who earn more than the average salary
SELECT name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

### Subquery in FROM (Derived Table)

```sql
-- Use the result of a subquery as a table
SELECT dept_name, avg_salary
FROM (
    SELECT department_id, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
) AS dept_averages
JOIN departments d ON dept_averages.department_id = d.id;
```

### Subquery in SELECT (Correlated)

```sql
-- Show each employee with their department's average salary
SELECT
    name,
    salary,
    (SELECT AVG(salary) FROM employees e2
     WHERE e2.department_id = e1.department_id) AS dept_avg
FROM employees e1;
```

### EXISTS — Check If Subquery Returns Rows

```sql
-- Departments that have at least one employee
SELECT dept_name
FROM departments d
WHERE EXISTS (
    SELECT 1 FROM employees e WHERE e.department_id = d.id
);
```

---

## 14. Set Operators — UNION, INTERSECT, EXCEPT

These combine results of two SELECT queries.

### UNION — Combine + Remove Duplicates

```sql
SELECT name FROM employees_2023
UNION
SELECT name FROM employees_2024;
```

### UNION ALL — Combine + Keep Duplicates

```sql
SELECT name FROM employees_2023
UNION ALL
SELECT name FROM employees_2024;
```

### INTERSECT — Only Common Rows

```sql
-- Names that appear in BOTH years
SELECT name FROM employees_2023
INTERSECT
SELECT name FROM employees_2024;
```

### EXCEPT / MINUS — Rows Only in First Query

```sql
-- Names in 2023 but NOT in 2024 (people who left)
SELECT name FROM employees_2023
EXCEPT
SELECT name FROM employees_2024;
```

> ⚠️ `INTERSECT` and `EXCEPT` are not supported in all MySQL versions. Use JOINs as alternatives.

---

## 15. SQL Functions — String, Date, Numeric

### String Functions

```sql
-- Convert to uppercase / lowercase
SELECT UPPER('hello');        -- HELLO
SELECT LOWER('HELLO');        -- hello

-- Length of a string
SELECT LENGTH('Hello');       -- 5

-- Extract part of a string
SELECT SUBSTRING('Hello World', 1, 5);  -- Hello

-- Remove spaces
SELECT TRIM('  hello  ');     -- hello

-- Replace text
SELECT REPLACE('Hello World', 'World', 'SQL');  -- Hello SQL

-- Combine strings
SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM students;

-- Reverse a string
SELECT REVERSE('SQL');        -- LQS

-- Find position of a substring
SELECT INSTR('Hello World', 'World');  -- 7
```

### Date Functions

```sql
-- Current date and time
SELECT NOW();                  -- 2024-01-15 14:30:00
SELECT CURDATE();              -- 2024-01-15
SELECT CURTIME();              -- 14:30:00

-- Extract parts of a date
SELECT YEAR('2024-01-15');     -- 2024
SELECT MONTH('2024-01-15');    -- 1
SELECT DAY('2024-01-15');      -- 15

-- Add/subtract time
SELECT DATE_ADD('2024-01-15', INTERVAL 30 DAY);   -- 2024-02-14
SELECT DATE_SUB('2024-01-15', INTERVAL 1 MONTH);  -- 2023-12-15

-- Difference between dates
SELECT DATEDIFF('2024-12-31', '2024-01-01');  -- 365

-- Format a date
SELECT DATE_FORMAT(NOW(), '%d/%m/%Y');  -- 15/01/2024
```

### Numeric Functions

```sql
SELECT ROUND(3.14159, 2);     -- 3.14
SELECT CEIL(4.1);             -- 5  (always round UP)
SELECT FLOOR(4.9);            -- 4  (always round DOWN)
SELECT ABS(-15);              -- 15 (absolute value)
SELECT MOD(10, 3);            -- 1  (remainder)
SELECT POWER(2, 8);           -- 256
SELECT SQRT(144);             -- 12
```

### Conditional Functions

```sql
-- IF: Simple condition
SELECT name, IF(salary > 60000, 'High', 'Low') AS pay_level
FROM employees;

-- CASE: Multiple conditions (like if-else)
SELECT name,
    CASE
        WHEN salary > 80000 THEN 'Senior'
        WHEN salary > 60000 THEN 'Mid-level'
        WHEN salary > 40000 THEN 'Junior'
        ELSE 'Intern'
    END AS seniority
FROM employees;
```

---

## 16. NULL Handling

`NULL` means **no value / unknown**. It is NOT zero, NOT an empty string.

### Checking for NULL

```sql
-- Wrong: This does NOT work
SELECT * FROM employees WHERE manager_id = NULL;

-- Correct: Use IS NULL
SELECT * FROM employees WHERE manager_id IS NULL;

-- Employees who DO have a manager
SELECT * FROM employees WHERE manager_id IS NOT NULL;
```

### COALESCE — Return First Non-NULL Value

```sql
-- Show phone, or mobile if phone is null, or 'N/A' if both null
SELECT name, COALESCE(phone, mobile, 'N/A') AS contact
FROM employees;
```

### IFNULL — Replace NULL with a Default

```sql
-- Replace NULL bonus with 0
SELECT name, IFNULL(bonus, 0) AS bonus
FROM employees;
```

### NULLIF — Return NULL if Two Values Are Equal

```sql
-- Avoid divide-by-zero errors
SELECT total_sales / NULLIF(total_orders, 0) AS avg_order_value
FROM sales_data;
```

---

## 17. Views

A **View** is a saved SQL query that acts like a virtual table. It doesn't store data itself — it just stores the query.

### Creating a View

```sql
CREATE VIEW high_earners AS
SELECT name, salary, department_id
FROM employees
WHERE salary > 70000;
```

### Using a View

```sql
-- Query the view like a regular table
SELECT * FROM high_earners;
SELECT name FROM high_earners WHERE department_id = 1;
```

### Updating a View

```sql
CREATE OR REPLACE VIEW high_earners AS
SELECT name, salary, department_id
FROM employees
WHERE salary > 80000;
```

### Dropping a View

```sql
DROP VIEW high_earners;
```

**Real-world use cases:**
- Simplify complex queries for reporting
- Restrict sensitive columns (e.g., hide salary from regular users)
- Reuse common query logic across applications

---

## 18. Indexes

An **Index** speeds up data retrieval. Think of it like a book's index page — instead of reading every page, you jump straight to the right one.

### Creating an Index

```sql
-- Create index on email column (speeds up WHERE email = ...)
CREATE INDEX idx_email ON students(email);

-- Create index on multiple columns
CREATE INDEX idx_name ON students(last_name, first_name);
```

### Unique Index

```sql
-- Ensures no duplicate values (similar to UNIQUE constraint)
CREATE UNIQUE INDEX idx_unique_email ON students(email);
```

### Dropping an Index

```sql
DROP INDEX idx_email ON students;
```

### When to Use Indexes

| Use Index | Don't Use Index |
|-----------|-----------------|
| Columns used in WHERE | Small tables |
| Columns used in JOINs | Columns rarely searched |
| Columns used in ORDER BY | Columns updated very frequently |
| Columns with many unique values | |

> ⚠️ **Pro Tip:** Indexes speed up **reads** but slow down **writes** (INSERT/UPDATE/DELETE) because the index must be updated too. Don't over-index!

---

## 19. Stored Procedures

A **Stored Procedure** is a reusable block of SQL code saved in the database. You write it once and call it many times.

### Creating a Stored Procedure

```sql
DELIMITER $$

CREATE PROCEDURE GetStudentsByGrade(IN grade_param CHAR(2))
BEGIN
    SELECT first_name, last_name, grade
    FROM students
    WHERE grade = grade_param;
END $$

DELIMITER ;
```

### Calling a Stored Procedure

```sql
CALL GetStudentsByGrade('A');
```

### Procedure with OUT Parameter

```sql
DELIMITER $$

CREATE PROCEDURE GetStudentCount(
    IN  grade_param CHAR(2),
    OUT total       INT
)
BEGIN
    SELECT COUNT(*) INTO total
    FROM students
    WHERE grade = grade_param;
END $$

DELIMITER ;

-- Usage:
CALL GetStudentCount('A', @count);
SELECT @count;
```

### Variables in Procedures

```sql
DELIMITER $$

CREATE PROCEDURE CalculateBonus(IN emp_id INT)
BEGIN
    DECLARE emp_salary  DECIMAL(10,2);
    DECLARE bonus_amount DECIMAL(10,2);

    SELECT salary INTO emp_salary FROM employees WHERE id = emp_id;
    SET bonus_amount = emp_salary * 0.10;

    SELECT emp_salary, bonus_amount;
END $$

DELIMITER ;
```

### Drop a Stored Procedure

```sql
DROP PROCEDURE IF EXISTS GetStudentsByGrade;
```

---

## 20. Triggers

A **Trigger** is SQL code that automatically runs **before** or **after** an INSERT, UPDATE, or DELETE on a table.

### Creating an AFTER INSERT Trigger

```sql
DELIMITER $$

CREATE TRIGGER after_student_insert
AFTER INSERT ON students
FOR EACH ROW
BEGIN
    INSERT INTO audit_log (action, student_id, action_time)
    VALUES ('INSERT', NEW.student_id, NOW());
END $$

DELIMITER ;
```

- `NEW` → Refers to the new row being inserted/updated
- `OLD` → Refers to the old row before update/delete

### BEFORE UPDATE Trigger

```sql
DELIMITER $$

CREATE TRIGGER before_salary_update
BEFORE UPDATE ON employees
FOR EACH ROW
BEGIN
    IF NEW.salary < 0 THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Salary cannot be negative';
    END IF;
END $$

DELIMITER ;
```

### Trigger Timing

| Timing | Event | Use Case |
|--------|-------|----------|
| BEFORE INSERT | Adding data | Validate data before saving |
| AFTER INSERT | Data added | Log the action |
| BEFORE UPDATE | Changing data | Prevent invalid changes |
| AFTER UPDATE | Data changed | Update related tables |
| BEFORE DELETE | Removing data | Archive before delete |
| AFTER DELETE | Data removed | Clean up related records |

---

## 21. Transactions & ACID Properties

### What is a Transaction?
A **transaction** is a group of SQL operations that must ALL succeed or ALL fail together.

**Real-world example:** Bank transfer
- Step 1: Deduct $500 from Account A
- Step 2: Add $500 to Account B

If Step 1 succeeds but Step 2 fails — that's a disaster! Transactions prevent this.

### Transaction Commands

```sql
START TRANSACTION;

UPDATE accounts SET balance = balance - 500 WHERE account_id = 1;
UPDATE accounts SET balance = balance + 500 WHERE account_id = 2;

-- If everything went well:
COMMIT;

-- If something went wrong:
ROLLBACK;
```

### SAVEPOINT

```sql
START TRANSACTION;

INSERT INTO orders VALUES (1, 'Product A', 100);
SAVEPOINT sp1;

INSERT INTO orders VALUES (2, 'Product B', 200);
SAVEPOINT sp2;

-- Oops, second insert was wrong — rollback to sp1 only
ROLLBACK TO sp1;

COMMIT;
```

### ACID Properties

| Property | Meaning | Example |
|----------|---------|---------|
| **A**tomicity | All or nothing | Bank transfer: either both updates happen or neither |
| **C**onsistency | Data stays valid | Balance can never go negative |
| **I**solation | Transactions don't interfere | Two users can't edit same record simultaneously |
| **D**urability | Committed changes are permanent | Power cut won't lose committed data |

---

## 22. Window Functions (Advanced)

**Window functions** perform calculations across a set of rows **related to the current row** — without collapsing rows like GROUP BY does.

```
Syntax:
function_name() OVER (
    PARTITION BY column   -- like GROUP BY for the window
    ORDER BY column       -- sort within the window
    ROWS/RANGE ...        -- frame size
)
```

### ROW_NUMBER — Assign Row Numbers

```sql
SELECT
    name,
    department_id,
    salary,
    ROW_NUMBER() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rank_in_dept
FROM employees;
```

**Output:**
```
+-------+---------------+--------+--------------+
| name  | department_id | salary | rank_in_dept |
+-------+---------------+--------+--------------+
| Carol |       1       | 80000  |      1       |
| Alice |       1       | 70000  |      2       |
| Bob   |       2       | 55000  |      1       |
+-------+---------------+--------+--------------+
```

### RANK vs DENSE_RANK vs ROW_NUMBER

```sql
SELECT name, salary,
    ROW_NUMBER()  OVER (ORDER BY salary DESC) AS row_num,
    RANK()        OVER (ORDER BY salary DESC) AS rank_val,
    DENSE_RANK()  OVER (ORDER BY salary DESC) AS dense_rank_val
FROM employees;
```

| salary | ROW_NUMBER | RANK | DENSE_RANK |
|--------|-----------|------|------------|
| 80000  | 1         | 1    | 1          |
| 70000  | 2         | 2    | 2          |
| 70000  | 3         | 2    | 2          |
| 55000  | 4         | 4    | 3          |

- `ROW_NUMBER` → Always unique (1,2,3,4)
- `RANK` → Same rank for ties, then skips (1,2,2,4)
- `DENSE_RANK` → Same rank for ties, no gaps (1,2,2,3)

### LAG & LEAD — Access Previous/Next Row

```sql
SELECT
    name,
    salary,
    LAG(salary, 1)  OVER (ORDER BY salary) AS prev_salary,
    LEAD(salary, 1) OVER (ORDER BY salary) AS next_salary
FROM employees;
```

### SUM / AVG as Window Functions

```sql
-- Running total of salary
SELECT name, salary,
    SUM(salary) OVER (ORDER BY name) AS running_total
FROM employees;

-- Each employee's salary vs department average
SELECT name, salary,
    AVG(salary) OVER (PARTITION BY department_id) AS dept_avg
FROM employees;
```

---

## 23. CTEs — Common Table Expressions

A **CTE** (using `WITH`) creates a temporary named result set that you can reference in the main query. It makes complex queries much more readable.

### Basic CTE

```sql
WITH high_earners AS (
    SELECT name, salary, department_id
    FROM employees
    WHERE salary > 70000
)
SELECT * FROM high_earners
WHERE department_id = 1;
```

### Multiple CTEs

```sql
WITH
dept_avg AS (
    SELECT department_id, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
),
above_avg AS (
    SELECT e.name, e.salary, e.department_id
    FROM employees e
    JOIN dept_avg d ON e.department_id = d.department_id
    WHERE e.salary > d.avg_salary
)
SELECT * FROM above_avg;
```

### Recursive CTE — For Hierarchical Data

```sql
-- Traverse employee hierarchy (who reports to whom)
WITH RECURSIVE org_chart AS (
    -- Base case: top-level managers (no manager)
    SELECT id, name, manager_id, 0 AS level
    FROM employees
    WHERE manager_id IS NULL

    UNION ALL

    -- Recursive case: employees reporting to someone
    SELECT e.id, e.name, e.manager_id, oc.level + 1
    FROM employees e
    JOIN org_chart oc ON e.manager_id = oc.id
)
SELECT * FROM org_chart ORDER BY level;
```

**CTE vs Subquery:**
- CTE is more **readable** and **reusable** within the same query
- CTE can be **recursive** (subqueries cannot)
- Performance is usually similar

---

## 24. Database Design & Normalization

### Entity-Relationship (ER) Concepts

- **Entity** → A real-world object (Student, Course, Employee)
- **Attribute** → Property of an entity (Student has name, email, DOB)
- **Relationship** → How entities are linked (Student **enrolls in** Course)

### Types of Relationships

```
One-to-One (1:1)
  A person has one passport
  
One-to-Many (1:N)
  A department has many employees
  
Many-to-Many (M:N)
  A student can enroll in many courses
  A course can have many students
  → Needs a JUNCTION TABLE (enrollment table)
```

### Normalization

Normalization is the process of organizing tables to **reduce data redundancy** and **improve data integrity**.

---

#### 1NF — First Normal Form
**Rule:** Each column must contain **atomic (single) values**. No repeating groups.

❌ **Unnormalized:**
```
+----+-------+---------------------------+
| id | name  | subjects                  |
+----+-------+---------------------------+
|  1 | Alice | Math, Science, English    |
+----+-------+---------------------------+
```

✅ **1NF:**
```
+----+-------+---------+
| id | name  | subject |
+----+-------+---------+
|  1 | Alice | Math    |
|  1 | Alice | Science |
|  1 | Alice | English |
+----+-------+---------+
```

---

#### 2NF — Second Normal Form
**Rule:** Must be in 1NF + every non-key column must depend on the **entire primary key** (no partial dependency).

---

#### 3NF — Third Normal Form
**Rule:** Must be in 2NF + no **transitive dependencies** (non-key column should not depend on another non-key column).

---

#### BCNF — Boyce-Codd Normal Form
Stricter version of 3NF — every determinant must be a candidate key.

> 💡 **Pro Tip:** For most real applications, achieving **3NF is sufficient**. Over-normalization can hurt performance.

---

## 25. Constraints & Keys

### Types of Keys

| Key | Description |
|-----|-------------|
| **Primary Key** | Uniquely identifies each row. NOT NULL + UNIQUE. Only one per table. |
| **Foreign Key** | Links one table to another. References Primary Key of another table. |
| **Unique Key** | Ensures all values in a column are unique (but allows one NULL). |
| **Composite Key** | Primary key made of multiple columns. |
| **Candidate Key** | Any column that could be a primary key. |

### Defining Constraints

```sql
CREATE TABLE orders (
    order_id    INT          PRIMARY KEY AUTO_INCREMENT,
    customer_id INT          NOT NULL,
    product_id  INT          NOT NULL,
    quantity    INT          DEFAULT 1,
    price       DECIMAL(10,2) CHECK (price > 0),
    status      VARCHAR(20)  DEFAULT 'pending',

    FOREIGN KEY (customer_id) REFERENCES customers(id) ON DELETE CASCADE,
    FOREIGN KEY (product_id)  REFERENCES products(id)  ON DELETE RESTRICT
);
```

### ON DELETE Options for Foreign Keys

| Option | Behavior |
|--------|----------|
| `CASCADE` | Delete child rows when parent is deleted |
| `SET NULL` | Set foreign key to NULL when parent is deleted |
| `RESTRICT` | Prevent deletion of parent if child rows exist |
| `NO ACTION` | Same as RESTRICT in most databases |

---

## 26. DCL — User Permissions & Security

### Create a User

```sql
CREATE USER 'alice'@'localhost' IDENTIFIED BY 'SecurePassword123!';
```

### Grant Permissions

```sql
-- Grant SELECT only (read-only user)
GRANT SELECT ON school.* TO 'alice'@'localhost';

-- Grant all permissions on one database
GRANT ALL PRIVILEGES ON school.* TO 'alice'@'localhost';

-- Apply changes
FLUSH PRIVILEGES;
```

### Revoke Permissions

```sql
REVOKE SELECT ON school.* FROM 'alice'@'localhost';
```

### Show User Permissions

```sql
SHOW GRANTS FOR 'alice'@'localhost';
```

### Drop a User

```sql
DROP USER 'alice'@'localhost';
```

---

## 27. Performance Optimization

### Use EXPLAIN to Analyze Queries

```sql
EXPLAIN SELECT * FROM employees WHERE department_id = 1;
```

This shows how MySQL executes your query — whether it uses an index or scans the whole table.

### Key Optimization Tips

**1. Use indexes on frequently searched columns**
```sql
CREATE INDEX idx_dept ON employees(department_id);
```

**2. Avoid SELECT \* — fetch only what you need**
```sql
-- Bad:
SELECT * FROM employees;

-- Good:
SELECT name, salary FROM employees;
```

**3. Use LIMIT to restrict result sets**
```sql
SELECT * FROM logs ORDER BY created_at DESC LIMIT 100;
```

**4. Avoid functions on indexed columns in WHERE**
```sql
-- Bad: Index on date_of_birth is NOT used
SELECT * FROM students WHERE YEAR(date_of_birth) = 2000;

-- Good: Index IS used
SELECT * FROM students
WHERE date_of_birth BETWEEN '2000-01-01' AND '2000-12-31';
```

**5. Use JOINs instead of subqueries where possible**
```sql
-- Subquery (slower)
SELECT name FROM employees
WHERE department_id IN (SELECT id FROM departments WHERE dept_name = 'Engineering');

-- JOIN (faster)
SELECT e.name FROM employees e
JOIN departments d ON e.department_id = d.id
WHERE d.dept_name = 'Engineering';
```

**6. Normalize your database to avoid redundancy**

**7. Archive old data — don't let tables grow indefinitely**

---

## 28. Interview Questions Cheatsheet

### Common SQL Interview Questions

**Q1: What is the difference between DELETE, TRUNCATE, and DROP?**

| Command | Removes | Rollback? | Speed |
|---------|---------|-----------|-------|
| `DELETE` | Specific rows (with WHERE) | Yes | Slow |
| `TRUNCATE` | All rows | No | Fast |
| `DROP` | Entire table + structure | No | Fastest |

---

**Q2: What is the difference between WHERE and HAVING?**
- `WHERE` filters **rows** before grouping
- `HAVING` filters **groups** after `GROUP BY`

---

**Q3: Find the second highest salary**

```sql
-- Method 1: Using LIMIT and OFFSET
SELECT DISTINCT salary FROM employees
ORDER BY salary DESC
LIMIT 1 OFFSET 1;

-- Method 2: Using Subquery
SELECT MAX(salary) FROM employees
WHERE salary < (SELECT MAX(salary) FROM employees);

-- Method 3: Using DENSE_RANK (best for Nth salary)
SELECT salary FROM (
    SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk
    FROM employees
) ranked
WHERE rnk = 2;
```

---

**Q4: Find duplicate records**

```sql
SELECT email, COUNT(*) AS count
FROM students
GROUP BY email
HAVING COUNT(*) > 1;
```

---

**Q5: Get employees who earn more than their manager**

```sql
SELECT e.name AS employee, e.salary AS emp_salary,
       m.name AS manager,  m.salary AS mgr_salary
FROM employees e
JOIN employees m ON e.manager_id = m.id
WHERE e.salary > m.salary;
```

---

**Q6: What is a Self Join? Give an example.**
A self join joins a table with itself. Used for hierarchical data like org charts.

---

**Q7: What are Window Functions?**
Functions that perform calculations over a related set of rows without collapsing them. Examples: `ROW_NUMBER()`, `RANK()`, `LAG()`, `LEAD()`, `SUM() OVER()`.

---

**Q8: What is the difference between UNION and UNION ALL?**
- `UNION` removes duplicates
- `UNION ALL` keeps all rows including duplicates (faster)

---

**Q9: What is normalization?**
The process of organizing database tables to reduce redundancy and improve data integrity. Common normal forms: 1NF, 2NF, 3NF.

---

**Q10: What are ACID properties?**
- **A**tomicity — All or nothing
- **C**onsistency — Data remains valid
- **I**solation — Transactions don't interfere
- **D**urability — Committed data is permanent

---

## 📌 Quick Reference Card

```sql
-- DATABASE
CREATE DATABASE db_name;
USE db_name;
DROP DATABASE db_name;

-- TABLE
CREATE TABLE t (col TYPE CONSTRAINT, ...);
ALTER TABLE t ADD col TYPE;
ALTER TABLE t DROP COLUMN col;
DROP TABLE t;
TRUNCATE TABLE t;

-- DATA
INSERT INTO t (cols) VALUES (vals);
UPDATE t SET col=val WHERE condition;
DELETE FROM t WHERE condition;

-- QUERY
SELECT cols FROM t
WHERE condition
GROUP BY col
HAVING condition
ORDER BY col [ASC|DESC]
LIMIT n OFFSET m;

-- JOINS
INNER JOIN t2 ON t1.col = t2.col
LEFT  JOIN t2 ON t1.col = t2.col
RIGHT JOIN t2 ON t1.col = t2.col

-- AGGREGATE
COUNT(*), SUM(col), AVG(col), MIN(col), MAX(col)

-- STRING
UPPER(), LOWER(), LENGTH(), SUBSTRING(), CONCAT(), TRIM(), REPLACE()

-- DATE
NOW(), CURDATE(), YEAR(), MONTH(), DAY(), DATEDIFF(), DATE_ADD()

-- NULL
IS NULL, IS NOT NULL, COALESCE(), IFNULL(), NULLIF()

-- ADVANCED
WITH cte AS (SELECT ...)   -- CTE
ROW_NUMBER() OVER (...)    -- Window Function
CALL procedure_name();     -- Stored Procedure
START TRANSACTION; ... COMMIT; ROLLBACK;  -- Transaction
```

---

## 🏆 Real-World Project Ideas

1. **Student Management System** — Students, courses, enrollment, grades
2. **E-Commerce Database** — Products, customers, orders, payments
3. **Hospital Management** — Patients, doctors, appointments, prescriptions
4. **HR System** — Employees, departments, salaries, leaves
5. **Library System** — Books, members, borrowed books, fines

---

*Made with ❤️ for SQL learners. Happy querying!* 🗄️
