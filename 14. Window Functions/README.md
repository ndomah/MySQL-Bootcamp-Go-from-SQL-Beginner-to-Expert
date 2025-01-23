# Window Functions
- Allow you to perform calculations across a subset of rows (a window) related to the current row, without collapsing the rows into a single aggregate result
- Unlike aggregate functions (e.g., SUM, AVG), window functions retain individual rows while providing calculated values across a defined set of data

**Key Features of Window Functions**:
- Operate on a "window" of rows that are related to the current row
- Do not group rows, meaning each row still appears in the result set
- Enable complex analytics, such as running totals, ranking, and moving averages
- Partitioning and ordering allow calculations over specific groups and sequences

**Setup Table**
```mysql
CREATE TABLE employees (
    emp_no INT PRIMARY KEY AUTO_INCREMENT,
    department VARCHAR(20),
    salary INT
);
 
INSERT INTO employees (department, salary) VALUES
('engineering', 80000),
('engineering', 69000),
('engineering', 70000),
('engineering', 103000),
('engineering', 67000),
('engineering', 89000),
('engineering', 91000),
('sales', 59000),
('sales', 70000),
('sales', 159000),
('sales', 72000),
('sales', 60000),
('sales', 61000),
('sales', 61000),
('customer service', 38000),
('customer service', 45000),
('customer service', 61000),
('customer service', 40000),
('customer service', 31000),
('customer service', 56000),
('customer service', 55000);
```
## Using `OVER()`
- Used to define a "window" (a set of rows) over which an aggregate or ranking fucntion should be applied **without collapsing the result set**
- Calculate average salary across all employees
```mysql
SELECT emp_no, department, salary, 
       AVG(salary) OVER() AS avg_salary
FROM employees;
```
| emp_no | department        | salary | avg_salary |
|--------|-------------------|--------|------------|
| 1      | engineering        | 80000  | 68428.5714 |
| 2      | engineering        | 69000  | 68428.5714 |
| 3      | engineering        | 70000  | 68428.5714 |
| 4      | engineering        | 103000 | 68428.5714 |
| 5      | engineering        | 67000  | 68428.5714 |
| 6      | engineering        | 89000  | 68428.5714 |
| 7      | engineering        | 91000  | 68428.5714 |
| 8      | sales             | 59000  | 68428.5714 |
| 9      | sales             | 70000  | 68428.5714 |
| 10     | sales             | 159000 | 68428.5714 |
| 11     | sales             | 72000  | 68428.5714 |
| 12     | sales             | 60000  | 68428.5714 |
| 13     | sales             | 61000  | 68428.5714 |
| 14     | sales             | 61000  | 68428.5714 |
| 15     | customer service  | 38000  | 68428.5714 |
| 16     | customer service  | 45000  | 68428.5714 |
| 17     | customer service  | 61000  | 68428.5714 |
| 18     | customer service  | 40000  | 68428.5714 |
| 19     | customer service  | 31000  | 68428.5714 |
| 20     | customer service  | 56000  | 68428.5714 |
| 21     | customer service  | 55000  | 68428.5714 |
- Calculate min and max salary acorss all employees
```mysql
SELECT emp_no, department, salary, 
       MIN(salary) OVER() AS min_salary,
       MAX(salary) OVER() AS max_salary
FROM employees;
```
| emp_no | department        | salary | min_salary | max_salary |
|--------|-------------------|--------|------------|------------|
| 1      | engineering        | 80000  | 31000      | 159000     |
| 2      | engineering        | 69000  | 31000      | 159000     |
| 3      | engineering        | 70000  | 31000      | 159000     |
| 4      | engineering        | 103000 | 31000      | 159000     |
| 5      | engineering        | 67000  | 31000      | 159000     |
| 6      | engineering        | 89000  | 31000      | 159000     |
| 7      | engineering        | 91000  | 31000      | 159000     |
| 8      | sales             | 59000  | 31000      | 159000     |
| 9      | sales             | 70000  | 31000      | 159000     |
| 10     | sales             | 159000 | 31000      | 159000     |
| 11     | sales             | 72000  | 31000      | 159000     |
| 12     | sales             | 60000  | 31000      | 159000     |
| 13     | sales             | 61000  | 31000      | 159000     |
| 14     | sales             | 61000  | 31000      | 159000     |
| 15     | customer service  | 38000  | 31000      | 159000     |
| 16     | customer service  | 45000  | 31000      | 159000     |
| 17     | customer service  | 61000  | 31000      | 159000     |
| 18     | customer service  | 40000  | 31000      | 159000     |
| 19     | customer service  | 31000  | 31000      | 159000     |
| 20     | customer service  | 56000  | 31000      | 159000     |
| 21     | customer service  | 55000  | 31000      | 159000     |
## `PARTITION BY`
- Used within window functions to divide the result set into partitions (groups of rows) based on specified column(s)
- Allows calculations (such as aggregations) to be performed **independently within each partition**, similar to how `GROUP BY` works, but without collapsing rows
- Department-level vs company-level salary averages
```mysql
SELECT emp_no, department, salary, 
    AVG(salary) OVER(PARTITION BY department) AS dept_avg,
    AVG(salary) OVER() AS company_avg
FROM employees;
```
| emp_no | department      | salary | dept_avg | company_avg |
|--------|-----------------|--------|----------|-------------|
| 15     | customer service| 38000  | 46571.4286| 68428.5714  |
| 16     | customer service| 45000  | 46571.4286| 68428.5714  |
| 17     | customer service| 61000  | 46571.4286| 68428.5714  |
| 18     | customer service| 40000  | 46571.4286| 68428.5714  |
| 19     | customer service| 31000  | 46571.4286| 68428.5714  |
| 20     | customer service| 56000  | 46571.4286| 68428.5714  |
| 21     | customer service| 55000  | 46571.4286| 68428.5714  |
| 1      | customer service| 80000  | 81285.7143| 68428.5714  |
| 2      | engineering     | 69000  | 81285.7143| 68428.5714  |
| 3      | engineering     | 70000  | 81285.7143| 68428.5714  |
| 4      | engineering     | 103000 | 81285.7143| 68428.5714  |
| 5      | engineering     | 67000  | 81285.7143| 68428.5714  |
| 6      | engineering     | 89000  | 81285.7143| 68428.5714  |
| 7      | engineering     | 91000  | 81285.7143| 68428.5714  |
| 8      | sales           | 59000  | 77428.5714| 68428.5714  |
| 9      | sales           | 70000  | 77428.5714| 68428.5714  |
| 10     | sales           | 159000 | 77428.5714| 68428.5714  |
| 11     | sales           | 72000  | 77428.5714| 68428.5714  |
| 12     | sales           | 60000  | 77428.5714| 68428.5714  |
| 13     | sales           | 61000  | 77428.5714| 68428.5714  |
| 14     | sales           | 61000  | 77428.5714| 68428.5714  |
- Counting employees per department
```mysql
SELECT emp_no, department, salary, 
       COUNT(*) OVER(PARTITION BY department) AS dept_count
FROM employees;
```
| emp_no | department      | salary | dept_count |
|--------|-----------------|--------|------------|
| 15     | customer service| 38000  | 7          |
| 16     | customer service| 45000  | 7          |
| 17     | customer service| 61000  | 7          |
| 18     | customer service| 40000  | 7          |
| 19     | customer service| 31000  | 7          |
| 20     | customer service| 56000  | 7          |
| 21     | customer service| 55000  | 7          |
| 1      | engineering     | 80000  | 7          |
| 2      | engineering     | 69000  | 7          |
| 3      | engineering     | 70000  | 7          |
| 4      | engineering     | 103000 | 7          |
| 5      | engineering     | 67000  | 7          |
| 6      | engineering     | 89000  | 7          |
| 7      | engineering     | 91000  | 7          |
| 8      | sales           | 59000  | 7          |
| 9      | sales           | 70000  | 7          |
| 10     | sales           | 159000 | 7          |
| 11     | sales           | 72000  | 7          |
| 12     | sales           | 60000  | 7          |
| 13     | sales           | 61000  | 7          |
| 14     | sales           | 61000  | 7          |
- Department vs total payroll calculation
```mysql
SELECT emp_no, department, salary, 
       SUM(salary) OVER(PARTITION BY department) AS dept_payroll,
       SUM(salary) OVER() AS total_payroll
FROM employees;
```
| emp_no | department      | salary | dept_payroll | total_payroll |
|--------|-----------------|--------|--------------|---------------|
| 15     | customer service| 38000  | 326000       | 1437000       |
| 16     | customer service| 45000  | 326000       | 1437000       |
| 17     | customer service| 61000  | 326000       | 1437000       |
| 18     | customer service| 40000  | 326000       | 1437000       |
| 19     | customer service| 31000  | 326000       | 1437000       |
| 20     | customer service| 56000  | 326000       | 1437000       |
| 21     | customer service| 55000  | 326000       | 1437000       |
| 1      | engineering     | 80000  | 569000       | 1437000       |
| 2      | engineering     | 69000  | 569000       | 1437000       |
| 3      | engineering     | 70000  | 569000       | 1437000       |
| 4      | engineering     | 103000 | 569000       | 1437000       |
| 5      | engineering     | 67000  | 569000       | 1437000       |
| 6      | engineering     | 89000  | 569000       | 1437000       |
| 7      | engineering     | 91000  | 569000       | 1437000       |
| 8      | sales           | 59000  | 542000       | 1437000       |
| 9      | sales           | 70000  | 542000       | 1437000       |
| 10     | sales           | 159000 | 542000       | 1437000       |
| 11     | sales           | 72000  | 542000       | 1437000       |
| 12     | sales           | 60000  | 542000       | 1437000       |
| 13     | sales           | 61000  | 542000       | 1437000       |
| 14     | sales           | 61000  | 542000       | 1437000       |
## `ORDER BY` with Windows
- Allows for calculations to be performed in a **specific sequence within each partition**
- Rolling department salary calculation
```mysql
SELECT emp_no, department, salary, 
       SUM(salary) OVER(PARTITION BY department ORDER BY salary) AS rolling_dept_salary,
       SUM(salary) OVER(PARTITION BY department) AS total_dept_salary
FROM employees;
```
| emp_no | department      | salary | rolling_dept_salary | total_dept_salary |
|--------|-----------------|--------|---------------------|-------------------|
| 19     | customer service| 31000  | 31000               | 326000            |
| 15     | customer service| 38000  | 69000               | 326000            |
| 18     | customer service| 40000  | 109000              | 326000            |
| 16     | customer service| 45000  | 154000              | 326000            |
| 21     | customer service| 56000  | 209000              | 326000            |
| 20     | customer service| 56000  | 265000              | 326000            |
| 17     | customer service| 61000  | 326000              | 326000            |
| 5      | engineering     | 67000  | 67000               | 569000            |
| 2      | engineering     | 69000  | 136000              | 569000            |
| 3      | engineering     | 70000  | 206000              | 569000            |
| 1      | engineering     | 80000  | 286000              | 569000            |
| 6      | engineering     | 89000  | 375000              | 569000            |
| 7      | engineering     | 91000  | 466000              | 569000            |
| 4      | engineering     | 103000 | 569000              | 569000            |
| 8      | sales           | 59000  | 59000               | 542000            |
| 12     | sales           | 60000  | 119000              | 542000            |
| 13     | sales           | 61000  | 241000              | 542000            |
| 14     | sales           | 61000  | 241000              | 542000            |
| 9      | sales           | 70000  | 311000              | 542000            |
| 10     | sales           | 72000  | 383000              | 542000            |
| 11     | sales           | 159000 | 542000              | 542000            |

