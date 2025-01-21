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

|cat_id|name|breed|age|
|---:|:---|:---|---:|
|1|Ringo|Tabby|4|
|2|Cindy|Maine Coon|10|
|3|Dumbledore|Maine Coon|11|
|4|Egg|Persian|4|
|5|Misty|Tabby|13|
|6|George Michael|Ragdoll|9|
|7|Jackson|Sphynx|7|

- You can view values for specific columns
```mysql
SELECT name
FROM cats;
```

|name|
|:---|
|Ringo|
|Cindy|
|Dumbledore|
|Egg|
|Misty|
|George Michael|
|Jackson|

```mysql
SELECT age
FROM cats;
```

|age|
|---:|
|4|
|10|
|11|
|4|
|13|
|9|
|7|

- You can view multiple columns at once
```mysql
SELECT name, age
FROM cats;
```

|name|age|
|:---|---:|
|Ringo|4|
|Cindy|10|
|Dumbledore|11|
|Egg|4|
|Misty|13|
|George Michael|9|
|Jackson|7|
## 3. The `WHERE` Clause
- Use `WHERE` to specify a condition
```mysql
SELECT *
FROM cats
WHERE age = 4;
```

|cat_id|name|breed|age|
|---:|:---|:---|---:|
|1|Ringo|Tabby|4|
|4|Egg|Persian|4|

```mysql
SELECT *
FROM cats
WEHRE name = 'Egg';
```

|cat_id|name|breed|age|
|---:|:---|:---|---:|
|4|Egg|Persian|4|
## 4. Rapid Fire Exercises
- Write SQL queries that produces the given outputs:
  
|cat_id|
|---:|
|1|
|2|
|3|
|4|
|5|
|6|
|7|
```mysql
SELECT cat_id
FROM cats;
```

|name|breed|
|:---|:---|
|Ringo|Tabby|
|Cindy|Maine Coon|
|Dumbledore|Main Coon|
|Egg|Persian|
|Misty|Tabby|
|George Michael|Ragdoll|
|Jackson|Sphynx|
```mysql
SELECT name, breed
FROM cats;
```

- Just the Tabby cats

|name|age|
|:---|---:|
|Ringo|4|
|Misty|13|
```mysql
SELECT name, age
FROM cats
WHERE breed = 'Tabby';
```

- `cat_id` is same as `age`

|cat_id|age|
|---:|---:|
|4|4|
|7|7|
```mysql
SELECT cat_id, age
FROM cats
WHERE cat_id = age;
```
## 5. Aliases
- Use `AS` to alias a column in your results
- It doesn't acutally change the name of the column in the table
```mysql
SELECT cat_id AS id,
       name
FROM cats;
```
|id|name|
|---:|:---|
|1|Ringo|
|2|Cindy|
|3|Dumbledore|
|4|Egg|
|5|Misty|
|6|George Michael|
|7|Jackson|
## 6. `UPDATE`
- How do we alter existing data?
- Change tabby cats to shorthair:
```mysql
UPDATE cats
SET breed = 'Shorthair'
WHERE breed = 'Tabby';
```
|cat_id|name|breed|age|
|---:|:---|:---|---:|
|1|Ringo|Shorthair|4|
|2|Cindy|Maine Coon|10|
|3|Dumbledore|Maine Coon|11|
|4|Egg|Persian|4|
|5|Misty|Shorthair|13|
|6|George Michael|Ragdoll|9|
|7|Jackson|Sphynx|7|

- Change Misty's age to 14
```mysql
UPDATE cats
SET age = 14
WHERE name = 'Misty';
```
|cat_id|name|breed|age|
|---:|:---|:---|---:|
|1|Ringo|Shorthair|4|
|2|Cindy|Maine Coon|10|
|3|Dumbledore|Maine Coon|11|
|4|Egg|Persian|4|
|5|Misty|Shorthair|14|
|6|George Michael|Ragdoll|9|
|7|Jackson|Sphynx|7|

