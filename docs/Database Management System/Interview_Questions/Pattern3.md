# Pattern 3: CTEs (Common Table Expressions) & Recursive Queries 

- CTEs are crucial for writing clean, readable queries. 
- Recursive CTEs are a key test for handling hierarchical data.

## Easy

### 1. Using a CTE, find the department with the highest average salary.
Department Table:
```
| department_id | department_name  |
|---------------|------------------|
| 1             | Engineering      |
| 2             | Human Resources  |
| 3             | Sales            |
| 4             | Marketing        |
| 5             | Finance          |
```
Employees Table:
```
| employee_id | employee_name  | salary    | department_id |
|-------------|----------------|-----------|---------------|
| 1           | Alice Johnson  | 95000.00  | 1             |
| 2           | Bob Williams   | 110000.00 | 1             |
| 3           | Charlie Brown  | 85000.00  | 1             |
| 4           | Diana Prince   | 120000.00 | 1             |
| 5           | Eve Adams      | 65000.00  | 2             |
| 6           | Frank White    | 70000.00  | 2             |
| 7           | Grace Hall     | 68000.00  | 2             |
| 8           | Henry Clark    | 80000.00  | 3             |
| 9           | Ivy Lewis      | 82000.00  | 3             |
| 10          | Jack Robinson  | 78000.00  | 3             |
| 11          | Karen Walker   | 90000.00  | 3             |
| 12          | Liam Scott     | 72000.00  | 4             |
| 13          | Mia King       | 75000.00  | 4             |
| 14          | Noah Green     | 71000.00  | 4             |
| 15          | Olivia Harris  | 100000.00 | 5             |
| 16          | Peter Wright   | 105000.00 | 5             |
| 17          | Quinn Hill     | 98000.00  | 5             |
```
SQL
```sql
with department_salary as (
    SELECT 
        e.department_id,
        d.department_name,
        AVG(e.salary) as avg_salary
    FROM employees e
        INNER JOIN departments d on d.department_id = e.department_id
    GROUP BY e.department_id, d.department_name
)

SELECT 
    department_id, 
    department_name, 
    avg_salary
from department_salary
ORDER BY avg_salary DESC LIMIT 1;
```
Result:
```
| department_id | department_name | avg_salary |
|---------------|-----------------|------------|
| 1             | Engineering     | 102500.00  |
```

### 2. Breaking Down a Join

- Rewrite a query that joins three tables (customers, orders, order_details) to calculate total revenue per customer, using a CTE to first aggregate the order_details.

Customers Table
```
| customer_id | customer_name |
|-------------|---------------|
| 1           | John Smith    |
| 2           | Jane Doe      |
| 3           | Peter Jones   |
```
Orders Table
```
| order_id | customer_id | order_date  |
|----------|-------------|-------------|
| 1        | 1           | 2023-10-01  |
| 2        | 1           | 2023-10-15  |
| 3        | 2           | 2023-10-05  |
| 4        | 3           | 2023-10-20  |
```
Order Details
```
| order_id | order_value |
|----------|-------------|
| 3        | 650.00      |
| 4        | 190.00      |
| 2        | 75.00       |
| 1        | 1225.00     |
```
SQL
```sql
WITH order_value_data AS (
SELECT
    od.order_id,
    SUM(od.quantity * price_per_unit) as order_value
from order_details od
GROUP BY od.order_id
)

SELECT
    o.customer_id,
    SUM(ov.order_value) as revenue
from order_value_data as ov
INNER JOIN orders o on ov.order_id = o.order_id
INNER JOIN customers c on c.customer_id = o.customer_id
GROUP BY o.customer_id
ORDER BY revenue DESC
```
Result:
```
| customer_id | revenue |
|-------------|---------|
| 1           | 1300.00 |
| 2           | 650.00  |
| 3           | 190.00  |
```