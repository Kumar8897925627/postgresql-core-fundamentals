# postgresql-core-fundamentals
A professional deep-dive into PostgreSQL schema design, data integrity constraints, and DDL commands (ALTER, RENAME, DROP).
-- ==========================================================
-- PROJECT: Student Database Management (Level 2)
-- CONCEPTS: Constraints, Data Integrity, Table Evolution
-- ==========================================================

-- 1. CLEANUP (Start fresh)
DROP TABLE IF EXISTS students;

-- 2. CREATE TABLE WITH CONSTRAINTS
-- We use specific types to ensure data matches real-world formats.
CREATE TABLE students (
    student_id SERIAL PRIMARY KEY,            -- PK: Unique ID for every row
    first_name VARCHAR(50) NOT NULL,          -- NOT NULL: Name is mandatory
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,       -- UNIQUE: No duplicate accounts
    date_of_birth DATE NOT NULL,              -- DATE: Uses YYYY-MM-DD format
    enrollment_date DATE DEFAULT CURRENT_DATE,-- DEFAULT: Auto-fills today's date
    gpa NUMERIC(3, 2)                         -- NUMERIC: Exact decimal precision
);

-- 3. INSERT VALID DATA
INSERT INTO students (first_name, last_name, email, date_of_birth, gpa) VALUES 
('Alice', 'Johnson', 'alice.j@example.com', '2002-05-14', 3.85),
('Bob', 'Smith', 'bob.s@example.com', '2001-09-20', 3.40),
('Charlie', 'Davis', 'charlie.d@example.com', '2003-01-10', 3.90),
('Diana', 'Prince', 'diana.p@example.com', '2002-11-30', 3.75),
('Ethan', 'Hunt', 'ethan.h@example.com', '2000-04-12', 3.20);

-- 4. TEST CONSTRAINTS (Uncomment to test failures)
-- These will cause errors - this is EXPECTED behavior for data integrity.

-- Test NOT NULL (Missing first_name):
-- INSERT INTO students (last_name, email, date_of_birth) VALUES ('Doe', 'j.doe@test.com', '2000-01-01');

-- Test UNIQUE (Duplicate email):
-- INSERT INTO students (first_name, last_name, email, date_of_birth) VALUES ('John', 'Doe', 'alice.j@example.com', '1999-01-01');


-- 5. MODIFYING THE TABLE (ALTER)

-- Add a new column
ALTER TABLE students ADD COLUMN phone_number VARCHAR(15);

-- Rename a column (Changing gpa to grade_point_average)
ALTER TABLE students RENAME COLUMN gpa TO grade_point_average;

-- Drop a column (Removing phone_number)
ALTER TABLE students DROP COLUMN phone_number;


-- 6. FINAL VIEW
SELECT * FROM students;

# PostgreSQL Core Fundamentals

This repository demonstrates advanced table design and data management techniques using PostgreSQL. 

## 🎯 Learning Objectives
1. **Schema Redesign:** Using proper types (`INT`, `VARCHAR`, `DATE`).
2. **Data Integrity:** Implementing `PRIMARY KEY`, `NOT NULL`, and `UNIQUE`.
3. **Table Evolution:** Using `ALTER`, `RENAME`, and `DROP` to modify live tables.



## 🛡️ Why Use Constraints?
Constraints are the "rules" of the database. They prevent:
- **Duplicates:** No two students can have the same Email.
- **Null Data:** Ensuring essential fields (like Name) are never empty.
- **Orphan Records:** Ensuring every student has a unique ID.

## 📋 Table Schema Description

| Column | Data Type | Constraint | Purpose |
| :--- | :--- | :--- | :--- |
| `student_id` | SERIAL | PRIMARY KEY | Unique identifier. |
| `first_name` | VARCHAR(50) | NOT NULL | Ensures identity is recorded. |
| `email` | VARCHAR(100) | UNIQUE | Prevents duplicate accounts. |
| `date_of_birth`| DATE | NOT NULL | Enforces date formatting. |
| `enrollment_date`| DATE | DEFAULT | Auto-stamps the join date. |

## 🛠️ How to Run
1. Open **pgAdmin**.
2. Create a database named `intern_training_db`.
3. Open the **Query Tool** and paste the contents of `setup.sql`.
4. Execute (F5) to see the table creation and modification in action.
