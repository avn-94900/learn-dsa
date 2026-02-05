# Database & SQL

### SQL vs NoSQL

| Number | Question |
| ------ | ---------- |
| 1 | SQL vs NoSQL comparison |
| 2 | When to use SQL over NoSQL |
| 3 | Difference between S3 and RDBMS? |

### SQL Query Problems

| Number | Query Problem |
| ------ | ---------- |
| 1 | Employee table with columns: `EmployeeID INT PRIMARY KEY`, `EmployeeName VARCHAR(50)`, `ManagerID INT` - Write SQL query to retrieve each employee's name and their corresponding manager's name |
| 2 | Employee table with columns: `id`, `name`, `dept`, `salary`, `hire_date` - Find the top 3 highest paid employees |
| 3 | Employee table with columns: `id`, `name`, `dept`, `salary`, `hire_date` - Find departments which have more than 5 employees |
| 4 | Employee table with columns: `id`, `name`, `dept`, `salary`, `hire_date` - Find second highest salary in each department |
| 5 | Orders table with columns: `order_id`, `customer_id`, `product_id`, `quantity`, `amount` - Find all customers who have ordered all the products that customer 1 ordered |

### Redis & Caching

| Number | Question |
| ------ | ---------- |
| 1 | Where to use Redis Cache |
| 2 | Redis retention policies |




<br/><br/><br/>



### SQL & Query Logic – Interview Notes

| No | Question                                                                                           |
| -- | -------------------------------------------------------------------------------------------------- |
| 1  | In the given query, can we remove the HAVING SUM(o.amount) > 1000 clause? What will be the effect? |
| 2  | What is the difference between WHERE and HAVING?                                                   |
| 3  | What precautions should be taken while using HAVING with aggregates?                               |

---

### Salary Ranking & Nth Salary – Interview Notes

| No | Question                                                                                 |
| -- | ---------------------------------------------------------------------------------------- |
| 1  | Find the second highest salary from the Employee table using LIMIT, OFFSET, or subquery. |
| 2  | Retrieve the Nth highest salary from the employees table.                                |
| 3  | Find max, min, Nth max, Nth min, and average salary.                                     |
| 4  | Retrieve all salaries above average.                                                     |
| 5  | Retrieve all salaries below average.                                                     |
| 6  | Retrieve top 10 salaries above average.                                                  |
| 7  | Retrieve top K salaries above average.                                                   |

---

### Salary vs Manager – Interview Notes

| No | Question                                                                       |
| -- | ------------------------------------------------------------------------------ |
| 1  | Retrieve employees who earn more than their manager.                           |
| 2  | Retrieve employees who earn more than their manager and live in the same city. |
| 3  | Find employees who have the same salary as their manager.                      |

---

### Salary vs Averages – Interview Notes

| No | Question                                                                                               |
| -- | ------------------------------------------------------------------------------------------------------ |
| 1  | Find employees who earn more than the average salary in the entire company.                            |
| 2  | Find employees whose salary is above their department's average but below the overall company average. |
| 3  | Find employees whose salary is within 10% of the highest salary in their department.                   |

---

### Grouping & Aggregations – Interview Notes

| No | Question                                                                                      |
| -- | --------------------------------------------------------------------------------------------- |
| 1  | Find max salary by city, age, or gender.                                                      |
| 2  | Group by department, salary, gender and sort salary or age in ascending and descending order. |
| 3  | Display department name with employee count.                                                  |
| 4  | Count males and females in each department.                                                   |
| 5  | Count departments having more than 5 employees.                                               |
| 6  | Find departments with the highest average salary.                                             |
| 7  | Find departments with the lowest average salary.                                              |
| 8  | Find how many employees are above average per department.                                     |
| 9  | Get departments with no employees.                                                            |

---

### Ranking & Percentile – Interview Notes

| No | Question                                                            |
| -- | ------------------------------------------------------------------- |
| 1  | Find the rank of employees based on salary within their department. |
| 2  | Retrieve employees whose salary falls in the top 5% company-wide.   |

---

### Hierarchy / Reporting – Interview Notes

| No | Question                                                               |
| -- | ---------------------------------------------------------------------- |
| 1  | Find employees who reported directly or indirectly to a given manager. |

---