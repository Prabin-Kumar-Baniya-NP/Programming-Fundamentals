# Pattern 4: Performance and Query Optimizations

## Easy

- Why is SELECT * considered a bad practice in production code?
    1. It fetches unnecessay columns which we may not require.
    2. When a new column is added, then select * will automatically include the new column and it may impact the schema changes for application server.
    3. The db query result size becomes big and it may lead to wastage of network and bandwidth.
    4. Security Concerns on leaking protected and sensitive columns.
    5. Performance Issues in Indexing.

- You have a users table and you frequently query it with WHERE email = '...'. What can you do to speed this up?
    1. Choose corect datatype to store email: Use charfield instead of Text field
    2. Use B-index on email column. SO db wont scan the entire table but instead use indexes to jump to that place where that email is stored.

- WHERE vs. HAVING: Explain the difference between the WHERE and HAVING clauses and how their placement affects a query.
    1. Use where, before peforming group by/ aggregation
    2. Use having, after performing group by/aggregation

- UNION vs. UNION ALL: What is the difference between UNION and UNION ALL? Which is more performant and why ?
    1. We use union to combine the result of two or more queries
    2. UNION removes duplicates and applies implict DISTINCT on the result. So it is slower due to sorting and duplicate removal process.
    3. UNION ALL does not remove duplicates and does not apply distinct on the result. It is faster than union as no duplication removal is added here.

- Slow Query on Large Table: A simple SELECT on a large table is slow. What's the most likely cause? 
    1. No index exists on the column(s) used in filtering (WHERE), joining, or sorting.
    2. The query is retrieving too many rows (no filters, or very broad filters). -> Use Pagination