- Rolling minimum salary calculation (descending order)
```mysql
SELECT emp_no, department, salary, 
       MIN(salary) OVER(PARTITION BY department ORDER BY salary DESC) AS rolling_min
FROM employees;
```
| emp_no | department      | salary | rolling_min |
|--------|-----------------|--------|-------------|
| 17     | customer service| 61000  | 61000       |
| 20     | customer service| 56000  | 56000       |
| 21     | customer service| 55000  | 55000       |
| 16     | customer service| 45000  | 45000       |
| 18     | customer service| 40000  | 40000       |
| 15     | customer service| 38000  | 38000       |
| 19     | customer service| 31000  | 31000       |
| 4      | engineering     | 103000 | 103000      |
| 7      | engineering     | 91000  | 91000       |
| 6      | engineering     | 89000  | 89000       |
| 1      | engineering     | 80000  | 80000       |
| 3      | engineering     | 70000  | 70000       |
| 2      | engineering     | 69000  | 69000       |
| 5      | engineering     | 67000  | 67000       |
| 10     | sales           | 159000 | 159000      |
| 11     | sales           | 72000  | 72000       |
| 9      | sales           | 70000  | 70000       |
| 13     | sales           | 61000  | 61000       |
| 14     | sales           | 61000  | 61000       |
| 12     | sales           | 60000  | 60000       |
| 8      | sales           | 59000  | 59000       |

