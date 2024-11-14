# SQL Commands and Queries

This document provides a comprehensive overview of SQL commands, data types, and query clauses with examples, explanations, and some sample interview questions.

---

## 1. SQL `CREATE` Statement

The `CREATE` statement is used to create a new table, view, or other database objects.

### Syntax:

```sql
CREATE TABLE table_name (
    column1 datatype [constraint],
    column2 datatype [constraint],
    column3 datatype [constraint],
    ...
);

CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(100),
    LastName VARCHAR(100),
    DateOfBirth DATE,
    HireDate DATE,
    Salary DECIMAL(10, 2)
);

```

### Interview Question:
- What is the difference between CREATE TABLE and CREATE DATABASE?

## 2. SQL INSERT Statement
The INSERT statement is used to add records to a table.

#### Syntax:
```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

#### Example: Inserting data into a table

```sql
INSERT INTO Employees (EmployeeID, FirstName, LastName, DateOfBirth, HireDate, Salary)
VALUES (1, 'John', 'Doe', '1985-01-15', '2010-03-25', 55000.00);

```

#### Interview Question:
- What happens if you INSERT a row without specifying values for all columns?


## 3. SQL UPDATE Statement
The UPDATE statement is used to modify existing records in a table.

#### Syntax:
``` sql

UPDATE table_name
SET column1 = value1, column2 = value2
WHERE condition;
```
#### Example: Updating data in a table

```sql
UPDATE Employees
SET Salary = 60000
WHERE EmployeeID = 1;
```

#### Interview Question:
- What will happen if you omit the WHERE clause in an UPDATE statement?

## 4. SQL ALTER Statement
The ALTER statement is used to modify an existing database object, such as a table.

#### Syntax:

```sql
ALTER TABLE table_name
ADD column_name datatype;
```

#### Example: Adding a new column to a table
```sql
ALTER TABLE Employees
ADD Department VARCHAR(100);
```

#### Interview Question:
- Can you rename a table using ALTER? If yes, how?

## 5. SQL DELETE Statement
The DELETE statement is used to remove records from a table.

#### Syntax:

```sql
DELETE FROM table_name
WHERE condition;
```

#### Example: Deleting a record from a table
```sql
DELETE FROM Employees
WHERE EmployeeID = 1;
```

#### Interview Question:
- What is the difference between DELETE and TRUNCATE?

## 6. SQL DROP Statement
The DROP statement is used to remove a database object, such as a table, from the database.

#### Syntax:
```sql
DROP TABLE table_name;
```
#### Example: Dropping a table
```sql
DROP TABLE Employees;
```

#### Interview Question:
- If a table is dropped, can the data be recovered? Why or why not?

## 7. SQL TRUNCATE Statement
The TRUNCATE statement is used to remove all records from a table, but it does not remove the table structure.

#### Syntax:
```sql
TRUNCATE TABLE table_name;
```
#### Example: Truncating a table
```sql
TRUNCATE TABLE Employees;
```

#### Interview Question:
- How is TRUNCATE different from DELETE in SQL?

## 8. SQL Data Types

SQL supports various data types. Here are some commonly used ones:

- INT: Integer numbers.
- VARCHAR(n): Variable-length string.
- CHAR(n): Fixed-length string.
- DATE: Date values (YYYY-MM-DD).
- DECIMAL(p, s): Fixed-point numbers with precision p and scale s.
- FLOAT: Floating-point numbers.
- BOOLEAN: TRUE or FALSE values.

#### Example:
```sql
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100),
    Price DECIMAL(10, 2)
);
```
#### Interview Question:
- What is the difference between VARCHAR and CHAR data types?

## 9. SQL SELECT Statement
The SELECT statement is used to query data from one or more tables.

#### Syntax:
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```
#### Example: Selecting data from a table
```sql
SELECT FirstName, LastName
FROM Employees
WHERE Salary > 50000;
```

#### Interview Question:
- How would you retrieve all columns from a table?


