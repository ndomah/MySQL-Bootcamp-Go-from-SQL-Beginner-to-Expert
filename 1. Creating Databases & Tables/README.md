# Creating Databases & Tables
## Databases
| Database Server | Databases |
|-----------------|-----------|
|![db-server](https://github.com/ndomah/MySQL-Bootcamp-Go-from-SQL-Beginner-to-Expert/blob/main/1.%20Creating%20Databases%20%26%20Tables/img/db-server.png) | ![db](https://github.com/ndomah/MySQL-Bootcamp-Go-from-SQL-Beginner-to-Expert/blob/main/1.%20Creating%20Databases%20%26%20Tables/img/db-tables.png) |
- A database server can contain multiple databases.
- Each database can contain multiple tables (in relational database).
### Showing Databases
- To list available databases: `SHOW DATABASES;`
### Creating Databases
- The general command for creating a datbase: `CREATE DATABASE <database_name>;`
- A specific example: `CREATE DATABASE soap_store;`
### Dropping and Using Databases
- To drop a database: `DROP DATABASE <database-name>;`
- To use a database: `USE <database-name>:`
## Tables
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