## `RANK()`, `DENSE_RANK` & `ROW_NUMBER()`
- `ROW_NUMBER()`: Assigns a unique number to each row
- `RANK()`: Assigns ranks with gaps for duplicate values
- `DENSE_RANK()`: Assigns ranks without gaps for duplicate values
```mysql
SELECT emp_no, department, salary,
    -- Assigns a unique row number within each department based on salary in descending order
    ROW_NUMBER() OVER(PARTITION BY department ORDER BY salary DESC) AS dept_row_number,

    -- Assigns ranks within each department, with gaps for duplicate salaries
    RANK() OVER(PARTITION BY department ORDER BY salary DESC) AS dept_salary_rank,

    -- Assigns rank for the entire dataset, with gaps for duplicate salaries
    RANK() OVER(ORDER BY salary DESC) AS overall_rank,

    -- Assigns rank for the entire dataset, without gaps for duplicate salaries
    DENSE_RANK() OVER(ORDER BY salary DESC) AS overall_dense_rank,

    -- Assigns a unique row number for the entire dataset based on salary in descending order
    ROW_NUMBER() OVER(ORDER BY salary DESC) AS overall_num

FROM employees 
ORDER BY overall_rank;
```
| emp_no | department      | salary | dept_row_number | dept_salary_rank | overall_rank | overall_dense_rank | overall_num |
|--------|-----------------|--------|-----------------|------------------|--------------|--------------------|-------------|
| 10     | sales           | 159000 | 1               | 1                | 1            | 1                  | 1           |
| 4      | engineering     | 103000 | 1               | 1                | 2            | 2                  | 2           |
| 7      | engineering     | 91000  | 2               | 2                | 3            | 3                  | 3           |
| 6      | engineering     | 89000  | 3               | 3                | 4            | 4                  | 4           |
| 1      | engineering     | 80000  | 4               | 4                | 5            | 5                  | 5           |
| 11     | sales           | 72000  | 2               | 2                | 6            | 6                  | 6           |
| 3      | engineering     | 70000  | 5               | 5                | 7            | 7                  | 7           |
| 9      | sales           | 70000  | 3               | 3                | 7            | 7                  | 8           |
| 2      | engineering     | 69000  | 6               | 6                | 9            | 8                  | 9           |
| 5      | engineering     | 67000  | 7               | 7                | 10           | 9                  | 10          |
| 17     | customer service| 61000  | 1               | 1                | 11           | 10                 | 11          |
| 13     | sales           | 61000  | 4               | 4                | 11           | 10                 | 12          |
| 14     | sales           | 61000  | 5               | 4                | 11           | 10                 | 13          |
| 12     | sales           | 60000  | 6               | 6                | 14           | 11                 | 14          |
| 8      | sales           | 59000  | 7               | 7                | 15           | 12                 | 15          |
| 20     | customer service| 56000  | 2               | 2                | 16           | 13                 | 16          |
| 21     | customer service| 55000  | 3               | 3                | 17           | 14                 | 17          |
| 16     | customer service| 45000  | 4               | 4                | 18           | 15                 | 18          |
| 18     | customer service| 40000  | 5               | 5                | 19           | 16                 | 19          |
| 15     | customer service| 38000  | 6               | 6                | 20           | 17                 | 20          |
| 19     | customer service| 31000  | 7               | 7                | 21           | 18                 | 21          |

