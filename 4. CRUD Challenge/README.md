# CRUD Challenge
## C - Creating
- Create a new database called shirts_db
```mysql
CREATE DATABASE shirts_db;
```
- Create a new table called shirts:
  - shirt_id (number, automatically incremented, primary key)
  - article (text)
  - color (text)
  - shirt_size (text, 5 characters max - S/M/L/XL/XXL/XXXL/XXXXXL)
  - last_worn (number)
```mysql
USE shirts_db;

CREATE TABLE shirts (
  shirt_id INT AUTO_INCREMENT PRIMARY KEY,
  article VARCHAR(100),
  color VARCHAR(100),
  shirt_size VARCHAR(1),
  last_worn INT
);

DESC shirts;
```
|Field|Type|Null|Key|Default|Extra|
|:---|:---|:---|:---|:---|:---|
|shirt_id|int|NO|PRI|NULL|auto_incremennt|
|article|varchar(50)|YES||NULL||
|color|varchar(50)|YES||NULL||
|shirt_size|varchar(50)|YES||NULL||
|last_worn|int|YES||NULL||
- Insert the given data into the table:
```mysql
INSERT INTO shirts (article, color, shirt_size, last_worn)  
VALUES ('t-shirt', 'white', 'S', 10),
	     ('t-shirt', 'green', 'S', 200),
	     ('polo shirt', 'black', 'M', 10),
	     ('tank top', 'blue', 'S', 50),
	     ('t-shirt', 'pink', 'S', 0),
	     ('polo shirt', 'red', 'M', 5),
	     ('tank top', 'white', 'S', 200),
	     ('tank top', 'blue', 'M', 15);
```
- Add a size M purple polo shirt that was last worn 50 days ago:
```mysql
INSERT INTO shirts (article, color, shirt_size, last_worn)
VALUES ('polo shirt','purple', 'M', 50);
```
## R - Reading
- Select all shirts but only print out the article and color:
```mysql
SELECT article, color
FROM shirts;
```
|article|color|
|:---|:---|
|t-shirt|white|
|t-shirt|green|
|polo shirt|black|
|tank top|blue|
|t-shirt|pink|
|polo shirt|red|
|tank top|white|
|tank top|blue|
|polo shirt|purple|
- Select all medium shirts and print out everything but shirt_id
```mysql
SELECT article, color, shirt_size, last_worn
FROM shirts
WHERE shirt_size='M';
```
|article|color|shirt_size|last_worn|
|:---|:---|:---|---:|
|polo shirt|black|M|10|
|polo shirt|red|M|5|
|tank top|blue|M|15|
|polo shirt|purple|M|50|
## U - Updating
- Update all polo shirts and change their size to L
```mysql
SELECT *
FROM shirts
WHERE article='polo shirt';
```
|shirt_id|article|color|shirt_size|last_worn|
|---:|:---|:---|:---|---:|
|3|polo shirt|black|M|10|
|6|polo shirt|red|M|5|
|9|polo shirt|purple|M|50
```mysql
UPDATE shirts
SET shirt_size='L'
WHERE article='polo shirt';

SELECT *
FROM shirts
WHERE article='polo shirt';
```
|shirt_id|article|color|shirt_size|last_worn|
|---:|:---|:---|:---|---:|
|3|polo shirt|black|L|10|
|6|polo shirt|red|L|5|
|9|polo shirt|purple|L|50
- Update the shirt last worn 15 days ago to 0
```mysql
SELECT *
FROM shirts
WHRE last_worn=15;
```
|shirt_id|article|color|shirt_size|last_worn|
|---:|:---|:---|:---|---:|
|8|tank top|blue|M|15|
```mysql
UPDATE shirts
SET last_worn=0
WHERE last_worn=15;

SELECT *
FROM shirts;
```
|shirt_id|article|color|shirt_size|last_worn|
|---:|:---|:---|:---|---:|
|1|t-shirt|white|S|10|
|2|t-shirt|green|S|200|
|3|polo shirt|black|M|10|
|4|tank top|blue|S|50|
|5|t-shirt|pink|S|0|
|6|polo shirt|red|M|5|
|7|tank top|white|S|200|
|8|tank top|blue|M|0|
|9|polo shirt|purple|L|50|
- Update all white shirts, change their size to XS and color to off white
```mysql
SELECT *
FROM shirts
WHERE color='white';
```
|shirt_id|article|color|shirt_size|last_worn|
|---:|:---|:---|:---|---:|
|1|t-shirt|white|S|10|
|7|tank top|white|S|200|
```mysql
UPDATE shirts
SET shirt_size='XS',
    color='off white'
WHERE color='white';

SELECT *
FROM shirts;
```
|shirt_id|article|color|shirt_size|last_worn|
|---:|:---|:---|:---|---:|
|1|t-shirt|off white|XS|10|
|2|t-shirt|green|S|200|
|3|polo shirt|black|M|10|
|4|tank top|blue|S|50|
|5|t-shirt|pink|S|0|
|6|polo shirt|red|M|5|
|7|tank top|off white|XS|200|
|8|tank top|blue|M|0|
|9|polo shirt|purple|L|50|
## D - Deleting
- Delete all old shirts worn 200 days ago
```mysql
SELECT *
FROM shirts
WHERE last_worn=200;
```
|shirt_id|article|color|shirt_size|last_worn|
|---:|:---|:---|:---|---:|
|2|t-shirt|green|S|200|
|7|tank top|off white|XS|200|
```mysql
DELETE FROM shirts
WHERE last_worn=200;

SELECT *
FROM shirts;
```
|shirt_id|article|color|shirt_size|last_worn|
|---:|:---|:---|:---|---:|
|1|t-shirt|off white|XS|10|
|3|polo shirt|black|M|10|
|4|tank top|blue|S|50|
|5|t-shirt|pink|S|0|
|6|polo shirt|red|M|5|
|8|tank top|blue|M|0|
|9|polo shirt|purple|L|50|
- Delete all tank tops
```mysql
SELECT *
FROM shirts
WHERE article='tank top';
```
|shirt_id|article|color|shirt_size|last_worn|
|---:|:---|:---|:---|---:|
|4|tank top|blue|S|50|
|8|tank top|blue|M|0|
```mysql
SELECT *
FROM shirts;
```
|shirt_id|article|color|shirt_size|last_worn|
|---:|:---|:---|:---|---:|
|1|t-shirt|off white|XS|10|
|3|polo shirt|black|M|10|
|5|t-shirt|pink|S|0|
|6|polo shirt|red|M|5|
|9|polo shirt|purple|L|50|
- Delete all shirts
```mysql
DELETE FROM shirts;
```
- Drop the entire shirts table
```mysql
DROP TABLE shirts;
```
