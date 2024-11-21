# SQL Statements and Operators
]

## SELECT Statement:

The SELECT statement is used to select data from a database.


- SELECT * FROM Customers;
- SELECT name FROM Customers;
- SELECT DISTINCT Country FROM Customers;


## WHERE Clause
The WHERE clause is used to filter records.
It is used to extract only those records that fulfill a specified condition.

- SELECT * FROM Customers WHERE CustomerID > 80;
- SELECT * FROM Customers WHERE CustomerID=1;
- We can use =,<,>,<=,>=,!,!=, <>, IN, Like , Between with where operator

## Operators:

### Arithmatic Operator:

| Operator | Description |
|----------|-------------|
| +        | Add         |  
| -        | Subtract    |   
| *        | Multiply    |   
| /        | Divide      |   
| %        | Modulo      |

### BITWISE Operator:

| Operator | Description          |
|----------|----------------------|
| &        | Bitwise AND          |
| |        | Bitwise OR           |
| ^        | Bitwise exclusive OR |

### Comparision Operator

| Operator | Description              |
|----------|--------------------------|
| =        | Equal to                 | 
| >        | Greater than             | 
| <        | Less than                | 
| >=       | Greater than or equal to | 
| <=       | Less than or equal to    |  
| <>       | Not equal to             |

### Compound Operators:

| Operator | Description              |
|----------|--------------------------|
| +=       | Add equals               |
| -=       | Subtract equals          |
| *=       | Multiply equals          |
| /=       | Divide equals            |
| %=       | Modulo equals            |
| &=       | Bitwise AND equals       |
| ^-=      | Bitwise exclusive equals |
| |*=      | Bitwise OR equals        |

### Logical Operators

| Operator | Description                                                  |
|----------|--------------------------------------------------------------|
| ALL      | TRUE if all of the subquery values meet the condition        |
| AND      | TRUE if all the conditions separated by AND is TRUE          |
| ANY      | TRUE if any of the subquery values meet the condition        |
| BETWEEN  | TRUE if the operand is within the range of comparisons       |
| EXISTS   | TRUE if the subquery returns one or more records             |
| IN       | TRUE if the operand is equal to one of a list of expressions |
| LIKE     | TRUE if the operand matches a pattern                        |
| NOT      | Displays a record if the condition(s) is NOT TRUE            |
| OR       | TRUE if any of the conditions separated by OR is TRUE        |
| SOME     | TRUE if any of the subquery values meet the condition        |

### Aggregate Functions

An aggregate function is a function that performs a calculation on a set of values, and returns a single value. 
Aggregate functions are often used with the GROUP BY clause of the SELECT statement. 
The GROUP BY clause splits the result-set into groups of values and the aggregate function can be used to return a single value for each group.

The most commonly used SQL aggregate functions are:

- MIN() - returns the smallest value within the selected column
- MAX() - returns the largest value within the selected column
- COUNT() - returns the number of rows in a set
- SUM() - returns the total sum of a numerical column
- AVG() - returns the average value of a numerical column

Important:
- Aggregate functions ignore null values (except for COUNT()).
- COUNT(column_name): Counts all non-NULL values in the specified column.
- COUNT(*): Counts all rows, including rows with NULL values.

### ORDER BY
The ORDER BY keyword is used to sort the result-set in ascending or descending order.

```sql
SELECT * FROM Products
ORDER BY Price;
```
### NULL Statement
A field with a NULL value is a field with no value.

If a field in a table is optional, it is possible to insert a new record or update a record without adding a value to this field. 
Then, the field will be saved with a NULL value.

- IS NULL Syntax
```sql
SELECT column_names
FROM table_name
WHERE column_name IS NULL;
```
- IS NOT NULL Syntax
```sql
SELECT column_names
FROM table_name
WHERE column_name IS NOT NULL;
```

### GROUP BY Statement
The GROUP BY statement groups rows that have the same values into summary rows, like "find the number of customers in each country".
The GROUP BY statement is often used with aggregate functions (COUNT(), MAX(), MIN(), SUM(), AVG()) to group the result-set by one or more columns.

```sql
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
ORDER BY COUNT(CustomerID) DESC;
```

### HAVING Clause
The HAVING clause was added to SQL because the WHERE keyword cannot be used with aggregate functions.
```sql
SELECT COUNT(CustomerID), Country
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5;
```

