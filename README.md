
### SQL Commands Used in Data Engineering

#### Data Retrieval and Manipulation

| SQL Command             | Description                                                                                      | Example Usage                                                                                     |
|-------------------------|--------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| **SELECT**              | Retrieves data from one or more tables.                                                           | `SELECT * FROM employees;`                                                                        |
| **INSERT INTO**         | Inserts new rows into a table.                                                                    | `INSERT INTO customers (customer_id, customer_name) VALUES (1, 'John Doe');`                        |
| **UPDATE**              | Modifies existing rows in a table.                                                                | `UPDATE products SET price = price * 1.05 WHERE category = 'Electronics';`                          |
| **DELETE**              | Deletes rows from a table.                                                                        | `DELETE FROM orders WHERE order_date < '2023-01-01';`                                               |
| **JOIN**                | Retrieves data from multiple tables based on a related column between them.                        | `SELECT orders.order_id, customers.customer_name FROM orders JOIN customers ON orders.customer_id = customers.customer_id;` |
| **INNER JOIN**          | Returns rows when there is at least one match in both tables.                                      | `SELECT customers.customer_name, orders.order_date FROM customers INNER JOIN orders ON customers.customer_id = orders.customer_id;` |
| **LEFT JOIN (OUTER)**   | Returns all rows from the left table and matching rows from the right table.                       | `SELECT customers.customer_name, orders.order_date FROM customers LEFT JOIN orders ON customers.customer_id = orders.customer_id;` |
| **RIGHT JOIN (OUTER)**  | Returns all rows from the right table and matching rows from the left table.                       | `SELECT customers.customer_name, orders.order_date FROM customers RIGHT JOIN orders ON customers.customer_id = orders.customer_id;` |
| **FULL OUTER JOIN**     | Returns all rows when there is a match in either left or right table.                              | `SELECT customers.customer_name, orders.order_date FROM customers FULL OUTER JOIN orders ON customers.customer_id = orders.customer_id;` |
| **UNION**               | Combines the result sets of two or more SELECT statements (removes duplicates).                     | `SELECT customer_name FROM customers WHERE city = 'New York' UNION SELECT customer_name FROM customers WHERE city = 'Los Angeles';` |
| **EXCEPT**              | Returns distinct rows from the left SELECT statement that are not returned by the right SELECT statement. | `SELECT customer_name FROM customers WHERE city = 'New York' EXCEPT SELECT customer_name FROM customers WHERE city = 'Los Angeles';` |
| **INTERSECT**           | Returns distinct rows that are output by both the left and right SELECT statements.                 | `SELECT customer_name FROM customers WHERE city = 'New York' INTERSECT SELECT customer_name FROM customers WHERE city = 'Los Angeles';` |

#### Table and Index Management

| SQL Command             | Description                                                                                      | Example Usage                                                                                     |
|-------------------------|--------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| **CREATE TABLE**        | Creates a new table in the database.                                                              | ```sql CREATE TABLE products (product_id INT, product_name VARCHAR(255));```                         |
| **ALTER TABLE**         | Modifies an existing table (e.g., add or drop columns, constraints).                              | `ALTER TABLE employees ADD COLUMN salary DECIMAL(10, 2);`                                            |
| **DROP TABLE**          | Deletes an existing table from the database.                                                       | `DROP TABLE customers;`                                                                            |
| **CREATE INDEX**        | Creates an index on a table to improve query performance.                                          | `CREATE INDEX idx_customer_id ON orders (customer_id);`                                              |
| **DROP INDEX**          | Removes an index from a table.                                                                    | `DROP INDEX idx_customer_id ON orders;`                                                             |
| **TRUNCATE TABLE**      | Deletes all rows from a table without logging individual row deletions.                            | `TRUNCATE TABLE customers;`                                                                        |
| **RENAME TABLE**        | Renames a table.                                                                                 | `RENAME TABLE products TO inventory;`                                                               |

#### Data Aggregation and Grouping

