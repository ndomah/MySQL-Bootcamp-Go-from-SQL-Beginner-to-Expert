# Inserting Data
## 1. The Basics
- Re-create the cats table:
```mysql
CREATE TABLE cats (
  name VARCHAR(50),
  age INT
);
```
- Insert a cat:
```mysql
INSERT INTO cats (name, age)
VALUES ('Blue Steele', 5);
```
- And another:
```mysql
INSERT INTO cats (name, age)
VALUES ('Jennkins', 7);
```
## 2. A Quick Preview of `SELECT`
- To view all rows in our table:
```mysql
SELECT *
FROM cats;
```
## 3. Multi-inserts
- Single insert (switching order of `name` and `age`):
```mysql
INSERT INTO cats (age, name)
VALUES (2, 'Beth');
```
- Multiple insert:
```mysql
INSERT INTO cats (name, age)
VALUES ('Meatball', 5),
       ('Turkey', 1),
       ('Potato Face', 15);
```
## 4. `INSERT` Exercise
- Create a `people` table
  - `first_name` - 20 char limit
  - `last_name` - 20 char limit
  - `age`
```mysql
CREATE TABLE people (
  first_name VARCHAR(20),
  last_name VARCHAR(20),
  age INT
);
```
- Insert your first person:

  |first_name|last_name|age|
  |:---|:---|:---|
  |Tina|Belcher|13|
```mysql
INSERT INTO people (first_name, last_name, age)
VALUES ('Tina', 'Belcher', 13);
```
- Insert your second person:

  |first_name|last_name|age|
  |:---|:---|:---|
  |Bob|Belcher|42|
```mysql
INSERT INTO people (first_name, last_name, age)
VALUES ('Bob', 'Belcher', 42);
```
- Multiple inserts:

  |first_name|last_name|age|
  |:---|:---|:---|
  |Linda|Belcher|45|
  |Phillip|Frond|38|
  |Calvin|Fischoeder|70|
```mysql
INSERT INTO people (first_name, last_name, age)
VALUES ('Linda', 'Belcher', 45),
       ('Phillip', 'Frond', 38),
       ('Calvin', 'Fischoeder', 70);
```
## 5. Working with `NOT NULL`
- `NULL`: "The value is not known"
- `NULL` does NOT mean zero!
- Specifying `NOT NULL` when creating a table:
```mysql
CREATE TABLE cats2 (
  name VARCHAR(100) NOT NULL,
  age INT NOT NULL
);
```
## 6. Adding `DEFAULT` Values
- You can specify `DEFAULT` values when creating a table
- This allows you to insert data without having to specify a specific column value
```mysql
CREATE TABLE cats3 (
  name VARCHAR(20) DEFAULT 'no name provided',
  age INT DEFAULT 99
);
```
- Insert a cat without a name:
```mysql
INSERT INTO cats3(age) VALUES (13);
```
- Or a nameless, ageless, cat:
```mysql
INSERT INTO cats3() VALUES();
```
- You can combine `NOT NULL` and `DEFAULT`:
```mysql
CREATE TABLE cats4 (
  name VARCHAR(20) NOT NULL DEFAULT 'unnamed',
  age INT NOT NULL DEFAULT 99
);
```
- It is NOT redundant to specify both `NOT NULL` and `DEFAULT`:
  - We can still manually set things to `NULL` if we don't specify `NOT NULL`
## 7. Introducing Primary Keys
- Before using primary keys:

  |Name|Breed|Age|
  |:---|:---|:---|
  |Monty|Tabby|10|
  |Monty|Tabby|10|
  |Monty|Tabby|10|
  |Monty|Tabby|10|

- Primary keys are unique identifiers
- They help differentiate rows in a table that are very similar
- After using primary keys:

  |Name|Breed|Age|CatID|
  |:---|:---|:---|:---|
  |Monty|Tabby|10|1|
  |Monty|Tabby|10|2|
  |Monty|Tabby|10|3|
  |Monty|Tabby|10|4|

- Option 1:
```mysql
CREATE TABLE unique_cats (
  cat_id INT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  age INT NOT NULL
);
```
- Option 2:
```mysql
CREATE TABLE unique_cats2 (
  cat_id INT,
  name VARCHAR(100) NOT NULL,
  age INT NOT NULL,
  PRIMARY KEY (cat_id_
);
```
## 8. Working with `AUTO_INCREMENT`
- You don't have to specify `PRIMARY KEY`s as `NOT NULL`; they are required to exist
- `AUTO_INCREMENT` allows the `PRIMARY KEY` to automatically increment for each new sample inserted into the table
- Implement:
```mysql
CREATE TABLE unique_cats3 (
  cat_id INT AUTO_INCREMENT,
  name VARCHAR(100) NOT NULL,
  age INT NOT NULL,
  PRIMARY KEY (cat_id)
);
```
## 9. Exercise
### 9.1 `CREATE` Table
- Define an `Employees` table, with the following fields:
  - `id` - number (automatically increments) and primary key
  - `last_name` - text, mandatory
  - `first_name` - text, mandatory
  - `middle_name` - text, not mandatory
  - `age` - number mandatory
  - `current_status` - text, mandatory, defaults to 'employed'
```mysql
CREATE TABLE Employees (
  id INT AUTO_INCREMENT PRIMARY KEY,
  last_name VARCHAR(100) NOT NULL,
  first_name VARCHAR(100) NOT NULL,
  middle_name VARCHAR(100),
  age INT NOT NULL,
  current_status VARCHAR(100) NOT NULL DEFAULT 'employed'
);
```
### 9.2 `INSERT`
- Insert the following employee: Dora Smith, age 58
```mysql
INSERT INTO Employees (first_name, last_name, age)
VALUES ('Dora', 'Smith', 58);
```
- Verify change
```mysql
SELECT * FROM Employees;
```
 
|id|last_name|first_name|middle_name|age|current_status|
|:---|:---|:---|:---|:---|:---|
|1|Smith|Dora|NULL|58|employed|