## 10. SQL DISTINCT Keyword
The DISTINCT keyword is used to return only unique values.

#### Syntax:
```sql
SELECT DISTINCT column_name
FROM table_name;
```

#### Example: Selecting unique job titles
```sql
SELECT DISTINCT Department
FROM Employees;
```

#### Interview Question:
- What is the performance impact of using DISTINCT in queries?

## 11. SQL WHERE Clause
The WHERE clause is used to filter records based on a specified condition.

#### Syntax:
```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```
#### Example: Using WHERE clause
```sql
SELECT FirstName, LastName
FROM Employees
WHERE Department = 'IT';
```

#### Interview Question:
- What are the logical operators that can be used in a WHERE clause?

## 12. SQL LIKE Operator

The LIKE operator is used to search for a specified pattern in a column.

#### Syntax:
```sql
SELECT column1
FROM table_name
WHERE column1 LIKE pattern;
```
#### Example: Using LIKE
```sql
SELECT FirstName
FROM Employees
WHERE FirstName LIKE 'J%';
```
#### Interview Question:
- What is the difference between LIKE and ILIKE in SQL?

## 13. SQL ORDER BY Clause
The ORDER BY clause is used to sort the result set in ascending or descending order.

#### Syntax:
```sql
SELECT column1, column2
FROM table_name
ORDER BY column1 [ASC|DESC];
```

#### Example: Ordering results by salary
```sql
SELECT FirstName, LastName, Salary
FROM Employees
ORDER BY Salary DESC;
```

#### Interview Question:
- Can you order by multiple columns in a SELECT statement? Give an example.

## 14. SQL LIMIT Clause
The LIMIT clause is used to specify the number of records to return.

#### Syntax:
```sql
SELECT column1
FROM table_name
LIMIT number;
```

#### Example: Limiting the number of results
```sql
SELECT FirstName, LastName
FROM Employees
LIMIT 5;
```

#### Interview Question:
- What is the difference between LIMIT and TOP?

## 15. SQL TOP Keyword (in SQL Server)
The TOP keyword is used in SQL Server to limit the number of rows returned.

#### Syntax:
```sql
SELECT TOP number column1, column2
FROM table_name;
```

#### Example: Getting top 3 highest paid employees
```sql
SELECT TOP 3 FirstName, LastName, Salary
FROM Employees
ORDER BY Salary DESC;
```

#### Interview Question:
- How do you get the top 5 records in PostgreSQL?

## 16. SQL Logical Operators: AND, OR, NOT

These logical operators are used to combine multiple conditions in a WHERE clause.

#### Syntax:
```sql
SELECT column1
FROM table_name
WHERE condition1 AND condition2;
```

#### Example: Using AND
```sql
SELECT FirstName, LastName
FROM Employees
WHERE Department = 'IT' AND Salary > 50000;
```

#### Interview Question:
- How would you use NOT in a query to exclude records where the salary is less than 50000?

## 17. SQL IN Operator
The IN operator is used to check if a value matches any value in a list of values.

#### Syntax:
```sql
SELECT column1
FROM table_name
WHERE column1 IN (value1, value2, ...);
```
#### Example: Using IN
```sql
SELECT FirstName, LastName
FROM Employees
WHERE Department IN ('HR', 'IT');
```
#### Interview Question:
- Can IN be used with subqueries? Provide an example.

## 18. SQL BETWEEN Operator
The BETWEEN operator is used to select values within a range.

#### Syntax:
```sql
SELECT column1
FROM table_name
WHERE column1 BETWEEN value1 AND value2;
```

#### Example: Using BETWEEN
```sql
SELECT FirstName, LastName, Salary
FROM Employees
WHERE Salary BETWEEN 50000 AND 70000;
```

#### Interview Question:
- How does BETWEEN handle NULL values in a column?


# SQL Aggregate Functions and Joins

## 1. SQL Aggregate Functions

