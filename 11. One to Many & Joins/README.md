# One to Many & Joins
## Data is Messy
- So far we've been working with simple data
- Real world data is messy and interrelated
## Relationships Basics
1. One to One 
2. One to Many
3. Many to Many 
## One to Many Relationship
- 1:MANY
- The most common relationship
- Let's say we have a customers with orders and we want to store
  - A customer's first and last name
  - A customer's email
  - The date of the purchase
  - The price of the order
- We could make it one big table

| first_name | last_name | email            | order_date  | amount |
|------------|-----------|------------------|-------------|--------|
| Boy        | George    | george@gmail.com  | '2016/02/10' | 99.99  |
| Boy        | George    | george@gmail.com  | '2017/11/11' | 35.50  |
| George     | Michael   | gm@gmail.com      | '2014/12/12' | 800.67 |
| George     | Michael   | gm@gmail.com      | '2015/01/03' | 12.50  |
| David      | Bowie     | david@gmail.com   | NULL        | NULL   |
| Blue       | Steele    | blue@gmail.com    | NULL        | NULL   |
- This is a BAD IDEA
- We should make one table for customers, and another for orders
### Customers Table

| Column Name  | Description  |
|--------------|--------------|
| customer_id  | Primary key, unique identifier for each customer |
| first_name   | First name of the customer  |
| last_name    | Last name of the customer   |
| email        | Email address of the customer |

| customer_id | first_name | last_name | email             |
|-------------|------------|-----------|-------------------|
| 1           | Boy         | George    | george@gmail.com  |
| 2           | George      | Michael   | gm@gmail.com      |
| 3           | David       | Bowie     | david@gmail.com   |
| 4           | Blue        | Steele    | blue@gmail.com    |

---

### Orders Table

| Column Name  | Description  |
|--------------|--------------|
| order_id     | Primary key, unique identifier for each order |
| order_date   | Date of the order |
| amount       | Total amount of the order  |
| customer_id  | Foreign key referencing `Customers.customer_id` |

| order_id | order_date  | amount | customer_id |
|----------|-------------|--------|-------------|
| 1        | '2016/02/10' | 99.99  | 1           |
| 2        | '2017/11/11' | 35.50  | 1           |
| 3        | '2014/12/12' | 800.67 | 2           |
| 4        | '2015/01/03' | 12.50  | 2           |

---

### Relationship

The `customer_id` in the **Orders** table is a **foreign key** that references the `customer_id` (**primary key**) in the **Customers** table, establishing a **one-to-many** relationship:

| Customers (1)  | ←  | Orders (Many)  |
|----------------|----|---------------|
| customer_id (PK) |    | customer_id (FK) |

