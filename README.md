# Task 8: Stored Procedures and Functions

## 📌 Objective
Learn how to create **reusable SQL blocks** using **stored procedures** and **functions**.  

## 🛠️ Tools
- MySQL Workbench

## 📂 Deliverables
- One **stored procedure**
- One **function**
- Sample database and table to demonstrate usage

---

## 🏗️ Database Setup

### 1. Create Database and Table
```sql
CREATE DATABASE school_db;
USE school_db;

CREATE TABLE students (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    marks INT NOT NULL
);

INSERT INTO students (name, marks) VALUES
('Alice', 95),
('Bob', 82),
('Charlie', 67),
('David', 45),
('Eve', 32);
```

### 2. Stored Procedure
- GetTopStudents:
A procedure that returns students with marks greater than or equal to a given value.
```sql
DELIMITER //
CREATE PROCEDURE GetTopStudents(IN min_marks INT)
BEGIN
    SELECT id, name, marks
    FROM students
    WHERE marks >= min_marks;
END //
DELIMITER ;
```
**Usage:**
```sql
CALL GetTopStudents(70);
```

### 3. 🧮 Function
- GetGrade:
A function that calculates grade based on marks.
```sql
DELIMITER //
CREATE FUNCTION GetGrade(marks INT)
RETURNS VARCHAR(2)
DETERMINISTIC
BEGIN
    DECLARE grade VARCHAR(2);

    IF marks >= 90 THEN
        SET grade = 'A+';
    ELSEIF marks >= 75 THEN
        SET grade = 'A';
    ELSEIF marks >= 60 THEN
        SET grade = 'B';
    ELSEIF marks >= 40 THEN
        SET grade = 'C';
    ELSE
        SET grade = 'F';
    END IF;

    RETURN grade;
END //
DELIMITER ;
```
**Usage:**
```sql
SELECT id, name, marks, GetGrade(marks) AS grade
FROM students;
```

### 📖 Summary
- **Stored Procedure:** Demonstrates parameterized reusable queries.
- **Function:** Demonstrates conditional logic and return values.
- Together, they show how SQL can be extended beyond simple queries to create reusable logic inside the database.

### Author
Created by Arpita Jitendra Sonparote