| SQL Command             | Description                                                                                      | Example Usage                                                                                     |
|-------------------------|--------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| **GROUP BY**            | Groups rows that have the same values into summary rows (aggregate functions can be used).        | `SELECT department, SUM(salary) AS total_salary FROM employees GROUP BY department;`                |
| **HAVING**              | Specifies a condition for filtering rows after a GROUP BY clause.                                   | `SELECT department, AVG(salary) AS avg_salary FROM employees GROUP BY department HAVING AVG(salary) > 50000;` |
| **ORDER BY**            | Sorts the result set in ascending or descending order.                                             | `SELECT product_name, unit_price FROM products ORDER BY unit_price DESC;`                            |
| **DISTINCT**            | Retrieves unique rows from a result set.                                                           | `SELECT DISTINCT category FROM products;`                                                           |
| **WINDOW FUNCTIONS**    | Functions that perform calculations across a set of table rows related to the current row.         | `SELECT product_name, unit_price, AVG(unit_price) OVER (PARTITION BY category) AS avg_category_price FROM products;` |
| **ROW_NUMBER()**        | Assigns a unique sequential integer to each row within a partition of a result set.                | `SELECT product_name, unit_price, ROW_NUMBER() OVER (ORDER BY unit_price DESC) AS rank FROM products;` |
| **RANK()**              | Assigns a unique rank to each row within the partition of a result set, with gaps in ranking values. | `SELECT product_name, unit_price, RANK() OVER (PARTITION BY category ORDER BY unit_price DESC) AS rank FROM products;` |
| **DENSE_RANK()**        | Assigns a unique rank to each row within the partition of a result set, without gaps in ranking values. | `SELECT product_name, unit_price, DENSE_RANK() OVER (PARTITION BY category ORDER BY unit_price DESC) AS rank FROM products;` |
| **CUBE and ROLLUP**     | Provides multi-dimensional analysis of GROUP BY results (CUBE generates all possible subtotals, ROLLUP generates hierarchical subtotals). | `SELECT department, SUM(salary) AS total_salary FROM employees GROUP BY ROLLUP(department);`         |

#### Joins and Subqueries

| SQL Command             | Description                                                                                      | Example Usage                                                                                     |
|-------------------------|--------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| **SUBQUERY**            | Executes a query nested within another query.                                                      | `SELECT product_name FROM products WHERE category_id IN (SELECT category_id FROM categories WHERE category_name = 'Electronics');` |
| **SELF JOIN**           | Joins a table to itself using table aliases to compare rows within the same table.                | `SELECT e1.employee_name, e2.manager_name FROM employees e1 INNER JOIN employees e2 ON e1.manager_id = e2.employee_id;` |
| **CROSS JOIN**          | Returns the Cartesian product of two tables (all possible combinations of rows).                   | `SELECT product_name, category_name FROM products CROSS JOIN categories;`                           |
| **EQUI JOIN**           | A specific type of JOIN where the joined tables have equivalent columns.                           | `SELECT customers.customer_name, orders.order_date FROM customers, orders WHERE customers.customer_id = orders.customer_id;` |
| **NATURAL JOIN**        | Performs a JOIN using all columns with the same name in both tables.                               | `SELECT customers.customer_name, orders.order_date FROM customers NATURAL JOIN orders;`             |
| **ANTI JOIN**           | Returns rows from the left table that do not have a match in the right table.                       | `SELECT customers.customer_name FROM customers LEFT JOIN orders ON customers.customer_id = orders.customer_id WHERE orders.customer_id IS NULL;` |
| **SEMANTI JOIN**        | Joins two tables based on the similarity of their content.                                         | `SELECT * FROM customers, orders WHERE customers SIMILAR TO orders;`                                |
| **LEFT SEMI JOIN**      | Returns all columns from the left table when a match exists in the right table.                     | `SELECT * FROM customers LEFT SEMI JOIN orders ON customers.customer_id = orders.customer_id;`      |

#### Data Analysis Functions

| SQL Command             | Description                                                                                      | Example Usage                                                                                     |
|-------------------------|--------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| **SUM()**               | Calculates the sum of values in a column or within a window frame.                                 | `SELECT department, SUM(salary) AS total_salary FROM employees;`                                     |
| **AVG()**               | Calculates the average of values in a column or within a window frame.                             | `SELECT department, AVG(salary) AS avg_salary FROM employees;`                                       |
| **COUNT()**             | Counts the number of rows or non-null values in a column or within a window frame.                 | `SELECT department, COUNT(*) AS employee_count FROM employees;`                                      |
| **MIN()**               | Finds the minimum value in a column or within a window frame.                                      | `SELECT department, MIN(salary) AS min_salary FROM employees;`                                       |
| **MAX()**               | Finds the maximum value in a column or within a window frame.                                      | `SELECT department, MAX(salary) AS max_salary FROM employees;`                                       |
| **PARTITION BY**        | Divides the result set into partitions to which the window function is applied.                    | `SELECT product_name, unit_price, AVG(unit_price) OVER (PARTITION BY category) AS avg_category_price FROM products;` |
| **ORDER BY**            | Specifies how rows
