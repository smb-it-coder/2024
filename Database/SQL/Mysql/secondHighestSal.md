To find the second highest salary from an `employee` table in MySQL, you can use several approaches. Here are some common methods:

### 1. **Using Subqueries**

A common method is to use a subquery to find the maximum salary less than the highest salary. Here's how you can do it:

```sql
SELECT MAX(salary) AS second_highest_salary
FROM employee
WHERE salary < (SELECT MAX(salary) FROM employee);
```

### 2. **Using a Derived Table**

You can also use a derived table (subquery in the `FROM` clause) to find the top salaries and then select the second highest:

```sql
SELECT salary
FROM (
    SELECT DISTINCT salary
    FROM employee
    ORDER BY salary DESC
    LIMIT 2
) AS subquery
ORDER BY salary
LIMIT 1;
```

### 3. **Using Variables (MySQL-Specific)**

In MySQL, you can use user-defined variables to rank salaries and then select the second highest:

```sql
SET @rank := 0;
SET @prev_salary := NULL;

SELECT salary
FROM (
    SELECT salary,
           @rank := IF(@prev_salary = salary, @rank, @rank + 1) AS rank,
           @prev_salary := salary
    FROM employee
    ORDER BY salary DESC
) AS ranked_salaries
WHERE rank = 2;
```

### 4. **Using `ROW_NUMBER()` (MySQL 8.0+ Only)**

If you're using MySQL 8.0 or later, you can use window functions to achieve this more cleanly:

```sql
WITH RankedSalaries AS (
    SELECT salary,
           ROW_NUMBER() OVER (ORDER BY salary DESC) AS rn
    FROM employee
)
SELECT salary
FROM RankedSalaries
WHERE rn = 2;
```

### Summary

- **Subquery Approach**: Good for older MySQL versions.
- **Derived Table Approach**: Handles distinct salaries and ordering.
- **User-Defined Variables**: MySQL-specific and useful for ranking without window functions.
- **Window Functions**: Best for MySQL 8.0+ for clean and efficient querying.

Choose the method that best fits your MySQL version and performance needs.