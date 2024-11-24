## BASIC SELECT STATEMENT

1. Retrieve all columns and rows from a table named students.
```SQL
SELECT * FROM STUDENTS
```

2. Fetch only the name and age columns from a table named customers.
```SQL
SELECT NAME,AGE FROM CUSTOMERS
```

3. Select all rows where the country column in the suppliers table is "India".
```SQL
SELECT * FROM SUPPLIERS
WHERE COUNTRY = 'India'
```

4. Retrieve the unique values from the department column in the employees table.
```SQL
SELECT DISTINCT DEPARTMENT FROM EMPLOYEES
```

5. Display the first 10 rows from the orders table.
```SQL
SELECT * FROM ORDERS
LIMIT 10
```

6. Fetch all columns from the products table, but only for rows where the price is greater than 100.
```SQL
SELECT * FROM PRODUCTS
WHERE PRICE > 100
```

7. Select the first_name and last_name columns from the users table and sort the result by last_name in ascending order.
```SQL
SELECT FIRST_NAME,LAST_NAME FROM USERS
ORDER BY LAST_NAME
```

8. Retrieve all rows from the sales table where the quantity column is greater than 5 and the status column is "completed".
```SQL
SELECT * FROM SALES
WHERE QUANTITY > 5
AND STATUS = 'COMPLETED'
```

9. Fetch only the product_name and category columns from the inventory table, ensuring no duplicate rows are included in the result.
```SQL
SELECT DISTINCT PRODUCT_NAME,CATEGORY FROM INVENTORY
```

10. Select all rows from the transactions table but display only the first 5 rows.
```SQL
SELECT * FROM TRANSACTIONS
LIMIT 5
```

## Intermediate SELECT Statement Questions
1. Select the name, age, and city columns from the customers table but display the results only for rows where the age is between 25 and 40.
```SQL
SELECT NAME,AGE,CITY FROM CUSTOMERS
WHERE AGE BETWEEN 25 AND 40
```
2. Retrieve all rows from the employees table, but display the results sorted by department in ascending order and salary in descending order.
```SQL
SELECT * FROM EMPLOYEES
ORDER BY DEPARTMENT ASC,SALARY DESC
```

3. Write a query to fetch all columns from the orders table where the order_date is in the last 30 days.
```SQL
SELECT * FROM ORDERS
WHERE CURRENT_DATE - ORDER_DATE <= 30
```

4. Use an alias to rename the product_name column as Product and the price column as Cost in the result set from the products table.
```SQL
SELECT PRODUCT_NAME AS PRODUCT, PRICE AS COST
FROM PRODUCTS
```

5. Combine the first_name and last_name columns in the users table into a single column called Full_Name and display the result.
```SQL
SELECT CONCAT(FIRST_NAME,' ',LAST_NAME) AS FULL_NAME FROM USERS
```

6. Select the top 3 highest salaries from the salaries table.
```SQL
SELECT * FROM SALARIES
ORDER BY SALARY DESC
LIMIT 3
```

7. Write a query to retrieve all columns from the sales table where the quantity is greater than 50 and the region is either "North" or "South."
```SQL
SELECT * FROM SALES
WHERE QUANTITY > 50
AND REGION IN ('NORTH','SOUTH')
```

8. Fetch all rows from the transactions table where the status is not "Pending" and the amount is greater than 500.
```SQL
SELECT * FROM TRANSACTIONS 
WHERE STATUS <> 'PENDING'
AND AMOUNT > 500
```

9. Count the total number of rows in the orders table where the status is "Shipped."
```SQL
SELECT COUNT(*) FROM ORDERS
WHERE STATUS = 'SHIPPED'
```

10. Display the distinct combination of department and location from the offices table.
```SQL
SELECT DISTINCT DEPARTMENT,LOCATION
FROM OFFICES
```


## Advanced SELECT Statement Questions
1. Join Two Tables
Retrieve the order_id, product_name, and quantity from the orders table, and the supplier_name from the suppliers table. 
Ensure that the results only include orders where the supplier_id from both tables match.
```SQL
SELECT ORDER_ID,PRODUCT_NAME,QUANTITY ,SUPPLIER_NAME
FROM ORDERS
JOIN SUPPLIERS
USING (SUPPLIER_ID)
```

2. Group and Aggregate
Write a query to find the total sales (amount) for each product from the sales table. Group the results by product_id.
```SQL
SELECT PRODUCT_ID, SUM(AMOUNT) FROM SALES
GROUP BY PRODUCT_ID
```

3. Subquery in WHERE Clause
Retrieve all the columns from the employees table where the department_id is greater than the average department_id from the departments table.
```SQL
SELECT * FROM EMPLOYEES
WHERE DEPARTMENT_ID > ( SELECT AVG(DEPARTMENT_ID) FROM DEPARTMENTS)
```

4. Self Join
Retrieve the employee_id, employee_name, and manager_id from the employees table. 
Show the employee's name and their manager_name (if available). Perform a self-join on the employees table using manager_id.

```SQL
SELECT E.EMPLOYEE_ID, E.EMPLOYEE_NAME, M.MANAGER_ID, M.MANAGER_NAME
FROM EMPLOYEES E
JOIN EMPLOYEES M
ON E.MANAGER_ID = M.EMPLOYEE_ID;
```

5. HAVING Clause
Write a query to find the departments in the employees table that have more than 5 employees. 
Group by department_id and filter the results using the HAVING clause.
```SQL
SELECT DEPARTMENTS FROM EMPLOYEES
GROUP BY DEPARTMENT_ID
HAVING COUNT(EMPLOYEES) > 5
```

6. Window Functions
Retrieve the employee_id, salary, and the rank of each employee based on their salary from the employees table. 
Rank employees in descending order of their salary.
```SQL
SELECT EMPLOYEE_ID,SALARY, RANK() OVER (ORDER BY SALARY DESC) FROM EMPLOYEES
```

7. UNION
Write a query to combine the first_name and last_name from the employees table and the first_name and last_name 
from the customers table, ensuring that no duplicates are included in the result.
```SQL
SELECT FIRST_NAME,LAST_NAME FROM EMPLOYEES
UNION
SELECT FIRST_NAME,LAST_NAME FROM CUSTOMERS
```

8. CASE Statement
Write a query to retrieve the product_name and a new column price_category from the products table. 
Assign a value of 'Expensive' if the price is greater than 100, and 'Affordable' if the price is less than or equal to 100.
```SQL
SELECT PRODUCT_NAME,
CASE
  WHEN PRICE > 100 THEN 'EXPENSIVE'
  ELSE 'AFFORDABLE'
  END AS PRICE_CATEGORY
FROM PRODUCTS
```

9. Multiple Joins
Retrieve the student_id, student_name, course_name, and instructor_name by joining the students, enrollments, and courses tables. 
Ensure that you show results for students enrolled in courses taught by instructors with the last name 'Smith'.
```SQL
SELECT S.STUDENT_ID, S.STUDENT_NAME, C.COURSE_NAME, C.INSTRUCTOR_NAME
FROM STUDENTS S
JOIN ENROLLMENTS E ON S.STUDENT_ID = E.STUDENT_ID
JOIN COURSES C ON E.COURSE_ID = C.COURSE_ID
WHERE C.INSTRUCTOR_NAME LIKE '%SMITH';
```

10. Nested Subquery
Write a query to retrieve all the employees from the employees table who earn more than the average salary of employees in the employees table.

```SQL
SELECT * FROM EMPLOYEES
WHERE SALARY > (SELECT AVG(SALARY) FROM EMPLOYEES)
```