## Working with `FOREIGN KEY`
```mysql
CREATE TABLE customers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(50)
);
 
CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    order_date DATE,
    amount DECIMAL(8,2),
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(id)
);
 
INSERT INTO customers (first_name, last_name, email) 
VALUES ('Boy', 'George', 'george@gmail.com'),
       ('George', 'Michael', 'gm@gmail.com'),
       ('David', 'Bowie', 'david@gmail.com'),
       ('Blue', 'Steele', 'blue@gmail.com'),
       ('Bette', 'Davis', 'bette@aol.com');
       
       
INSERT INTO orders (order_date, amount, customer_id)
VALUES ('2016-02-10', 99.99, 1),
       ('2017-11-11', 35.50, 1),
       ('2014-12-12', 800.67, 2),
       ('2015-01-03', 12.50, 2),
       ('1999-04-11', 450.25, 5);
```
## `CROSS JOIN`
![cross join](https://github.com/ndomah/MySQL-Bootcamp-Go-from-SQL-Beginner-to-Expert/blob/main/11.%20One%20to%20Many%20%26%20Joins/img_cross_join.png)
- A `CROSS JOIN` produces the Cartesian product of two tables
  - Each row from the first table is combined with every row from the second table
- Kind of useless in the real world 
 ```mysql
SELECT *
FROM customers, orders;
```
| id | first_name | last_name | email             | id2 | order_date | amount  | customer_id |
|----|------------|-----------|-------------------|-----|------------|---------|-------------|
| 5  | Bette      | Davis     | bette@aol.com     | 1   | 2016-02-10  | 99.99   | 1           |
| 4  | Blue       | Steele    | blue@gmail.com    | 1   | 2016-02-10  | 99.99   | 1           |
| 3  | David      | Bowie     | david@gmail.com   | 1   | 2016-02-10  | 99.99   | 1           |
| 2  | George     | Michael   | gm@gmail.com      | 1   | 2016-02-10  | 99.99   | 1           |
| 1  | Boy        | George    | george@gmail.com  | 1   | 2016-02-10  | 99.99   | 1           |
| 5  | Bette      | Davis     | bette@aol.com     | 2   | 2017-11-11  | 35.50   | 1           |
| 4  | Blue       | Steele    | blue@gmail.com    | 2   | 2017-11-11  | 35.50   | 1           |
| 3  | David      | Bowie     | david@gmail.com   | 2   | 2017-11-11  | 35.50   | 1           |
| 2  | George     | Michael   | gm@gmail.com      | 2   | 2017-11-11  | 35.50   | 1           |
| 1  | Boy        | George    | george@gmail.com  | 2   | 2017-11-11  | 35.50   | 1           |
| 5  | Bette      | Davis     | bette@aol.com     | 3   | 2014-12-12  | 800.67  | 2           |
| 4  | Blue       | Steele    | blue@gmail.com    | 3   | 2014-12-12  | 800.67  | 2           |
| 3  | David      | Bowie     | david@gmail.com   | 3   | 2014-12-12  | 800.67  | 2           |
| 2  | George     | Michael   | gm@gmail.com      | 3   | 2014-12-12  | 800.67  | 2           |
| 1  | Boy        | George    | george@gmail.com  | 3   | 2014-12-12  | 800.67  | 2           |
| 5  | Bette      | Davis     | bette@aol.com     | 4   | 2015-01-03  | 12.50   | 2           |
| 4  | Blue       | Steele    | blue@gmail.com    | 4   | 2015-01-03  | 12.50   | 2           |
| 3  | David      | Bowie     | david@gmail.com   | 4   | 2015-01-03  | 12.50   | 2           |
| 2  | George     | Michael   | gm@gmail.com      | 4   | 2015-01-03  | 12.50   | 2           |
| 1  | Boy        | George    | george@gmail.com  | 4   | 2015-01-03  | 12.50   | 2           |
| 5  | Bette      | Davis     | bette@aol.com     | 5   | 1999-04-11  | 450.25  | 5           |
| 4  | Blue       | Steele    | blue@gmail.com    | 5   | 1999-04-11  | 450.25  | 5           |
| 3  | David      | Bowie     | david@gmail.com   | 5   | 1999-04-11  | 450.25  | 5           |
| 2  | George     | Michael   | gm@gmail.com      | 5   | 1999-04-11  | 450.25  | 5           |
| 1  | Boy        | George    | george@gmail.com  | 5   | 1999-04-11  | 450.25  | 5           |
## `INNER JOIN`
![inner join](https://github.com/ndomah/MySQL-Bootcamp-Go-from-SQL-Beginner-to-Expert/blob/main/11.%20One%20to%20Many%20%26%20Joins/img_inner_join.png)
- An `INNER JOIN` retrieves records from two or more tables **only when there is a match* between columns in both tables
  - If no match is found, the rows from either table are excluded from the result
```mysql
SELECT first_name, last_name
       order_date, amount
FROM customers c
JOIN orders o
  ON o.customer_id = c.id; 
```
| first_name | order_date | amount  |
|------------|------------|---------|
| Boy        | George     | 99.99   |
| Boy        | George     | 35.50   |
| George     | Michael    | 800.67  |
| George     | Michael    | 12.50   |
| Bette      | Davis      | 450.25  |
## `INNER JOIN` with `GROUP BY`
- `INNER JOIN` is used to combine rows from 2 or more tables based on a related column, typically using **foreign keys**
- When combined with `GROUP BY`, it allows you to aggregate data across related records, such as calculating sums, counts, or averages
```mysql
SELECT first_name, last_name,
       SUM(amount) AS total
FROM customers c
JOIN orders o
  ON o.customer_id = c.id
GROUP BY first_name, last_name
ORDER BY total;
```
| first_name | last_name | total  |
|------------|-----------|--------|
| Boy        | George    | 135.49 |
| Bette      | Davis     | 450.25 |
| George     | Michael   | 813.17 |
## `LEFT JOIN`
![left join](https://github.com/ndomah/MySQL-Bootcamp-Go-from-SQL-Beginner-to-Expert/blob/main/11.%20One%20to%20Many%20%26%20Joins/img_left_join.png)
- `LEFT JOIN` (a.k.a `LEFT OUTER JOIN`) returns **all records from the left table, and the matching records from the right table.**
- If there is no match, the result will contain `NULL` values for the columns from the right table.
```mysql
SELECT first_name, last_name,
       order_date, amount
FROM customers c
LEFT JOIN orders o
  ON o.customer_id = c.id;
```
| first_name | last_name | order_date | amount |
|------------|-----------|------------|--------|
| Boy        | George    | 2017-11-11  | 35.50  |
| Boy        | George    | 2016-02-10  | 99.99  |
| George     | Michael   | 2015-01-03  | 12.50  |
| George     | Michael   | 2014-12-12  | 800.67 |
| David      | Bowie     | (NULL)      | (NULL) |
| Blue       | Steele    | (NULL)      | (NULL) |
| Bette      | Davis     | 1999-04-11  | 450.25 |
```mysql
SELECT order_date, amount
       first_name, last_name
FROM orders o
LEFT JOIN customers c
  ON o.customer_id = c.id;
```
| order_date | first_name | last_name |
|------------|------------|-----------|
| 2016-02-10 | 99.99      | George    |
| 2017-11-11 | 35.50      | George    |
| 2014-12-12 | 800.67     | Michael   |
| 2015-01-03 | 12.50      | Michael   |
| 1999-04-11 | 450.25     | Davis     |
## `LEFT JOIN` with `GROUP BY`
- The combination of `LEFT JOIN` with `GROUP BY` is used when you want to aggregate data while ensuring that all records from the left table are retained
- Even if there are no corresponding matches in the right table, the records from the left table will still be included in the result, with `NULL` values appearing in the aggregated columns where no match exists.
```mysql
SELECT first_name,
       last_name,
       IFNULL(SUM(amount), 0) AS money_spent
FROM customers c
LEFT JOIN orders o
  ON c.id = o.customer_id
GROUP BY first_name, last_name;
```
| first_name | last_name | money_spent |
|------------|-----------|-------------|
| Boy        | George    | 135.49       |
| George     | Michael   | 813.17       |
| David      | Bowie     | 0.00         |
| Blue       | Steele    | 0.00         |
| Bette      | Davis     | 450.25       |
## `RIGHT JOIN`
![right joint](https://github.com/ndomah/MySQL-Bootcamp-Go-from-SQL-Beginner-to-Expert/blob/main/11.%20One%20to%20Many%20%26%20Joins/img_right_join.png)

## On Delete Cascade


## Joins Exercise