| Aspect              | GROUP BY                                           | HAVING                                                        |
|---------------------|----------------------------------------------------|---------------------------------------------------------------|
| Purpose             | Groups rows based on column(s) values.             | Filters the grouped rows based on aggregate function results. |
| Used With           | Aggregate functions (e.g., SUM(), COUNT(), etc.)   | Aggregate functions (e.g., SUM(), COUNT(), etc.).             |
| Filter Point        | Applies before the aggregation (rows are grouped). | Applies after the aggregation (groups are filtered).          |
| Usage               | Always used with GROUP BY for grouping.            | Used to filter groups created by GROUP BY.                    |
| Can Be Used Without | Cannot be used without GROUP BY.                   | Can be used with GROUP BY but can also be used without it.    |




String Functions:
# SQL String Functions

SQL provides a wide range of string functions to manipulate and analyze text data in queries. 
These functions can help you work with string values, such as extracting parts of strings, modifying case, searching for substrings, and more.

## 1. `CONCAT()`

The `CONCAT()` function is used to concatenate (combine) two or more strings together into one string.

### Syntax:
```sql
CONCAT(string1, string2, ...);
```
Example:
```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM employees;
```
This query concatenates the first_name and last_name columns to create a full name for each employee.

2. LENGTH() / LEN()
The LENGTH() function (or LEN() in some databases like SQL Server) returns the number of characters in a string.

Syntax:
```sql
LENGTH(string);
```

Example:
```sql
SELECT LENGTH(first_name) AS name_length
FROM employees;
```
This query returns the length of each employee's first_name.

3. UPPER() / LOWER()

UPPER() converts a string to uppercase.
LOWER() converts a string to lowercase.
Syntax:
```sql
UPPER(string);
LOWER(string);
```
Example:
```sql
SELECT UPPER(first_name) AS upper_name
FROM employees;
```
This query converts the first_name of each employee to uppercase.

4. TRIM()
The TRIM() function removes leading and trailing spaces (or other specified characters) from a string.

Syntax:
```sql
TRIM([trim_character] FROM string);
```
Example:
```sql
SELECT TRIM(first_name) AS trimmed_name
FROM employees;
```
This removes any extra spaces from the beginning and end of the first_name.

5. SUBSTRING() / SUBSTR()
The SUBSTRING() or SUBSTR() function extracts a portion of a string, starting at a specified position and extending for a specified number of characters.

Syntax:
```sql
SUBSTRING(string, start_position, length);
-- or
SUBSTR(string, start_position, length);
```
Example:
```sql
SELECT SUBSTRING(first_name, 1, 3) AS name_part
FROM employees;
```
This extracts the first 3 characters from the first_name column.

6. REPLACE()
The REPLACE() function is used to replace occurrences of a substring within a string with another substring.

Syntax:
```sql
REPLACE(string, old_substring, new_substring);
```
Example:
```sql
SELECT REPLACE(email, 'gmail.com', 'yahoo.com') AS updated_email
FROM employees;
```
This query replaces all occurrences of 'gmail.com' with 'yahoo.com' in the email column.

7. INSTR() / CHARINDEX()
The INSTR() (or CHARINDEX() in SQL Server) function returns the position of the first occurrence of a substring within a string. If the substring is not found, it returns 0.

Syntax:
```sql
INSTR(string, substring);
-- or
CHARINDEX(substring, string);  -- For SQL Server
```
Example:
```sql
SELECT INSTR(email, '@') AS at_symbol_position
FROM employees;
```
This returns the position of the '@' symbol in the email column.

8. LEFT() / RIGHT()
LEFT() returns the leftmost n characters of a string.
RIGHT() returns the rightmost n characters of a string.
Syntax:
```sql
LEFT(string, length);
RIGHT(string, length);
```
Example:
```sql
SELECT LEFT(first_name, 3) AS left_name
FROM employees;
```
This returns the first 3 characters from the first_name column.

9. REVERSE()
The REVERSE() function returns a string with its characters in reverse order.

Syntax:
```sql
REVERSE(string);
```
Example:
```sql
SELECT REVERSE(first_name) AS reversed_name
FROM employees;
```
This reverses the first_name of each employee.

