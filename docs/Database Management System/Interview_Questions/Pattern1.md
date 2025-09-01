# Pattern 1: Window Functions & Time-Series Analysis

These scenarios test your ability to perform complex calculations across related sets of rows, which is essential for analytics, reporting, and feature logic.

## Easy

### 1. Simple Ranking: Find the top 5 employees with the highest salaries in the entire company.

```sql
SELECT emp.id, emp.name 
from employee emp
order by emp.salary DESC 
LIMIT 5
```

### 2. Departmental Ranking: List employees in each department, ranked by their salary from highest to lowest.
Table:
```
| id | name            | department   | salary |
| 1  | "Alice Johnson" | "Engineering" | 95000  |
| 2  | "Bob Williams"  | "Engineering" | 90000  |
| 3  | "Charlie Brown" | "Engineering" | 90000  |
| 4  | "David Smith"   | "Engineering" | 82000  |
| 5  | "Grace Lee"     | "Engineering" | 110000 |
| 6  | "Eve Davis"     | "Sales"       | 88000  |
| 7  | "Frank Miller"  | "Sales"       | 76000  |
| 8  | "Diana Moore"   | "Sales"       | 89000  |
| 9  | "Henry Wilson"  | "Marketing"   | 75000  |
| 10 | "Ivy Taylor"    | "Marketing"   | 75000  |
| 11 | "Jack Anderson" | "Marketing"   | 81000  |
| 12 | "Karen Thomas"  | "HR"          | 65000  |
| 13 | "Leo Jackson"   | "HR"          | 68000  |
| 14 | "Mia White"     | "HR"          | 65000  |
| 15 | "Noah Harris"   | "Sales"       | 91000  |

```
SQL:
```sql
SELECT
    name,
    department,
    salary,
    RANK() OVER (PARTITION BY department order by salary) as department_rank
FROM
    employee;
```
Result:
```
| name           | department   | salary | rank |
| :------------- | :----------- | :----- | :--- |
| "David Smith"  | "Engineering" | 82000  | 1    |
| "Bob Williams" | "Engineering" | 90000  | 2    |
| "Charlie Brown"| "Engineering" | 90000  | 2    |
| "Alice Johnson"| "Engineering" | 95000  | 4    |
| "Grace Lee"    | "Engineering" | 110000 | 5    |
| "Mia White"    | "HR"          | 65000  | 1    |
| "Karen Thomas" | "HR"          | 65000  | 1    |
| "Leo Jackson"  | "HR"          | 68000  | 3    |
| "Henry Wilson" | "Marketing"   | 75000  | 1    |
| "Ivy Taylor"   | "Marketing"   | 75000  | 1    |
| "Jack Anderson"| "Marketing"   | 81000  | 3    |
| "Frank Miller" | "Sales"       | 76000  | 1    |
| "Eve Davis"    | "Sales"       | 88000  | 2    |
| "Diana Moore"  | "Sales"       | 89000  | 3    |
| "Noah Harris"  | "Sales"       | 91000  | 4    |
```
### 3. Previous and Next Value: For each order, show the order ID, order date, and the date of the very next order placed by the same customer.
Table:
```
| order_id | customer_id | order_date   | order_amount |
| :------- | :---------- | :----------- | :----------- |
| 101      | 1           | 2023-01-15   | 150.50       |
| 102      | 2           | 2023-01-17   | 200.00       |
| 103      | 1           | 2023-02-10   | 75.25        |
| 104      | 3           | 2023-02-20   | 320.00       |
| 105      | 2           | 2023-03-05   | 50.75        |
| 106      | 1           | 2023-03-12   | 220.40       |
| 107      | 3           | 2023-04-01   | 180.00       |
| 108      | 2           | 2023-04-22   | 90.10        |
| 109      | 1           | 2023-05-18   | 110.00       |
| 110      | 3           | 2023-05-21   | 450.60       |
```
SQL Query:
```sql
SELECT 
    customer_id,
    order_id,
    order_date,
    LEAD(order_date, 1) OVER (PARTITION by customer_id ORDER by order_date asc) as next_order_date
from orders
order by customer_id ASC, order_date asc;
```
Result:
```
| customer_id | order_id | order_date   | next_order_date |
| :---------- | :------- | :----------- | :-------------- |
| 1           | 101      | 2023-01-15   | 2023-02-10      |
| 1           | 103      | 2023-02-10   | 2023-03-12      |
| 1           | 106      | 2023-03-12   | 2023-05-18      |
| 1           | 109      | 2023-05-18   |                 |
| 2           | 102      | 2023-01-17   | 2023-03-05      |
| 2           | 105      | 2023-03-05   | 2023-04-22      |
| 2           | 108      | 2023-04-22   |                 |
| 3           | 104      | 2023-02-20   | 2023-04-01      |
| 3           | 107      | 2023-04-01   | 2023-05-21      |
| 3           | 110      | 2023-05-21   |                 |
```