Aggregate functions perform a calculation on a set of values and return a single result. Common aggregate functions include `SUM`, `MAX`, `MIN`, `COUNT`, and `AVG`.

### 1.1. `SUM` Function

The `SUM()` function calculates the total sum of a numeric column.

#### Syntax:

```sql
SELECT SUM(column_name)
FROM table_name
WHERE condition;
```
#### Example:

```sql
SELECT SUM(Salary)
FROM Employees
WHERE Department = 'IT';
```

#### Interview Question:
- What happens if you use SUM on a column with NULL values?

## 1.2. MAX Function
The MAX() function returns the largest value in a numeric column.

#### Syntax:

```sql
SELECT MAX(column_name)
FROM table_name
WHERE condition;
```

#### Example:

```sql
SELECT MAX(Salary)
FROM Employees;
```
#### Interview Question:
- Can MAX() be used with non-numeric data types? Give an example.

## 1.3. MIN Function
The MIN() function returns the smallest value in a numeric column.

#### Syntax:

```sql
SELECT MIN(column_name)
FROM table_name
WHERE condition;
```

#### Example:

```sql
SELECT MIN(Salary)
FROM Employees
WHERE Department = 'Sales';
```

#### Interview Question:
- What will the result be if the column contains NULL values?

## 1.4. COUNT Function
The COUNT() function counts the number of rows that match a specified condition.

#### Syntax:

```sql
SELECT COUNT(column_name)
FROM table_name
WHERE condition;
```

#### Example:

```sql
SELECT COUNT(EmployeeID)
FROM Employees
WHERE Department = 'HR';
```

#### Interview Question:
- What is the difference between COUNT(*) and COUNT(column_name)?

## 1.5. AVG Function

The AVG() function calculates the average value of a numeric column.

#### Syntax:

```sql
SELECT AVG(column_name)
FROM table_name
WHERE condition;
```

#### Example:

```sql
SELECT AVG(Salary)
FROM Employees
WHERE Department = 'Finance';
```

#### Interview Question:

- How does AVG() handle NULL values in the column?

## 2. SQL GROUP BY Clause

The GROUP BY clause groups rows that have the same values in specified columns into summary rows, like finding the total salary per department.

#### Syntax:

```sql
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE condition
GROUP BY column_name;
```

#### Example:

```sql
SELECT Department, AVG(Salary)
FROM Employees
GROUP BY Department;
```

#### Interview Question:
- Can you group by multiple columns? If yes, give an example.

## 3. SQL HAVING Clause

The HAVING clause is used to filter the results of a GROUP BY query. It is similar to the WHERE clause, but it is used for aggregate functions.

#### Syntax:

```sql
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE condition
GROUP BY column_name
HAVING condition;
```

#### Example:

```sql
SELECT Department, AVG(Salary)
FROM Employees
GROUP BY Department
HAVING AVG(Salary) > 60000;
```

#### Interview Question:
- How does HAVING differ from WHERE?

## 4. SQL JOIN Types

A JOIN clause is used to combine rows from two or more tables based on a related column between them. Here are the different types of joins:

## 4.1. INNER JOIN

The INNER JOIN keyword returns records that have matching values in both tables.

#### Syntax:

```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

#### Example:

```sql
SELECT Employees.EmployeeID, Employees.FirstName, Departments.DepartmentName
FROM Employees
INNER JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID;
```

#### Interview Question:
- What will happen if there is no matching record in either of the tables?

## 4.2. RIGHT JOIN (or RIGHT OUTER JOIN)
The RIGHT JOIN returns all records from the right table and the matched records from the left table. If there is no match, NULL values are returned for columns from the left table.

#### Syntax:

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```

#### Example:

```sql
SELECT Employees.EmployeeID, Employees.FirstName, Departments.DepartmentName
FROM Employees
RIGHT JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID;
```

#### Interview Question:
- What does a RIGHT JOIN return when there is no match in the left table?