10. CONCAT_WS()
The CONCAT_WS() function concatenates multiple strings with a specified separator.

Syntax:
```sql
CONCAT_WS(separator, string1, string2, ...);
```
Example:
```sql
SELECT CONCAT_WS(', ', first_name, last_name) AS full_name
FROM employees;
```
This query concatenates first_name and last_name with a comma and a space as the separator.

11. POSITION() / LOCATE()
The POSITION() (or LOCATE() in some databases) function returns the position of a substring within a string.

Syntax:
```sql
POSITION(substring IN string);
-- or
LOCATE(substring, string);  -- For MySQL
```
Example:
```sql
SELECT POSITION('@' IN email) AS at_symbol_position
FROM employees;
```
This returns the position of the '@' symbol in the email column.

12. FORMAT()
The FORMAT() function is used to format a string or number based on a specified format.

Syntax:
```sql
FORMAT(number, format);
```
Example:
```sql
SELECT FORMAT(salary, 2) AS formatted_salary
FROM employees;
```
This formats the salary column to two decimal places.

## Date Time Functions

# SQL Date Functions

SQL provides a variety of date functions that allow you to manipulate and perform calculations with date and time values. These functions are used to extract specific parts of a date (like the year, month, or day), format dates, and perform operations like adding or subtracting time intervals.

## 1. `NOW()` / `CURRENT_TIMESTAMP`

The `NOW()` function returns the current date and time of the database server in the format `YYYY-MM-DD HH:MI:SS`.

### Syntax:
```sql
NOW();
```
Example:
```sql
SELECT NOW();
```
This will return the current date and time.

2. CURDATE() / CURRENT_DATE
The CURDATE() function returns the current date without the time portion, formatted as YYYY-MM-DD.

Syntax:
```sql
CURDATE();
-- or
CURRENT_DATE;
```
Example:
```sql
SELECT CURDATE();
```
This will return today's date in the format YYYY-MM-DD.

3. CURTIME() / CURRENT_TIME
The CURTIME() function returns the current time without the date portion, formatted as HH:MM:SS.

Syntax:
```sql
CURTIME();
-- or
CURRENT_TIME;
```
Example:
```sql

SELECT CURTIME();
```
This will return the current time in the format HH:MM:SS.

4. DATE()
The DATE() function extracts the date portion (without time) from a DATETIME or TIMESTAMP value.

Syntax:
```sql
DATE(datetime_value);
```
Example:
```sql
SELECT DATE(NOW());
```
This will return only the date portion of the current DATETIME value.

5. YEAR(), MONTH(), DAY()
These functions extract specific parts of a date:

YEAR(): Extracts the year from a date.
MONTH(): Extracts the month from a date.
DAY(): Extracts the day of the month from a date.
Syntax:
```sql
YEAR(date);
MONTH(date);
DAY(date);
```
Example:
```sql
SELECT YEAR(NOW()) AS current_year, MONTH(NOW()) AS current_month, DAY(NOW()) AS current_day;
```
This will return the current year, month, and day.

6. DAYOFWEEK() / WEEKDAY()
DAYOFWEEK(): Returns the day of the week as a number (1 = Sunday, 7 = Saturday).
WEEKDAY(): Returns the day of the week as a number (0 = Monday, 6 = Sunday).
Syntax:
```sql
DAYOFWEEK(date);
-- or
WEEKDAY(date);
```
Example:
```sql
SELECT DAYOFWEEK(NOW()) AS day_of_week;
-- or
SELECT WEEKDAY(NOW()) AS weekday;
```
This will return the numeric value representing the current day of the week.

7. DATE_ADD() / ADDDATE()
The DATE_ADD() function adds a specified time interval to a date or DATETIME value.

Syntax:
```sql
DATE_ADD(date, INTERVAL value unit);
-- or
ADDDATE(date, INTERVAL value unit);
```
Example:
```sql
SELECT DATE_ADD(CURDATE(), INTERVAL 7 DAY);
```
This will add 7 days to the current date and return the new date.

8. DATE_SUB() / SUBDATE()
The DATE_SUB() function subtracts a specified time interval from a date or DATETIME value.