## `NTILE()`
- Used to distribute rows into a specified number of **equal-sized groups**, based on the order specified in the `OVER()` clause
- It is commonly used for percentile analysis and quartile-based segmentation of data
```mysql
SELECT emp_no, department, salary,

       -- Divide employees within each department into 4 quartiles based on salary in descending order
       -- Highest salary in quartile 1, lowest in quartile 4
       NTILE(4) OVER(PARTITION BY department ORDER BY salary DESC) AS dept_salary_quartile,

       -- Divides entire employee table into 4 quartiles rankedon salary in descending order
       -- Provides quartiles across whole dataset, regardless of department
       NTILE(4) OVER(ORDER BY salary DESC) AS salary_quartile

FROM employees;
```
| emp_no | department      | salary | dept_salary_quartile | salary_quartile |
|--------|-----------------|--------|----------------------|-----------------|
| 10     | sales           | 159000 | 1                    | 1               |
| 4      | engineering     | 103000 | 1                    | 1               |
| 7      | engineering     | 91000  | 1                    | 1               |
| 6      | engineering     | 89000  | 2                    | 1               |
| 1      | engineering     | 80000  | 2                    | 1               |
| 11     | sales           | 72000  | 1                    | 1               |
| 3      | engineering     | 70000  | 2                    | 2               |
| 9      | sales           | 70000  | 2                    | 2               |
| 2      | engineering     | 69000  | 3                    | 2               |
| 5      | engineering     | 67000  | 4                    | 2               |
| 17     | customer service| 61000  | 1                    | 2               |
| 13     | sales           | 61000  | 3                    | 3               |
| 14     | sales           | 61000  | 3                    | 3               |
| 12     | sales           | 60000  | 3                    | 3               |
| 8      | sales           | 59000  | 4                    | 3               |
| 20     | customer service| 56000  | 1                    | 3               |
| 21     | customer service| 55000  | 2                    | 4               |
| 16     | customer service| 45000  | 2                    | 4               |
| 18     | customer service| 40000  | 3                    | 4               |
| 15     | customer service| 38000  | 3                    | 4               |
| 19     | customer service| 31000  | 4                    | 4               |
## `FIRST_VALUE`
- Returns the **first value** from a set of ordered rows within a partition
- It allows you to retrieve the top-most value based on the specified `ORDER BY` clause inside the `OVER()` window
```mysql
SELECT emp_no, department, salary,

    -- Finds the employee with the highest salary within each department.
    FIRST_VALUE(emp_no) 
        OVER(PARTITION BY department ORDER BY salary DESC) AS highest_paid_dept,

    -- Finds the employee with the highest salary in the entire company.
    FIRST_VALUE(emp_no) 
        OVER(ORDER BY salary DESC) AS highest_paid_overall

FROM employees;
```
| emp_no | department      | salary | highest_paid_dept | highest_paid_overall |
|--------|-----------------|--------|-------------------|----------------------|
| 10     | sales           | 159000 | 10                | 10                   |
| 4      | engineering     | 103000 | 4                 | 10                   |
| 7      | engineering     | 91000  | 4                 | 10                   |
| 6      | engineering     | 89000  | 4                 | 10                   |
| 1      | engineering     | 80000  | 4                 | 10                   |
| 11     | sales           | 72000  | 10                | 10                   |
| 3      | engineering     | 70000  | 4                 | 10                   |
| 9      | sales           | 70000  | 10                | 10                   |
| 2      | engineering     | 69000  | 4                 | 10                   |
| 5      | engineering     | 67000  | 4                 | 10                   |
| 17     | customer service| 61000  | 17                | 10                   |
| 13     | sales           | 61000  | 10                | 10                   |
| 14     | sales           | 61000  | 10                | 10                   |
| 12     | sales           | 60000  | 10                | 10                   |
| 8      | sales           | 59000  | 10                | 10                   |
| 20     | customer service| 56000  | 17                | 10                   |
| 21     | customer service| 55000  | 17                | 10                   |
| 16     | customer service| 45000  | 17                | 10                   |
| 18     | customer service| 40000  | 17                | 10                   |
| 15     | customer service| 38000  | 17                | 10                   |
| 19     | customer service| 31000  | 17                | 10                   |
## `LAG`
- Used to access the next or previous row's data in a result set without needing to use self-joins
- They are used to compare values between rows in a specific order (defined by `ORDER BY`), or within partitions (defined by `PARTITION BY`)
```mysql
SELECT emp_no, department, salary,

       -- Orders salary in descending order, subtracts previous row salary from current row
       salary - LAG(salary) OVER(ORDER BY salary DESC) as salary_diff

FROM employees;
```
| emp_no | department      | salary | salary_diff |
|--------|-----------------|--------|-------------|
| 10     | sales           | 159000 | (NULL)      |
| 4      | engineering     | 103000 | -56000      |
| 7      | engineering     | 91000  | -12000      |
| 6      | engineering     | 89000  | -2000       |
| 5      | engineering     | 80000  | -9000       |
| 11     | sales           | 72000  | -8000       |
| 3      | engineering     | 70000  | -2000       |
| 9      | sales           | 70000  | 0           |
| 2      | engineering     | 69000  | -1000       |
| 5      | engineering     | 67000  | -2000       |
| 13     | sales           | 61000  | -6000       |
| 14     | sales           | 61000  | 0           |
| 17     | customer service| 61000  | 0           |
| 12     | sales           | 60000  | -1000       |
| 8      | sales           | 59000  | -1000       |
| 20     | customer service| 56000  | -3000       |
| 21     | customer service| 55000  | -1000       |
| 16     | customer service| 45000  | -10000      |
| 18     | customer service| 40000  | -5000       |
| 15     | customer service| 38000  | -2000       |
| 19     | customer service| 31000  | -7000       |
```mysql
SELECT emp_no, department, salary,

       -- implements LAG within each department individually
       salary - LAG(salary) OVER(PARTITION BY department ORDER BY salary DESC) as dept_salary_diff

FROM employees;
```
| emp_no | department      | salary | dept_salary_diff |
|--------|-----------------|--------|------------------|
| 17     | customer service| 61000  | (NULL)           |
| 20     | customer service| 56000  | -5000            |
| 21     | customer service| 55000  | -1000            |
| 16     | customer service| 45000  | -1000            |
| 18     | customer service| 40000  | -5000            |
| 15     | customer service| 38000  | -2000            |
| 19     | customer service| 31000  | -7000            |
| 4      | engineering     | 103000 | (NULL)           |
| 7      | engineering     | 91000  | -12000           |
| 6      | engineering     | 89000  | -2000            |
| 1      | engineering     | 80000  | -9000            |
| 3      | engineering     | 70000  | -10000           |
| 2      | engineering     | 69000  | -1000            |
| 5      | engineering     | 67000  | -2000            |
| 10     | sales           | 159000 | (NULL)           |
| 11     | sales           | 72000  | -87000           |
| 9      | sales           | 70000  | -2000            |
| 13     | sales           | 61000  | -9000            |
| 14     | sales           | 61000  | 0                |
| 12     | sales           | 60000  | -1000            |
| 8      | sales           | 59000  | -1000            |