## 4.3. LEFT JOIN (or LEFT OUTER JOIN)
The LEFT JOIN returns all records from the left table and the matched records from the right table. If there is no match, NULL values are returned for columns from the right table.

#### Syntax:

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```

#### Example:

```sql
SELECT Employees.EmployeeID, Employees.FirstName, Departments.DepartmentName
FROM Employees
LEFT JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID;
```

#### Interview Question:
- What happens if a LEFT JOIN does not find a match for a record in the left table?

## 4.4. OUTER JOIN
An OUTER JOIN returns all records when there is a match in either the left or right table. This can be written as LEFT OUTER JOIN, RIGHT OUTER JOIN, or FULL OUTER JOIN.

#### Syntax:

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

#### Example:

```sql
SELECT Employees.EmployeeID, Employees.FirstName, Departments.DepartmentName
FROM Employees
FULL OUTER JOIN Departments
ON Employees.DepartmentID = Departments.DepartmentID;
```

#### Interview Question:
- What is the difference between INNER JOIN and OUTER JOIN?

## 4.5. SELF JOIN
A SELF JOIN is a regular join but the table is joined with itself.

#### Syntax:

```sql
SELECT a.column, b.column
FROM table a, table b
WHERE a.common_column = b.common_column;
```

#### Example:

```sql
SELECT E1.EmployeeID, E1.FirstName, E2.FirstName AS ManagerName
FROM Employees E1
INNER JOIN Employees E2
ON E1.ManagerID = E2.EmployeeID;
```

#### Interview Question:
- Why would you use a SELF JOIN? Can you think of any real-world scenarios?


## Interview Question:
- What is the difference between COUNT(*) and COUNT(column_name)?
- Explain the difference between HAVING and WHERE.
- Can INNER JOIN return unmatched rows? Why or why not?
- What is the difference between LEFT JOIN and RIGHT JOIN?
- Explain the use of FULL OUTER JOIN with an example.
- How do NULL values affect aggregate functions like AVG or SUM?


# SQL Advanced Topics: EXISTS, UNION, UNION ALL, Date Time Functions, CTE, and Subqueries


---

## 1. SQL `EXISTS` Keyword

The `EXISTS` keyword in SQL is used to test whether a subquery returns any rows. It is often used in a `WHERE` clause to check the existence of rows without needing to return any specific data from the subquery. The query returns `TRUE` if the subquery returns one or more rows, and `FALSE` if the subquery returns no rows.

### Syntax:

```sql
SELECT column_name
FROM table_name
WHERE EXISTS (subquery);

```
#### Example:
```sql

SELECT FirstName, LastName
FROM Employees
WHERE EXISTS (
    SELECT 1
    FROM Departments
    WHERE Departments.DepartmentID = Employees.DepartmentID
);
```
#### Interview Question:

- How does EXISTS differ from IN in SQL?
## 2. SQL UNION and UNION ALL

The UNION and UNION ALL operators are used to combine the results of two or more SELECT statements.

### 2.1. UNION Operator
The UNION operator combines the results of two SELECT queries and removes any duplicate records from the result set.

#### Syntax:
```sql

SELECT column_name
FROM table1
UNION
SELECT column_name
FROM table2;
```
#### Example:
```sql

SELECT FirstName, LastName FROM Employees
UNION
SELECT FirstName, LastName FROM Contractors;
```
#### Interview Question:
- What is the difference between UNION and UNION ALL?
### 2.2. UNION ALL Operator
The UNION ALL operator combines the result sets of two SELECT queries but does not remove duplicates.

#### Syntax:
```sql

SELECT column_name
FROM table1
UNION ALL
SELECT column_name
FROM table2;
```
#### Example:
```sql