Syntax:
```sql
DATE_SUB(date, INTERVAL value unit);
-- or
SUBDATE(date, INTERVAL value unit);
```
Example:
```sql
SELECT DATE_SUB(CURDATE(), INTERVAL 7 DAY);
```
This will subtract 7 days from the current date and return the new date.

9. DATEDIFF()
The DATEDIFF() function returns the number of days between two dates.

Syntax:
```sql
DATEDIFF(date1, date2);
```
Example:
```sql
SELECT DATEDIFF('2024-12-31', '2024-01-01') AS days_difference;
```
This will return the number of days between 2024-12-31 and 2024-01-01.

10. TIMESTAMPDIFF()
The TIMESTAMPDIFF() function returns the difference between two DATETIME or TIMESTAMP values in a specified unit (e.g., seconds, minutes, hours, days, months, years).

Syntax:
```sql
TIMESTAMPDIFF(unit, datetime1, datetime2);
```
Example:
```sql
SELECT TIMESTAMPDIFF(DAY, '2024-01-01', '2024-12-31') AS day_difference;
```
This will return the difference in days between 2024-01-01 and 2024-12-31.

11. STR_TO_DATE()
The STR_TO_DATE() function converts a string into a date using a specified format.

Syntax:
```sql
STR_TO_DATE(string, format);
```
Example:
```sql
SELECT STR_TO_DATE('2024-12-31', '%Y-%m-%d') AS date_value;
```
This will convert the string '2024-12-31' into a DATE value.

12. DATE_FORMAT()
The DATE_FORMAT() function formats a date or DATETIME value into a specific string format.

Syntax:
```sql
DATE_FORMAT(date, format);
```
Example:
```sql
SELECT DATE_FORMAT(NOW(), '%W, %M %d, %Y') AS formatted_date;
```
This will return the current date in the format Tuesday, November 20, 2024.

13. EXTRACT()
The EXTRACT() function is used to retrieve specific parts of a date or DATETIME value, such as the year, month, day, etc.

Syntax:
```sql
EXTRACT(unit FROM date);
```
Example:
```sql
SELECT EXTRACT(YEAR FROM NOW()) AS year_part;
```
This will return the year part of the current date.

14. LAST_DAY()
The LAST_DAY() function returns the last day of the month for a given date.

Syntax:
```sql
LAST_DAY(date);
```
Example:
```sql
SELECT LAST_DAY('2024-02-15') AS last_day_of_month;
```
This will return 2024-02-29 as the last day of February in a leap year.



## SQL `LIKE` Operator

The `LIKE` operator in SQL is used in a **`WHERE`** clause to search for a specified pattern in a column. 
It is typically used with **wildcards** to match part of a string value.

## Syntax

```sql
SELECT column1, column2, ...
FROM table_name
WHERE column_name LIKE pattern;
```

Pattern Matching with Wildcards
You can use wildcards to define the pattern for the LIKE operator.

Common Wildcards:
- %: Represents zero or more characters.
Example: %abc% will match any string that contains "abc" anywhere in the string.
- _: Represents exactly one character.
Example: a__c will match any string that starts with "a", ends with "c", and has exactly two characters in between.

1. Using % (Matches Zero or More Characters)
```sql
SELECT first_name
FROM employees
WHERE first_name LIKE 'J%';
```
2. Using _ (Matches Exactly One Character)

```sql
SELECT first_name
FROM employees
WHERE first_name LIKE 'J_n';
```

3. Case Sensitivity in LIKE
   The behavior of the LIKE operator with regard to case sensitivity depends on the database system and its collation settings.
   In some databases like MySQL, the LIKE operator is case-insensitive by default. In others, such as PostgreSQL,
   it is case-sensitive unless you use specific functions to ignore case.

# SQL Regular Expressions (Regex)

Regular expressions (regex) are powerful patterns used to match strings and manipulate text. 
Many SQL database systems support regular expressions for pattern matching, though the specific syntax and functions may vary across different systems.

## Regular Expressions in SQL

Regular expressions allow you to perform complex pattern matching on text data. 
We can use them to validate, search, and extract specific patterns within strings. 

## Basic Regular Expression Syntax

Regular expressions use a combination of literal characters and special symbols to define patterns. 
Here are some common elements used in regular expressions:

