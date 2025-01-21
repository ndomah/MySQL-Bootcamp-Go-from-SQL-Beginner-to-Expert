# CRUD Basics
## 1. Introduction
- **CRUD** = **C**reate **R**ead **U**pdate **D**elete
- We already know **C**reate --> `INSERT`
- The rest of this lesson will teach us about the **RUD**
- Setup the table:
```mysql
DROP TABLE cats;

CREATE TABLE cats (
  cat_id INT AUTO_INCREMENT,
  name VARCHAR(100),
  breed VARCHAR(100),
  age INT,
  PRIMARY KEY (cat_id)
);

-- Insert some cats:
INSERT INTO cats (name, breed, age)
VALUES ('Ringo', 'Tabby', 4),
       ('Cindy', 'Maine Coon', 10),
       ('Dumbledore', 'Maine Coon', 11),
       ('Egg', 'Persian', 4),
       ('Misty', 'Tabby', 13),
       ('George Michael', 'Ragdoll', 9),
       ('Jackson', 'Sphynx', 7); 
```
## 2. Officialy Introducing `SELECT`
- **R**ead: How do we retrieve and search data?
- Use `*` to select values for all columns
```mysql
SELECT * FROM cats; 
```

|`cat_id`|`name`|`breed`|`age`|
|---:|:---|:---|---:|
|`1`|`Ringo`|`Tabby`|`4`|
|`2`|`Cindy`|`Maine Coon`|`10`|
|`3`|`Dumbledore`|`Maine Coon`|`11`|
|`4`|`Egg`|`Persian`|`4`|
|`5`|`Misty`|`Tabby`|`13`|
|`6`|`George Michael`|`Ragdoll`|`9`|
|`7`|`Jackson`|`Sphynx`|`7`|

- You can view values for specific columns
```mysql
SELECT name FROM cats;
```

|`name`|
|:---|
|`Ringo`|
|`Cindy`|
|`Dumbledore`|
|`Egg`|
|`Misty`|
|`George Michael`|
|`Jackson`|

```mysql
SELECT age FROM cats;
```

|`age`|
|---:|
|`4`|
|`10`|
|`11`|
|`4`|
|`13`|
|`9`|
|`7`|

- You can view multiple columns at once
```mysql
SELECT name, age FROM cats;
```

|`name`|`age`|
|:---|---:|
|`Ringo`|`4`|
|`Cindy`|`10`|
|`Dumbledore`|`11`|
|`Egg`|`4`|
|`Misty`|`13`|
|`George Michael`|`9`|
|`Jackson`|`7`|
## 3. The `WHERE` Clause