SELECT FirstName, LastName FROM Employees
UNION ALL
SELECT FirstName, LastName FROM Contractors;
```
#### Interview Question:

- When would you prefer UNION ALL over UNION?

## 3. SQL Date and Time Functions

SQL provides a variety of built-in functions for working with date and time values. These functions allow you to manipulate, extract, and format date and time data in your queries.

### 3.1. GETDATE() or CURRENT_TIMESTAMP

Returns the current date and time of the system.

```sql

SELECT GETDATE();  -- Returns current date and time
```

### 3.2. DATEADD() Function

Adds a specified time interval (e.g., day, month, year) to a date.

#### Syntax:

```sql

DATEADD(datepart, number, date)
```

#### Example:
```sql
SELECT DATEADD(DAY, 5, GETDATE());  -- Adds 5 days to the current date
```

### 3.3. DATEDIFF() Function
Returns the difference between two dates.

#### Syntax:
```sql
DATEDIFF(datepart, start_date, end_date)
```

#### Example:

```sql
SELECT DATEDIFF(DAY, '2023-01-01', '2023-12-31');  -- Returns the number of days between the two dates
```

## 3.4. DATEPART() Function

Extracts a part (e.g., year, month, day) from a date.

#### Syntax:

```sql

DATEPART(datepart, date)
```

#### Example:

```sql

SELECT DATEPART(MONTH, '2023-10-15');  -- Returns 10 (October)
```

### 3.5. CONVERT() or CAST() Functions

Used to convert a date into a specific format.

#### Example:
```sql

SELECT CONVERT(VARCHAR, GETDATE(), 103);  -- Converts the date to 'dd/mm/yyyy' format
```

#### Interview Question:
- How do you handle time zones when using GETDATE() or CURRENT_TIMESTAMP?

## 4. SQL Common Table Expression (CTE)

A Common Table Expression (CTE) is a temporary result set that can be referenced within a SELECT, INSERT, UPDATE, or DELETE statement. CTEs can improve query readability and structure, especially for complex queries.

#### Syntax:

```sql
WITH CTE_Name AS (
    SELECT column1, column2
    FROM table_name
    WHERE condition
)
SELECT * FROM CTE_Name;
```

#### Example:

```sql

WITH DepartmentSalaries AS (
    SELECT Department, AVG(Salary) AS AvgSalary
    FROM Employees
    GROUP BY Department
)
SELECT * FROM DepartmentSalaries
WHERE AvgSalary > 60000;
```

#### Interview Question:
- What is the difference between a CTE and a subquery?

## 5. SQL Subqueries
A subquery is a query nested inside another query. Subqueries can be used in SELECT, INSERT, UPDATE, and DELETE statements. They are often used to retrieve data for comparison or filtering.

### 5.1. Subquery in the SELECT Clause
A subquery can be used in the SELECT clause to return a computed value.

#### Example:
```sql

SELECT EmployeeID,
       (SELECT DepartmentName FROM Departments WHERE DepartmentID = Employees.DepartmentID) AS Department
FROM Employees;
```

### 5.2. Subquery in the WHERE Clause

A subquery in the WHERE clause can be used to filter results based on the result of another query.

#### Example:

```sql

SELECT FirstName, LastName
FROM Employees
WHERE DepartmentID IN (
    SELECT DepartmentID FROM Departments WHERE DepartmentName = 'HR'
);
```

### 5.3. Correlated Subquery
A correlated subquery references columns from the outer query. The subquery is executed for each row returned by the outer query.

#### Example:

```sql
SELECT e.FirstName, e.LastName
FROM Employees e
WHERE e.Salary > (
    SELECT AVG(Salary)
    FROM Employees
    WHERE DepartmentID = e.DepartmentID
);
```

#### Interview Question:
- What is the difference between a correlated subquery and a non-correlated subquery?

## Interview Questions:
- What is the difference between EXISTS and IN in SQL?
- What is the performance impact of using UNION vs UNION ALL?
- How do you handle time zone issues in date and time functions?
- Explain the difference between a correlated subquery and a non-correlated subquery.
- When would you use a CTE instead of a subquery or temporary table?