### 4. Basic Running Total: Provide a daily report of sales that includes the day's total sales and a cumulative sum of sales since the beginning of the month. 
Table:
```
| id | date        | amount |
| :- | :---------- | :----- |
| 1  | "2025-08-01" | 150.50 |
| 2  | "2025-08-01" | 200.00 |
| 3  | "2025-08-02" | 300.25 |
| 4  | "2025-08-03" | 50.75  |
| 5  | "2025-08-03" | 75.00  |
| 6  | "2025-08-04" | 450.00 |
| 7  | "2025-08-05" | 120.50 |
| 8  | "2025-08-05" | 80.00  |
| 9  | "2025-08-06" | 210.75 |
```
SQL:
```sql
SELECT 
    saledate,
    daily_total,
    SUM(daily_total) OVER (ORDER BY saledate) as cumulative_sum
from 
    (
        SELECT saledate, SUM(amount) as daily_total from sales GROUP by saledate
    ) as daily_sales;
```
Result:
```
| saledate    | daily_total | cumulative_sum |
| :---------- | ----------: | --------------:|
| "2025-08-01" | 350.50      | 350.50        |
| "2025-08-02" | 300.25      | 650.75        |
| "2025-08-03" | 125.75      | 776.50        |
| "2025-08-04" | 450.00      | 1226.50       |
| "2025-08-05" | 200.50      | 1427.00       |
| "2025-08-06" | 210.75      | 1637.75       |
```
Explanation:
- SUM(DailyTotal) OVER (ORDER BY SaleDate) AS RunningTotal: This is the window function that does the magic. ✨
- SUM(DailyTotal): This specifies that we want to sum the DailyTotal column.
- OVER (...): This keyword indicates that it's a window function, which performs a calculation across a set of table rows.
- ORDER BY SaleDate: This is the "window frame." It tells the SUM function how to accumulate the values. It sorts the rows by SaleDate and, for each row, it sums the DailyTotal of all rows from the beginning up to and including the current row.

### 5.  Row Numbering: Assign a unique sequential number to each user based on their sign-up date.
Table:
```
| user_id | username  | signup_date          |
| :------ | :-------- | :------------------- |
| 1       | "alice"   | "2023-01-15 10:30:00" |
| 2       | "bob"     | "2023-01-15 10:30:00" |
| 3       | "charlie" | "2023-02-05 11:15:00" |
| 4       | "diana"   | "2023-01-10 09:00:00" |
| 5       | "edward"  | "2023-03-20 18:45:00" |
| 6       | "fiona"   | "2023-02-05 11:14:00" |
```
SQL:
```sql
SELECT
    user_id,
    username,
    ROW_NUMBER() OVER (ORDER by signup_date) as unique_id
from users;
```
Result:
```
| user_id | username  | unique_id |
| :------ | :-------- | --------: |
| 4       | "diana"   | 1         |
| 1       | "alice"   | 2         |
| 2       | "bob"     | 3         |
| 6       | "fiona"   | 4         |
| 3       | "charlie" | 5         |
| 5       | "edward"  | 6         |
```
Note:
- ROW_NUMBER(): Always assigns a unique, consecutive number to each row, even if there's a tie in the ordering column. It will arbitrarily assign the next number in the sequence to one of the tied rows.

- RANK(): Assigns the same rank to tied rows. However, it then skips the next number(s) in the sequence. For example, if two users tie for 2nd place, they both get rank 2, and the next user gets rank 4 (skipping 3).

### 6. Simple Partitioning: What is the most expensive product in each product category ?
Table:
```
| product_id | product_name                   | category      | price   |
| :--------- | :----------------------------- | :-----------  | ------: |
| 1          | "4K OLED TV"                   | "Electronics" | 1499.99 |
| 2          | "Gaming Laptop"                | "Electronics" | 1499.99 |
| 3          | "High-End Smartphone"          | "Electronics" | 999.99  |
| 4          | "Noise-Cancelling Headphones"  | "Electronics" | 349.00  |
| 5          | "The Art of SQL"               | "Books"       | 45.50   |
| 6          | "A Tale of Two Databases"      | "Books"       | 25.00   |
| 7          | "Learning PostgreSQL: First Edition" | "Books" | 59.95   |
| 8          | "Advanced Python Programming"  | "Books"       | 75.25   |
| 9          | "Leather Jacket"               | "Clothing"    | 450.00  |
| 10         | "Designer Jeans"               | "Clothing"    | 150.75  |
| 11         | "Cashmere Sweater"             | "Clothing"    | 220.00  |
| 12         | "Silk Scarf"                   | "Clothing"    | 85.50   |
| 13         | "Robotic Vacuum Cleaner"       | "Home Goods"  | 600.00  |
| 14         | "Espresso Machine"             | "Home Goods"  | 850.99  |
| 15         | "Smart Refrigerator"           | "Home Goods"  | 2500.00 |
| 16         | "Air Purifier"                 | "Home Goods"  | 320.50  |
```
SQL:
```sql
WITH RankedProducts As (
    SELECT 
        product_id, 
        product_name, 
        category,
        price,
    ROW_NUMBER() OVER (PARTITION BY category ORDER by price DESC) as rank_by_price
    from products
)

SELECT product_id, product_name, category, price from RankedProducts where rank_by_price = 1;
```
Result:
```
| product_id | product_name                  | category     | price   |
| :--------- | :-------------------------    | :----------- | ------: |
| 8          | "Advanced Python Programming" | "Books"      | 75.25   |
| 9          | "Leather Jacket"              | "Clothing"   | 450.00  |
| 2          | "Gaming Laptop"               | "Electronics"| 1499.99 |
| 15         | "Smart Refrigerator"          | "Home Goods" | 2500.00 |

```

- CTE stands for Common Table Expression.
    - It's defined using the WITH keyword.
    - It creates a temporary "table" called RankedProducts.
    - This temporary table contains all the original columns (product_name, category, price) plus a new calculated column called rank_num.
    - The rank_num is calculated by the window function, which finds the rank of each product based on its price within each category.