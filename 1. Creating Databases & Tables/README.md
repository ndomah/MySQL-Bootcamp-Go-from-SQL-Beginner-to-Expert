# Creating Databases & Tables
## 1. Databases
| Database Server | Databases |
|-----------------|-----------|
|![db-server](https://github.com/ndomah/MySQL-Bootcamp-Go-from-SQL-Beginner-to-Expert/blob/main/1.%20Creating%20Databases%20%26%20Tables/img/db-server.png) | ![db](https://github.com/ndomah/MySQL-Bootcamp-Go-from-SQL-Beginner-to-Expert/blob/main/1.%20Creating%20Databases%20%26%20Tables/img/db-tables.png) |
- A database server can contain multiple databases.
- Each database can contain multiple tables (in relational database).
### 1.1 Showing Databases
- To list available databases:
```mysql
SHOW DATABASES;
```
### 1.2 Creating Databases
- The general command for creating a datbase:
```mysql
CREATE DATABASE <database_name>;
```
- A specific example:
```mysql
CREATE DATABASE soap_store;
```
### 1.3 Dropping and Using Databases
- To drop a database:
```mysql
DROP DATABASE <database-name>;
```
- To use a database:
```mysql
USE <database-name>:
```
## 2. Tables
### 2.1 Introduction to Tables
- A database is just a bunch of tables.
  - *In a relational database, at least.*
- Tables hold the data: "a collection of related data held in a structured format within a database"
- Example: The Cats Table
  
| Name | Breed | Age |
| :--- | :--- | :--- |
|Blue |Scottish Fold |1 |
|Rocket |Persian |3 |
|Monty |Tabby |10 |
|Sam |Munchkin |5

- Columns: headers
- Rows: the actual data/samples
- Databases are made up of lots of tables.
### 2.2 Data Types
- We have to define the data type for each column in the table for consistency and manipulation.
- Cat Table Example:
  - Name - must be text - `VARCHAR(100)` <-- `100`: max length of string
  - Breed - must be txt - `VARCHAR(100)`
  - Age - must be number - `INT`
- In reality, there are A LOT of different MySQL data types
  - *Numeric Types:*
    - **INT:** A whole number (with a max (signed) value of 2147483647)
    - SMALLINT
    - TINYINT
    - MEDIUMINT
    - BIGINT
    - DECIMAL
    - NUMERIC
    - FLOAT
    - DOUBLE
    - BIT
  - *String Types:*
    -  CHAR
    -  **VARCHAR:** A variable-length string
    -  BINARY
    -  VARBINARY
    -  BLOB
    -  TINYBLOB
    -  MEDIUMBLOB
    -  LONGBLOB
    -  TEXT
    -  TINYTEXT
    -  MEDIUMTEXT
    -  LONGTEXT
    -  ENUM
  - *Date Types:*
    - DATE
    - DATETIME
    - TIMESTAMP
    - TIME
- Refer to [MySQL Documentation](https://dev.mysql.com/doc/refman/8.4/en/data-types.html) for more info
### 2.3 Data Types Challenge
- Draw a Tweets Table that contains:
  - A username (max 15 chars)
  - The tweet content (max 140 chars)
  - Number of favorites

| Tweets |
| --- |
| Username `VARCHAR(15)` |
| Content `VARCHAR(140)` |
| Num_Favorites `INT` |
### 2.4 Creating Tables
```mysql
CREATE TABLE cats (
  name VARCHAR(50),
  age INT
);

CREATE TABLE dogs (
  name VARCHAR(50),
  breed VARCHAR(50),
  age INT
);
```
### 2.5 How Do We Know It Worked?
```mysql
SHOW tables;
```
```mysql
SHOW COLUMNS FROM cats;
```
```mysql
DESC cats;
```
### 2.6 Dropping Tables
- To drop a table:
```mysql
DROP TABLE <table-name>;
```
- To specifically drop the cats table:
```mysql
DROP TABLE cats;
```
### 2.6 Table Basics Activity
- Create a *pastries* table
  - It should include 2 columns: name and quantity
  - Name is 50 characters max
```mysql
CREATE TABLE pastries (
  name VARCHAR(50),
  quantity INT
);
```
- Inspect table and columns
```mysql
SHOW TABLES;
```
```mysql
DESC pastries;
```
- Delete table
```mysql
DROP TABLE pastries;
```
### 2.7 Comments
- Use: `--`
```mysql
-- To list all tables in DB
SHOW TABLES;
```