- **`.` (Dot)**: Matches any single character (except newline).
- **`^`**: Anchors the match at the beginning of the string.
- **`$`**: Anchors the match at the end of the string.
- **`[]` (Character class)**: Matches any one of the characters inside the brackets. E.g., `[a-z]` matches any lowercase letter.
- **`|` (Alternation)**: Acts as a logical OR to match one of several alternatives.
- **`*`**: Matches zero or more of the preceding element.
- **`+`**: Matches one or more of the preceding element.
- **`?`**: Matches zero or one of the preceding element.
- **`\`**: Escapes a special character to treat it as a literal character.

## Regex Functions

### 1. `REGEXP` / `RLIKE` (MySQL)

In MySQL, you can use the `REGEXP` or `RLIKE` operator for regular expression matching.

#### Syntax:
```sql
SELECT column_name
FROM table_name
WHERE column_name REGEXP 'pattern';
```

1.
```sql
SELECT email
FROM users
WHERE email REGEXP '^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$';
```

# SQL Nested Queries (Subqueries)

A **nested query** (or **subquery**) is a query that is embedded within another query. 
Subqueries are often used to perform operations where the result of one query is needed to complete another query. 
A subquery can be placed in various parts of a SQL query, such as the `SELECT`, `FROM`, or `WHERE` clause.

## Types of Nested Queries

1. **Single-row Subquery**: Returns a single row of data.
2. **Multiple-row Subquery**: Returns multiple rows of data.
3. **Multiple-column Subquery**: Returns multiple columns of data.
4. **Correlated Subquery**: A subquery that references columns from the outer query.
5. **Non-correlated Subquery**: A subquery that is independent of the outer query.

## Syntax of Nested Queries

### 1. Simple Subquery

A basic subquery is written within parentheses and can be used in the `WHERE`, `FROM`, or `SELECT` clauses.

#### Example of a Subquery in the `WHERE` Clause:
```sql
SELECT first_name, last_name
FROM employees
WHERE department_id = (SELECT department_id FROM departments WHERE department_name = 'Sales');
```
In this query, the subquery retrieves the department_id of the 'Sales' department, 
and the outer query uses that result to find all employees in that department.

Example of a Subquery in the SELECT Clause:
```sql
SELECT first_name, 
       (SELECT department_name FROM departments WHERE department_id = employees.department_id) AS department_name
FROM employees;
```
Here, the subquery retrieves the department_name for each employee by matching the department_id.

### 2. Single-row Subquery
A single-row subquery returns a single row and is commonly used with operators like =, <, >, <=, >=, and <>.

Example:
```sql
SELECT first_name, last_name
FROM employees
WHERE salary = (SELECT MAX(salary) FROM employees);
```
This query finds the employee(s) with the highest salary. The subquery returns a single value (the maximum salary), which is used in the WHERE condition.

### 3. Multiple-row Subquery
A multiple-row subquery returns multiple rows of data and is typically used with operators like IN, ANY, or ALL.

Example with IN:
```sql
SELECT first_name, last_name
FROM employees
WHERE department_id IN (SELECT department_id FROM departments WHERE location_id = 1400);
```
This query finds all employees who belong to departments located in location 1400. 
The subquery returns multiple department_id values, and the IN operator is used to match those values in the outer query.

Example with ANY:
```sql
SELECT first_name, last_name
FROM employees
WHERE salary > ANY (SELECT salary FROM employees WHERE department_id = 10);
```
This query returns employees whose salary is greater than any salary in department 10. 
The subquery returns multiple salary values, and ANY allows the outer query to compare each employee’s salary against those values.

4. Correlated Subquery
A correlated subquery references columns from the outer query, and it is evaluated once for each row processed by the outer query.
Unlike a regular subquery, which is executed independently, a correlated subquery depends on the outer query for its values.

Example of a Correlated Subquery:
```sql
SELECT first_name, last_name
FROM employees e
WHERE salary > (SELECT AVG(salary) FROM employees WHERE department_id = e.department_id);
```
In this query, the subquery calculates the average salary for each department and compares it with the salary of each employee. 
The subquery is correlated because it references the department_id from the outer query (e.department_id).

5. Non-correlated Subquery
A non-correlated subquery does not reference any columns from the outer query.
It is independent and executes once, returning a result that is used by the outer query.

Example of a Non-correlated Subquery:
```sql
SELECT first_name, last_name
FROM employees
WHERE department_id = (SELECT department_id FROM departments WHERE department_name = 'HR');
```
The subquery is non-correlated because it does not depend on the outer query. It simply returns the department_id of the 'HR' department.

### Nested Queries in FROM Clause
You can also use subqueries in the FROM clause, treating the subquery result as a virtual table (or derived table).

Example:
```sql
SELECT dept_avg.department_name, dept_avg.avg_salary
FROM (SELECT department_id, AVG(salary) AS avg_salary
      FROM employees
      GROUP BY department_id) AS dept_avg
