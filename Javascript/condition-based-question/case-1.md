## We have a array contains n number of object of employe with salary department etc I want to mean salary of those employe as a position manager using javascript

To calculate the mean (average) salary of employees who hold a specific position, such as "manager", from an array of employee objects in JavaScript, you can follow these steps:

1. **Filter the Array**: Extract only the employees who have the desired position.
2. **Calculate the Total Salary**: Sum up the salaries of the filtered employees.
3. **Compute the Mean Salary**: Divide the total salary by the number of employees in the filtered list.

Here’s a step-by-step example using JavaScript:

### Example Data

```javascript
const employees = [
  { name: "Alice", position: "Manager", salary: 90000 },
  { name: "Bob", position: "Developer", salary: 80000 },
  { name: "Charlie", position: "Manager", salary: 95000 },
  { name: "David", position: "Designer", salary: 70000 },
  { name: "Eve", position: "Manager", salary: 85000 }
];
```

### JavaScript Code

```javascript
function meanSalaryByPosition(employees, position) {
  // Filter the employees based on the position
  const filteredEmployees = employees.filter(employee => employee.position === position);

  // Check if there are any employees in the filtered list
  if (filteredEmployees.length === 0) {
    return 0; // Return 0 or an appropriate message if no employees match the position
  }

  // Calculate the total salary of the filtered employees
  const totalSalary = filteredEmployees.reduce((sum, employee) => sum + employee.salary, 0);

  // Calculate the mean (average) salary
  const meanSalary = totalSalary / filteredEmployees.length;

  return meanSalary;
}

// Usage
const position = "Manager";
const averageSalary = meanSalaryByPosition(employees, position);

console.log(`The mean salary for ${position}s is: $${averageSalary}`);
```

### Explanation

1. **Filter the Array**:
   ```javascript
   const filteredEmployees = employees.filter(employee => employee.position === position);
   ```
   This line filters out employees whose position matches the specified position ("Manager" in this case).

2. **Calculate the Total Salary**:
   ```javascript
   const totalSalary = filteredEmployees.reduce((sum, employee) => sum + employee.salary, 0);
   ```
   `reduce` iterates over the filtered array and accumulates the total salary.

3. **Compute the Mean Salary**:
   ```javascript
   const meanSalary = totalSalary / filteredEmployees.length;
   ```
   This calculates the average salary by dividing the total salary by the number of employees.

4. **Handle Edge Cases**:
   The code handles cases where there are no employees with the specified position by checking if `filteredEmployees.length` is zero and returning `0`.

This approach efficiently calculates the mean salary for employees holding a specific position and can be adapted to handle various positions and datasets.

### Note - This question was asked into HCL 