To update the gender field in an `employee` table where the gender values need to be swapped—i.e., changing 'male' to 'female' and 'female' to 'male'—you can use the SQL `UPDATE` statement with a `CASE` expression to perform the swap in a single query. 

Assuming the `employee` table has a column named `gender` that stores values 'male' and 'female', the SQL query to achieve this would look like this:

### SQL Query

```sql
UPDATE employee
SET gender = CASE
    WHEN gender = 'male' THEN 'female'
    WHEN gender = 'female' THEN 'male'
    ELSE gender
END;
```

### Explanation

- `UPDATE employee`: Specifies the table to update.
- `SET gender = CASE ... END`: Uses a `CASE` expression to determine the new value for the `gender` field based on its current value.
  - `WHEN gender = 'male' THEN 'female'`: If the current value of `gender` is 'male', it will be updated to 'female'.
  - `WHEN gender = 'female' THEN 'male'`: If the current value of `gender` is 'female', it will be updated to 'male'.
  - `ELSE gender`: In case there are any unexpected values in the `gender` column, they will remain unchanged. This is a safety measure and can be omitted if you're certain only 'male' and 'female' values are present.

### Example with Sample Data

Assume the `employee` table has the following records:

| id | name      | gender |
|----|-----------|--------|
| 1  | Alice     | female |
| 2  | Bob       | male   |
| 3  | Carol     | female |
| 4  | Dave      | male   |
| 5  | Eve       | female |
| 6  | Frank     | male   |
| 7  | Grace     | female |
| 8  | Hank      | male   |
| 9  | Irene     | female |
| 10 | John      | male   |

After executing the `UPDATE` query, the table will be updated as follows:

| id | name      | gender |
|----|-----------|--------|
| 1  | Alice     | male   |
| 2  | Bob       | female |
| 3  | Carol     | male   |
| 4  | Dave      | female |
| 5  | Eve       | male   |
| 6  | Frank     | female |
| 7  | Grace     | male   |
| 8  | Hank      | female |
| 9  | Irene     | male   |
| 10 | John      | female |

This query is efficient for swapping values in a single pass through the data and ensures all rows are updated correctly.


## Second 

UPDATE employees
SET gender = CASE
    WHEN gender = 'male' THEN 'female'
    ELSE 'male'
END;


## Third Case 

    -- Create a temporary table with the new gender values
    CREATE TEMPORARY TABLE temp_gender (
        employee_id INT,
        new_gender ENUM('male', 'female')
    );

    -- Populate the temporary table with the swapped gender values
    INSERT INTO temp_gender (employee_id, new_gender)
    SELECT employee_id,
        CASE
            WHEN gender = 'male' THEN 'female'
            ELSE 'male'
        END AS new_gender
    FROM employees;

    -- Update the employees table using the temporary table
    UPDATE employees e
    INNER JOIN temp_gender tg ON e.employee_id = tg.employee_id
    SET e.gender = tg.new_gender;

    -- Drop the temporary table
    DROP TEMPORARY TABLE temp_gender;