JOIN departments d ON dept_avg.department_id = d.department_id;
```
Here, the subquery computes the average salary for each department, and the outer query joins this result with the departments table.

### Using EXISTS with Subqueries
The EXISTS operator is used with a subquery to check for the existence of rows. 
The subquery returns a Boolean value, and EXISTS returns TRUE if the subquery returns at least one row.

Example:
```sql
SELECT first_name, last_name
FROM employees e
WHERE EXISTS (SELECT 1 FROM departments d WHERE d.department_id = e.department_id AND d.department_name = 'HR');
```
This query returns employees who belong to the 'HR' department. 
The subquery checks for the existence of an 'HR' department with the same department_id as the outer query's employee.department_id.

### Benefits of Using Nested Queries
- Modularity: Break down complex queries into smaller, more manageable components.
- Readability: Improve the readability of the query by isolating certain logic into subqueries.
- Efficiency: Use subqueries for operations where the result of one query is needed in another,
- reducing the need for multiple joins or complex filtering.

### Performance Considerations
While subqueries are a powerful tool, they can sometimes lead to performance issues, especially when correlated subqueries are involved. 
In some cases, subqueries can be replaced with joins to improve performance.

- Non-correlated subqueries are often more efficient because they are executed only once.
- Correlated subqueries can be slower since they are evaluated once for each row processed by the outer query.

In general, test and analyze query performance to determine the most efficient approach.


## CTE:
# SQL Common Table Expressions (CTE)

A **Common Table Expression (CTE)** is a temporary result set that can be referenced within a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement. CTEs make it easier to write and read complex queries by breaking them down into simpler, reusable components.

## Syntax of CTE

A CTE is defined using the `WITH` keyword, followed by the CTE name, an optional column list, and a query that defines the CTE.

```sql
WITH cte_name AS (
    -- Query that defines the CTE
    SELECT column1, column2
    FROM table_name
    WHERE condition
)
SELECT column1, column2
FROM cte_name;
```
Explanation:
WITH: Starts the definition of the CTE.
cte_name: The name you give to the CTE, which you can reference in the main query.

The subquery inside the parentheses defines the result set for the CTE.

### Benefits of Using CTE
- Readability: CTEs allow you to break down complex queries into simpler parts, making them easier to read and understand.
- Reusability: You can reference the CTE multiple times within the same query.
- Recursion: CTEs can be recursive, which allows you to perform operations such as traversing hierarchical or tree-structured data (e.g., organizational charts, bill of materials).
- Improved Organization: Organize the query logic into a single query block rather than embedding subqueries in the FROM or WHERE clause.

EG:
```sql
WITH avg_salary AS (
    SELECT department_id, AVG(salary) AS avg_dept_salary
    FROM employees
    GROUP BY department_id
)
SELECT e.first_name, e.last_name, e.salary, a.avg_dept_salary
FROM employees e
JOIN avg_salary a ON e.department_id = a.department_id
WHERE e.salary > a.avg_dept_salary;
```


# SQL Views

A **View** in SQL is a virtual table that represents the result of a query. It doesn't store data physically but stores the SQL query that can be used to retrieve the data. Views are useful for simplifying complex queries, providing a layer of abstraction, and enhancing security by limiting access to certain columns or rows.

## What is a View?

A **View** is a saved query that you can treat like a table. It can be used in `SELECT`, `INSERT`, `UPDATE`, and `DELETE` statements, just like a regular table, but the data in a view is dynamically retrieved from the underlying base tables every time it is accessed.

### Key Points:
- A view contains a **SELECT query**.
- Views do not store data themselves; they pull data from the underlying tables each time they are queried.
- They are often used to simplify complex queries, encapsulate business logic, and restrict data access.

---

## Creating a View

A view is created using the `CREATE VIEW` statement, followed by the view name and the query that defines it.

### Syntax:
```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

