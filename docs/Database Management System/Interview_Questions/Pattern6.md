# Pattern 6: Data Transformation & Tricky Scenarios

## Easy

### Pivoting with CASE

- You have a sales table with month and amount. Write a query to show total sales for 'Jan', 'Feb', and 'Mar' as columns in a single row.

```sql
SELECT
    SUM(CASE WHEN month = 'JAN' THEN amount ELSE 0 END)
    SUM(CASE WHEN month = 'FEB' THEN amount ELSE 0 END)
    SUM(CASE WHEN month = 'MAR' THEN amount ELSE 0 END)
From sales;
```

### Handling NULLs: What is the difference between COUNT(\*) , COUNT(column), and COUNT(DISTINCT column)? How does each one handle NULL values?
| Expression               | Counts                       | NULL Handling  |
| ------------------------ | ---------------------------- | -------------- |
| `COUNT(*)`               | All rows                     | Includes NULLs |
| `COUNT(column)`          | Non-NULL rows in that column | Excludes NULLs |
| `COUNT(DISTINCT column)` | Unique non-NULL values       | Excludes NULLs |



### COALESCE: A users table has display_name and full_name columns. The display_name is sometimes NULL.

- Write a query to return the display_name if it exists, otherwise return the full_name.
```sql
SELECT 
    COALESCE(display_name, full_name) AS name
FROM users;
```
- What is COALESCE?
    - COALESCE(expr1, expr2, expr3, …)
    - It returns the first non-NULL value from the list of expressions.
    - If all are NULL, then it returns NULL.