- *Rule of Thumb:* Try `SELECT`ing before you `UPDATE`
## 7. `UPDATE` Exercises
- Change Jackson's name to Jack
```mysql
SELECT *
FROM cats
WHERE name='Jackson';
```
|cat_id|name|breed|age|
|---:|:---|:---|---:|
|7|Jackson|Sphynx|7|
```mysql
UPDATE cats
SET name = 'Jack'
WHERE name = 'Jackson';

SELECT *
FROM cats;
```
|cat_id|name|breed|age|
|---:|:---|:---|---:|
|1|Ringo|Shorthair|4|
|2|Cindy|Maine Coon|10|
|3|Dumbledore|Maine Coon|11|
|4|Egg|Persian|4|
|5|Misty|Shorthair|14|
|6|George Michael|Ragdoll|9|
|7|Jack|Sphynx|7|
- Change Ringo's breed to British Shorthair
```mysql
SELECT *
FROM cats
WHERE name='Ringo';

SELECT *
FROM cats;
```
|cat_id|name|breed|age|
|---:|:---|:---|---:|
|1|Ringo|Shorthair|4|
```mysql
UPDATE cats
SET breed = 'British Shorthair'
WHERE name = 'Ringo';

SELECT *
FROM cats;
```
|cat_id|name|breed|age|
|---:|:---|:---|---:|
|1|Ringo|British Shorthair|4|
|2|Cindy|Maine Coon|10|
|3|Dumbledore|Maine Coon|11|
|4|Egg|Persian|4|
|5|Misty|Shorthair|14|
|6|George Michael|Ragdoll|9|
|7|Jack|Sphynx|7|
- Update both Maine Coons' ages to be 12
```mysql
SELECT *
FROM cats
WHERE breed='Maine Coon';
```
|cat_id|name|breed|age|
|---:|:---|:---|---:|
|2|Cindy|Maine Coon|10|
|3|Dumbledore|Maine Coon|11|
```mysql
UPDATE cats
SET age = 12
WHERE breed = 'Maine Coon';

SELECT *
FROM cats;
```
|cat_id|name|breed|age|
|---:|:---|:---|---:|
|1|Ringo|British Shorthair|4|
|2|Cindy|Maine Coon|12|
|3|Dumbledore|Maine Coon|12|
|4|Egg|Persian|4|
|5|Misty|Shorthair|14|
|6|George Michael|Ragdoll|9|
|7|Jack|Sphynx|7|
## 8. `DELETE`
- Delete all cats with name of 'Egg':
```mysql
DELETE FROM cats
WHERE name='Egg';

SELECT *
FROM cats;
```
|cat_id|name|breed|age|
|---:|:---|:---|---:|
|1|Ringo|British Shorthair|4|
|2|Cindy|Maine Coon|12|
|3|Dumbledore|Maine Coon|12|
|5|Misty|Shorthair|14|
|6|George Michael|Ragdoll|9|
|7|Jack|Sphynx|7|
- Delete all rows in the cats table:
```mysql
DELETE FROM cats;
```
## 9. `DELETE` Exercise
- Delete all 4 year old cats
```mysql
DELETE FROM cats
WHERE age=4;

SELECT *
FROM cats;
```
|cat_id|name|breed|age|
|---:|:---|:---|---:|
|2|Cindy|Maine Coon|12|
|3|Dumbledore|Maine Coon|12|
|5|Misty|Shorthair|14|
|6|George Michael|Ragdoll|9|
|7|Jack|Sphynx|7|
- Delete cats whose age is the same as their cat_id
```mysql
DELETE FROM cats
WHERE age=cat_id;

SELECT *
FROM cats;
```
|cat_id|name|breed|age|
|---:|:---|:---|---:|
|2|Cindy|Maine Coon|12|
|3|Dumbledore|Maine Coon|12|
|5|Misty|Shorthair|14|
|6|George Michael|Ragdoll|9|
- Delete all cats
```mysql
DELETE FROM cats;
```
