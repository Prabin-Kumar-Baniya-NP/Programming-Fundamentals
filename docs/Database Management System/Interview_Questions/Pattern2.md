# Pattern 2: Complex Joins, Aggregations, and Self-Joins

- This pattern tests your ability to synthesize information from multiple sources, correctly filter aggregated results, and find relationships within the same dataset.

## Easy 

### 1. Manager-Employee Salary Comparison 

- As part of a compensation fairness analysis, write a query to find all employees who earn more than their direct manager. 
- The employees table contains id, name, salary, and manager_id.
Table
```
| id | name            | salary  | manager_id |
| :- | :-------------- | ------: | ---------- |
| 1  | "John Smith"    | 100000  |            |
| 2  | "Jane Doe"      | 80000   | 1          |
| 3  | "Peter Jones"   | 60000   | 2          |
| 4  | "Lisa Williams" | 85000   | 2          |
| 5  | "David Brown"   | 70000   | 1          |
| 6  | "Emily Davis"   | 65000   | 5          |
| 7  | "Michael Miller"| 72000   | 5          |
| 8  | "Sarah Wilson"  | 50000   | 2          |
```
SQL:
```sql
SELECT 
    e.name as employee_name, 
    e.salary as employee_salary,
    m.name as manager_name,
    m.salary as manager_salary
from employees e
INNER JOIN employees m on e.manager_id = m.id
where e.salary > m.salary
```
Result:
```
| employee_name   | employee_salary | manager_name | manager_salary |
| :-------------- | --------------: | :----------- | --------------: |
| "Lisa Williams" | 85000           | "Jane Doe"   | 80000           |
| "Michael Miller"| 72000           | "David Brown"| 70000           |
```

### 2. Finding Orphaned Records
- For data cleanup, you need to find all authors who have no books associated with them. 
- A LEFT JOIN is a good approach here, but explain why and how you'd structure the query.

Author Table:
```
| author_id | author_name      |
|-----------|------------------|
| 1         | J.K. Rowling     |
| 2         | George Orwell    |
| 3         | J.R.R. Tolkien   |
| 4         | Virginia Woolf   |
| 5         | Jane Austen      |
```
Book Table
```
| book_id | title                                   | author_id |
|---------|-----------------------------------------|-----------|
| 1       | Harry Potter and the Sorcerer's Stone   | 1         |
| 2       | 1984                                    | 2         |
| 3       | Animal Farm                             | 2         |
| 4       | The Hobbit                              | 3         |
| 5       | The Lord of the Rings                   | 3         |
| 6       | Pride and Prejudice                     | 5         |
| 7       | Sense and Sensibility                   | 5         |
```
SQL Query:
```sql
SELECT
    a.author_id,
    a.author_name
From authors a
LEFT JOIN books b on b.author_id = a.author_id
where b.author_id is null;
```
Result:
```
| author_id | author_name   |
|-----------|---------------|
| 4         | Virginia Woolf |
```

### 3. Basic Aggregation with Filtering

- List all departments that have more than 10 employees. 
Department Table:
```
| department_id | department_name  |
|---------------|------------------|
| 1             | Engineering      |
| 2             | Human Resources  |
| 3             | Sales            |
| 4             | Marketing        |
```
Employee Table:
```
| employee_id | employee_name | department_id |
|-------------|---------------|---------------|
| 1           | Alice         | 1             |
| 2           | Bob           | 1             |
| 3           | Charlie       | 1             |
| 4           | David         | 1             |
| 5           | Eve           | 1             |
| 6           | Frank         | 1             |
| 7           | Grace         | 1             |
| 8           | Heidi         | 1             |
| 9           | Ivan          | 1             |
| 10          | Judy          | 1             |
| 11          | Karl          | 1             |
| 12          | Liam          | 1             |
| 13          | Mallory       | 2             |
| 14          | Niaj          | 2             |
| 15          | Olivia        | 2             |
| 16          | Peggy         | 2             |
| 17          | Quentin       | 2             |
| 18          | Rupert        | 3             |
| 19          | Sybil         | 3             |
| 20          | Trent         | 3             |
| 21          | Ursula        | 3             |
| 22          | Victor        | 3             |
| 23          | Walter        | 3             |
| 24          | Xavier        | 3             |
| 25          | Yvonne        | 3             |
| 26          | Zelda         | 3             |
| 27          | Aaron         | 3             |
| 28          | Brian         | 3             |
| 29          | Catherine     | 4             |
| 30          | Diana         | 4             |
| 31          | Edward        | 4             |
| 32          | Fiona         | 4             |
| 33          | George        | 4             |
| 34          | Hannah        | 4             |
| 35          | Ian           | 4             |
| 36          | Jack          | 4             |
```
SQL Query:
```sql
SELECT
    d.department_name,
    COUNT(e.employee_id) as num_of_employee
from employees e
INNER JOIN departments d ON d.department_id = e.department_id
GROUP By d.department_id
HAVING COUNT(e.employee_id) > 10
```
Result
```
| department_name | num_of_employee |
|-----------------|-----------------|
| Sales           | 11              |
| Engineering     | 12              |
```

### 4. Joining Three Tables
- Get a list of customer names, the products they bought, and the date of the transaction. 
- This requires joining customers, orders, and products.
Product Table:
```
| product_id | product_name | price  |
|------------|--------------|--------|
| 1          | Laptop       | 1200.00|
| 2          | Mouse        | 25.50  |
| 3          | Keyboard     | 75.00  |
| 4          | Monitor      | 300.00 |
```
Customers Table:
```
| customer_id | customer_name |
|-------------|---------------|
| 1           | John Smith    |
| 2           | Jane Doe      |
| 3           | Peter Jones   |
```
Orders Table:
```
| order_id | customer_id | product_id | order_date  |
|----------|-------------|------------|-------------|
| 1        | 1           | 1          | 2023-01-15  |
| 2        | 1           | 2          | 2023-01-15  |
| 3        | 2           | 4          | 2023-01-20  |
| 4        | 1           | 3          | 2023-01-22  |
| 5        | 3           | 1          | 2023-02-10  |
| 6        | 3           | 4          | 2023-02-10  |
```
SQL
```sql
SELECT
    c.customer_name,
    p.product_name,
    o.order_date
FROM orders o
INNER JOIN customers c ON c.customer_id = o.customer_id
INNER JOIN products p on p.product_id = o.product_id
```
Result:
```
| customer_name | product_name | order_date  |
|---------------|--------------|-------------|
| John Smith    | Laptop       | 2023-01-15  |
| John Smith    | Mouse        | 2023-01-15  |
| Jane Doe      | Monitor      | 2023-01-20  |
| John Smith    | Keyboard     | 2023-01-22  |
| Peter Jones   | Laptop       | 2023-02-10  |
| Peter Jones   | Monitor      | 2023-02-10  |
```
