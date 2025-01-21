# Creating Databases & Tables
## 1. Databases
| Database Server | Databases |
|-----------------|-----------|
|![db-server](https://github.com/ndomah/MySQL-Bootcamp-Go-from-SQL-Beginner-to-Expert/blob/main/1.%20Creating%20Databases%20%26%20Tables/img/db-server.png) | ![db](https://github.com/ndomah/MySQL-Bootcamp-Go-from-SQL-Beginner-to-Expert/blob/main/1.%20Creating%20Databases%20%26%20Tables/img/db-tables.png) |
- A database server can contain multiple databases.
- Each database can contain multiple tables (in relational database).
### 1.1 Showing Databases
- To list available databases: `SHOW DATABASES;`
### 1.2 Creating Databases
- The general command for creating a datbase: `CREATE DATABASE <database_name>;`
- A specific example: `CREATE DATABASE soap_store;`
### 1.3 Dropping and Using Databases
- To drop a database: `DROP DATABASE <database-name>;`
- To use a database: `USE <database-name>:`
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
  - Name - must be text
  - Breed - must be txt
  - Age - must be number (imagine trying to multiply the age column by a number, but a value in the age column is text)
- In reality, there are A LOT of different MySQL data types

  | Numeric Types | String Types | Date Types |
  | :--- | :--- | :--- |
  | - INT | - CHAR | - DATE |
    -  SMALLINT
    -  TINYINT
    -  MEDIUMINT