Example of Creating a Simple View:
```sql
CREATE VIEW employee_view AS
SELECT first_name, last_name, department_id
FROM employees
WHERE department_id = 10;
```

In this example:

A view named employee_view is created.
The view retrieves the first_name, last_name, and department_id columns from the employees table, but only for employees who belong to department 10.
Querying a View
Once a view is created, you can query it just like a table.

Example:
```sql
SELECT * FROM employee_view;
```
This query retrieves all columns and rows defined in the employee_view view.

### Updating Data Through a View
In some cases, you can update data through a view, but only if the view meets certain criteria:

The view must reference a single base table.
The view should not contain aggregates, GROUP BY, DISTINCT, or JOINs.

Example of an Updatable View:

```sql
CREATE VIEW salary_view AS
SELECT employee_id, salary
FROM employees;

UPDATE salary_view
SET salary = 55000
WHERE employee_id = 1001;
```
In this case, the salary_view can be updated because it references only a single table (employees) and does not have any complex logic.

### Dropping a View
To remove a view, you can use the DROP VIEW statement.

Syntax:
```sql
DROP VIEW view_name;
```
Example:
```sql
DROP VIEW employee_view;
```
This command removes the employee_view from the database.

### Advantages of Using Views
- Simplify Complex Queries: You can encapsulate complex queries into views and use them as if they were tables, making your SQL code cleaner and more readable.
- Data Abstraction: Views can hide complex joins, calculations, and data structures, providing a simpler interface for users and applications.
- Security: Views can be used to restrict access to specific columns or rows of a table. For example, you can create a view that shows only a subset of columns, providing limited access to sensitive data.
- Consistency: Views allow you to present a consistent interface to the data, even if the underlying schema changes.

## Types of Views
- Simple View: A view that directly retrieves data from one or more base tables, without any complex calculations or aggregates.

Example: A simple SELECT query from a table or basic JOIN.

- Complex View: A view that involves complex queries, such as multiple JOIN statements, aggregates (SUM(), AVG()), GROUP BY, etc.

Example: A view that combines data from multiple tables using JOIN or performs calculations.

- Materialized View (or Snapshot View): Unlike regular views, materialized views store the results of the query in the database, 
making data retrieval faster. They need to be manually refreshed when the data changes.

## Updating Data Through a View
In some scenarios, you can insert, update, or delete data through a view, but there are conditions:

The view must refer to only one base table.
The view must not include aggregated data, DISTINCT, GROUP BY, or JOIN.

Example of Inserting Data Through a View:
```sql
CREATE VIEW department_view AS
SELECT employee_id, department_id, salary
FROM employees
WHERE department_id = 10;

INSERT INTO department_view (employee_id, department_id, salary)
VALUES (2005, 10, 55000);
```
In this case, the department_view is created, and new records can be inserted into the underlying table through the view.

### Limitations of Views
1. Performance: Views do not improve query performance directly. Since views are just stored queries, 
they may introduce overhead if the underlying query is complex.
1. Non-Updatable Views: Views that contain JOINs, GROUP BY, or aggregation functions are often non-updatable, 
meaning you cannot perform INSERT, UPDATE, or DELETE operations directly on them.
No Physical Storage: Views do not store any data physically. They are virtual and are executed every time you query them.


## Views vs CTE:

| Feature         | View                               | CTE                                                 |
|-----------------|------------------------------------|-----------------------------------------------------|
| Persistence     | Persistent (remains in the schema) | Temporary (only lasts for one query)                |
| Reusability     | Reusable across multiple queries   | Only valid for the duration of the query            |
| Performance     | May cause overhead if complex      | Can have performance overhead if complex            |
| Complex Queries | Can encapsulate complex logic      | Helps organize complex queries within one query     |
| Recursion       | Does not support recursion         | Supports recursion (for hierarchical data)          |
| Updateability   | Can be updatable or non-updatable  | Generally not directly updatable                    |
| Security        | Can restrict data access           | Does not provide security features                  |
| Use Cases       | Reusable data abstraction          | Temporary, simplifying complex queries or recursion |
