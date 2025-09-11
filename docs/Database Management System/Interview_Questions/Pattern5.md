# Data Modeling and Schema Design

## Easy

### Normalization: What is database normalization? Briefly explain the purpose of 1NF, 2NF, and 3NF.

- Database normalization is the process of organizing data in a database to reduce redundancy (duplicate data) and improve data integrity (accuracy and consistency)

- First Normal Form:

    - Purpose: Eliminate repeating groups and ensure atomicity.
    - Instead of storing multiple phone numbers in one column, create separate rows for each number.

- Second Normal Form:

    - Purpose: Remove partial dependency.
    - A partial dependency happens when a non-key attribute depends on part of a composite primary key (not the whole key).
    - All non-key attributes must depend on the whole primary key, not just part of it.
    - If a table’s primary key is (StudentID, CourseID), then attributes like StudentName (which depends only on StudentID) should be moved to a separate table.

- Third Normal Form:
    - Purpose: Remove transitive dependency.
    - A transitive dependency happens when a non-key attribute depends on another non-key attribute, instead of depending directly on the primary key.
    - Non-key attributes should depend only on the primary key, not on other non-key attributes.
    - If Students table has columns (StudentID, DepartmentID, DepartmentName), then DepartmentName depends on DepartmentID, not directly on StudentID. So, split Department details into a separate table.

### Surrogate vs. Natural Key: What is the difference between a surrogate key and a natural key?

- Natural Key

    - A natural key is a primary key that comes directly from the business data itself.
    - It’s an attribute (or set of attributes) that naturally identifies a row.
    - Examples:
        - Social Security Number (SSN) for a person.
        - ISBN for a book.
        - Email address for a user.

- Surrogate Key
    - A surrogate key is an artificial key introduced by the system (usually an auto-increment integer or UUID).
    - It has no business meaning and only exists to uniquely identify a row.
    - Examples:
        - customer_id = 101 (auto-increment integer).
        - order_id = UUID.
