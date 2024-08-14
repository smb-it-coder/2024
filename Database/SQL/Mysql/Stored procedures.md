A stored procedure in MySQL is a set of SQL statements that you can save and reuse. You can think of it as a function or routine in other programming languages. Stored procedures can help you encapsulate complex logic, improve performance, and enhance security by controlling access to data.

### Key Features of Stored Procedures

1. **Modularity:** Encapsulate logic in a single unit, making it easier to manage and update.
2. **Reusability:** Write the logic once and reuse it multiple times.
3. **Performance:** Reduce the amount of information sent between the application and the database.
4. **Security:** Restrict access to data by controlling which operations can be performed and by whom.

### Creating a Stored Procedure

Let's walk through an example of creating a stored procedure in MySQL. Suppose you have a database named `company` with a table called `employees`:

```sql
CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    department VARCHAR(50),
    salary DECIMAL(10, 2)
);
```

**Objective:** Create a stored procedure to add a new employee to the `employees` table.

#### Step 1: Define the Stored Procedure

Here's how you can define a stored procedure to insert a new employee:

```sql
DELIMITER //

CREATE PROCEDURE AddEmployee(
    IN p_name VARCHAR(100),
    IN p_department VARCHAR(50),
    IN p_salary DECIMAL(10, 2)
)
BEGIN
    INSERT INTO employees (name, department, salary)
    VALUES (p_name, p_department, p_salary);
END //

DELIMITER ;
```

**Explanation:**

- `DELIMITER //`: Changes the statement delimiter from `;` to `//`. This allows you to include semicolons within the procedure without ending the procedure definition.
- `CREATE PROCEDURE AddEmployee(...)`: Defines a new stored procedure named `AddEmployee`.
- `IN p_name VARCHAR(100)`, `IN p_department VARCHAR(50)`, `IN p_salary DECIMAL(10, 2)`: These are the input parameters for the procedure.
- `BEGIN ... END`: Encapsulates the SQL statements that make up the procedure's body.
- `INSERT INTO employees ...`: The SQL statement to insert a new record into the `employees` table.
- `DELIMITER ;`: Resets the statement delimiter back to `;`.

#### Step 2: Call the Stored Procedure

To use the stored procedure and insert a new employee, you execute the following command:

```sql
CALL AddEmployee('John Doe', 'Engineering', 75000.00);
```

**Explanation:**

- `CALL AddEmployee(...)`: Invokes the `AddEmployee` procedure, passing in the parameters for the new employee.

#### Step 3: Verify the Insertion

To check if the employee was added correctly, you can query the `employees` table:

```sql
SELECT * FROM employees;
```

### Additional Features

1. **Output Parameters:**
   You can also define output parameters to return values from the procedure.

   ```sql
   DELIMITER //

   CREATE PROCEDURE GetEmployeeSalary(
       IN p_id INT,
       OUT p_salary DECIMAL(10, 2)
   )
   BEGIN
       SELECT salary INTO p_salary
       FROM employees
       WHERE id = p_id;
   END //

   DELIMITER ;
   ```

   **Calling the procedure with output parameter:**

   ```sql
   SET @salary = 0;
   CALL GetEmployeeSalary(1, @salary);
   SELECT @salary;
   ```

2. **Exception Handling:**
   MySQL doesn't support traditional exception handling in stored procedures like other databases, but you can use condition handling to manage errors:

   ```sql
   DELIMITER //

   CREATE PROCEDURE SafeAddEmployee(
       IN p_name VARCHAR(100),
       IN p_department VARCHAR(50),
       IN p_salary DECIMAL(10, 2)
   )
   BEGIN
       DECLARE CONTINUE HANDLER FOR SQLEXCEPTION
       BEGIN
           -- Error handling code here
           ROLLBACK;
       END;

       START TRANSACTION;
       INSERT INTO employees (name, department, salary)
       VALUES (p_name, p_department, p_salary);
       COMMIT;
   END //

   DELIMITER ;
   ```

**Explanation:**

- `DECLARE CONTINUE HANDLER FOR SQLEXCEPTION`: Declares an exception handler that will be executed if a SQL exception occurs.
- `START TRANSACTION` and `COMMIT`: Encapsulate the insert operation in a transaction to ensure atomicity.

Stored procedures can significantly enhance your database operations by providing modularity, efficiency, and security. They are especially useful in complex applications where SQL operations are frequent and require consistent logic.